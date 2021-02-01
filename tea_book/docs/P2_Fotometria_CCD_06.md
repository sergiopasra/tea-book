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


# Fotometría de las estrellas estándar
La observación de estrellas estándar tiene como objetivo tener referencias en flujo que nos permitan pasar de cuentas/s a flujo. El primer paso de la calibración es medir precisamente cuanta señal (cuentas/s) tenemos en las imágenes de las estrellas. Para ello usamos las imágenes calibradas con la reducción de los pasos anteriores.

## Fotometría con Photutils

Hagamos un ejemplo con las tres primeras observaciones de la serie de la primera noche de observación (NOT_2008). Mirando el cuaderno de observaciones vemos que son imágenes de HZ44 en banda R y en una banda estrecha. 

```{code-cell} ipython3
directory='NOT_2008_N1/'
files = ['120077','120078','120079']       # fzt_ALrd+files[i]
````


```{code-cell} ipython3
image = []
for i in range(len(files)):
    image.append(fits.open(directory+'fzt_ALrd'+str(files[i])+'.fits')[0])
for i in range(len(files)):
    print(image[i].header['FILENAME'],image[i].header['OBJECT'],image[i].header['EXPTIME'])
```    

<pre>
fzt_ALrd120077.fits HZ44 R 5.0
fzt_ALrd120078.fits HZ44 R 5.0
fzt_ALrd120079.fits HZ44 #79 50.0
</pre>

```{figure} /_static/lecture_specific/p2_fotometria/p2_08_star_phot_1.png
---
width: 800px
name: star-phot-1-fig
---
Las tres primeras observaciones de estrellas estándar.
```
Podemos buscar HZ44 en [SIMBAD](http://simbad.u-strasbg.fr/simbad/sim-id?Ident=HZ44) que nos ofrece una pantalla de [ALADIN](http://simbad.u-strasbg.fr/simbad/sim-id?Ident=HZ44) cuyo campo de visión (muy estrecho al principio) puede ser ampliado. Reconocemos fácilmente el campo y de esa forma comprobamos que nuestra estrella estándar es precisamente la del centro de nuestra imagen.

```{figure} /_static/lecture_specific/p2_fotometria/p2_08_star_phot_2.png
---
width: 400px
name: star-phot-2-fig
---
El campo centrado en HZ44 buscado en SIMBAD y mostrado con ALADIN.
```
Este comprobación es necesaria ya que aunque apuntemos el telescopio a la estrella estandar con las coordenadas de catálogo, alguna estrella tiene un movimiento propio grande y su imagen no aparece en el centro.

Es interesante apreciar que necesitamos exposiciones más largas en el filtro estrecho ya que la banda de paso es menor.

### Localizando las posiciones de las estrellas 
Podemos buscar las coordenadas de la estrella usando ``find_peaks()`` una función de ``Photutils`` para encontrar máximos locales en una imagen. Hay que definir un nivel de umbral y la función devuelve la posición de las imágenes con píxeles con valores por encima de ese valor. La función es inteligente para encontrar fuentes separadas y no listar varias posiciones para el mismo objeto. 

Tomemos la primera imagen como ejemplo y usemos la función con un umbral muy alto porque sólo queremos detectar las estrellas muy brillantes del campo. Lo hemos construido con la mediana + 500 veces la desviación estándar. 


```{code-cell} ipython3
ximage = image[0].data
mean, median, std = sigma_clipped_stats(ximage, sigma=3.0)
threshold = median + (500. * std)
tbl = find_peaks(ximage, threshold, box_size=40)
tbl['peak_value'].info.format = '%.8g'  # for consistent table output
print(tbl[:10])  # print only the first 10 peaks
```    
<pre>
x_peak y_peak peak_value
------ ------ ----------
   378    434  5473.2654
  1022    964  10068.373
  1462   1112  18964.459
  1797   1282  4085.3169
</pre>

De las cuatro fuentes detectadas la nuestra HZ44 es la que está más en el centro de la imagen, es decir la segunda.

Mostramos otra vez la imagen y las aperturas sobre ella. Estas aperturas se han fabricado en las posiciones de los máximos encontrados por ``find_peaks`` y con un radio de 30 píxeles.

```{code-cell} ipython3
fig = plt.figure(figsize=(9, 9))
radius = 30
vmin, vmax = 10, 1200
positions = np.transpose((tbl['x_peak'], tbl['y_peak']))
apertures = CircularAperture(positions, r=radius)
plt.imshow(ximage, cmap='gray', origin='lower',vmin=vmin, vmax=vmax , norm=LogNorm())
plt.grid()
apertures.plot(color='red', lw=1.5)
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_08_star_phot_3.png
---
width: 500px
name: star-phot-3-fig
---
Las aperturas de 30 píxeles de radio centradas en las posiciones encontradas por ``find_peaks``.
```
#### Midiendo en las aperturas
Podemos realizar ya la medida de flujo (en cuentas) en esas aperturas

```{code-cell} ipython3
phot_table = aperture_photometry(ximage, apertures)
phot_table['aperture_sum'].info.format = '%.4g'  # for consistent table output
print(phot_table)
````
<pre>
id xcenter ycenter aperture_sum
      pix     pix               
