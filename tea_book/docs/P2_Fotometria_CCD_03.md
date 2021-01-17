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


# Correción de Flat Field 


## Generación de un máster flat field por filtro
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

## Corrigiendo de variación espacial de sensibilidad 
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
```

<pre>
      file       
   flat_N1_78.fits
zt_ALrd120021.fits
zt_ALrd120023.fits
zt_ALrd120024.fits
......
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
```

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
sci_list_78 = sci_list_78[19:26]
print(sci_list_78)
````
<pre>
   file       
zt_ALrd120067.fits
zt_ALrd120068.fits
zt_ALrd120073.fits
zt_ALrd120074.fits
zt_ALrd120079.fits
zt_ALrd120083.fits
zt_ALrd120087.fits
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
Las líneas del final de la cabecera de las imágenes corregidas tienen información del procesado hasta ahora, incluyendo el recorte, la substracción del BIAS y la corrección de Flat Field.
```

Análogamente para los otros filtros,

```{code-cell} ipython3
matches = (ic1.summary['FBFLTID'] == 49)
sci_list_49 = ic1.summary['file'][matches]
print(sci_list_49)
sci_list_49 = sci_list_49[19:27]
print(sci_list_49)
```

```{code-cell} ipython3
for file in sci_list_49:
    image = CCDData.read(directory+file)
    f_image = ccdproc.flat_correct(image,master_flat_49)
    name_of_file = 'f'+ str(image.header['FILENAME'])
    f_image.header['FILENAME']  = name_of_file
    f_image.header['HISTORY']   = str(datetime.datetime.now())[0:18]+' astropy ccdproc flat_correct '
    f_image.header['HISTORY']   = 'using NOT2008/N1/master_flat_49.fits master FLAT' 
    print('writting '+name_of_file+ ' in '+directory)
    f_image.write(directory+name_of_file,overwrite='yes')
```

```{code-cell} ipython3
matches = (ic1.summary['ALFLTID'] == 76)
sci_list_76 = ic1.summary['file'][matches]
print(sci_list_76)
sci_list_76 = sci_list_76[17:41]
print(sci_list_76)
```

```{code-cell} ipython3
for file in sci_list_76:
    image = CCDData.read(directory+file)
    f_image = ccdproc.flat_correct(image,master_flat_76)
    name_of_file = 'f'+ str(image.header['FILENAME'])
    f_image.header['FILENAME']  = name_of_file
    f_image.header['HISTORY']   = str(datetime.datetime.now())[0:18]+' astropy ccdproc flat_correct '
    f_image.header['HISTORY']   = 'using NOT2008/N1/master_flat_76.fits master FLAT' 
    print('writting '+name_of_file+ ' in '+directory)
    f_image.write(directory+name_of_file,overwrite='yes')
 ```

Una vez acabado este paso despejamos el directorio de trabajo moviendo los ficheros recortados y corregidos de BIAS ("zt_*") a un subdirectorio auxiliar que llamamos 2_corregidos_bias.

<pre>
N1 $> mkdir 2_corregidos_bias
N1 $> mv zt_* 2_corregidos_bias
</pre>

quedando nuestro directorio de trabajo,
<pre>
N1 $ ls
0_originales        fzt_ALrd120070.fits fzt_ALrd120081.fits fzt_ALrd120091.fits fzt_ALrd120111.fits
1_recortados        fzt_ALrd120071.fits fzt_ALrd120082.fits fzt_ALrd120095.fits fzt_ALrd120112.fits
2_corregidos_bias   fzt_ALrd120072.fits fzt_ALrd120083.fits fzt_ALrd120096.fits fzt_ALrd120116.fits
flat_N1_49.fits     fzt_ALrd120073.fits fzt_ALrd120084.fits fzt_ALrd120097.fits fzt_ALrd120117.fits
flat_N1_76.fits     fzt_ALrd120074.fits fzt_ALrd120085.fits fzt_ALrd120102.fits fzt_ALrd120118.fits
flat_N1_78.fits     fzt_ALrd120075.fits fzt_ALrd120086.fits fzt_ALrd120103.fits zero_N1.fits
fzt_ALrd120066.fits fzt_ALrd120077.fits fzt_ALrd120087.fits fzt_ALrd120104.fits
fzt_ALrd120067.fits fzt_ALrd120078.fits fzt_ALrd120088.fits fzt_ALrd120105.fits
fzt_ALrd120068.fits fzt_ALrd120079.fits fzt_ALrd120089.fits fzt_ALrd120106.fits
fzt_ALrd120069.fits fzt_ALrd120080.fits fzt_ALrd120090.fits fzt_ALrd120110.fits
</pre>


Podemos y denbemos ver el resultado del procesado por si hay algún error muy evidente. 

```{figure} /_static/lecture_specific/p2_fotometria/p2_05_flats_10.png
---
width: 800px
name: flats-10-fig
---
Flat field en el filtro #76, una imagen original y la misma imagen corregida. Se han corregido efectos aparentes en la variación espacial de la sensibilidad y se nota que el fondo se ha aplanado.
```
