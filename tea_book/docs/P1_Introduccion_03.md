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

#  Visualización e inspección de imágenes 
Existen visualizadores de las imágenes procedentes de observaciones astronómicas en formato FITS. Incluso pueden estar incluidos en programas de manejo de imágenes de uso general. Por supuesto los paquetes de reducción mencionados anteriormente disponen de sus comandos para visualización. 

## SAOimageDS9
[SAOimageDS9](https://sites.google.com/cfa.harvard.edu/saoimageds9)
es uno de los programas favoritos que, por ejemplo, funciona dentro de IRAF como como su sistema de visualización. Pero una de las características más importantes de este software que permite cargar y ver varias imágenes FITS (y tablas binarias) a la vez es que funciona independientemente (stand-alone application) de otros paquetes de software y no necesita instalación o ficheros adicionales. Funciona con menús desde su GUI (graphical user interface) o por medio de comandos. SAOimageDS9 tiene su origen en SAOimage desarrollado por Mike Van Hilst en el Smithsonian Astrophysical Observatory, Center for Astrophysics, Harvard University en 1990. Unos años después Eric Mandel desarrolla SAOtng (SAOImage, The Next Generation) y a finales de los 1990s William Joye empezó a reescribir el software que se llama desde entonces SAOimageDS9 (Deep Space 9). 

El programa se descarga desde [http://ds9.si.edu](http://ds9.si.edu) y existen versiones para Windows, Mac y Linux. Los manuales, guía y tutoriales se encuentran en la página de [documentación SAOimageDS9](https://sites.google.com/cfa.harvard.edu/saoimageds9/documentation). 

- [SAOImageDS9 Reference Manual](http://ds9.si.edu/doc/ref/index.html)
- [SAOImageDS9 Users Manual](http://ds9.si.edu/doc/user/index.html)
- [Introduction to the ds9 Interface](http://ds9.si.edu/doc/user/gui/index.html)
- [Introduction to Astronomy Images and the DS9 Image Viewer](http://www.jb.man.ac.uk/~gbendo/Sci/Pict/DS9guide.pdf) tutorial de George J. Bendo
- [IPAC introduction to DS9, en cuatro videos](https://www.youtube.com/watch?v=C8QBwrKbEtc) by [Luisa Rebull](https://www.ipac.caltech.edu/science/staff/luisa-rebull) si tienes más tiempo y te gustan los tutoriales en video.  

La recomendación es ir aprendiendo poco a poco usando la herramienta y encontrando las funcionalidades a medida que las necesitamos. Se puede añadir a DS9 [Funtools](https://github.com/ericmandel/funtools) que es una librería FITS y paquete con utilidades.  
##### Ejemplo de uso de DS9  
Como una primera introducción podemos descargarnos imágenes FITS del par de galaxias NGC274-NGC275 en las bandas u, g y r de la exploración [SDSS](https://www.sdss.org/) del [DR12 Science Archive Server (SAS)](https://dr12.sdss.org/fields)

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_1.png
---
width: 500px
name: ds9_1-fig
---
Imagen del par de galaxias en interación e la página de descarga de SDSS 
[https://dr12.sdss.org/fields/name?name=NGC274](https://dr12.sdss.org/fields/name?name=NGC274)
```
Tras descargarlas tenemos las tres imágenes como ficheros FITS frame-u-008067-4-0054.fits, frame-g-008067-4-0054.fits, frame-r-008067-4-0054.fits. Empecemos mostrando la imagen en banda g. Para ello en DS9 usamos los menús 'file' + 'open' y selecionamos el directorio y fichero. Se mostrará en la ventana. 

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_2.png
---
width: 500px
name: ds9_2-fig
---
Tras cargar la primera imagen.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_3.png
---
width: 500px
name: ds9_3-fig
---
No se ve la imagen completa sino un trozo. Arriba a la derecha vemos una miniatura y un cuadrado verde con al zona recortada que vemos en la ventana. El cuadro de más a la derecha muestra una ampliación del punto donde tenemos el cursor.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_4.png
---
width: 500px
name: ds9_4-fig
---
Tras hacer zoom para imagen completa. Nótese que aparecen arriba a la izquierda el nombre del fichero y las coordenadas de imagen (píxeles) y celestes (WCS world coordinate system) ya que en este caso es una imagen completamente procesada incluyendo astrometría.
```

Las imágenes de las galaxias aparecen saturadas porque la escala empleada para mostrar la imagen se queda corta y hay valores en los píxeles de las galaxias por encima de 0.12 que es el límite superior elegido automáticamente (abajo a la derecha). Con el menú de escala y colocando nuestros límites a mano entre 0 y 5 unidades se obtiene una representación que permite ver las variaciones en la galaxia.

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_5.png
---
width: 500px
name: ds9_4-fig
---
Diálogo de límites para la escala de la representación gráfica que muestra un histograma de los valores de los píxeles de la imagen. Se pueden cambiar con el cursor o escribiendo los valores deseados.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_6.png
---
width: 500px
name: ds9_6-fig
---
Tras hacer zoom y centrar las galaxias usando una tabla de color ('lookup table') de tipo arcoiris.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_7.png
---
width: 500px
name: ds9_7-fig
---
Tras hacer zoom y centrar las galaxias usando una tabla de color ('lookup table') de tipo arcoiris.
```

Podemos cargar otra imagen en otro canal o 'frame' usando el menú 'frame'+'new' y eligiendo el fichero.


```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_8.png
---
width: 500px
name: ds9_8-fig
---
Nuevo fichero cargado en el canal ('frame') 2. De momento usa el mismo zoom que el canal 1 pero no está centrado en las galaxias.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_9.png
---
width: 500px
name: ds9_9-fig
---
Usando el menu de 'frame'+'match'+'image'+'WCS' centramos las dos imágenes en el mismo sitio. Se usa de referencia la imagen seleccionada. En este caso la primera.
```
Podemos ver las dos imágenes porque estamos en modo tejar ('tile') pero podemos seleccionar para ver sólo una ('single') o incluso hacer parpadeo entre las cargadas. Cargemos la última imagen correspondiente a la banda u.

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_10.png
---
width: 500px
name: ds9_10-fig
---
Vemos las tres imágenes cargadas en 3 canales diferentes. Para que se vean así en columnas hay que elegirlo en el menu de 'frame'+'farme parameters'+'tile'.
```

```{admonition} DS9 Ejercicio 1
Busca imágenes en NASA/IPAC Extragalactic Database [NED](https://ned.ipac.caltech.edu/) en dos bandas fotométricas de una galaxia del catálogo de Arp y muéstralas en DS9.
```
```{admonition} DS9 Ejercicio 2
Busca observaciones espectroscópicas obtenidas por [TWIN](http://www.caha.es/CAHA/Instruments/TWIN/HTML/twin.html) en el telescopio de 3.5m del observatorio de Calar Alto que tengan tiempo de exposición de 1800 s y muéstralas en DS9. Las observaciones se encuentran en el Observatorio Virtual Español [SVO](https://svo.cab.inta-csic.es/main/index.php).
```

DS9 permite crear regiones y realizar estadísticas y fotometría sencilla como se verá en la práctica de Fotometría CCD.

## ALADIN
[Aladin](https://aladin.u-strasbg.fr/), etc.