--- ------- ------- ------------
  1   378.0   434.0    8.854e+05
  2  1022.0   964.0    1.467e+06
  3  1462.0  1112.0    2.401e+06
  4  1797.0  1282.0    5.808e+05
</pre>
Es decir que el flujo en la apertura centrada en nuestra estrella HZ44 (la segunda en esta tabla) es de 1.467e+06 cuentas. Claro la mayor parte son de la estrella pero hay una contribución del fondo de cielo que debemos restar.

### Estimación del fondo de cielo
Una manera sería usar aperturas similares cercanas a la imagen de la estrella en regones libres de otras fuentes. Podemos hacer un listado de posiciones y aperturas de forma manual. Por ejemplo en otra estrella y en dos zonas libres cerca de la estrella problema que servirían para determinar fondo de cielo. 

```{code-cell} ipython3
positions_new = [(560, 440), (1000, 750), (800, 1000)]
```

```{code-cell} ipython3
fig = plt.figure(figsize=(9, 9))
radius = 30
vmin, vmax = 10, 1200
positions = np.transpose((tbl['x_peak'], tbl['y_peak']))
apertures = CircularAperture(positions, r=radius)
plt.imshow(ximage, cmap='gray', origin='lower',vmin=vmin, vmax=vmax , norm=LogNorm())
plt.grid()
apertures.plot(color='red', lw=1.5)
apertures_new = CircularAperture(positions_new, r=radius)
apertures_new.plot(color='yellow', lw=1.5)
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_08_star_phot_4.png
---
width: 500px
name: star-phot-4-fig
---
Las aperturas de 30 píxeles de radio centradas en las posicones encontradas por ``find_peaks`` y las añadidas manualmente.
```

```{code-cell} ipython3
phot_table = aperture_photometry(ximage, apertures_new)
phot_table['aperture_sum'].info.format = '%.4g'  # for consistent table output
print(phot_table)
```
<pre>
id xcenter ycenter aperture_sum
      pix     pix               
--- ------- ------- ------------
  1   560.0   440.0    5.519e+05
  2  1000.0   750.0    1.008e+05
  3   800.0  1000.0    9.981e+04
</pre>

El fondo de cielo es de unas 100000 cuentas. Entonces las cuentas netas de HZ44 serían 1.467e+06 - 1e+05 = 1.367e+06 cuentas.

Otra forma de determinar el fondo de cielo de forma global es usar la mediana de la imagen completa o mejor de una zona libre de objetos cerca de nuestra estrella.

