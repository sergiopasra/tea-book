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


# Correción de BIAS 

## Generación del master BIAS
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

## Corrección de bias 
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

## Corrigiendo todas las imágenes
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

