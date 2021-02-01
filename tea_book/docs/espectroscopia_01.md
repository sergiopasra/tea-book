# Espectroscopía astronómica
 

## Introducción 
La información que se obtiene con la espectroscopía es mucho mayor que con la fotometría. Por ejemplo, por citar sólo el caso de las estrellas, permite clasificar directamente su tipo espectral de acuerdo a sus características espectrales. Además la medida del flujo y cocientes de sus líneas informa temperaturas y abundancias de elementos en la atmósfera, rotación, velocidad de desplazamiento respecto al observador etc. 

```{figure} /_static/lecture_specific/espectroscopia/spec_01_tipos_espectrales.png
---
width: 800px
name: tipos_espectrales-fig
---
Espectros de estrellas en color verdadero (el que vería un humano). Nótese no sólo el cambio de intensidad de color en diferentes regiones dele spectro sino en las líneas de absorción. Gara Mora Carrillo (2000) UCM Trabajo Académicamente dirigido [Espectros estelares en color real](http://www.ucm.es/info/Astrof/users/jaz/TRABAJOS/COLOR/colorspectra.html). 
```


```{figure} /_static/lecture_specific/espectroscopia/spec_02_Vega_Sun.png
---
width: 800px
name: Vega-Sun-fig
---
Comparación de los espectros del Sol y de Vega de muy diferentes tipos espectrales en la región de H$\beta$ [Professor Simon Jeffery stellar spectra graphs](http://193.63.77.2:2805/~SJeffery/articles.popular/spectra/sim.html). 
```

## Parámetros de un espectrógrafo y su impacto en las observaciones
Recordemos que en un espectrómetro las líneas espectrales monocromáticas son las imagenes en el plano focal del espectrógrafo de la rendija. La combinación colimador-cámara (con el elemento dispersor en medio) proyecta la imagen de la rendija en el detector. 

```{figure} /_static/lecture_specific/espectroscopia/spec_03_esquema.png
---
width: 800px
name: esquema-fig
---
Esquema de un espectrómetro adaptado a un telescopio de diámetro D (no a escala). La rendija se encuentra en el plano focal del telescopio (si está bien enfocado). El colimador se encuentra a una distancia igual a su focal $f_1$. Tras él se encuentra el elemento dispersor y luego la cámara que es el sistema óptico que produce el espectro en el plano focal (a distancia $f_2$). 
```

La rendija tiene dimensiones $w$ anchura y $h$ longitud y proyectada en el cielo subtiende ángulos $\phi = w/f$ y $\phi' = h/f$ donde $f$ es la distancia focal del telescopio. Esa zona del cielo es la que entra en el sistema óptico y cuyo espectro se registra.  Análogamente, la rendija proyectada en el colimador $\theta = w/f_1$ y $\theta' = h/f_1$. Finalmente la imagen monocromática de la rendija tiene un tamaño  $w' = w f_2/f_1$ y $h' = h f_2/f_1$. Como se ve las relación entre la rendija y su imagen dependen del factor de amplificación $f_2/f_1$. Por ejemplo si la focal de la cámara es el doble que la del colimador la imagen de la rendija es de doble tamaño que la rendija.

### pureza espectral
La pureza espectral es un parámetro fundamental de los espectrómetros que mide la capacidad del instrumento da idea de la capacidad para resolver líneas de longitud de onda cercana y de observar detalles en las líneas. La pureza espectral es el perfil instrumental y se mide como la anchura de la imagen de la rendija iluminada con luz monocromática. En el criterio de Rayleight una línea está resuelta por el espectrómetro si su anchura es mayor que la pureza espectral $\Delta \lambda > \delta \lambda$

```{figure} /_static/lecture_specific/espectroscopia/spec_04_Rayleigh.png
---
width: 400px
name: Rayleigh-fig
---
Criterio de Rayleigh: el espectrógrafo separa dos líneas cuando la diferencia de longitud de onda de los máximos sea mayor o igual a la pureza espectral $\Delta \lambda > \delta \lambda$. 
```

Algunas ecuaciones para determinar esta pureza espectral $\delta\lambda$,

$$
\delta\lambda = w' \frac{d\lambda}{dx} =  \frac{w'}{f_2} \frac{d\lambda}{d\beta} 
\quad \quad \quad \delta\lambda = \frac{w}{f_1} \frac{d\lambda}{d\beta} =  \frac{f \phi }{f_1} \frac{d\lambda}{d\beta} =  \frac{D \phi }{d_1} \frac{d\lambda}{d\beta}
\quad \quad \quad \delta\lambda =  \frac{D \phi }{d_1} \frac{1}{d\beta/d\lambda}
$$