```{code-cell} ipython3
median     = np.median(ximage)
median_sky = np.median(ximage[1000:1250,250:500])
print('median', median, ' sky ', median_sky)
````
<pre>
median 35.73486368629405  sky  34.7267088174489
</pre>
Unas 34.7 cuentas/pixel aproximadamente. Podemos usar esta estimación del fondo de cielo para determinar las cuentas netas de HZ44.

```{code-cell} ipython3
bkg = median_sky
phot_table = aperture_photometry(ximage - bkg, apertures) 
phot_table['aperture_sum'].info.format = '%.4g'  # for consistent table output
print(phot_table)
```

<pre>
id xcenter ycenter aperture_sum
      pix     pix               
--- ------- ------- ------------
  1   378.0   434.0    7.872e+05
  2  1022.0   964.0    1.368e+06
  3  1462.0  1112.0    2.302e+06
  4  1797.0  1282.0    4.826e+05
  </pre>
  
  Y llegamos a un valor parecido al de antes 1.368e+06 cuentas netas.

### Usando múltiples aperturas
Es posible definir varias aperturas centradas en la misma posición. Tradicionalmente se usaba este método para lograr el valor asintótico de las cuentas según vamos aumentando el radio.

Podemos hacer un ejemplo usando cuatro aperturas centradas en HZ44. Nos aseguramos de que es la segunda en esta lista 

```{code-cell} ipython3
print(apertures)
HZ44_pos = positions[1]
print(HZ44_pos)
````
<pre>
Aperture: CircularAperture
positions: [[ 378.,  434.],
            [1022.,  964.],
            [1462., 1112.],
            [1797., 1282.]]
r: 30.0
[1022  964]
</pre>

```{code-cell} ipython3
radii = [10., 20., 30., 40.]
apertures = [CircularAperture(HZ44_pos, r=r) for r in radii]
phot_table = aperture_photometry(ximage, apertures)
for col in phot_table.colnames:
     phot_table[col].info.format = '%.5g'  # for consistent table output
print(phot_table)
```

<pre>
id xcenter ycenter aperture_sum_0 aperture_sum_1 aperture_sum_2 aperture_sum_3
      pix     pix                                                              
--- ------- ------- -------------- -------------- -------------- --------------
  1    1022     964     1.0696e+06      1.364e+06     1.4665e+06      1.559e+06
</pre>
Nuestra tabla sólo tiene una fila porque hemos decidido medir sólo una estrella.

### Local Background Subtraction
La fotometría de apertura suele usar una estimación del fondo de cielo en un anillo circular cerca de la estrella pero lo suficientemente alejado para mo incluir las alas de la imagen. Por ejemplo usamos una apertura de 30 píxeles para medir el flujo de la estrella (en bruto) y un anillo de radios interior y exterior de 50 y 70 píxeles para estimar el fondo de cielo.

```{code-cell} ipython3
aperture = CircularAperture(HZ44_pos, r=30)
annulus_aperture = CircularAnnulus(HZ44_pos, r_in=50., r_out=70.)
plt.figure(figsize=(14,9))
plt.imshow(ximage, cmap='gray', origin='lower', vmin=vmin, vmax=vmax , norm=LogNorm())
aperture.plot(color='yellow', lw=1)
annulus_aperture.plot(color='red', lw=1)
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_08_star_phot_5.png
---
width: 500px
name: star-phot-5-fig
---
Apertura y anillo centrado en HZ44 para medir el flujo y estimar el fondo de cielo.
```

```{code-cell} ipython3
apers = [aperture, annulus_aperture]
phot_table = aperture_photometry(ximage, apers)
for col in phot_table.colnames:
    phot_table[col].info.format = '%.8g'  # for consistent table output
print(phot_table)
````
<pre>
id xcenter ycenter aperture_sum_0 aperture_sum_1
      pix     pix                                
--- ------- ------- -------------- --------------
  1    1022     964      1466526.3      273523.19
</pre>
Hemos elegido aperturas que tienen diferente área y por lo tanto no podemos restar directamente. Debemos escalar el fondo de cielo a una apertura como la que usamos para medir la estrella.

```{code-cell} ipython3
print(aperture.area, annulus_aperture.area)
````
<pre>
2827.4333882308138 7539.822368615503
</pre> 

