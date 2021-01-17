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
# P2 Fotometría CCD

## Campaña de observación 
Se realiza la reducción de una campaña de observación de objetos extensos realizada
con el Nordic Optical Telescope (La Palma) en abril de 2008. Se empleó el espectrógrafo [Alhambra Faint Object Spectrograph and Camera](http://www.not.iac.es/instruments/alfosc/). En particular, se trata del proyecto Calibrating the [OII]158 micron line as a star formation rate tracer (PI: A. Gil de Paz; Observadores: Pablo G. Pérez González & Jaime Zamorano). Se muestran a continuación, con cierto detalle, los pasos necesarios para su reducción.

```{figure} /_static/lecture_specific/p2_fotometria/p2_01_ALFOSC_plan.png
---
height: 400px
name: alfosc-fig
---
Esquema de ALFOSC que es el espectrógrafo de objetos débiles usado ene sta campaña de observación. 
```

### Información previa
Es importante abrir el cuaderno de observación (logbook_NOT_2008.pdf) donde se encuentra la información necesaria sobre esta campaña de observación. En particular la secuencia de las observaciones. Se indica, por ejemplo, que los ficheros que se fueron grabando en un directorio un ordenador del NOT  /data/alfosc/ con nombres numerados consecutivamente. El primero sería entonces ALrd12001.fits donde Al viene de ALFOSC, r es el año, d el mes (abril), 12 el día y 001 el número de orden.  

Los filtros empleados son 
<pre>
FILTROS
#74 BESSEL B
#75 BESSEL V
#76 BESSEL R
#49 660.7 nm estrecho 661.5
#78 658.0 nm          658.4
</pre>

### Descarga de los ficheros
Los ficheros de las observaciones se encuentran disponibles en un ftp anónimo, y el cuaderno de observación (logbook), ubicado en el Campus Virtual de la asignatura. Las imágenes originales en el ftp de astrax /pub/users/jaz/NOT_2008_04_12-14/2008-04-14 tienen nombres como ALrd140129.fits y son ficheros FITS con extensión. Para facilitar la reducción en los directorios /pub/users/jaz/NOT_2008_04_12-14/N1 (primera noche) y /N2 (segunda noche) hemos renombrado los ficheros retirando algunos caracteres AL12146.fits y convertido a FITS sin extensión. Las observaciones también se pueden descargar de [http://guaix.fis.ucm.es/~jaz/master_TEA/observaciones_NOT_2008/N1/](http://guaix.fis.ucm.es/~jaz/master_TEA/observaciones_NOT_2008/N1/) 

Es aconsejable tener un árbol de directorios que permita en todo momento saber donde se encuentran los ficheros en sus dirferentes fases de porcesado. Como veremos conviene nombrar a los ficheros de manera que identifiquen su contenido y sean fácil recordar sus nombres.

Recordemos que los comandos usuales de Linux para navegar por los directorios y explorar su contenido  son:
<pre>
$> cd ..		# baja al directorio inferior
$> cd -			# vuelve al directorio anterior
$> cd 			# nos situa de nuevo en /home/alumnos/
$> pwd			# nos informa del directorio actual
$> ls			# listado del contenido del directorio
$> ls -la		# listado con más información
$> ls -lah		# idem con tamaños de fichero  en kb y Mb
$> ls -lart		# reverse time listado no alfabético sino temporal
				# sirve para ver los últimos ficheros creados
$> more filename 	# muestra el contenido del fichero filename
$> head filename	# muestra solo las primeras líneas de filename
$> tail filename	# muestra solo las últimas líneas de filename
</pre>
Otros comandos de Linux que vamos a usar son
<pre>
$> cp file1 file2	# crea una copia del fichero file1 de nombre file2
$> mv file2 file_2	# renombra file2 a file_2
</pre>


### Inspección de las imágenes
Antes de empezar la reducción propiamente dicha vamos explorar las cabeceras FITS de los ficheros y a visualizar alguna imagen. Para ello lo ideal es abrir DS9. La terminal gráfica DS9 permite cambiar la forma de visualización (tablas de color, zoom etc) con los menús desplegables y botones. Simplemente moviendo el cursor podemos saber en qué zona de la imagen estamos y su valor en cuentas. Hay que jugar un poco con los controles para ganar experiencia.

```{figure} /_static/lecture_specific/p2_fotometria/p2_02_ds9_1.png
---
height: 400px
name: ds9-1-fig
---
Imagen AL12102.fits cargada en DS9. Se ha hecho ``zoom`` para mostar la imagen completa y se ha modificado la forma de la ventana de DS9 para hacerla más cuadrada. 
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_02_ds9_2.png
---
height: 400px
name: ds9-2-fig
---
Se ha marcado en verde una región que contiene la parte con señal de la imagen. Después recortaremos los que sobre. Para ello hemos usado ``region`` y hemos escogido que fuera tipo cuadrado (box). Luego hemos modificado su tamaño y posición.
```


```{figure} /_static/lecture_specific/p2_fotometria/p2_02_ds9_3.png
---
height: 400px
name: ds9-3-fig
---
En el menu desplegable de  ``file`` de DS9 se ha seleccionado ``display header``. Se muestra la primera parte de la cabecera FITS. 
```

Es importante inspeccionar la cabecera porque cada telescopio/instrumento escribe las cabeceras FITS de sus observaciones de forma un poco particular. En particular para los ``keyword`` de  [ALFOSC at NOT](http://www.not.iac.es/instruments/alfosc/) se escribe ``ALFLTID`` and  ``FBFLTID`` en las cabeceras en lugar de ``FILTER`` que suele ser el nombre de este keyword. La razón es que ALFOSC (espectrógrafo de objetos débiles) está diseñado de forma que posee dos ruedas de filtros (FASU) filterwheel A y filterwheel B. Los filtros se colocan en una u otra rueda dependiendo de su tamaño y/o anchura de la banda.  Más información en [NOT filters](http://www.not.iac.es/instruments/filters/).

Los extremos están entre (3,52) en el lado izquierdo y (2101,2198) en el derecho. La información se suele encontrar en la cabecera FITS como biassec y trimsec. Esta última no aparece en la cabecera en este caso. Finalmente tomaremos 
<pre>
BIASSEC= [3:52,1:2052]       TRIMSEC= [54:2100,1:2052]
</pre>
donde los números en los corchetes indican desde la columna 3 a la 52 es región de overscan que puede usarse para medida de BIAS y que desde 54 a 2100 (para todas las filas de la imagen) tenemos imagen útil. En realidad arriba y abajo (tenemos zonas sin señal debido en este caso a que el filtro era un poco más pequeño y reducía el campo de visión (FoV).

```{figure} /_static/lecture_specific/p2_fotometria/p2_02_ds9_4.png
---
height: 400px
name: ds9-4-fig
---
Detalle en la esquina inferior izquierda de DS9 mostrando el cursor justo en la frontera entre la parte oscura y la región con imagen. Se ha usado el ``zoom``. Los números arriba muestran la posición del cursor.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_02_ds9_5.png
---
height: 400px
name: ds9-5-fig
---
Detalle en la esquina inferior derecha de DS9 mostrando el cursor justo en la frontera entre la parte oscura y la región con imagen.
```




## Reducción de las observaciones.
Reduciremos a continuación la primera noche de observación. Los pasos seguidos son idénticos para la segunda noche pero se prefiere construir los master BIAS y master FLATs para cada noche y usarlos para las observaciones correspondientes.

Estamos siguiendo en gran parte los pasos descritos en [CCD Data Reduction Guide](https://mwcraig.github.io/ccd-as-book/00-00-Preface.html) una guía muy completa escrita por Matt Craig and Lauren Chambers y editada por Lauren Glattly. En esa guía se dan detalles muy interesantes sobre cómo es una imagen CCD fabricando imágenes artificiales y procesándolas de diferentes maneras.

Se han escrito cuadernos de Jupyter para cada paso y se muestran sólo partes de los mismos en este documento. Se usa en preferencia [ccdproc](https://ccdproc.readthedocs.io/en/latest/).  "Ccdproc is is an Astropy affiliated package for basic data reductions of CCD images. It provides the essential tools for processing of CCD images in a framework that provides error propagation and bad pixel tracking throughout the reduction process." (© Copyright 2020, Steve Crawford, Matt Craig, and Michael Seifert.)

### Creación de las listas de imágenes
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

### Sustracción del overscan
Se puede usar la región de ``overscan`` que representa bien la señal de DARK de la imagen para  restarla y corregirla de esta señal de BIAS + DARK. Para CCDs que no presentan señal de DARK apreciable el ``overscan`` representa la señal de BIAS. Esto ocurre en la mayoría de las cámaras profesionales refrigeradas. En otras cámaras la substracción del overscan mejoraría la reducción si hay pequeñas diferencias de BIAS entre exposiciones. Pero en el caso general esta señal ya la tenemos bien caracterizada en la imágenes de calibración de BIAS si el sistema tiene la temperatura bien estabilizada. Combinando esas imágenes podemos crear un master BIAS que restaremos a las imágenes de ciencia. Por lo tanto este paso no es estrictamente necesario y nos lo saltamos en este ejemplo.

### Recorte de las imágenes
Es importante recordar que python tiene una manera diferente de indexar las matrices (arrays) que FITS. Mientras that python empieza los índices en 0, FITS comienza en 1, y además el orden de los índices está cambiado: (FITS sigue la convención FORTRAN y python la de C). Descripción más completa en [indexing python and FITS](https://ccdproc.readthedocs.io/en/latest/reduction_toolbox.html#subtract-overscan-and-trim-images).

Nuestras imágenes tienen dimensión (2198,2052) correspondiente a NAXIS = 2, NAXIS1 = 2198 y NAXIS2 = 2052. En notación FITS nuestro BIASSEC= [3:52,1:2052] lo que indica que las columnas entre 3 y 52 (52 incluido) contienen el overscan. En los corchetes aparece 1:2052 es decir que se tiene en cuenta todas las filas desde la primera 1 hasta la última 2052. Si leemos esta imagen FITS en una matriz de python el overscan sería img[0:2052,2:52] o de forma más compacta img[:,2:52] indicando todas las filas y entre las columnas 2 y 51.

Esto es un poco lioso pero se puede atacar de diferentes formas. Pensando en modo python (que se recomienda) o en modo FITS. 

#### Aprendiendo a recortar
##### recortar con python
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
##### recortar con ccdproc trim_image
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

#### Recortando nuestras imágenes
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


### Generación del master BIAS
Combinando los BIAS obtendremos un master_BIAS o master_DARK que será el que usemos en la correción de BIAS. Como veremos se consigue una imagen con menor dispersión y en la que desaparecen los píxeles de alta señal correspondientes a la llegada de rayos cósmicos mientras se lee el detector.

Podemos empezar preparando la lista completa de ficheros en nuestro directorio de trabajo. De ella seleccionaremos luego los ficheros de BIAS de esa noche como hemos aprendido antes.
```{code-cell} ipython3
import os
from glob import glob
directory='/Users/jzamorano/Desktop/NOT_2008/N1/'   # write here your working directory
# os.path.join is a platform-independent way to join two directories
globpath = os.path.join(directory, 't_*.fits')      # already trimmed files names begin with 't_'
print(globpath)
# glob searches through directories similar to the Unix shell
filelist = sorted(glob(globpath))
print(filelist[100:105])    # printing only from 10 to 20
```
Nos preparamos para buscar los ficheros de BIAS de nuestra lista completa de imágenes

```{code-cell} ipython3
from ccdproc import ImageFileCollection
from ccdproc.utils.sample_directory import sample_directory_with_files
keys = ['imagetyp','OBJECT' , 'EXPTIME' , 'ALFLTID' , 'FAFLTID' , 'FBFLTID']
ic1 = ImageFileCollection(directory, keywords=keys) # only keep track of keys
ic1.summary.colnames
print(keys)
```
Seleccionamos los que tienen 'BIAS' en el descriptor ``imagetyp``
```{code-cell} ipython3
matches = (ic1.summary['imagetyp'] == 'BIAS') 
my_bias_files = ic1.summary['file'][matches]
print(my_bias_files)
```
Leemos los ficheros a objetos CCDData ya que queremos usar ``ccdproc``para combinarlos.

```{code-cell} ipython3
image_bias = []
for file in my_bias_files:
    image_bias.append(CCDData.read(directory+file)) #, unit="adu"))
```
La recomendación es visualizarlos con DS9 para comprobar que son todos útiles y que no hay alguno con dimensiones distintas o algún otro problema. Podemos hacer un poco de estadística.

```{code-cell} ipython3
print('Filename          Object        exp Mean std min  max')
exposure = []
for i in range(len(my_bias_files)):
    print(image_bias[i].header['FILENAME'], 
          image_bias[i].header['OBJECT'], 
          image_bias[i].header['EXPTIME'], 
          int(np.mean(image_bias[i])), 
          int(np.std(image_bias[i])), 
          np.min(image_bias[i]), 
          np.max(image_bias[i]))
````
<pre>
Filename          Object        exp Mean std min  max
t_ALrd120001.fits Bias afternoon 0.0 353 7 311 10680
t_ALrd120002.fits Bias afternoon 0.0 355 8 313 10558
t_ALrd120003.fits Bias afternoon 0.0 357 8 314 8746
t_ALrd120004.fits Bias afternoon 0.0 358 5 312 5407
t_ALrd120005.fits Bias afternoon 0.0 358 7 313 8782
t_ALrd120006.fits Bias afternoon 0.0 358 5 317 4349
t_ALrd120007.fits Bias afternoon 0.0 358 4 317 1631
t_ALrd120008.fits Bias afternoon 0.0 358 10 317 10974
t_ALrd120009.fits Bias afternoon 0.0 358 4 316 1518
t_ALrd120010.fits Bias afternoon 0.0 358 6 319 7516
</pre>

Y también preparar unos histogramas para comprobar que son similares entre sí.  
Para hacer el histograma se necesita 
- usar los datos del objeto ``CCDData``  image_bias[i].data
- colapsar el array resultante a una dimensión con ``flatten()``  image_bias[i].data.flatten()  

```{note}
astropy dispone de una rutina de histograma más completa si se desea:  [astropy hist](https://docs.astropy.org/en/stable/api/astropy.visualization.hist.html#astropy.visualization.hist).  
Esa rutina de histograma forma parte de [astropy Data Visualization](https://docs.astropy.org/en/stable/visualization/index.html#module-astropy.visualization)
```


```{code-cell} ipython3
bins = np.arange(330, 380, 5)
fig, axarr = plt.subplots(ncols=5, nrows=1, figsize=(12, 4))
for i in range(0,5): #len(my_bias_files)):
    ax = axarr[i]
    ax.hist(image_bias[i].data.flatten(), alpha=0.8, bins=bins, label=i)
    ax.grid()
    ax.set_xticks([340,360,380])
    ax.set_title('BIAS '+image_bias[i].header['FILENAME'][8:12])
    if i > 0:
        ax.label_outer()
plt.xlim(330,380)

fig, axarr = plt.subplots(ncols=5, nrows=1, figsize=(12, 4))
for i in range(5,10): #len(my_bias_files)):
    ax = axarr[i-5]
    ax.hist(image_bias[i].data.flatten(), alpha=0.8, bins=bins, label=i)
    ax.grid()
    ax.set_xticks([340,360,380])
    ax.set_title('BIAS '+image_bias[i].header['FILENAME'][8:12])
    if i > 0:
        ax.label_outer()
plt.xlim(330,380)
```
Hemos elegido representar entre valores cercanos al valor medio que encontramos antes


```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_1.png
---
width: 600px
name: bias-1-fig
---
Histograma de las imágenes de BIAS correspondientes a la noche primera.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_2.png
---
width: 600px
name: bias-2-fig
---
Representación de las imágenes de BIAS usando los mismos cortes. Se aprecian pequeñas diferencias.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_3.png
---
width: 600px
name: bias-3-fig
---
Imagen del último BIAS de la serie de 10 y detalle del mismo en una región con impactos aparentes de rayos cósmicos. 
```
Para combinar las imágenes de BIAS usaremos algunos paquetes de astropy


```{code-cell} ipython3
# Some astropy packages 
import ccdproc
from ccdproc import CCDData, Combiner
from astropy import stats
from astropy.stats import sigma_clip, mad_std
from astropy.stats import sigma_clipped_stats
```
Para combinar imágenes ``astropy`` dispone de ``Combiner`` 
```{code-cell} ipython3
# Combiner is a class for combining CCDData objects.
# https://ccdproc.readthedocs.io/en/latest/api/ccdproc.Combiner.html
# The Combiner class is used to combine together CCDData objects 
# including the method for combining the data, rejecting outlying data, 
# and weighting used for combining frames.

combiner = Combiner(image_bias)
```
Antes de combinar podemos rechazar los valores altos que aparecen en los píxeles impactados por rayos cósmicos.  
El master_dark se puede ahora crear con la combinación de nuestro gusto. Para 10 ficheros de BIAS las diferencias van a ser mínimas entre ``median_combine`` o ``mean_combine``. Puede leerse sobre este tema en: [CCD data reduction guide  Image combination](https://mwcraig.github.io/ccd-as-book/01-06-Image-combination.html)

```{code-cell} ipython3
# clipping all values over 800 to remove cosmic rays hits 
combiner.minmax_clipping(min_clip=None, max_clip=800)
# median combine 
master_dark = combiner.median_combine()
# median filter  
master_dark_filtered = ccdproc.median_filter(master_dark, 3)
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_4.png
---
width: 800px
name: bias-4-fig
---
Detalles de y estadística (media y desviación estándar) de una imagen individual de BIAS y la combinación de mediana. La última imagen es el resultado de aplicar un filtro de mediana a éste último dark. La región amarilla presenta una estadística con mayor desviación debido a los impactos de rayos cósmicos pero en el master_dark este problema se arregla. Nótese que los píxeles de valor alto han desaparecido.
```
Copiamos la cabecera de uno de los BIAS y le añadimos información del procesado hasta llegar al master_dark. usamos como FILENAME 'N1_master_dark' que es un nombre más descriptivo. 

```{code-cell} ipython3
# Copy primary header from single dark file and copy into master_dark header
master_dark.header = image_bias[0].header.copy()
```
```{code-cell} ipython3
# Replace FILENAME keyword and add information
master_dark.header['HISTORY']  = 'super DARK combining '+ str(len(image_bias)) + ' BIAS images'
master_dark.header['HISTORY']  =  str(datetime.datetime.now())[0:18]+' astropy median combine'
master_dark.header['HISTORY']  = 'BIAS images from ' + str(image_bias[0].header['FILENAME'])+' to ' + str(image_bias[9].header['FILENAME'])
master_dark.header['FILENAME'] = 'N1_master_dark' 
```
A continuación escribimos esta imagen como fichero FITS en el directorio de trabajo como 'zero_N1.fits'
```{code-cell} ipython3
master_dark.write(directory+'zero_N1.fits',overwrite='yes')
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_5.png
---
width: 700px
name: bias-5-fig
---
Estas tres líneas aparecen en el final de la cabecera del master_dark informando de cómo se ha preparado esta imagen. Se conservan las dos primeras líneas de HISTORY donde se apuntaba el recorte ('trimming') que habían sufrido anteriormente.
```

### Corrección de bias 
En este paso utilizaremos el master_DARK (o master_BIAS) para corregir todas las imágenes de este nivel de BIAS. No es necesario seleccionar por filtro empleado en este caso porque el nivel es independiente de la cantidad y tipo de luz que llegue al chip.

Si hemos seguido los pasos anteriores nuestro master DARK se llama 'zero_N1.fits' y se encuentra en nuestro directorio de trabajo. En este directorio están también las imágenes recortadas.

```{code-cell} ipython3
# reading master_bias from 'zero_N1.fits'
filename = 'zero_N1.fits'
master_bias = CCDData.read(directory+filename)
```
Haremos una corrección de BIAS en dos imágenes como ejemplo para ver que el comando ccdproc_subtract_bias que usaremos luego es una simple resta de imágenes. Una de ellas es una observación de nuestro proyecto y la otra una imagen de calibración, uno de los BIAS individuales que usamos para construir el maaster BIAS. 

```{code-cell} ipython3
science = CCDData.read(filelist[102])    # file with a science observation
onebias = CCDData.read(filelist[9])      # file with a single BIAS frame
```
```{code-cell} ipython3
# Statistics of the example images
print('Filename          Object            exp  Mean std min  max')
print(science.header['FILENAME'], science.header['OBJECT'], science.header['EXPTIME'], 
          int(np.mean(science)), int(np.std(science)), np.min(science), np.max(science))
print(bias.header['FILENAME'], onebias.header['OBJECT'], onebias.header['EXPTIME'], 
          int(np.mean(onebias)), int(np.std(onebias)), np.min(onebias), np.max(onebias))
```
<pre>
Filename          Object            exp  Mean std min  max
t_ALrd120103.fits GC4496A R 3x300s 300.0 6431 456 367 65535
t_ALrd120010.fits Bias afternoon 0.0 358 6 319 7516
</pre>
La imagen de ciencia es la primera observación de una serie de tres observaciones de 300s de exposición de NGC4496A con el filtro R. Nótese que el observador puso 'GC4496A' en lugar de 'NGC4496A'. El valor máximo es de 65535 que resulta ser el número más alto que se puede reperesentar con números binarios de 16-bits (unsigned) y por lo tanto indica que hay algún píxel completamente saturado.  ( 65535 =  2^16 -1 )

```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_6.png
---
width: 700px
name: bias-6-fig
---
Imágenes de prueba a las que vamos a restar el master BIAS. Los recuadros muestran el valor medio y la desviación estándar.
```

```{code-cell} ipython3
# Corrección de BIAS usando numpy subtract
onebias_minus_bias = np.subtract(onebias,master_bias)
science_minus_bias = np.subtract(science,master_bias)
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_7.png
---
width: 700px
name: bias-7-fig
---
Las imágenes de prueba a las que hemos restado el master BIAS. Los recuadros muestran el valor medio y la desviación estándar. Como esperábamos la señal de un BIAS al que restamos un master BIAS se queda en cero y la desviación típica no cambia. En el caso de la imagen de ciencia tenemos el nivel reducido en unas 358 cuentas (el valor medio del master BIAS).
```
Corregir con el comando de ccdproc es muy sencillo y produce el mismo resultado.
```{code-cell} ipython3
# Corrección de BIAS usando numpy subtract
bias_subtracted_onebias = ccdproc.subtract_bias(onebias, master_bias)
bias_subtracted_science = ccdproc.subtract_bias(science, master_bias)
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_8.png
---
width: 700px
name: bias-8-fig
---
Las imágenes de prueba a las que vamos hemos restado el master BIAS usando ccdproc.subtract_bias). El resultado es idéntico.
```

#### Corrigiendo todas las imágenes
Este sencillo paso que haremos a continuación falla al llegar al fichero 't_ALrd120063.fits' ya que ésta es una imagen de menor tamaño. Esta observación es un enfoque del telescopio y no tiene utilidad científica. Por eso es conveniente mirar el cuaderno de observaciones. Por lo tanto la borramos.
<pre>
$ rm t_ALrd120063.fits
</pre>

ahora simplemente recorremos toda la lista de imágenes y para cada una de ellas efectuamos la substracción de BIAS, le cambiamos el nombre añadiendo una z (de 'zero corrected') y añadimos información con descriptores HISTORY.

```{code-cell} ipython3
for i in range (len(filelist)):
    image = CCDData.read(filelist[i]) #, unit="adu")
    z_image = ccdproc.subtract_bias(image,master_bias)
    name_of_file = 'z'+ str(image.header['FILENAME'])
    z_image.header['FILENAME']  = name_of_file
    z_image.header['HISTORY']   = str(datetime.datetime.now())[0:18]+' astropy ccdproc substract_bias'
    z_image.header['HISTORY']   = 'using NOT2008/N1/zero_N1.fits master BIAS' 
    print('writting '+name_of_file+ ' in '+directory)
    z_image.write(directory+name_of_file,overwrite='yes')
```
Si todo ha ido bien tendremos en el directorio de trabajo imágenes con nombre 'zt_ALrd120062.fits' por ejemplo y que en cuya cabecera FITS se puede leer la información de su procesado.

```{figure} /_static/lecture_specific/p2_fotometria/p2_04_bias_9.png
---
width: 600px
name: bias-9-fig
---
Estas líneas aparecen en el final de la cabecera de las imágenes corregidas de BIAS informando de cómo se ha procesado esta imagen. Se conservan las dos primeras líneas de HISTORY donde se apuntaba el recorte ('trimming') que habían sufrido anteriormente.
```
Los ficheros se han creado en el mismo directorio del que leimos las imágenes. La recomendación es dejarlos ahí y crear un subdirectorio para meter las imágenes recortadas (primer paso). De esta forma nuestro directorio de trabajo sigue siendo el mismo y las imágenes originales y recortadas siguen a nuestra disposición por si nos equivocamos en alguno de los pasos. Tendríamos entonces

<pre>
NOT_2008/N1                directorio de trabajo con los t_AL*.fits ficheros recortados
NOT_2008/N1/0_originales   donde mantenemos los ficheros antes de procesado
NOT_2008/N1/1_recortados   donde almacenaremos el resultado del primer paso 
                           $> mkdir 1_recortados
                           $> mv t_AL*.fits 1_recortados/.
</pre>

Si hacemos un listado nuestro directorio de trabajo tendrá este aspecto:
<pre>
N1 jzamorano$ ls
0_originales       zt_ALrd120011.fits zt_ALrd120024.fits zt_ALrd120037.fits zt_ALrd120050.fits
1_recortados       zt_ALrd120012.fits zt_ALrd120025.fits zt_ALrd120038.fits zt_ALrd120051.fits
zero_N1.fits       zt_ALrd120013.fits zt_ALrd120026.fits zt_ALrd120039.fits zt_ALrd120052.fits
zt_ALrd120001.fits zt_ALrd120014.fits zt_ALrd120027.fits zt_ALrd120040.fits zt_ALrd120053.fits
zt_ALrd120002.fits zt_ALrd120015.fits zt_ALrd120028.fits zt_ALrd120041.fits zt_ALrd120054.fits
zt_ALrd120003.fits zt_ALrd120016.fits zt_ALrd120029.fits zt_ALrd120042.fits zt_ALrd120055.fits
zt_ALrd120004.fits zt_ALrd120017.fits zt_ALrd120030.fits zt_ALrd120043.fits zt_ALrd120056.fits
zt_ALrd120005.fits zt_ALrd120018.fits zt_ALrd120031.fits zt_ALrd120044.fits zt_ALrd120057.fits
zt_ALrd120006.fits zt_ALrd120019.fits zt_ALrd120032.fits zt_ALrd120045.fits zt_ALrd120058.fits
zt_ALrd120007.fits zt_ALrd120020.fits zt_ALrd120033.fits zt_ALrd120046.fits zt_ALrd120059.fits
...
</pre>

### Generación de un máster flat field por filtro
El FlatField representa la respuesta espacial del CCD y necesitamos determinarlo bien ya que se aplicará a todas las imágenes para corregir este efecto. Normalmente se obtienen FlatFields de cúpula y FlatField de cielo. En el primer caso tenemos la ventaja de disponer del tiempo que sea necesario ya que se trata de iluminar la cúpula con lámparas y tomar imágenes. Los FlatField de cielo se toman en los crepúsculos apuntando el telescopio a regiones libres de estrellas brillantes (Blank Fields). No siempre es fácil conseguirlos ya que el tiempo es limitado y las condiciones de luz varían muy rápidamente. Recordemos que deben tomarse para cada filtro de los que se estén empleando. En primera aproximación, se prefiere FlatField de cielo ya que reproduce mejor el color del cielo pero si no son de calidad suficiente o no se dispone de ellos se usan los de cúpula. 

Veamos de cuantos FlatField disponemos y si son de calidad suficiente. Para buscamos en el resultado los ficheros correspondientes a FlatFields. Ya vimos que esta información aparece en el nombre del objeto observado ``object`` pero no en el descriptor ``ccdtype`` como es lo habitual. Puede usarse también el cuaderno de observaciones para comprobar. Usamos Image.Collection que ya aprendimos a usar antes.

```{code-cell} ipython3
keys = ['imagetyp','OBJECT' , 'EXPTIME' , 'ALFLTID' , 'FAFLTID' , 'FBFLTID']
ic1 = ImageFileCollection(directory, keywords=keys) # only keep track of keys
ic1.summary.colnames
print(keys)
```

<pre>
['imagetyp', 'OBJECT', 'EXPTIME', 'ALFLTID', 'FAFLTID', 'FBFLTID']
</pre>

```{code-cell} ipython3
list_of_flats = ic1.files_filtered(regex_match=True,object='flat')
print(list_of_flats)
```
<pre>
['zt_ALrd120011.fits' 'zt_ALrd120012.fits' 'zt_ALrd120013.fits'
 'zt_ALrd120014.fits' 'zt_ALrd120015.fits' 'zt_ALrd120016.fits'
 'zt_ALrd120017.fits' 'zt_ALrd120018.fits' 'zt_ALrd120019.fits'
 'zt_ALrd120020.fits' 'zt_ALrd120021.fits' 'zt_ALrd120022.fits'
 'zt_ALrd120023.fits' 'zt_ALrd120024.fits' 'zt_ALrd120025.fits'
...
 'zt_ALrd120056.fits' 'zt_ALrd120057.fits' 'zt_ALrd120058.fits'
 'zt_ALrd120059.fits' 'zt_ALrd120060.fits' 'zt_ALrd120061.fits'
 'zt_ALrd120062.fits']
</pre>

O mejor todavía listamos los ficheros, sus nombres, filtros y tiempo de exposición. La identificación de los filtros de las observaciones con filtros de banda ancha aparece en 'ALFLTID' y las correspondientes a banda estrecha (que se colocan en FASU B) en  'FBFLTID'

```{code-cell} ipython3
for i in range(len(list_of_flats)):
    HDUList_object = fits.open(directory+list_of_flats[i])
    primary_header = HDUList_object[0].header
    print(primary_header['FILENAME'],primary_header['OBJECT'],primary_header['exptime']
          ,primary_header['ALFLTID'],primary_header['FBFLTID'])
```
<pre>
zt_ALrd120011.fits Dome Flat R 1.0 76 0
zt_ALrd120012.fits Dome Flat R 1.0 76 0
zt_ALrd120013.fits Dome Flat R 1.0 76 0
zt_ALrd120014.fits Dome Flat R 1.0 76 0
...
zt_ALrd120049.fits Sky Flat evening 11.0 0 78
zt_ALrd120050.fits Sky Flat evening 17.0 0 78
zt_ALrd120051.fits Sky Flat evening 18.0 0 49
zt_ALrd120052.fits Sky Flat evening 27.0 0 49
zt_ALrd120053.fits Sky Flat evening 43.0 0 49
zt_ALrd120054.fits Sky Flat evening 10.0 0 49
...
zt_ALrd120059.fits Sky Flat evening 4.9 76 0
zt_ALrd120060.fits Sky Flat evening 7.0 76 0
zt_ALrd120061.fits Sky Flat evening 10.0 76 0
zt_ALrd120062.fits Sky Flat evening 15.0 76 0
</pre>

Con esta información y la del cuaderno de observación tenemos una tabla completa donde ya anticipa algunos problemas de exceso de cuentas o filtro girado. Como siempre visualizarlo con DS9 ayuda a salir de dudas.


<pre>
zt_AL12011-ztAL12020   Dome Flat R       1s 
zt_AL12021             Dome Flat NB#78   10s   9 kcuentas
zt_AL12022             Dome Flat NB#49   30s  39 kc demasiado alto
zt_AL12023-zt_AL12032  Dome Flat NB#78   30s  24
zt_AL12033-zt_AL12042  Dome Flat NB#49   20s  no valen (filtro girado)
zt_AL12043             Dome Flat NB#49   10s  filtro en posición correcta

zt_AL12044             Sky Flat NB#78    0.1s   3 kc
zt_AL12045             Sky Flat NB#78    1.2s  11 kc
zt_AL12046             Sky Flat NB#78    3.5s  27 kc
zt_AL12047             Sky Flat NB#78    5.0s  30 kc
zt_AL12048             Sky Flat NB#78    7.5s  29 kc
zt_AL12049             Sky Flat NB#78     11s  32 kc
zt_AL12050             Sky Flat NB#78     17s  31 kc
zt_AL12051             Sky Flat NB#49     18s  30 kc
zt_AL12052             Sky Flat NB#49     27s  30 kc
zt_AL12053             Sky Flat NB#49     43s  28 kc a otro blank field
zt_AL12054             Sky Flat NB#49     10s  18 kc
zt_AL12055             Sky Flat NB#49     22s  24 kc
zt_AL12056             Sky Flat NB#49     33s  24 kc

zt_AL12057             Sky Flat #76      2.5s  26 kc   Filtro R de Bessel
zt_AL12058             Sky Flat #76      3.3s  24 kc
zt_AL12059             Sky Flat #76      4.9s  27 kc
zt_AL12060             Sky Flat #76      7.0s  27 kc
zt_AL12061             Sky Flat #76       10s  28 kc
zt_AL12062             Sky Flat #76       15s  27 kc
</pre>


```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_1.png
---
width: 600px
name: flats-1-fig
---
Imágenes de flats zt_ALrd120033 y zt_ALrd120043. La primera muestra el filtro descolocado en la rueda de filtros. Toda la serie con ese problema debe descartarse. Los observadores se dieron cuenta al final de la serie de 10 flats y se puedo corregir el problema.
```

Se aprenden varias cosas con esta tabla construida con el cuaderno de observaciones: (a) Se ha buscado que los FlatField tengan alrededor de 30 kc para que, siendo un nivel alto, estemos seguros de estar en el régimen lineal del CCD; (b) Los filtros estrechos se han observado antes que el filtro ancho ya que en la puesta de sol cada vez tenemos menos luz disponible y (c) se ha conseguido un buen registro de FlatFields de cielo con un nivel de cuentas adecuado. Para el cálculo de los tiempos de exposición se usaron las tablas que aparecen en Tyson et al. (1993) AJ 105,1206. Los valores de señal en cada imagen se pueden obtener realizando estadística para comprobar que coinciden con lo anotado en el cuaderno de observaciones.

En nuestro caso tenemos tres filtros empleados y un número reducido de imágenes y mejor que hacer un procedimiento automático trae cuenta generar directamente las listas de ficheros correspondientes a FLATS de cada banda fotométrica. así que tras la inspección de las imágenes decidimos incluir en las listas los ficheros

```{code-cell} ipython3
FF_list_78 = ['120044' , '120045' , '120046' , '120047'
            , '120048' , '120049' , '120050']
FF_list_49 = ['120051' , '120052' , '120053' 
            , '120054' , '120055' , '120056']
FF_list_76 = ['120057' , '120058' , '120059' 
            , '120060' , '120061' , '120062']
```
donde para ahorrarnos ecribir sólo hemos puesto parte del nombre. Así 120044 corresponde al fichero ALrd120044.fits.

Leemos los ficheros correspondientes a cada filtro

```{code-cell} ipython3
image_flats_78 = []
for file in FF_list_78:
    image_flats_78.append(CCDData.read(directory+'zt_ALrd'+file+'.fits')) 
image_flats_49 = []
for file in FF_list_49:
    image_flats_49.append(CCDData.read(directory+'zt_ALrd'+file+'.fits')) 
image_flats_76 = []
for file in FF_list_76:
    image_flats_76.append(CCDData.read(directory+'zt_ALrd'+file+'.fits')) 
```
para poder trabajar con ellos. De momento es interesante visualizarlos y hacer un poco de estadística. No queremos usar una imagen con poca señal para combinar con otras de mejor calidad porque seguramente estropearemos el resultado.

```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_2.png
---
width: 800px
name: flats-2-fig
---
Se muestran seis de los Flats correspondientes al filtro estrecho #78 tomadas consecutivamente en el crepúsculo vespertino. 
```
El oscurecimiento del cielo es muy rápido y la cantidad de luz disponible es cada vez menor por lo que los observadores deben aumentar el tiempo de exposición en cada toma para lograr imágenes con al señal adecuada. En este caso se pretendía obtener unas 30 mil cuentas y se fue aumentando la exposición al principio hasta llegar a ese valor y se eligió el tiempo de las siguientes tomas para mantenerlo en ese nivel.

Como los dos primeros FLATs tienen menos cuentas podríamos retirarlos de la combinación. Desde luego el primero con 3000 cuentas frente a 30000 hay que retirarlo. Como tenemos suficientes retiramos los dos primeros


```{code-cell} ipython3
#FF_list_78 = ['120044' , '120045' , '120046' , '120047'
#            , '120048' , '120049' , '120050']
FF_list_78 = ['120046' , '120047', '120048' , '120049' , '120050']
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_3.png
---
width: 800px
name: flats-3-fig
---
Se muestran dos de los Flats correspondientes al filtro ancho #76 (filtro R de Bessel) tomadas consecutivamente en el crepúsculo vespertino. 
```
En este caso las observaciones con filtro ancho (más señal que en los estrechos) se realizaron al final del crepúsculo cuando ya estaba el cielo más oscuro. En estas dos últimas tomas se aprecia la imagen de una estrella. Los apuntados del telescopio para Flats de cielo se hacen a zonas 'libres de estrellas' ('Blank fields') para evitar en lo posible que suceda esto. Además entre cada toma se mueve un poco el telescopio para que las posibles imágenes de estrellas aparezcan en diferentes lugares del detector. 

Agrupamos los ficheros correspondientes a los FLats de cada filtro en un ``combiner``.

```{code-cell} ipython3
combiner_49 = Combiner(image_flats_49)
combiner_76 = Combiner(image_flats_76)
combiner_78 = Combiner(image_flats_78)
```
y combinamos para cada filtro

```{code-cell} ipython3
# median combine 
master_flat_76 = combiner_76.median_combine()
master_flat_78 = combiner_78.median_combine()
master_flat_49 = combiner_49.median_combine()
```


```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_4.png
---
width: 800px
name: flats-4-fig
---
Se muestran un flat del filtro ancho donde aparece al imagen de una estrella y la combinación de  los flats donde desaparece esa estrella. 
```

El master FLAT presenta una degradación del número de cuentas hacia los bordes que puede ser en parte debido a viñeteo. La corrección con estos FLATS permitirá corregir este efecto.

Antes de procesar las imágenes de ciencia vamos a comprobar que la rutina ``ccdproc.flat_correct`` divide por un FLAT normalizado. Si no fuere así tendríamos que normalizar el master FLAT. La división por una imagen con valores 
cercanos a la unidad permite mantener el nivel aproximado de cuentas que es muy útil para calcular la relación señal ruido. Usamos la imagen 102 

```{code-cell} ipython3
image = CCDData.read(filelist[102])
print(image.header['object'],'  filter: ',image.header['ALFLTID'])
```
<pre>
GC4496A R 3x300s   filter:  76
</pre>

y la procesamos para corregir de FLAT

```{code-cell} ipython3
reduced_image = ccdproc.flat_correct(image, master_flat_76)
```
Si las mostramos juntas comprobamos que tienen niveles parecidos.

```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_5.png
---
width: 800px
name: flats-5-fig
---
Se muestran una imagen de ciencia y la misma una vez corre¡gida de FLAT.
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_6.png
---
width: 800px
name: flats-6-fig
---
Detalle en la esquina inferior izquierda de las imágenes de la figura anterior.
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_7.png
---
width: 800px
name: flats-7-fig
---
Los tres master FLAT correspondientes a los tres filtros empleados en al noche 1.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_8.png
---
width: 800px
name: flats-8-fig
---
Los tres master FLAT correspondientes a los tres filtros empleados en al noche 1 mostrados en DS9 con otra tabla de color.
```

Finalmente, para los tres master FLAT,

```{code-cell} ipython3
master_flat_49.header = image_flats_49[0].header.copy()
master_flat_49.header['HISTORY']  = 'super FLAT combining '+ str(len(image_flats_49)) + ' FLATS images'
master_flat_49.header['HISTORY']  =  str(datetime.datetime.now())[0:18]+' astropy median combine'
master_flat_49.header['HISTORY']  = 'FLATS images from ' + str(image_flats_49[0].header['FILENAME'])+' to ' + str(image_flats_49[-1].header['FILENAME'])

master_flat_49.header['FILENAME'] = 'N1_master_flat_49' 

master_flat_49.write(directory+'flat_N1_49.fits',overwrite='yes')
```

### Corrigiendo de variación espacial de sensibilidad 
Ya estamos preparados para corregir de Flat Field ('Flat Fielding') todas las imágenes que interesen. Recordemos que debemos aplicar el Flat Field correspondiente a cada filtro. Entonces la primera tarea es hacer una lista con las imágenes que queremos procesar en este paso. No tiene sentido corregir BIAS o FLATs de Flat Field, por ejemplo. 

```{code-cell} ipython3
from ccdproc import ImageFileCollection
from ccdproc.utils.sample_directory import sample_directory_with_files

directory='/Users/jzamorano/Desktop/NOT_2008/N1/'   # change the path to your working directory
```

```{code-cell} ipython3
keys = ['OBJECT' , 'EXPTIME' , 'ALFLTID' , 'FAFLTID' , 'FBFLTID']
ic1 = ImageFileCollection(directory, keywords=keys) # only keep track of keys
ic1.summary.colnames
```
Seleccionamos todas las imágenes obtenidas con el filtro con id=78

```{code-cell} ipython3
matches = (ic1.summary['FBFLTID'] == 78)
sci_list_78 = ic1.summary['file'][matches]
print(sci_list_78)
````
<pre>
      file       
   flat_N1_78.fits
zt_ALrd120021.fits
zt_ALrd120023.fits
zt_ALrd120024.fits
---------
zt_ALrd120119.fits
zt_ALrd120120.fits
zt_ALrd120121.fits
zt_ALrd120122.fits
Length = 36 rows
</pre>



```{code-cell} ipython3
sci_images_78 = []
for file in sci_list_78:
    sci_images_78.append(CCDData.read(directory+file))
````

Y listamos la información de algunos descriptores

```{code-cell} ipython3
print('Filename          Object        exp Mean std min  max')
exposure = []
for i in range(len(sci_list_78)):
    print(i,sci_images_78[i].header['FILENAME'], 
          sci_images_78[i].header['OBJECT'], 
          sci_images_78[i].header['EXPTIME'], 
          int(np.mean(sci_images_78[i])), 
          int(np.std(sci_images_78[i])), 
          np.min(sci_images_78[i]), 
          np.max(sci_images_78[i]))
```
<pre>
Filename            Object            exp Mean  std  min  max
0 N1_master_flat_78  Sky Flat evening 0.1 22789 8116 32.5 32932.0
1 zt_ALrd120021.fits Dome Flat NB#78 10.0 6753 2509 -8.5 16666.0
2 zt_ALrd120023.fits Dome Flat NB#78 30.0 20303 7538 11.5 29560.5
3 zt_ALrd120024.fits Dome Flat NB#78 30.0 20363 7560 11.5 29627.0
4 zt_ALrd120025.fits Dome Flat NB#78 30.0 20356 7557 21.5 29766.0
5 zt_ALrd120026.fits Dome Flat NB#78 30.0 20313 7541 20.5 29711.0
6 zt_ALrd120027.fits Dome Flat NB#78 30.0 20242 7514 16.5 33439.5
7 zt_ALrd120028.fits Dome Flat NB#78 30.0 20229 7509 16.5 41590.0
8 zt_ALrd120029.fits Dome Flat NB#78 30.0 20227 7509 27.5 30235.5
9 zt_ALrd120030.fits Dome Flat NB#78 30.0 20333 7548 16.5 37827.5
10 zt_ALrd120031.fits Dome Flat NB#78 30.0 20320 7543 12.5 29711.5
11 zt_ALrd120032.fits Dome Flat NB#78 30.0 20320 7543 16.5 31909.0
12 zt_ALrd120044.fits Sky Flat evening 0.1 2693 962 -29.0 6723.0
13 zt_ALrd120045.fits Sky Flat evening 1.199 8912 3405 13.5 65182.0
14 zt_ALrd120046.fits Sky Flat evening 3.5 20878 7435 32.5 34683.5
15 zt_ALrd120047.fits Sky Flat evening 5.0 22790 8114 27.5 32932.0
16 zt_ALrd120048.fits Sky Flat evening 7.5 24451 8705 46.5 35316.0
17 zt_ALrd120049.fits Sky Flat evening 11.0 23964 8531 33.5 39714.0
18 zt_ALrd120050.fits Sky Flat evening 17.0 23630 8412 34.5 34251.5
19 zt_ALrd120067.fits HZ44 focusing 30.0 11 11 -44.5 9684.5
20 zt_ALrd120068.fits HZ44 focusing 30.0 11 12 -45.0 7712.5
21 zt_ALrd120073.fits HZ44 focusing 20.0 9 8 -37.0 3707.5
22 zt_ALrd120074.fits HZ44 focusing 20.0 9 8 -40.0 3870.0
23 zt_ALrd120079.fits HZ44 #79 50.0 10 26 -43.5 9088.5
24 zt_ALrd120083.fits BD+75d325 #78 30.0 12 80 -35.5 44488.0
25 zt_ALrd120087.fits Feige34 #78 40.0 9 27 -47.5 15274.5
26 zt_ALrd120098.fits C3982 #78 3x900s 900.0 140 74 -50.0 12259.5
27 zt_ALrd120099.fits C3982 #78 3x900s 900.0 339 131 -47.0 16072.5
28 zt_ALrd120100.fits C3982 #78 3x900s 900.0 204 93 -48.0 19197.0
29 zt_ALrd120113.fits C4941 #78 3x900s 900.0 119 223 -45.0 65179.5
30 zt_ALrd120114.fits C4941 #78 3x900s 900.0 116 186 -45.5 65179.5
31 zt_ALrd120115.fits C4941 #78 3x900s 900.0 77 196 -50.0 65181.5
32 zt_ALrd120119.fits C5363 #78 3x900s 900.0 50 159 -46.0 65179.0
33 zt_ALrd120120.fits C5363 #78 3x900s 900.0 49 157 -47.5 65179.5
34 zt_ALrd120121.fits C5363 #78 3x900s 900.0 52 162 -50.5 65180.0
35 zt_ALrd120122.fits C5363 #78 3x900s 180.0 11 31 -46.5 48333.0
</pre>

Al imprimir colocando el número de orden me es más fácil seleccionar. Antes de sci_list_78[19] son imágenes de Flat Field y desde sci_list_78[26] en adelante son observaciones de un GRB (Gamma Ray Burst) que una alerta nos obligó a realizar y parar nuestro proyecto. Por lo tanto  

```{code-cell} ipython3
sci_list_78 = sci_list_78[19:25]
print(sci_list_78)
````
<pre>
   file       
------------------
zt_ALrd120067.fits
zt_ALrd120068.fits
zt_ALrd120073.fits
zt_ALrd120074.fits
zt_ALrd120079.fits
zt_ALrd120083.fits
</pre>

Y ahora corregimos de Flat Field esas imágenes y las grabamos en nuestro directorio añadiéndole información de esta parte del procesado. En el nombre le añadimos una 'f'.

```{code-cell} ipython3
for file in sci_list_78:
    image = CCDData.read(directory+file)
    f_image = ccdproc.flat_correct(image,master_flat_78)
    name_of_file = 'f'+ str(image.header['FILENAME'])
    f_image.header['FILENAME']  = name_of_file
    f_image.header['HISTORY']   = str(datetime.datetime.now())[0:18]+' astropy ccdproc flat_correct '
    f_image.header['HISTORY']   = 'using NOT2008/N1/master_flat_78.fits master FLAT' 
    print('writting '+name_of_file+ ' in '+directory)
    f_image.write(directory+name_of_file,overwrite='yes')
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_9.png
---
width: 500px
name: flats-9-fig
---
Las líneas del final de la cabecera de las imágenes corregidas tienen información del procesado hasta ahora.
```



### Procesado de las imágenes de estándares de flujo y científicas
Sustracción de bias, corrección de flat field (aplicando a cada imagen el obtenido con el mismo filtro).
### Eliminación de rayos cósmicos
mediante combinación de 3 o más imágenes similares (de existir), lo que precisa alineamiento previo, o limpieza individual mediante proceso semi-interactivo con el programa cleanest.

### Calibración astrométrica
Para ello se utilizará [Astrometry.net](http://astrometry.net/) y las herramientas disponibles en [AstrOmatic.net](15http://www.astromatic.net/).

### Calibración fotométrica
Determinación de las constantes instrumentales y coeficientes de extinción para cada noche.
