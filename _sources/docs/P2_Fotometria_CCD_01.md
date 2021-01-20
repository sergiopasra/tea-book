---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---


# Primeros pasos en la reducción de las observaciones


## Creación de las listas de imágenes
Para generar el BIAS maestro de la primera noche necesitamos combinar las observaciones de BIAS de esa noche. Por eso es comveniente crearse una lista que contenga sus nombres. análogamente desearíamos tener listas de los ficheros de FlatFileds o otras correspondientes a observaciones obtenidas con diferentes filtros, etc. 

Siguiendo las indicaciones en los documentos de ayuda de  [image management](https://ccdproc.readthedocs.io/en/latest/image_management.html) podemos generar listas usando [ImageFileCollection](https://ccdproc.readthedocs.io/en/latest/api/ccdproc.ImageFileCollection.html#ccdproc.ImageFileCollection).

La primera lista sería la de todos los ficheros ya que queremos aplicarles a todos un recorte para quedarnos con la región útil. Esto no es estrictamente necesario pero es más bonito ver las imagenes recortadas y las estadísticas de las imágenes completas no incluyen esos valores oscuros similares al valor de BIAS. 

Podemos seleccionar alguno de los ``keywords`` pare luego seleccionar los ficheros de acuerdo a los valores de éstos o directamente usarlos todos (keywords='*') 

```{code-cell} ipython3
from ccdproc import ImageFileCollection
from ccdproc.utils.sample_directory import sample_directory_with_files
directory='/Users/jzamorano/Desktop/NOT_2008/N1/'
ic_all = ImageFileCollection(directory, keywords='*')
print(ic_all.summary.colnames)
```

```{code-cell} ipython3
keys = ['imagetyp', 'object', 'filter', 'exptime']
ic1 = ImageFileCollection(directory, keywords=keys) # only keep track of keys
ic1.summary.colnames
```

Desgraciadamente nuestros ficheros no siempre contienen relleno el keyword ``ccdtype`` que informa sobre el tipo de imagen y que nos facilitaría el trabajo ya que podríamos listas las imágenes de cada clase ('bias', 'object', 'flat'  ...) y tampoco ``filter`` así que creamos nuestra lista de keywords que usaremos en la selección. 


```{code-cell} ipython3
keys = ['OBJECT' , 'EXPTIME' , 'ALFLTID' , 'FAFLTID' , 'FBFLTID']
ic1 = ImageFileCollection(directory, keywords=keys) # only keep track of keys
ic1.summary.colnames
```

Y podríamos seleccionar, por ejemplo, las observaciones con tiempo de exposición mayor que 600s

```{code-cell} ipython3
matches = (ic1.summary['EXPTIME'] > 600)
my_files = ic1.summary['file'][matches]
print(my_files)
```
También se puede hacer de esta forma

```{code-cell} ipython3
some_files = ic1.files_filtered(FBFLTID=78, exptime=3.5)
print(some_files)
```

Por último tenemos un método para seleccionar ficheros que contengan una palabra dentro de un ``keyword``. Para la lista de imágenes de BIAS usaremos

```{code-cell} ipython3
bias_list = ic1.files_filtered(regex_match=True,imagetyp='bias|light')
print(bias_list)
````
Y gracias a este método podemos crear nuestras listas de modo inteligente buscando, por ejemplo, la palabra 'flat' en el descriptor ``object``.

```{code-cell} ipython3
list_of_flats = ic1.files_filtered(regex_match=True,object='flat')
print(list_of_flats)
```

En cualquier caso siempre se puede acudir al cuaderno de observaciones y crear las listas a mano incluyendo los nombres de los ficheros

```{code-cell} ipython3
my_list = ['AL12011.fits' , 'AL12012.fits' , 'AL12013.fits']
```

En el procesado que vamos a realizar se asume que los ficheros son similares y proceden de imágenes obtenidas con la misma instrumentación y en la misma campaña. Es importante detectar y retirar fichers de nuestro directorio que corresponden a imágenes de diferente tamaño, por ejemplo. Esto puede ocurrir si hemos estado tomando imágenes de prueba con una ventana recortada del CCD y se nos ha olvidado volver a la configuración de observación.

Podemos mirar el cuaderno de observaciones y/o listar los tamaños de todas las imágenes para detectar algún problema.

```{code-cell} ipython3
for i in range(len(filelist)):
    HDUList_object = fits.open(filelist[i])
    primary_header = HDUList_object[0].header
    print(primary_header['FILENAME'],primary_header['OBJECT'],primary_header['NAXIS1'],primary_header['NAXIS2']
```
<pre>
...
ALrd120060.fits Sky Flat evening 2198 2052
ALrd120061.fits Sky Flat evening 2198 2052
ALrd120062.fits Sky Flat evening 2198 2052
ALrd120063.fits Sky Flat evening 800 800
ALrd120064.fits HZ44 focusing 2198 2052
ALrd120065.fits HZ44 focusing 2198 2052
ALrd120066.fits HZ44 focusing 2198 2052
...
</pre>
La imagen ALrd120063.fits 'Sky Flat evening' (que forma parte de una serie de enfoque) tiene dimensiones distintas: (800,800) por lo tanto hay que retirarla.

<pre>
$ rm ALrd120063.fits
</pre>

## Sustracción del overscan
Se puede usar la región de ``overscan`` que representa bien la señal de DARK de la imagen para  restarla y corregirla de esta señal de BIAS + DARK. Para CCDs que no presentan señal de DARK apreciable el ``overscan`` representa la señal de BIAS. Esto ocurre en la mayoría de las cámaras profesionales refrigeradas. En otras cámaras la substracción del overscan mejoraría la reducción si hay pequeñas diferencias de BIAS entre exposiciones. Pero en el caso general esta señal ya la tenemos bien caracterizada en la imágenes de calibración de BIAS si el sistema tiene la temperatura bien estabilizada. Combinando esas imágenes podemos crear un master BIAS que restaremos a las imágenes de ciencia. Por lo tanto este paso no es estrictamente necesario y nos lo saltamos en este ejemplo.

## Recorte de las imágenes
Es importante recordar que python tiene una manera diferente de indexar las matrices (arrays) que FITS. Mientras that python empieza los índices en 0, FITS comienza en 1, y además el orden de los índices está cambiado: (FITS sigue la convención FORTRAN y python la de C). Descripción más completa en [indexing python and FITS](https://ccdproc.readthedocs.io/en/latest/reduction_toolbox.html#subtract-overscan-and-trim-images).

Nuestras imágenes tienen dimensión (2198,2052) correspondiente a NAXIS = 2, NAXIS1 = 2198 y NAXIS2 = 2052. En notación FITS nuestro BIASSEC= [3:52,1:2052] lo que indica que las columnas entre 3 y 52 (52 incluido) contienen el overscan. En los corchetes aparece 1:2052 es decir que se tiene en cuenta todas las filas desde la primera 1 hasta la última 2052. Si leemos esta imagen FITS en una matriz de python el overscan sería img[0:2052,2:52] o de forma más compacta img[:,2:52] indicando todas las filas y entre las columnas 2 y 51.

Esto es un poco lioso pero se puede atacar de diferentes formas. Pensando en modo python (que se recomienda) o en modo FITS. 

### Aprendiendo a recortar
#### recortar con python
Después de mostar la imagen original con python comprobamos que tiene el mismo aspecto que cuando la visualizamos con DS9.  


```{figure} /_static/lecture_specific/p2_fotometria/p2_02_ds9_6.png
---
width: 600px
name: ds9-6-fig
---
Imagen AL12102.fits mostrada con DS9 (izquierda) y usando python (derecha). Se ha procurado usar los mismos cortes aunque son diferentes tablas de color .
```
Recortar un trozo de un array es fácil con python. Vamos a cortar para quedarnos con la esquina inferior izquierda,

```{code-cell} ipython3
# Trimming using python 
new_image = image[0:1000,0:1250]
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_03_trim_1.png
---
width: 600px
name: trim-1-fig
---
Imagen original y recorte usando los comandos de python para seleccionar la zona inferior izquierda del array.
```

Usando DS9 de nuevo buscamos la región que vamos a recortar que resulta ser [20:-20,60:2100] en la convención de python. Estos valores no son críticos y, por ejemplo podríamos recortar un poco más pero no deseamos perder FoV. Entonces en python,

```{code-cell} ipython3
new_image = image[20:-20,60:2100]
print(new_image.shape)
```

De la imagen original de dimensión (2052,2198) hemos recortado una nueva imagen de prueba de  tamaño (2012,2040) porque le hemos retirado 20 filas arriba y otras 20 abajo y las primeras 60 columnas y desde la columna 2100 en adelante.


```{figure} /_static/lecture_specific/p2_fotometria/p2_03_trim_2.png
---
width: 600px
name: trim-2-fig
---
Imagen original y recortada usando los comandos de python para seleccionar la región de interés.
```
#### recortar con ccdproc trim_image
ccdproc dispone de un comando para recorte de imágenes [trim_image](https://ccdproc.readthedocs.io/en/latest/api/ccdproc.trim_image.html#ccdproc.trim_image) que permite pasar los parámetros de la zona a recortar bien en modo FITS o en modo python. La ventaja del modo FITS es que el descriptor ``TRIM_SEC`` se encuentra en la mayoría de las cabeceras FITS y puede ser usado directamente sin necesidad de buscar cual es la zona de recorte.

```{code-cell} ipython3
# Cargamos los paquetes necesarios
from astropy import units as u
from astropy.nddata import CCDData
import ccdproc
# Convertimos nuesto numpy array (image) en un objeto CCDData
data_image = CCDData(image,unit=u.adu)
```

```{code-cell} ipython3
# recortamos al estilo FITS
t_image_1 = ccdproc.trim_image(data_image,fits_section='[60:2099, 21:2032]')
# y al estilo python:
t_image_2 = ccdproc.trim_image(data_image[20:-20,60:2100])
print(t_image_1.shape,t_image_2.shape)
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_03_trim_3.png
---
width: 600px
name: trim-3-fig
---
Imagenes recortadas con el comando ```trim_image``` en los dos modos descritos llegando al mismo resultado.
```
Ahora podemos escribir el resultado como una imagen FITS pero queremos que conserve la cabecera del fichero original al que vamos a añadir información sobre el procesado que le hemos realizado. Por suerte el comando ``trim_image``conserva la cabecera original.

```{code-cell} ipython3
# Replace FILENAME keyword and add information
t_image_1.header['FILENAME']  = 't_ALrd120102.fits' 
t_image_1.header['TRIMIM']  = 'fits_section=[60:2099, 21:2032]' 
t_image_1.header['HISTORY'] = str(datetime.datetime.now())[0:18]+' astropy ccdproc trim_image'
```
```{code-cell} ipython3
t_image_1.write('dummy.fits',overwrite='yes')
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_03_trim_4.png
---
width: 400px
name: trim-4-fig
---
Estas líneas se han añadido al final de la cabecera FITS de la imagen de prueba que hemos recortado dummy.fits.
```

### Recortando nuestras imágenes
Como vamos a usar ``ccdproc`` usaremos el método descrito anteriormente para recortar todas las imágenes de la primera noche de nuestra campaña.  
Generamos la lista completa de imágenes simplemente explorando el directorio de los ficheros originales. Esto se hace con ayuda de utilidades de python de la siguiente manera,

```{code-cell} ipython3
directory='/Users/jzamorano/Desktop/NOT_2008/N1/'  # Change to your working directory path 
import os
from glob import glob
# os.path.join is a platform-independent way to join two directories
globpath = os.path.join(directory, '*.fits')
print(globpath)
# glob searches through directories similar to the Unix shell
filelist = sorted(glob(globpath))   # sort filelist alphabetically 
print(filelist[100:120])    # printing only from 10 to 20
```
En la lista ``filelist`` tenemos almacenados los nombres de nuestros ficheros.  
Ahora recorremos la lista (hay formas más exquisitas de hacerlo en python)   
- efectuando el recorte de cada imagen,   
- creando un nombre de fichero similar al descriptor FILENAME pero añadiéndole 't_' al principio para indicar que es el fichero recortado,   
- escribiendo la información del procesado y cambiando el descriptor FILENAME,  
- creando el fichero FITS.  


```{code-cell} ipython3
for i in range (len(filelist)):
    image = CCDData.read(filelist[i], unit="adu")
    t_image = ccdproc.trim_image(image[20:-20,60:2100])
    name_of_file = 't_'+ str(image.header['FILENAME'])
    t_image.header['FILENAME']  = name_of_file
    t_image.header['HISTORY'] = str(datetime.datetime.now())[0:18]+' astropy ccdproc trim_image'
    t_image.header['HISTORY']  = 'trimming fits_section=[60:2099, 21:2032]' 
    print('writting '+name_of_file+ ' in '+directory)
    t_image.write(directory+name_of_file,overwrite='yes')
```

Los ficheros se han creado en el mismo directorio del que leimos las imágenes. La recomendación es dejarlos ahí y crear un subdirectorio para meter las imágenes originales. De esta forma nuestro directorio de trabajo sigue siendo el mismo y las imágenes originales siguen a nuestra disposición por si nos equivocamos en alguno de los pasos. Tendríamos entonces

<pre>
NOT_2008/N1                directorio de trabajo con los t_AL*.fits ficheros recortados
NOT_2008/N1/0_originales   donde moveríamos los ficheros originales 
                           $> mkdir 0_originales
                           $> mv AL*.fits originales/.
</pre>


