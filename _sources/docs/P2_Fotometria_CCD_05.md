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


# Alineamiento de imágenes
Cuando no se dispone de astrometría en las imágenes necesitamos realizarla antes de comparar dos imágenes en diferentes bandas fotométricas de nuestras propias observaciones o descargadas de archivo. 
Se puede realizar con [``astroalign``](https://astroalign.readthedocs.io/en/latest/) que precisamente ha sido desarrollado para resolver este problema.

<pre>
Astroalign: A Python module for astronomical image registration. 
Beroiz, M., Cabral, J. B., and Sanchez, B. 
Astronomy and Computing, Volume 32, July 2020, 100384.
</pre>

El proceso de alinear (o registrar que es la palabra que se usa en fotografía) se suele realizar buscando imágenes de estrellas en el campo e identificando las mismas estrellas en las dos imágenes a alinear. Se busca entonces la transformación de una de las imágenes que dejaría a las estrellas en la misma posición que la imagen que tomamos como referencia. Finalmente se aplica la transformación que implica rotación y cambio de escala en el caso general. 

En el cuaderno de jupyter "example_05_register_images" se muestra un ejemplo donde se pretende alinear dos imágenes de una galaxia (M51) obtenidas en banda ancha B en diferentes épocas con el objetivo final de combinarlas para aumentar la relación señal/ruido.

```{figure} /_static/lecture_specific/p2_fotometria/p2_07_aligning_1.png
---
width: 800px
name: aligning-1-fig
---
Las dos imágenes de M51 a registrar. La de la derecha se tomará como referencia. 
```
En la figura se observa la imagen tomada en 2019 a la izquierda y la de 2016 a la derecha. Se aprecia que hay un giro entre ambas aunque no se espera cambio de escala al estar tomadas con el mismo instrumento y chip CCD. 

Leemos los ficheros de las imágenes,
```{code-cell} ipython3
# Files of observations used in this example 
directory = 'FITS_files/'
file_reference_image = directory+'afztUCM0070.fits'    #2016-04-28
file_original_image  = directory+'fztucmP_0044.fits'   #2019-04-11
```

```{code-cell} ipython3
HDUList_object = fits.open(file_reference_image)
reference_header  = HDUList_object[0].header
reference_image   = HDUList_object[0].data
print('reference image',reference_header['FILENAME'], reference_header['INSFLNAM'],
      reference_header['DATE-OBS'],'    BITPIX:',reference_header['BITPIX'])
HDUList_object  = fits.open(file_original_image)
original_header = HDUList_object[0].header
original_image  = HDUList_object[0].data
print('image to align ',original_header['FILENAME'], original_header['INSFLNAM'],
      original_header['DATE-OBS'],'  BITPIX:',original_header['BITPIX'])
```      
Usaremos ``astroalign`` que debe cargarse siguiendo las instrucciones en [https://cleanest.readthedocs.io/en/latest/installation.html ](https://cleanest.readthedocs.io/en/latest/installation.html)


```{code-cell} ipython3
import astroalign as aa 
````

Transformamos la imagen con esta utilidad 

```{code-cell} ipython3
# To transform the image (align & rotate) using the reference image 
registered_image, footprint = aa.register(original, reference)
````

```{figure} /_static/lecture_specific/p2_fotometria/p2_07_aligning_2.png
---
width: 800px
name: aligning-2-fig
---
La imagen transformada coincide perfectamente con la que tomamos de referencia.
```

Podemos ver qué transformación se ha realizado,

```{code-cell} ipython3
p, (pos_img, pos_img_rot) = aa.find_transform(original, reference)
print("Rotation: {:.2f} degrees".format(p.rotation * 180.0 / np.pi))
print("\nScale factor: {:.2f}".format(p.scale))
print("\nTranslation: (x, y) = ({:.2f}, {:.2f})".format(*p.translation))
print("\nTranformation matrix:\n{}".format(p.params))
print("\nPoint correspondence:")
for (x1, y1), (x2, y2) in zip(pos_img, pos_img_rot):
    print("({:.2f}, {:.2f}) in source --> ({:.2f}, {:.2f}) in target"
          .format(x1, y1, x2, y2))
````

<pre>
Rotation: 17.88 degrees
Scale factor: 1.00
Translation: (x, y) = (45.33, -284.58)
Tranformation matrix:
[[   0.95318451   -0.30753652   45.33333586]
 [   0.30753652    0.95318451 -284.58026185]
 [   0.            0.            1.        ]]

Point correspondence:
(222.70, 577.92) in source --> (79.88, 335.14) in target
(666.64, 758.36) in source --> (447.69, 642.81) in target
(315.09, 719.98) in source --> (124.39, 498.49) in target
(764.40, 687.24) in source --> (562.19, 606.04) in target
(400.82, 177.33) in source --> (373.03, 8.08) in target

(115.49, 401.06) in source --> (31.76, 133.68) in target
(655.55, 434.77) in source --> (537.20, 332.10) in target
(362.49, 607.05) in source --> (204.21, 405.34) in target
(400.54, 741.97) in source --> (199.16, 545.82) in target
</pre>

Como esperábamos el factor de escala es la unidad porque proceden de la misma configuración instrumental. En la transformación ha tenido que rotar un ángulo de 18 grados aproximadamente. Se muestra en el listado la matriz de transformación aplicada. Finalmente se listan las fuentes empleadas para realizar el ajuste.

Podemos mostrar algunas de las estrellas identificadas (véanse los detalles en el cuaderno de jupyter)

```{figure} /_static/lecture_specific/p2_fotometria/p2_07_aligning_3.png
---
width: 800px
name: aligning-3-fig
---
Las estrellas usadas etiquetadas en colores para que sea fácil encontrarlas en cada una de las imagenes.
```
Y guardamos el resultado

```{code-cell} ipython3
# A new FITS file to contain the registered image is created 
hdu = fits.PrimaryHDU(registered_image)
hdul = fits.HDUList([hdu])
hdul.writeto('afztucmP_0044.fits') # A warning raises when the file already exits

# We use the original image header 
update('afztucmP_0044.fits', registered_image, original_header)
````