```{code-cell} ipython3
bkg_mean = phot_table['aperture_sum_1'] / annulus_aperture.area
bkg_sum  = bkg_mean * aperture.area
final_sum = phot_table['aperture_sum_0'] - bkg_sum
phot_table['residual_aperture_sum'] = final_sum
phot_table['residual_aperture_sum'].info.format = '%.8g'  
print(phot_table['residual_aperture_sum'])  
````
<pre>
residual_aperture_sum
            1363955.1
</pre>

Nótese que hemos generado una columna más en la tabla 'residual_aperture_sum' con el valor neto de cuentas.

```{code-cell} ipython3
for col in phot_table.colnames:
    phot_table[col].info.format = '%.8g'  # for consistent table output
print(phot_table)
````
<pre>
id xcenter ycenter aperture_sum_0 aperture_sum_1 residual_aperture_sum
      pix     pix                                                      
--- ------- ------- -------------- -------------- ---------------------
  1    1022     964      1466526.3      273523.19             1363955.1
</pre>
La última columna tiene en flujo neto en cuentas que es igual al que hemos encontrado antes con otro tipo de estimaciones del fondo de cielo.

Podemos repetir el proceso para la segunda observación de HZ44 para verlo de forma más compacta.


```{code-cell} ipython3
ximage = image[1].data
mean, median, std = sigma_clipped_stats(ximage, sigma=3.0)
threshold = median + (500. * std)
tbl = find_peaks(ximage, threshold, box_size=40)
tbl['peak_value'].info.format = '%.8g'  # for consistent table output
print(tbl[:10])  # print only the first 10 peaks
```
<pre>
x_peak y_peak peak_value
------ ------ ----------
  1354    158  5152.9339
   377    433  12810.798
   558    440  7772.4841
  1021    962  25675.776
  1462   1111  39351.295
  1796   1281  8302.7578
</pre>

```{code-cell} ipython3
positions = np.transpose((tbl['x_peak'], tbl['y_peak']))
apertures = CircularAperture(positions, r=radius)

print(apertures)
HZ44_pos = positions[3]
print(HZ44_pos)
````
<pre>
Aperture: CircularAperture
positions: [[1354.,  158.],
            [ 377.,  433.],
            [ 558.,  440.],
            [1021.,  962.],
            [1462., 1111.],
            [1796., 1281.]]
r: 30.0
[1021  962]
</pre>

```{code-cell} ipython3
aperture = CircularAperture(HZ44_pos, r=30)
annulus_aperture = CircularAnnulus(HZ44_pos, r_in=50., r_out=70.)

apers = [aperture, annulus_aperture]

phot_table = aperture_photometry(ximage, apers)
for col in phot_table.colnames:
    phot_table[col].info.format = '%.8g'  # for consistent table output
print(phot_table)
````
<pre>
 id xcenter ycenter aperture_sum_0 aperture_sum_1
      pix     pix                                
--- ------- ------- -------------- --------------
  1    1021     962      1483541.9      275957.24
</pre>

