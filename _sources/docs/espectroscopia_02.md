# Elección del espectrógrafo y configuración instrumental
De entre todas las diferentes modelos de espectrógrafos, describiremos brevemente los espectrógrafos cuyas observaciones usaremos en estas prácticas. 

## Espectroscopía de rendija larga
Estos espectrógrafos de rendija larga ('long slit') disponen de una sóla rendija alargada, es decir que la altura es mucho mayor que la anchura. Estos instrumentos se colocan sobre rotadores de manera que se pueden girar a cualquier ángulo de posición (PA) para conseguir alinear la rendija con el objeto cuyo espectro deseamos obtener. En el caso de un objeto extenso podemos obtener el espectro de diferentes regiones del mismo o podemos meter en la rendija varios objetos alineados. Hay una relación directa entre posición en la rendija y posición del espectro en la imagen espectroscópica por lo que podemos saber a qué región corresponde cada espectro. En las zonas libres de objetos celestes se registra el espectro del fondo de cielo.

```{figure} /_static/lecture_specific/espectroscopia/spec_14_rendija_larga_1.png
---
width: 800px
name: larga_1-fig
---
Esquema de la rendija que ha sido colocada de manera que la luz de tres estrellas alineadas entra en el espectrógrafo. En la derecha la imagen espectral en el plano focal del espectrógrafo ilustrando los espectros de las tres estrellas y del cielo entre ellas.
```
Las ventajas son evidentes ya que por una parte ahorramos tiempo de observación (varios objetos + cielo en al misma observación) y es fácil la determinación de variaciones espaciales porque los espectros son comparables al ser la observación simultánea. En realidad en una forma de espectroscopía multiobjeto pero con claras limitaciones.


```{figure} /_static/lecture_specific/espectroscopia/spec_15_rendija_larga_2.png
---
width: 800px
name: larga_2-fig
---
Ejemplo de observación con espectrógrafo de rendija larga donde se muestra la imagen de las galaxias observadas junto a la rendija utilizada (izda.). En los espectros de la derecha se aprecian los espectros de diferentes objetos o regiones de una galaxia en la dirección espacial (a lo largo de la rendija).
```

### Ejemplo de elección de configuración para IDS

Los espectrógrafos de red plana suelen tener varias redes de diferente paso y pueden tener varias cámaras para lograr diferentes dispersiones. Con estos espectrógrafos podemos abordar proyectos científicos que requieran diferentes configuraciones en cuanto a intervalo espectral, dispersión, resolución etc.

