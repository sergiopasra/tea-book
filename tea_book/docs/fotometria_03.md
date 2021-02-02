# Fotometría absoluta

## Introducción
Las observaciones de fotometría astronómica necesitan, aparte de las observaciones de los objetos problema que son nuestro objetivo científico, medir los flujos de estrellas estándar (magnitud conocida) para calibrar nuestro sistema. De nuestras magnitudes instrumentales queremos llegar a magnitudes en el sistema estándar de manera que cualquier otro grupo de investigación pueda comparar sus medidas con las nuestras. 

    La fotometría de objetos celestes deben presentar en sus resultados 
    magnitudes corregidas del efecto de la atmósfera y referidos al sistema estándar 

Recordemos lo fundamental de la fotometría absoluta. La atmósfera terrestre actúa como un filtro absorbiendo parte de la radiación que la atraviesa. La absorción depende de la frecuencia de los fotones. El contribuyente principal de la extinción es la difusión Rayleight. El ozono impide observar por debajo de ~300nm que es el límite abrupto de nuestra atmósfera. Mientras la extinción por dispersión de Rayleight depende de lambda^-4, la extinción por aerosoles (partículas de polvo fino, gotas de agua y contaminación atmosférica que se encuentran más bajas que las moléculas que causan la difusión Rayleigh) depende poco de λ: es más gris.

La fotometría absoluta es un método observacional que permite determinar la magnitud de los objetos observados. Hay que observar estrellas estándar a lo largo de la noche para determinar el coeficiente de extinción y la constante instrumental.


````{panels}

```{figure} /_static/lecture_specific/fotometria/foto_14_absorcion.png

La absorción atmosférica en el visible depende fuertemente de la longitud de onda.
++++

----

```{figure} /_static/lecture_specific/fotometria/foto_14_absorcion_2.png

Curva de extinción media y los diferentes componentes.
```
````


````{panels}

```{figure} /_static/lecture_specific/fotometria/aa15537-10-fig1.jpg

Modelo de transmisión media de la atmósfera para Cerro Paranal. Patat et al. A&A
527 (2011) A91 https://doi.org/10.1051/0004-6361/201015537
++++

----

```{figure} /_static/lecture_specific/fotometria/aa15537-10-fig3.jpg

Aerosol extinction derived from the observed data and the LBLRTM model. The long-dashed line is a best fit model for kaer(λ), with k0 = 0.014 and α = −1.38. Overplotted are also the Rayleigh (short-dashed), ozone (solid thin curve), and clean tropospheric aerosol (thick solid) Patat et al. A&A 527 (2011) A91 https://doi.org/10.1051/0004-6361/201015537
```
````

```{figure} /_static/lecture_specific/fotometria/foto_caha_extincion.png
---
width: 800px
name: CAHA-extincion-fig
---
Curva de extinción media y sus diferentes contribuyentes (izda) y coeficientes de extinción en Calar Alto y ajuste  de los contribuyentes.U. Hopp & M. Fernández en Calar Alto Newsletter nov. 2002.

```

## Ecuaciones fundamentales
En fotometría astronómica usamos el sistema de magnitudes que es una escala logarítmica e inversa. La magnitud observada de un objeto celeste se obtiene a partir del flujo medido con nuestro sistema instrumental. Si tenemos un detector digital que transforma fotones en señal en cuentas (ADUs analog to digital units) la magnitud en una cierta banda se obtiene a partir del flujo medido en cuentas/s

$$
m_{\lambda}=C_{\lambda} - 2.5 \times log_{10} F_{\lambda}(c/s)
$$

donde 
- $C_{\lambda}$ es la constante instrumental. 
- $m_{\lambda}$ es la magnitud observada. 
- $F_{\lambda}$ es el flujo neto (corregido de brillo de fondo de cielo) en cuentas por segundo. 


La constante instrumental es un parámetro de nuestro sistema que varía con la banda fotométrica ya que depende de la respuesta espectral de los filtros, de la reflectividad de los espejos, del tamaño del telescopio, de la eficiencia cuántica del detector. No se espera que este parámetro varíe durante una campaña de observación pero puede ser diferente cuando vuelves a observar con el mismo instrumental unos meses después si, por ejemplo, se ha degradado el sistema óptico o han aluminizado de nuevo los espejos del telescopios.

El flujo que medimos en tierra de un objeto celeste es menor que el que mediríamos fuera de la atmósfera ya que ésta absorbe y difunde la radiación que la atraviesa. Esta extinción depende de la transparencia de la atmósfera a cada longitud de onda en un momento dado y en la dirección de observación y del recorrido de la radiación en la atmósfera. 