donde $d\lambda/d\beta$ y $d\lambda/dx$ son la dispersión angular (que depende del dispersor y del orden) y la dispersión lineal recíproca que se mide en Å/mm o nm/mm. Lo interesante de estas ecuaciones es que si queremos mejorar la resolución espectral (disminuyendo el valor de la pureza espectral) tenemos que disminuir la anchura de la rendija o usar una red más grande que permita un haz colimado mayor o usar una red más dispersiva.


```{figure} /_static/lecture_specific/espectroscopia/spec_06_anchura.png
---
width: 400px
name: anchura-fig
---
La resolución espectral es directamente proporcional a la anchura de la rendija. Pero hay que llegar a un compromiso para que la rendija no sea tan estrecha que no permita la entrada de luz en el espectrógrafo.  
```

### resolución espectral 
La resolución $R = \frac{\lambda} {\delta \lambda}$ es el cociente entre la longitud de onda $\lambda$ y la pureza espectral $\delta \lambda$. De acuerdo a este parámetro adimensional se habla de resolución baja ($\sim 10^3$), intermedia ($\sim 10^4$) o alta ($> 5 \times 10^4$).

```{figure} /_static/lecture_specific/espectroscopia/spec_05_resolucion.png
---
width: 200px
name: resolucion-fig
---
REPETIR Ejemplo de espectro con un doblete observado con espectrómetros de resolucón R creciente de arriba abajo. 
```

## Dispersores
Aunque se emplean prismas en algunos espectrómetros especiales, la mayoría de la veces se usa una red de difracción. La ecuación fundamental es,

$$
m \lambda = \sigma (sen \alpha + cos \beta)
$$

Sin entrar en los detalles de la óptica de redes recordemos que normalmente se tallan los surcos de forma especial para que el máximo de la luz no se vaya al orden m=0.  



```{figure} /_static/lecture_specific/espectroscopia/spec_07_blaze.png
---
width: 600px
name: blaze-fig
---
Esquema de una red de difracción iluminada en un ángulo de incidencia $\alpha$.
```
En el orden cero la dispersión es nula. Interesa que la luz vaya en preferencia a otros órdenes. La dirección en la que se difracta el máximo de radiación corresponde a la reflexión especular en las facetas.
 
```{figure} /_static/lecture_specific/espectroscopia/spec_08_blaze-2.png
---
width: 600px
name: blaze-2-fig
---
(Izda.) En incidencia normal ($\alpha = 0$, luz colimada impactando de cara en la red) la reflexión especular no está en el orden cero sino en otra dirección de acuerdo an ángilo de 'blaze'.  
(Dcha.) Para cualquier otro ángulo de incidencia $\alpha$, la dirección de salida $\beta$ mostrada en la figura es la de mayor eficiencia (reflexión especular en las facetas).
```

La máxima eficiencia de la red ocurre justo a la reflexión especular en las facetas. Para un cierto orden m, sucede en la longitud de onda que cumple la ecuación,

$$
m \lambda = \sigma (sen 2 \theta_b) 
$$

$$
\beta - \theta_b =   \theta_b  - \alpha  \quad \quad \alpha + \beta = 2 \theta_b 
$$

```{figure} /_static/lecture_specific/espectroscopia/spec_09_blaze-3.png
---
width: 400px
name: blaze-3-fig
---
Geometría de la reflexión especular en las facetas.
```