```{code-cell} ipython3
bkg_mean = phot_table['aperture_sum_1'] / annulus_aperture.area
bkg_sum  = bkg_mean * aperture.area
final_sum = phot_table['aperture_sum_0'] - bkg_sum
phot_table['residual_aperture_sum'] = final_sum

for col in phot_table.colnames:
    phot_table[col].info.format = '%.8g'  # for consistent table output
print(phot_table)
````
<pre>
id xcenter ycenter aperture_sum_0 aperture_sum_1 residual_aperture_sum
      pix     pix                                                      
--- ------- ------- -------------- -------------- ---------------------
  1    1021     962      1483541.9      275957.24               1380058
</pre>

Que es un valor similar al encontrado en la primera observación de HZ44

<pre>
 id xcenter ycenter aperture_sum_0 aperture_sum_1 residual_aperture_sum
      pix     pix                                                      
--- ------- ------- -------------- -------------- ---------------------
  1    1022     964      1466526.3      273523.19             1363955.1
</pre>

Resumiendo
<pre>
fzt_ALrd120077.fits HZ44 R 5.0    1363955.1 c / 5s = 272791.02 c/s  
fzt_ALrd120078.fits HZ44 R 5.0    1380058   c / 5s = 276011.6  c/s 
</pre>


## Fotometría con DS9
DS9 permite hacer una medida de flujos dentro de regiones que pueden ser creadas del tamaño que queramos y centradas en nuestros puntos de interés. La creación de regiones es sencilla simplemente pinchando con el cursor en el lugar que queramos. En el menú se puede cambiar la forma geométrica de la región. Además con un doble click sobre la región obtenemos la información de sus parámetros que puede editarse para cambiarlos a nuestra elección. Es fácil cuando se ha hecho una vez. 

En el ejemplo que mostramos se ha cargado la imagen fzt_ALrd120077.fits y se han creado tres regines circulares del mismo radio (40 píxeles) 


```{figure} /_static/lecture_specific/p2_fotometria/p2_09_ds9_phot_1.png
---
width: 500px
name: ds9-phot-1-fig
---
Captura de DS9 con tres regiones circulares de 40 píxeles de radio creadas para medir el flujo de HZ44 y de fondo de cielo adyacente.
```
Con el menú de análisis podemos mostrar la estadística de esas regiones.

```{figure} /_static/lecture_specific/p2_fotometria/p2_09_ds9_phot_2.png
---
width: 700px
name: ds9-phot-2-fig
---
Estadística de suma de cuentas en las regiones mostradas en la figura anterior.
```
<pre>
 reg   net_counts     error     area          pixeles
---- ------------ ---------  ---------       ---------
   1  1558695.609  1248.477  65098080000.00    5023
   2   179693.232   423.902  65214720000.00    5032 
   3   183289.369   428.123  65136960000.00    5026 
</pre>

Si se selecciona en las opciones de "region" al cear o modificar una region te proporciona la estadística como vemos en la siguiente captura.


```{figure} /_static/lecture_specific/p2_fotometria/p2_09_ds9_phot_3.png
---
width: 800px
name: ds9-phot-3-fig
---
Menú desplegado de "region" para mostrar la opción de auto estadística y pantallas con las estadísticas generadas al modificar las regiones.
```
Para la región centrada en HZ44 tenemos, por ejemplo,

<pre>
center=1189.5206 1199.5732
image

reg  sum     error     area      surf_bri      surf_err
                       (pix**2)  (sum/pix**2)  (sum/pix**2)
1  179693.23 423.90239 5032      35.710102     0.084241333

reg sum     npix  mean      median    min       max        var       stddev    rms 
1 179693.23 5032  35.710102 35.52132  6.2430902 82.270042  62.149973 7.8835254 36.569951
</pre>

Es decir 179693.23 cuentas en cielo en un área de 5032 pixeles lo que supone 35.7 cuentas/pixel. Y para la apertura centrada en la estrella.

<pre>
center=1024.0151 964.87335
image

reg  sum     error     area      surf_bri      surf_err
                       (pix**2)  (sum/pix**2)  (sum/pix**2)
1  1558695.6 1248.4773 5023      310.31169     0.24855212
reg sum     npix  mean      median    min       max        var       stddev    rms 
1 1558695.6 5023  310.31169 53.757399 12.027513 10068.373 1006073.9 1003.0324 1049.9368
</pre>

Ahora la estadística de cuentas/pixel no nos sirve de mucho como tampoco la varianza o la desviación estándard ya que hay mucha variación en esa apertura. Pero sí es interesante ver que el máximo de cuentas en la estrella es de 10068 o sea que la imagen no está saturada. 

Resumiendo tenemos 1558695.6 cuentas brutas (estrella + cielo) y 179693.23 cuentas en el cielo. Luego el flujo neto de HZ44 en esta observación es 1558695.6 - 179693.23 = 1379002.37 cuentas en 5s de observación que es un valor similar al que encontramos con ``Photutils``

<pre>
fzt_ALrd120077.fits HZ44 R 5.0    Photutils  1363955.1  c / 5s = 272791.02 c/s    
fzt_ALrd120077.fits HZ44 R 5.0    DS9        1379002.37 c / 5s = 275800.5 c/s
</pre>