```{figure} /_static/lecture_specific/fotometria/foto_15_airmass.png
---
width: 400px
name: airmass-fig
---
La extinción atmosférica depende de la cantidad de atmósfera atravesada por la radiación. 
```

\begin{gather*}
F_{\lambda}=F_{\lambda}^o \times 10^{-0.4 \; K_{\lambda} \; sec(z)}\\
m_{\lambda}=m_{\lambda}^o - K_{\lambda} \; sec(z)
\end{gather*}

donde 
- $F_{\lambda}$ es el flujo observado 
- $F_{\lambda}^o$ es el flujo fuera de la atmósfera 
- $K_{\lambda}$ es el coeficiente de extinción y  
- sec(z) la secante de la distancia cenital o masa de aire (airmass). 
- $m_{\lambda}$ es la magnitud observada y 
- $m_{\lambda}^o$ la magnitud corregida de extinción o magnitud fuera de la atmósfera.


Para realizar observaciones de fotometría absoluta necesitamos que las condiciones de transparencia de la atmósfera sean buenas y constantes a lo largo de una noche. Esas noches especiales se llaman noches fotométricas. Son noches despejadas con valores pequeños de la extinción: transparentes. Durante la noche se observan estrellas estándar (de flujo bien conocido) en un amplio valor de masas de aire, es decir diferentes alturas sobre el horizonte. La menor extinción (menon masa de aire) se consigue cuando se observa el objeto en el cénit: $sec(z)=1$).

Se puede aplicar la técnica de fotometría absoluta a medias noches que de repente se estropean si se han conseguido suficientes observaciones de estrellas estándar pero es peligroso extrapolar. No se recomienda.

$$
m_{\lambda}=m_{\lambda}^o + K_{\lambda} \; sec(z)
\; ; \; m_{\lambda}=C_{\lambda} - 2.5 \times log_{10} F_{\lambda}(c/s)
$$
$$
m_{\lambda}^o + 2.5 \times log_{10} F_{\lambda} (c/s) = C_{\lambda} - K_{\lambda} \; sec(z)
$$

De la combinación de las ecuaciones obtenemos la ecuación fundamental que liga las observaciones (flujo $F_{\lambda} (c/s)$) de las estrellas estándar cuya magnitud fuera de la atmósfera es conocida $m_{\lambda}^o$ con la constante instrumental $C_{\lambda}$, el coeficiente de extinción $K_{\lambda}$ y la masa de aire $sec(z)$. 

Podemos construir la gráfica $m_{\lambda}^o + 2.5 \times log_{10} F_{\lambda} (c/s)$ versus $sec(z)$ en la que cada observación de una estrella estándar proporciona un punto. El ajuste de una recta nos proporciona la ordenada en el origen que será $C_{\lambda}$ y la pendiente $K_{\lambda}$. Los puntos seguirán una recta (recta de Bouguer) si el coeficiente de extinción ha permanecido constante a lo largo de la noche que es una condición impuesta a las noches fotométricas. O al revés, cuanto más se separen estas observaciones de una recta peor ha sido la noche. 


```{figure} /_static/lecture_specific/fotometria/foto_16_ecuacion.png
---
width: 600px
name: ecuacion-fig
---
```
El coeficiente de extinción varía a lo largo de la noche para noches de baja calidad. La transparencia de la atmósfera no tiene por qué ser la misma en todas las direcciones. Las noches fotométricas deben tener transparencia constante en el tiempo y la dirección.

La importancia de esta ecuación es que diferentes estrellas observadas en varios momentos y masas de aire contribuyen a determinar las constantes de la calibración. Si sólo deseáramos determinar la magnitud de un objeto fuera de la atmósfera podríamos observarlo durante toda la noche y usando la ecuación $m_{\lambda}=m_{\lambda}^o + K_{\lambda} \; sec(z)$ extrapolar a $sec(z)=0$ (fuera de la atmósfera). 

```{figure} /_static/lecture_specific/fotometria/foto_17_Bouguer_1.png
---
width: 600px
name: Bouguer_1-fig
---
Ejemplo de dos rectas de Bouguer ajustadas a observaciones en bandas B y V de Johnson. Nótese la pendiente mayor en la banda B (mayor coeficiente de extinción).
```

```{figure} /_static/lecture_specific/fotometria/foto_18_Bouguer_2.png
---
width: 600px
name: Bouguer_2-fig
---
La dispersión de los datos da idea de la calidad de la noche y permite estimar la precisión de la fotometría. 
```