La longitud de onda de blaze (la correspondiente al máximo para el orden 1 (m=1) y el máximo en otros ordenes se determina como,

$$
\lambda_b = 2 \sigma \; cos(\delta/2) \quad \quad \quad \lambda_m = \lambda_b / m
$$

```{figure} /_static/lecture_specific/espectroscopia/spec_10_eficiencia.png
---
width: 600px
name: eficiencia-fig
---
Las curvas de eficiencia en diferentes órdenes tienen su máximo en $\lambda_m$ y son progresivamente más estrechas según aumenta el orden. En este gráfico sencillo han sido normalizadas.
```
Para el caso particular de la incidencia normal: 

$$
\alpha = 0 \quad \quad \beta = 2 \theta_b  \quad \quad \lambda_b = 2 \sigma \; sen \theta_b cos \theta_b \quad \quad \lambda_b = \sigma \; sen 2 \theta_b
$$

### dispersión
La dispersión angular se determina (a partir de la ecuación fundamental de las redes)

$$
\frac{d\beta}{d\lambda} = \frac{m}{\sigma cos\beta}
$$

donde vemos que es directamente proporcional al orden $m$ e inversamente proporcional al paso de la red $\sigma$. La dispersión lineal y la dispersión lineal recíproca dependen además de la distancia focal de la cámara del espectrógrafo $f_2$,

$$
\frac{dx}{d\lambda} = f_2 \frac{d\beta}{d\lambda} \quad \quad \quad \frac{d\lambda}{dx} = f_2 \frac{\sigma cos\beta}{m f_2} 
$$
es decir que cámaras con focales mayores producen mayores dispersiones (directamente proporcional). 

```{figure} /_static/lecture_specific/espectroscopia/spec_11_dispersion.png
---
width: 800px
name: dispersion-fig
---
Se muestra el tamaño relativo de los espectros del mismo objeto observados con un espectrógrafo en diferentes órdenes o usando redes de paso diferente o cambiando la cámara del espectrógrafo. 
```

A la dispersión lineal recíproca $d\lambda/dx$ se mide en unidades de Å/mm o nm/mm se la llama a veces dispersión lineal por abuso de lenguaje. Hay que prestar atención porque una dispersión lineal alta se traduce en una dispersión lineal recíproca baja. Veamos un ejemplo para comprobar cómo las relaciones de la dispersión con los parámetros del espectrómetro son lineales, bien directamente o inversamente proporcionales.

En un espectrógrafo una red de 600 trazos/mm se consigue una dispersión de 48 Å/mm en el segundo orden. Determínese la dispersión en el primer y tercer órdenes para esa red y otras de 300 y 1200 tr/mm. Idem si se cambia a una cámara del doble de distancia focal.

```{figure} /_static/lecture_specific/espectroscopia/spec_12_ejemplo.png
---
width: 600px
name: ejemplo-fig
---
```
Se rellenan las tablas recordando la dependencia lineal de la dispersión con el orden, el paso de la red y la focal de la cámara. Por ejemplo, como la dispersión es directamente proporcional al orden la dispersión lineal recíproca en m=2 es de 48 Å/mm luego será de 96 Å/mm en m=1. La dispersión es inversamente  proporcional al paso de la red que podemos calcular con el inverso de la densidad de surcos (o líneas o trazos) de la red $\sigma_2 = 1/600 = 1.65\mu m \quad \quad \sigma_1 = 2 \sigma_2 \quad \quad \sigma_3 = \sigma_2 / 2$.  
La dispersión es directamente proporcional a la focal de la cámara luego la dispersión lineal recíproca se hace la mitad al doblar la focal de la cámara $f_2$.
 
### solapamiento de órdenes
Para un cierto ángulo de incidencia $\alpha$, en la dirección $\beta$ se difractan fotones de longitud de onda diferente según el orden. Para $\alpha$ y $\beta$ fijos, las longitudes de onda $\lambda$ y $\lambda '$ en órdenes sucesivos son,

$$
m \lambda = cte.  \quad \quad m \lambda ' = (m+1) \lambda 
$$



```{figure} /_static/lecture_specific/espectroscopia/spec_13_solapamiento.png
---
width: 800px
name: solapamiento-fig
---
Dependiendo del orden $m$ en una dirección $\beta$ aparecen fotones de diferente longitud de onda. Los órdenes han sido desplazados para que se aprecie mejor el solapamiento. Se muestran algunos ejemplos de valores de longitud de onda de los fotones que salen en la misma dirección en sucesivos órdenes.
```
El rango espectral libre se determina como $\lambda - \lambda ' = \lambda / m$. El efecto de solapamiento es cada vez mayor en órdenes altos por que el rango espectral libre (sin solapamiento) se hace menor. Para evitarlo se utilizan filtros cortadores. Por ejemplo si estamos observando en el orden $m=1$ y no queremos que en la zona roja aparezcan fotones azules del orden $m=2$ ponemos un filtro que corte por debajo de 360 nm (filtro de paso alto, long- pass filter) y tendremos un rango espectral libre entre 360 nm y 720nm.


dispersión angular de los medios dispersores, dispersión lineal recíproca, resolución espectral. Eficiencia de las redes/grismas, solapamiento de órdenes. Espectroscopía sin rendija, con rendija única, multirendija, multiobjeto con fibras y rebanadores de imágenes


