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

#  Calibración CCD
## Imágenes CCD
La observación con un detector de imagen como un CCD da lugar a un fichero que almacena un número (cuentas) recibidas en cada pixel. Por lo tanto la imagen resultante es una matriz de datos. Las cuentas en cada pixel se corresponden a la llegada de fotones de forma que la imagen calibrada puede usarse para medir en diferentes partes de la imagen y extraer información científica.    
Ya sabemos que los fotones producen en el substrato del chip pares electrón-hueco y que los electrones se almacenan en el pozo de potencial creado bajo los electrodos de cada pixel. En la lectura ordenada del CCD estos electrones se cuentan con un conversor analógico-digital que los transforma en un número de cuentas o ADUs (analog-to-digital units'). La relación entre electrones y cuentas es la ganancia del detector. Para evitar efectuar esta conversión en las cuentas de píxeles que recibieron poca señal se suma una señal de pedestal o BIAS y así ya no estamos en valores cercanos a cero en sitios oscuros. Estos detectores se refrigeran para reducir la corriente de oscuridad que se añade a nuestra señal.  


```{figure} /_static/lecture_specific/p1_intro/intro_05_CCD_1.png
---
width: 600px
name: CCD_1-fig
---
La medida en cada pixel del CCD está relacionada con la cantidad de fotones que llegaron a cada pixel a través de esta expresión.
```

Para llegar a la imagen reducida ($I_{i,j}$) desde la matriz de nuestra observación ($X_{i,j}$) debemos conocer el valor del BIAS que se añadió a la imagen y también la corriente de oscuridad ($A_{i,j}$). Este ruido es muy pequeño en los detectores modernos si están convenientemente refrigerados. Es señal que se va acumulanto con el tiempo así que es mayor para observaciones largas. Una característica importante de los CCD es que su respuesta depende la posición del pixel en el chip. La variación de la respuesta espacial que aquí indicamos con ($B_{i,j}$) se determina también con imágenes de calibración.

El número de cuentas X(i,j) obtenidas en el pixel (i,j) de una
cámara CCD se puede expresar de la siguiente forma:

$$X(i,j) = BIAS + B(i,j) \times I(i,j) + A(i,j)  +  (términos\_ no\_ lineales)$$

donde I(i,j) es el flujo de luz incidente sobre ese pixel. Esta
ecuación no tiene en cuenta las ineficiencias en la transferencia
de carga y otros efectos que se sabe tienen lugar en estos
detectores.

La eficiencia cuántica y la eficiencia en la transferencia de
carga están incluidos en el término multiplicativo. La
corriente de oscuridad y las "columnas frías" contribuyen al
término aditivo A(i,j). La respuesta de los detectores CCD es
esencialmente lineal, por lo que pueden despreciarse los términos
no lineales. El BIAS se añade a la señal electrónica de
salida del detector para evitar el digitalizar valores próximos a
cero.

El objetivo del primer paso de la calibración de las imágenes
CCD es determinar la intensidad relativa I(i,j). El segundo paso
consiste en obtener, por comparación con las medidas realizadas
para objetos de brillo conocido, una imagen calibrada en flujo
absoluto.

Para realizar este proceso de conversión a intensidades relativas,
además de la imagen del objeto de estudio obtenida a través
del filtro que nos interese (SCIE\_FRM), necesitamos dos imágenes
más: una imagen obtenida iluminando el CCD con una fuente emisora
uniforme, conocida como Flat-Field (FLAT\_FRM), que nos permitirá
determinar el término B(i,j) es decir, cuáles son las
variaciones de la sensibilidad a lo largo del detector; y una imagen
obtenida en ausencia de toda señal externa, conocida como Dark
(DARK\_FRM).

A partir de la primera ecuación se obtiene:

\begin{eqnarray*}
FLAT\_FRM(i,j) & = & BIAS + DARK\_FRM(i,j) + B(i,j) \; ICONS \\ 	
SCIE\_FRM(i,j) & = & BIAS + DARK\_FRM(i,j) + B(i,j) \; INT\_FRM(i,j) \\
DARK\_FRM(i,j) & = & BIAS + DARK\_FRM(i,j)
\end{eqnarray*}

La imagen Dark (DARK\_FRM) contiene la señal de dark que se va acumulando con el tiempo y la de BIAS ya que ésta aparece en todas las observaciones. Combinando estas ecuaciones se obtiene:

\begin{eqnarray*}
INT\_FRM(i,j) & = & \frac{SCIE\_FRM(i,j) - DARK\_FRM(i,j)}
{FLAT\_FRM(i.j) - DARK\_FRM(i,j)} \;\; ICONS
\end{eqnarray*}

\noindent 
El valor ICONS puede ser cualquier n\'{u}mero. Para que los valores de
INT\_FRM sean similares a los de SCIE\_FRM, se suele normalizar de
modo que

\begin{eqnarray*}
ICONS & = & FLAT\_FRM - DARK\_FRM 
\end{eqnarray*}

Por eso debemos restar el DARK a todas las imágenes (incluido el FLAT) para quedarnos con los términos lineales. Buscamos una imagen reducida INT_FRAME(i,j) donde los valores de cuentas de cada pixels sean proporcionales a la cantidad de fotones recibida.

## (La llegada de fotones a un detector)
Utilizando un array de pequeñas dimensiones, se simula la llegada poissoniana de fotones a un detector y la posterior conversión analógica-digital. Esta simulación permite ilustrar conceptos básicos de relación señal/ruido y propagación de incertidumbres.  
Pendiente de hacer pero se puede consultar [CCD data reduction guide](https://mwcraig.github.io/ccd-as-book/01-00-Understanding-an-astronomical-CCD-image.html) written by Matt Craig and Lauren Chambers. Editing was done by Lauren Glattly.

## Imágenes de calibración
Para calibrar las observaciones de ciencia se deben tomar imágenes auxiliares que sirven de calibración. Estas imágenes de calibración son los BIAS, DARKS y los FLATS. Es importante notar que las imágenes de calibración se toman en las mismas condiciones de temperatura ya que el ruido electrónico y la sensibilidad del CCD varían con la temperatura. Por eso se utilizan criostatos.

### BIAS
Se obtienen las imágenes de BIAS con exposiciones de tiempo de exposición nulo (0s) con el obturador cerrado. Por eso se llaman también  DARK 0. Representan el punto cero de la señal de un CCD que es un valor que decidieron los ingenieros que montaron el sistema. El BIAS puede contener algo de estructura, es decir que no es completamente plano. Como cualquier imagen CCD presenta ruido de lectura y electrónico. aunque el tiempo de exposición es nulo el tiempo de lectura no lo es. Durante ese tiempo caen rayos cósmicos que dejan su marca en forma de píxeles con señal alta. Se realizan series de BIAS para combinarlos ya que el BIAS final debe estar libre de rayos cósmicos. La combinación ('average' + 'sigma clipping') reduce el ruido un factor $\sqrt(N)$. En algunos casos puede ser necesario usar el 'overscan' que es una lectura de columnas del CCD que no existen o columnas tapadas del chip. La región de overscan está presente en todas las imágenes incluidas las de ciencia.

#### FLAT FIELDs
Los 'Flat Fields' que podríamos traducir como imágenes de campo plano, se obtienen iluminando el CCD uniformemente.
Son necesarios para determinar la variación espacial de sensibilidad. Esta variación depende de la longitud de onda por lo que debe determinarse para cada filtro empleado en las observaciones. Pero además las motas de polvo en el chip, la ventana o los filtros nos obligan a tomar flat fields en la misma noche de nuestra observación. Si una de estas motas se mueve de sitio el flat field de antes ya no vale ya que no corregirá la zona del chip donde se ha parado la mota de polvo y sobre corregirá la zona donde estaba antes.

Se eligen los tiempos de exposición para que el número de cuentas esté aproximadamente a la mitad del nivel de saturación. También se realizan observaciuones de series de Flats para combinarlos en un ‘master Flat’.

- Flats de cúpula (‘dome flat’)  
Se obtienen iluminando con lámparas el interior de la cúpula.
Se pueden realizar en cualquier momento (día o noche).

- Flats de cielo (‘sky flat’)  
Se apunta al cielo libre de objetos (‘blank field’) o a una nube.
Se realizan en los crepúsculos  (anochecer o amanecer) (‘twilight’).
Pueden obtenerse combinando muchas imágenes de ciencia si los objetos no llenan el campo de visión.


Recordemos que los Flat Fields dependen del chip, de su temperatura, del filtro utilizado, de la posición de las motas de polvo. Por lo tanto se toman

(a) en las mismas condiciones de temperatura del criostato porque la sensibilidad del CCD varía con la temperatura.  
(b) para cada filtro empleado ya que la respuesta del CCD varía con la longitud de onda.

Por supuesto estas condiciones se deben mantener a lo largo de la observación de los objetos problema.


### DARKs
En los CCDs profesionales de la actualidad la corriente de oscuridad es inapreciable. Se comprueba tomando exposiciones largas con el obturador cerrado. Si existe corriente de oscuridad se deben tomar imágenes DARK del mismo tiempo de exposición que las de ciencia.
Se obtienen series de DARKs para combinarlos en un ‘master Dark’.

## Pasos de la calibración
Para cada noche de observación se visualizan y analizan las imágenes disponibles. Esto sirve para no procesar la imágenes 'a ciegas' y que se nos cuele un fichero mal grabado, por ejemplo. Tras este paso se retiran las imágenes que no sirven. Si es necesario se recorta de las imágenes la región de interés. Por razones obvias, es importante aplicar este recorte a todas las imágenes.

```{figure} /_static/lecture_specific/p1_intro/intro_05_CCD_2.png
---
width: 400px
name: CCD_2-fig
---
Ejemplo de imagen original y recortada para retirar la zona sin señal válida.
```

- Corrección de nivel cero  
Se combinan los BIAS para crear un BIAS maestro  (ZERO)  
Se resta la imagen ZERO a todas las imágenes

- Corrección de FLAT  
Se combinan los FLATS de cada filtro  
Se normaliza dividiendo por el número medio de cuentas para crear el FLAT maestro  
Se dividen las imágenes de ciencia por el FLAT maestro  

```{figure} /_static/lecture_specific/p1_intro/intro_05_CCD_3.png
---
width: 500px
name: CCD_3-fig
---
Ejemplo de flat fileds de cielo individuales y Flat Field maestro (abajo a la derecha). La combinación ha retirado las estrellas que aparecieron en las tomas de crepúsculo. 
```
```{figure} /_static/lecture_specific/p1_intro/intro_05_CCD_4.png
---
width: 500px
name: CCD_4-fig
---
Ejemplo de imagen original y dividida por el Flat Field maestro.
```
- Combinación de imágenes individuales  
Si se ha observado el mismo campos en varias exposiciones, éstas se combinan para crear una imagen única. En el proceso hay que registrar (hacer que coincidan) las imágenes si el telescopio se desplazó entre las tomas individuales. La combinación de imágenes ayuda a retirar rayos cósmicos cuya posición de caida en el chip es aleatoria.  

```{figure} /_static/lecture_specific/p1_intro/intro_05_CCD_5.png
---
width: 500px
name: CCD_5-fig
---
Misma región del chip de tres observaciones consecutivas del mismo campo con la misma estrella marcada en cada exposición.
```
```{figure} /_static/lecture_specific/p1_intro/intro_05_CCD_8.png
---
width: 200px
name: CCD_7-fig
---
Identificación de estrellas usadas en la alineación de la imágenes.  
```

```{figure} /_static/lecture_specific/p1_intro/intro_05_CCD_7.png
---
width: 600px
name: CCD_7-fig
---
Las tres imágenes alineadas a la misma referencia. Se han utilizado los mismos cortes para que se note cómo ha variado el brillo de cielo entre las tomas. 
```

Estos pasos se siguen en las prácticas. 




Bias, dark, flat fields de baja y alta frecuencia, arcos para calibración en longitud de onda. Se explican sus características y utilización. Definición de región útil del detector y regiones de under/overscan. Utilización de binning durante las observaciones para incrementar la relación señal/ruido y/o reducir el tiempo de lectura.

## Ejemplo de reducción de imágenes CCD
Utilizando un subconjunto de las imágenes disponibles para la Práctica 2, se ilustrará la aplicación de calibraciones básicas (corrección de cero, corrección de flat field, corrección de rayos cósmicos), la combinación de imágenes individuales y la calibración astrométrica.


## Ejemplo de reducción de espectros CCD
Utilizando un subconjunto de las imágenes disponibles para la Práctica 3, se ilustrará la aplicación de calibraciones básicas (corrección de cero, corrección de flat field, corrección de rayos cósmicos, calibración en longitud de onda, corrección de iluminación) y la combinación de imágenes individuales.

## Estrategias para la estimación de incertidumbres
Propagación analítica frente a la utilización de técnicas de bootstrapping y Monte Carlo.