```{figure} /_static/lecture_specific/fotometria/foto_19_absoluta_metodo.png
---
width: 600px
name: Bouguer_3-fig
---
Las observaciones auxiliares de estrellas estándar nos permiten determinar las constantes instrumentales y el coeficiente de exrtinción de esa noche.  
```


```{figure} /_static/lecture_specific/fotometria/foto_20_absoluta_calibracion.png
---
width: 600px
name: Bouguer_4-fig
---
Con el flujo en c/s de nuestro objeto de interés podemos determinar la magnitud instrumental y luego corregirla del efecto de la atmósfera gracias a que hemos determinado previamente $C_\lambda$ y $K_\lambda$ 
```

## Observaciones de calibración para fotometría absoluta
Se deben seleccionar estrellas estándar de l sistema fotométrico empleado y observarlas en diferentes momentos a lo largo de la noche. Normalmente se haven pausas en las observaciones de los objetos problema para hacer series de observaciiones de estrellas estándar, dos o tres cada noche. Esto permite disponer de medidas en diferentes horas para comprobar la estabilidad de la noche. Se eligen los momentos que no interfieran con nuestro proyecto científico y seleccionamos estrellas para conseguir muestrear a diferentes alturas sobre el horizonte para aumentar el rango de masas de aire.  
Durante la observación se puede comprobar si esta estabilidad en cuanto a la transparencia atmosférica se mantiene con ayuda de los instrumentos dedicados a esta monitorización que tiene cada observatorio. Por ejemplo [CAHA extinction monitor](http://www.caha.es/CAVEX/cavex.php) es una cámara de 55 grados de campo de visión que observa en dirección norte continuamente para medir el flujo en banda Johnson V de unas 15 o 20 estrellas brillantes y determinar la extinción que puede ser consultada en tiempo real. 

Para seleccionar las estrellas se puede recabar la información de artículos y páginas web. Por ejemplo Landolt & Uomoto de 2007 The Astronomical Journal, Volume 133, Issue 3, pp. 768-790 [Optical Multicolor Photometry of Spectrophotometric Standard Stars](https://iopscience.iop.org/article/10.1086/510485)

- [ING standards](http://www.ing.iac.es/~astrosw/standards.html)
- [ESO Optical and UV Spectrophotometric Standard Stars](https://www.eso.org/sci/observing/tools/standards/spectra.html)
- [CAHA Standard Stars and On-line Surveys ](http://www.caha.es/pedraz/SSS/sss.html)

Para elegir los mejores momentos de observación de las estrellas estándar se usan las aplicaciones que muestran la posición de las estrellas a lo largo de la noche como 

- [ING STARALT](http://catserver.ing.iac.es/staralt/index.php)
- [CAHA VES](http://www.caha.es/pedraz/ves.html)

```{figure} /_static/lecture_specific/fotometria/foto_38_standard_visibility.png
---
width: 800px
name: visibility-fig
---
Gráfico con las alturas y masas de aire de estrellas estándar que pueden ser observadas una noche particular. 
```
En el gráfico realizado con STARALT de la figura se muestra cómo las estrellas de la lista culminan a diferentes horas de la noche de observación de acuerdo a su ascensión recta. El eje Y muestra alturas (izda.) y masas de aire (dcha.) para cada estrella. De todas las estrellas de la lista original se han seleccionado tres (marcadas en rojo) que se observarán en los momentos marcados en magenta. Este es un ejemplo simplificado ya que normalmente se observan más estrellas.

## Transformación al sistema estándar 
Los sistemas fotométricos se definen con unas bandas fotométricas y un conjunto de estrellas estándar. Cuando se pretende hacer fotometría refereida a un cierto sistema se busca una instrumentación que proporcione bandas similares. Por mucho cuidado que se tenga cada banda depende de los filtros empleados y de la respuesta espectral del CCD y seguramente difiere de lo empleado a la hora de difinir el sistema fotométrico. Dicho de otro modo la banda Johnson V que estamos usando no es exactamente la banda V que definió Johnson: existen pequeñas diferencias en la banda de paso.

Cuando hacemos fotometría absoluta observamos estrellas cuya magnitud en las bandas del sistema fotométrico son conocidas. Son nuestras fuentes calibradoras. Eso permite determinar el punto cero (zero point) de nuestro sistema ($C_\lambda$, constante instrumental) que nos permite pasar de flujos medidos a magnitudes en esa banda. Ocurre con frecuencia que la calibración no es muy buena y muestra dispersión incluso en noches fotométricas y que por lo tanto no es achacable a la variabilidad de la transmisión de la atmósfera.  

```{figure} /_static/lecture_specific/fotometria/foto_21_comp_v_pass.png
---
width: 600px
name: Band_differences-fig
---
REPETIR
The transmission curves of the standard Bessell V passband (which is a model for manufacturers of filters), and the "Harris V" filter at the WIYN Telescope at Kitt Peak National Observatory
From: http://spiff.rit.edu/classes/phys445/lectures/color_terms/color_terms.html
```

```{figure} /_static/lecture_specific/fotometria/foto_22_hot-cool.png
---
width: 600px
name: Hot-cool-fig
---
REPETIR
Para estrellas de diferentes tipos espectrales estas diferencias de paso de banda son importantes.
From: http://spiff.rit.edu/classes/phys445/lectures/color_terms/color_terms.html
```

El número de total de fotones $N_\gamma$ ($fotones/s/cm^2$) integrado en la banda fotométrica depende del espectro del objeto modulado por la respuesta espectral del sistema $T(\lambda)$ (véase fotometría sintética). Al integrar los espectros de estrellas de diferentes tipos espectrales modulados por esas respuestas ligeramente diferentes producirán deasjustes que tenemos que corregir.

En el cuaderno de Jupyter 'Fotometria 1' se muestra un ejemplo de fotometría absoluta con observaciones en el JKT del observatorio del Roque de los Muchachos realizadas en Julio de 1999 para la tesis doctoral de Pablo Pérez González. Mostramos aquí sólo algunas gráficas.

```{figure} /_static/lecture_specific/fotometria/foto_23_JKT_color-term.png
---
width: 600px
name: color-term-1-fig
---
Gráfica para las observaciones de estrellas estándar de la noche 7 de la campaña de obsercvación. Se ha codificado el color de cada observación de acuerdo al índice de color de la estrella estándar.
```
Se observa que las estrellas más rojas (índice de color (B-V) más grande) se separan hacia arriba del ajuste sencillo de la recta de Bouguer y viceversa. Pablo Pérez Gonzalez ajustó un término de color en la forma 
\begin{equation*}
m_B + 2.5 log(F_B)  =  C - K_B X + K_{B-R} (B-R) 
\end{equation*}

resultando

```{figure} /_static/lecture_specific/fotometria/foto_24_JKT_color-term-2.png
---
width: 600px
name: color-term-2-fig
---
La dispersión original de los datos observacionales (izda.) ha quedado reducida con la corrección de color (dcha.).
```

|Night   |  $C_B$ | $K_B$ | $K_{B-R}$ |

|Night 1 | 23.096 | 0.506 | 0.045     |

|Night 2 | 22.770 | 0.204 | 0.056     |

|Night 6 | 22.754 | 0.197 | 0.061     |

|Night 7 | 22.872 | 0.289 | 0.061     |

El resultado final del ajuste de rectas de Bouguer a cada noche muestra que la primera noche fue de peor transparencia. Las constantes instrumentales determinadas son un poco diferentes de noche a noche, lo que no es esperable. Una mejor determinación sería obligar en los ajustes a que la constante instrumental sea la misma a lo largo de toda la campaña. 

Para aplicar este término de color a las observaciones de los objetos problema se necesita observar éstos en al menos las dos bandas utilizadas y, por supuesto, conocer las magnitudes de las estrellas estándar en estas bandas.

## Pasos en la reducción de las observaciones:

    1. Medir los flujos observados de cada estrella estándar
        - Integrar señal en un círculo que contenga la estrella y otro(s) cercanos para obtener el valor del fondo de cielo
        - Restar para obtener flujo neto de la estrella --> F(cuentas)
        - Dividir por el tiempo de exposición -->  F (cuentas/s)
    2. Preparar una tabla con los resultados de cada observación
        - Anotar la masa de aire de cada observación X = sec(z)
        - Convertir flujos a magnitudes instrumentales
        $m = C -2.5 log F(c/s)$        (C constante arbitraria)

    3. Obtener la constante instrumental y el coeficiente de extinción
       - Representar 
       - Ajustar recta de Bouguer   

Una práctica completa de fotometría absoluta puede encontrase en [CCD photometry project](http://skinakas2.physics.uoc.gr/en/outreach/projects/CCD_Photometry_project2/P2_CCD_PHOTOMETRY.pdf)
