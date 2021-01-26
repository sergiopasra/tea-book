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


# Combinación de imágenes
Las observaciones que estamos procesando se fraccionaron en 3 observaciones individuales. Podemos combinar el resultado en una imagen final que contenga la señal de las tres observaciones.

Veamos el caso de NGC4941 observada en banda R en tres exposiciones de 300s (fzt_ALrd120110.fits, fzt_ALrd120111.fits, fzt_ALrd120112.fits).

```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_1.png
---
width: 800px
name: combining-1-fig
---
Imágenes de las tres observaciones de NGC4941 en banda R.  Se muestran las imágenes completas.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_2.png
---
width: 800px
name: combining-2-fig
---
Imágenes de las tres observaciones de NGC4941 en banda R.  Se muestra una zona ampliada con el zoom de DS9 y se registran las imágenes de acuerdo a su posición de imagen (píxeles). 
```
Se precia en esta visualización que las estrellas no aparecen en los mísmos píxeles ya que se movió un poco el apuntado entre exposiciones para lograr este efecto.

```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_3.png
---
width: 800px
name: combining-3-fig
---
Imágenes de las tres observaciones de NGC4941 en banda R.  Se muestra una zona ampliada con el zoom de DS9 y se registran las imágenes de acuerdo a sus coordenadas  WCS (World Coordinate System). 
```
En este caso las imágenes FITS tienen determinada su astrometría desde el origen. Por lo tanto si hacemos coincidir por coordenadas WCS (World Coordinate System) si coinciden. Esto es de gran ayuda a la hora de combinar las imágenes en una sola.

Siguiendo el cuaderno de Jupyter ccdproc_07_Combining podemos representar las imágenes de la forma habitual

```{code-cell} ipython3
sky_mean , std = [] , []
fig, axarr = plt.subplots(ncols=3, nrows=1, figsize=(12, 12))
for n in range(3):
    ax = axarr[n]
    ax.imshow(image[n].data, cmap='gray', origin='lower',vmin=1000, vmax=5000,norm=LogNorm())
    ax.text(200,200,n,fontsize=15,color="w")
    ax.set_xlabel('X axis')
    mean_n,std_n = draw_rectangle(ax, image[n].data, 100, 500, 1500, 1900, color='w',text=True)
    print(n,int(mean_n),int(std_n))
    sky_mean.append(mean_n)
    std.append(std_n)
    ax.grid()
````
<pre>
0 1705 95
1 1300 97
2 1323 104
</pre>


```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_4.png
---
width: 800px
name: combining-4-fig
---
Imágenes de las tres observaciones de NGC4941 en banda R y estadística en una región de la esquina de la imagen. La primera imagen tiene más señal en el fondo de cielo. 
```

Pero también podemos representar los ejes de las imágenes en coordenadas celestes. Para ello se necesita el paquete  [WCS](https://docs.astropy.org/en/stable/wcs/) de ``astropy``.

```{code-cell} ipython3
from astropy.wcs import WCS
```

```{code-cell} ipython3
fig = plt.subplots(figsize=(14, 12))
for n in range(3):
    ax1 = plt.subplot(1,3,n+1, projection=WCS(headers[n]))
    ax1.imshow(image[n].data, origin='lower', vmin=1000., vmax=5000.)
    ax1.coords['ra'].set_axislabel('Right Ascension')
    ax1.coords['dec'].set_axislabel('Declination')
    plt.grid(color='w')
    ax1.set_title(headers[n]['FILENAME'])
```


```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_5.png
---
width: 800px
name: combining-5-fig
---
Imágenes de las tres observaciones de NGC4941 en banda R usando ejes de coordenadas ecuatoriales ya que las imágenes tienen astrometría y descriptores WCS en la cabecera. Las imágenes están alineadas en esta forma de gráfico ya que usamos la transformación pixel a coordenadas celestes.
````

### Reproyectando las imágenes.