En la práctica de espectroscopía de rendija larga se usan observaciones conseguidas con el IDS ['Intermediate Dispersion Spectrograph'](https://www.ing.iac.es/astronomy/instruments/ids/) del telescopio INT (Isaac Newton Telescope) del Observatorio del Roque de los Muchachos en la isla de la Palma. Es un espectrógrafo veterano que ahora se ofrece sólo en la configuración de la cámara más luminosa (menos dispersiva) pero que dispone de dos cámaras de focales 235 y 500 mm.

```{figure} /_static/lecture_specific/espectroscopia/spec_16_IDS_table_235.gif
---
width: 800px
name: IDS_table_235-fig
---
Parámetros del espectrógrafo IDS para la cámara de 235mm. 
```


```{figure} /_static/lecture_specific/espectroscopia/spec_17_IDS_table_500.gif
---
width: 800px
name: IDS_table_500-fig
---
Parámetros del espectrógrafo IDS para la cámara de 500mm. 
```

Veamos un ejemplo que nos ayude a comprender la utilidad de estas tablas. Supongamos un proyecto científico que requiere espectros de galaxias en el intervalo espectral 6000-7500 Å y que disponemos de tiempo de observación en el IDS. Supongamos que se dispone de dos detectores CCD posibles el TEK#5 (1024 píxeles de 24$\mu m$) y el EEV4280 (2048 píxeles de 13$\mu m$). 

Como está colocado en el foco Cassegrain del INT (de 2.5m de diámetro) que tiene relación focal f/15, la focal del telescopio es $f = 2.5 \times 15 = 38.130 m$. Por lo tanto su escala de placa es $P = 206265 / 38130 = 5.41 arcsec/mm $. Ya hemos visto que las cámaras del IDS son de $f_2^a = 235mm$ y $f_2^b = 500mm$ mientras que el colimador es de $f_1 = 1275mm$. El factor de amplificación $f_2 / f_1$ se puede calcular con esta información y nos permite determinar el tamaño de la rendija proyectada en el plano focal del espectrógrafo. Esa información está en las tablas mostradas anteriormente. 

Como la región espectral es la zona roja del espectro elegiremos una red optimizada en esas longitudes de onda. En la codificación de los nombres de las redes del IDS son las que su nombre termina por R. De entre las opciones elegimos R600R donde 600 significa que tiene un tallado de 600 trazos/mm (en la tabla es la columna de 'ruling'). Vemos que está optimizada al rojo ($\lambda_b = 6700 Å$) y que porporciona con la cámara de 235mm una dispersión lineal recíproca de 69.8 Å/mm. 

Veamos ahora si el intervalo espectral encaja en nuestro CCD. Los tamaños son parecidos ya que son 1024 x 24$\mu m$/pixel = 24.6 mm y 2048 x 13$\mu m$/pixel = 26.6 mm respectivamente   
TEK#5       $24.6 mm \times 69.8 Å/mm$ -->  1717 Å  
EEV4280     $26.6 mm \times 69.8 Å/mm$ -->  1857 Å  
cualquiera valdría porque los intervalos registrados son mayores de lo que necesito (7500 -6000 = 1500 Å), elijo de momento TEK#5. Con 1717 Å de intervalo espectral registrado en ese CCD podría girar la red al ángulo de incidencia adecuado para registrar el espectro entre 5900Å y 7617 Å.

Para comprobación final de que hemos elegido bien comprobemos la resolución espectral que conseguimos con una rendija de tamaño razonable. Queremos que una línea monocromática (la imagen de la rendija en el plano focal del spectrógrafo) se muestree en al menos tres píxeles  
$w' = 3\;píxeles \times 24 \mu m/píxel = 72 \mu m$.  
Eso significa que (usando el factor de amplificación al revés) $w  =  72 \mu m \times 1275 mm / 235 mm = 391 \mu m$.   
Esta rendija proyectada en el cielo subtiende un ángulo $\phi = w / f = 391 \mu m \times 5.42 arcsec/mm = 2.1 arcsec$, donde hemos usado la escada de placa. La pureza espectral con esta configuración es $\delta \lambda = 72 \mu m \times 69.8  Å/mm = 5 Å$.

Para saber qué zona del cielo estamos muestreando en cada columna del CCD tenemos que determinar la escala espacial. $24 \mu m$ (1 pixel) en plano focal del espectrógrafo (CCD) se transforman en $h_i'= 24 \mu m$ -->  $h_i= 24 \mu m/pixel \times 1275/235 = 130 \mu m$  
$130 \mu m$ en plano focal del telescopio son $130 \mu m \times 5.41 arcsec/mm = 0.7 arcsec$ en el CCD. Luego la escala en la dirección espacial del detector es $0.7\;arcsec/pixel$.

## Espectroscopía con grismas 
Existe un tipo de espectrógrafo diseñado inicialmente para objetos débiles que combina la posibilidad de obtener imágenes y espectros de resolución no muy alta. Un ejemplo de este instrumento es el espectrógrafo CAFOS (Calar Alto Faint Object Spectrograph). Los dispersores son redes de transmisión colocados sobre prismas (grisms: 'grating+prism'). 

```{figure} /_static/lecture_specific/espectroscopia/spec_18_grisma_1.png
---
width: 200px
name: grisma_1-fig
---
Esquema de la desviación de los órdenes m=1 y m=-1 a ambos lados del eje óptico mientras el orden m=0 sigue la dirección del ángulo de incidencia en una red de transmisión.
```
```{figure} /_static/lecture_specific/espectroscopia/spec_18_grisma_2.png
---
width: 200px
name: grisma_2-fig
---
Un espectrógrafo con redes de transmisión tiene que estar doblado para que la cámara enfoque el espectro.Como esa desviación depende de la red usada sólo serviría para una red en particular. 
```
```{figure} /_static/lecture_specific/espectroscopia/spec_18_grisma_3.png
---
width: 500px
name: grisma_3-fig
---
Esquema de un grisma que es simplemente una red de transmisión tallada sobre un prisma. La misión del prisma es desviar el orden deseado m en la dirección del eje óptico.
```
El ángulo de los prismas de estos grismas está calculado para que el orden deseado del espectro (generalmente el orden m=1) salga en dirección del eje óptico. Esto permite utilizar un conjunto de grismas seleccionables colocados en una rueda selectora.

$$ m \lambda = \sigma (\mu \; sen \alpha - sen \beta) \quad \quad m \lambda = \sigma (\mu -1) sen \delta $$

```{figure} /_static/lecture_specific/espectroscopia/spec_18_grisma_4.png
---
width: 500px
name: grisma_4-fig
---
Esquema de un espectrógrafo de grismas con la rueda de filtros y la de grismas.
```
Con los grismas podemos construir espectrógrafos que puedan seleccionar grismas de diferente dispersión. Como todos los grismas envían en el eje óptico la luz del orden decidido en su diseño, puede emplearse una rueda de grismas de diferente dispersión que sea seleccionable. Como el paso de red es grande en estas redes se reducen las aberraciones de coma ($\propto 1/\sigma$) y astigmatismo ($\propto 1/\sigma^2$), permitiendo campo amplio de visión.

Los espectrógrafos de objetos débiles con grismas permiten configuración de modo imagen y de espectroscopía. En este caso con diferentes grismas y rendijas.

```{figure} /_static/lecture_specific/espectroscopia/spec_18_grisma_5.png
---
width: 600px
name: grisma_5-fig
---
Diferentes ruedas con elementos seleccionables para introducir en el camino óptico de un espectrógrafo de objetos débiles con grismas.
```
La rueda con las aperturas es la primera en el camino óptico ya que se encuentra en el foco del telescopio. Puede seleccionarse bien una apertura circular grande (vacío, nada en el camnino) para poder tomar imágenes o una máscara con aperturas. En este caso (para hacer spectroscopía) se puede usar una rendija larga multipropósito o se fabrican máscaras especiales para el campo elegido conocida la astrometría de los objetos de los que deseamos obtener el espectro (espectroscopía multiobjeto). 

La segunda rueda contiene los filtros. Si queremos hacer espectroscopía seguramente lo dejemos abierto, sin filtro. Por último, la tercera rueda sirve para seleccionar los dispersores (grismas) y se deja abierto si hacemos imagen.

En modo imagen abierto-filtro-abierto y modo espectro rendija-abierto-grisma. Un esquema de observación en el que se usan los dos modos se muestra en la figura. Sólo se obtienen los espectros de los objetos qeu cayeron dentro de las rendijas. Estas rendijas se tallaron con una herramienta robotizada en una placa sabiendo la escala de placa y la astrometría del campo observado.


```{figure} /_static/lecture_specific/espectroscopia/spec_18_grisma_6.png
---
width: 500px
name: grisma_6-fig
---
Imagen directa del campo y espectros de los objetos usando una máscara de rendijas.
```

Resumiendo, estos espectrógrafos se emplean como cámaras directas para obtener imágenes del campo al que apunta el telescopio o como espectrógrafos de resolución baja. Se pueden usar como espectrógrafo simple (una rendija) o multiobjeto usando una placa con múltiples rendijas. Estas placas de rendijas (o aperturas) se construyen a medida de cada observación con anterioridad y son intercambiables: se pueden poner las que queramos en la rueda de aperturas y retirarla para otro proyecto observacional que necesite otra placa diferente. Son espectrógrafos pensados para objetos débiles (cúmulos de galaxias, por ejemplo) ya que son sistemas muy luminosos.


### Ejemplo de configuración espectroscopía de grismas
El observatorio de Calar Alto dispone de CAFOS que es una cámara con un reductor de focal (para obtener más campo de visión) y un espectrógrafo pensado para objetos débiles. 

```{figure} /_static/lecture_specific/espectroscopia/spec_19_CAFOS_1.png
---
width: 400px
name: CAFOS_1-fig
---
Esquema de CAFOS en sección. Se aprecia arriba el sistema de lámparas de calibración (fuera del camino óptico en este esquema), la óptica del colimador, las ruedas y la cámara con el criostato del CCD.
```

El colimador ($f_1=310 mm$) y la cámara ($f_2 = 163 mm$) reducen la focal del telescopio
de f/8 a f/4.2. La escala de placa final pasa de $85.4 \mu m/arcsec$ del telescopio en el foco Cassegrain a $45.32 \mu m/arcsec$.

```{figure} /_static/lecture_specific/espectroscopia/spec_19_CAFOS_2.png
---
width: 600px
name: CAFOS_2-fig
---
Tabla de detectores CCD disponibles en CAFOS y sus parámetros.
```

```{figure} /_static/lecture_specific/espectroscopia/spec_19_CAFOS_3.png
---
width: 600px
name: CAFOS_3-fig
---
Tabla de detectores CCD disponibles en CAFOS y sus parámetros.
```

```{figure} /_static/lecture_specific/espectroscopia/spec_19_CAFOS_4.png
---
width: 400px
name: CAFOS_4-fig
---
Eficiencias de las redes B400 y R400.
```

```{figure} /_static/lecture_specific/espectroscopia/spec_19_CAFOS_5.png
---
width: 400px
name: CAFOS_5-fig
---
Eficiencias de las redes B200, G200 y R200.
```

Si necesitamos por ejemplo un espectro que abarque un intervalo de longitud de onda amplio usaríamos las redes menos dispersivas (B400 ó R400) dependiendo de la región espectral. La B-400 por ejemplo cubre el visible entre el azul y el rojo. Los grismas B200, G200 y R200 son más dispersivas y cubren menos intervalo espectral. Cada una está optimizada para el azul, verde y rojo respectivamente. 


```{figure} /_static/lecture_specific/espectroscopia/spec_19_CAFOS_7.png
---
width: 400px
name: CAFOS_7-fig
---
Eficiencia de las redes B100, G100 y R100..
```
Por último los grismas B100, G100 y R100 permiten obtener espectros con mejor resolución espectral, menos dispersión y menor intervalo espectral. De nuevo elegiremos la que tenga mejor eficiencia en la región espectral que deseemos observar. 

La dispersión es del orden de 0.2 nm/pixel y la resolución depende del ancho de la rendija o del tamaño angular del objeto si se usa sin rendija: 0.38 nm/arcsec, es decir $\delta \lambda = 0.38 nm$ para una rendija de 1 arcsec.





## Observaciones espectroscópicas

El espectrógrafo se elige en base a los requerimientos del proyecto de investigación y a la disponibilidad de instrumentos. Existen espectrógrafos multipropósito que permiten abordar proyectos observacionales muy distintos usando diferentes configuraciones (redes, cámaras etc). Otros espectrógrafos son muy especializados: alta resolución, de objetos débiles, etc.

La lista de espectrógrafos y sus características se pueden consultar en los portales de los observatorios. Con la ayuda de los astrónomos de apoyo se configura de manera óptima a nuestras necesidades los espectrógrafos.

Como detector se emplea un CCD. Las imágenes espectroscópicas suelen ser rectangulares con la parte larga correspondiente a la dirección espectral. Esa dirección del CCD se suele emplear completa. En la dirección espacial no se necesita tanto CCD normalmente ya que la óptica no es capaz de producir la imagen de una rendija tan larga. Por lo tanto, de todo el CCD sólo se utiliza una región y es ésa la que se selecciona en el momento de la observación para no grabar y almacenar partes del CCD que no necesitamos.

Por ejemplo, con el CCD Tek#3 usado en las observaciones INT IDS de las prácticas de $1124 \times 1124$ píxeles de $24 \mu m  \times 24 \mu m$  la zona recortada es una ventana de 1124 (dirección espectral, parte de la imagen es overscan) x 250 pixeles (dirección espacial).

```{figure} /_static/lecture_specific/espectroscopia/spec_20_long_1.png
---
width: 200px
name: long_1-fig
---
Recorte del CCD Tek#3 para la zona de interés en onbservaciones espectroscópicas con el IDS.
```

La rendija proyectada sobre el cielo  
$17\;arcsec/mm \times 250\;pix \times 0.024\;mm/pix = 102\;arcsec$  

Luego cada fila muestrea:
$17\;arcsec/mm \times 1\;pix \times 0.024\;mm/pix = 0.41\;arcsec$
 
```{figure} /_static/lecture_specific/espectroscopia/spec_20_long_2.png
---
width: 600px
name: long_2-fig
---
Se podría recortar también una ventana del chip de cualquier tamaño, por ejemplo limitando el intervalo espectral.
```
Los programas de control de instrumentos en los observatorios permiten recortar esas zonas o ventanas. Esto sirve tanto para espectroscopía como para fotometría. En el ejemplo mostrado se ve en caso del CCD usado en las observaciones procesadas en la práctica 3. Se define una zona de ‘underscan’ y otra de ‘overscan’ que sirven para determinar en valor de BIAS en cada imagen.

Para el caso de CAFOS que permite tanto imagen como espectroscopía, el recorte es diferente en cada caso. Las ventanas habituales son cuadradas para imagen y rectangulares para espectroscopía. 

```{figure} /_static/lecture_specific/espectroscopia/spec_20_long_4.png
---
width: 600px
name: long_4-fig
---
Recortes de la imagen del CCD de CAFOS de 2048 x 2048 píxeles para el caso de imagen (en verde) y de espectroscopía (rojo). En este caso la dirección espectral es la vertical. 
```

Las observaciones espectroscópicas incluyen 

- Las imágenes usadas para calibración del CCD: los BIAS y DARK para medir el nivel de pedestal y la corriente de oscuridad si la hubiera. De esta manera podemos retirar la parte aditiva de la señal.
Los Flat Field (bien con espectros de lámparas internas y mediante espectros de cielo en crepúsculo) para determinar la variación espacial de la sensibilidad del CCD.

- Los espectros de lámparas de calibración en longitud de onda. Los espectros de estas lámparas presentan multitud de líneas de emisión cuya longitud de onda es bien conocida y está tabulada. La calibración se obtiene por comparación de la posición x de estas líneas de referencia con su longitud de onda $\lambda$.

- Espectros de los objetos motivo de nuestro proyecto científico.

- Espectros de estrellas estándar de flujo para calibración fotométrica. El espectro de estas estándares espectrofotométricas es conocido y por comparación entre el resultado de la observación y esa distribución espectral de energía podemos determinar la curva respuesta espectral.

```{figure} /_static/lecture_specific/espectroscopia/spec_20_long_3.png
---
width: 600px
name: long_3-fig
---
Imágenes espectroscópicas mostrando el espectro de las galaxias y la identificación de las líneas. Se aprecia la zona de overscan a ambos lados y las lineas de cielo que discurren todo a lo largo de la dirección espacial.
```