Vamos a usar [``reproject``](https://reproject.readthedocs.io/en/stable/) para poner las tres imágenes en un marco común. Este comando usa la información astrométrica de las cabeceras (WCS) y asume que la astrometría es correcta. Se usa para comparar observaciones hechas con distintos instrumentos con diferentes campos de visión, escalas de placa, orientaciones y distintos rangos espectrales. Por ejemplo no sería útil para comparar una imagen H$\alpha$ obtenida en nuestro proyecto con otra observación de la misma galaxia en banda R recuperada de un archivo.

En nuestro caso el problema es más sencillo porque las imágenes están obtenidas consecutivamente con la misma instrumentación. Las diferencias son la variación de apuntado de telescopio al que se le aplicaron pequeños desplazamientos ('offsets') entre las tomas. Esto es una práctica habitual para precisamente hacer que la combinación de imágenes resuelva problemas cosméticos del chip.

```{code-cell} ipython3
from reproject import reproject_interp
```
Reproyectamos la segunda y tercera imagen a la referencia de la primera (image[0].header)

```{code-cell} ipython3
n_image_1, footprint = reproject_interp(image[1], image[0].header)
n_image_2, footprint = reproject_interp(image[2], image[0].header)
```
Representamos la imagen original y las reproyectadas usando coordenadas WCS.  
Nótese que en todas ellas usamos la astrometría de la primera imagen projection=WCS(headers[0])

```{code-cell} ipython3
fig = plt.subplots(figsize=(14, 12))

ax1 = plt.subplot(1,3,1, projection=WCS(headers[0]))
ax1.imshow(image[0].data, origin='lower', vmin=1000., vmax=5000.)
ax1.coords['ra'].set_axislabel('Right Ascension')
ax1.coords['dec'].set_axislabel('Declination')
plt.grid(color='w')
ax1.set_title(headers[0]['FILENAME'])

ax1 = plt.subplot(1,3,2, projection=WCS(headers[0]))
ax1.imshow(n_image_1, origin='lower', vmin=1000., vmax=5000.)
ax1.coords['ra'].set_axislabel('Right Ascension')
ax1.coords['dec'].set_axislabel('Declination')
plt.grid(color='w')
ax1.set_title(headers[1]['FILENAME'])

ax1 = plt.subplot(1,3,3, projection=WCS(headers[0]))
ax1.imshow(n_image_2, origin='lower', vmin=1000., vmax=5000.)
ax1.coords['ra'].set_axislabel('Right Ascension')
ax1.coords['dec'].set_axislabel('Declination')
plt.grid(color='w')
ax1.set_title(headers[1]['FILENAME'])
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_6.png
---
width: 800px
name: combining-6-fig
---
Tras realizar las transformaciones. 
```
Las nuevas imágenes presentas bandas blancas que indican que en esas regiones no tenemos medida (a la izquierda en la segunda imagen y ala izquierda y arriba en la tercera. En esos píxeles los valores son "nan" ('not a number'). Esas regiones no están cubiertas por las imágenes de la segunda y tercera observación ya que el apuntado del telescopio fue ligeramente desplazado ('offsets') por los observadores. 

```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_7.png
---
width: 800px
name: combining-7-fig
---
Las imágenes ya están alineadas en coordenadas de imagen (píxeles) y podemos combinarlas. 
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_8.png
---
width: 800px
name: combining-8-fig
---
Detalle de las imágenes para comprobar la bondad del alineado. Si nos fijamos en las estrellas parece que están en los mismos píxeles en todas las imágenes. 
```

El alineamiento no es perfecto. Para poderlo apreciar usaremos DS9. Por eso vamos primero a guardar las imágenes como ficheros FITS.

```{code-cell} ipython3
nimage_1 = image[1].copy()
nimage_1.data = n_image_1
nimage_1.header = image[0].header
nimage_1.header['FILENAME'] = 'nfzt_ALrd120111.fits' 
nimage_1.header['HISTORY'] = 'projected to fzt_ALrd120111.fits'
nimage_1.writeto(directory+'nfzt_ALrd120111.fits',overwrite='yes')
````
y lo mismo para la otra imagen n_image_2.
Ahora ya podemos cargarlas y mostrarlas con DS9 y si se hace zoom sobre una imagen de estrella y luego se utiliza el efecto de parpadeo (`blinking`) se nota un ligero desplazamiento entre ellas.

```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_9.png
---
width: 800px
name: combining-9-fig
---
Detalle de una imagen de estrella en las tres imágenes para comprobar que no están perfectamente alineadas.
```

Leemos y almacenamos las tres imágenes para crear una lista de objetos CCDData para combinar.

```{code-cell} ipython3
ccd = []
ccd.append(CCDData.read(directory+'fzt_ALrd120110.fits')) 
ccd.append(CCDData.read(directory+'nfzt_ALrd120111.fits',unit='adu')) 
ccd.append(CCDData.read(directory+'nfzt_ALrd120112.fits')) 
combiner = Combiner(ccd)
```

Usamos una función de escalado muestreando una parte de la imagen. Hacemos esto para evitar la estadística de toda la imagen que contiene píxeles con valor "nan". Podríamos usar máscaras pero este recurso nos saca del problema.

```{code-cell} ipython3
scaling_func = lambda arr: 1400/np.ma.average(arr[500:1000,1500:2000])
combiner.scaling = scaling_func 
print(combiner.scaling)
```
<pre>
[[[0.83099987]]

 [[1.08822194]]

 [[1.06939605]]]
</pre>

Podríamos usar un escalado introduciendo los valores de las estadísticas que hicimos antes. Los valores del escalado indican que la primera imagen tiene más señal y las dos siguientes son parecidas con un 20% más de valos aproximadamente. 

Combinamos 

```{code-cell} ipython3
# median combine 
combined_image_average_scaled = combiner.average_combine()
````
y lo visualizamos

```{code-cell} ipython3
fig = plt.figure(figsize=(14, 12))
ax0 = fig.add_subplot(131)
box = combined_image_average_scaled.data
img = ax0.imshow(box, cmap='gray', origin='lower',vmin=1300, vmax=2000,norm=LogNorm())
ax0.grid(color='w')
ax1 = fig.add_subplot(132)
box = combined_image_average_scaled.data[1200:1500,1000:1300]
img = ax1.imshow(box, cmap='gray', origin='lower',vmin=1300, vmax=2000,norm=LogNorm())
ax1.grid(color='w')
ax2 = fig.add_subplot(133)
box = ccd[0].data[1200:1500,1000:1300]
img = ax2.imshow(box, cmap='gray', origin='lower',vmin=1300, vmax=2000,norm=LogNorm())
ax2.grid(color='w')
````

```{figure} /_static/lecture_specific/p2_fotometria/p2_06_combining_10.png
---
width: 800px
name: combining-10-fig
---
Imágenes completa combinada (izquierda) y detalle de la combinación (centro) junto a detalle de la misma región en la primera imagen.
```

