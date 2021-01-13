# Fotometría
 

```{note}
Este capítulo asume conocimientos básicos de fotometría astronómica 
explicados en la signaturas de Astrofísica previas al Máster. 
En particular de Astrofísica y de Astronomía Observacional del Grado en Física 
y de Instrumentación Astronómica del máster en Astrofísica.  
```

## Fotometría astronómica


La fotometría astronómica es una medida directa del flujo de energía recibido de los objetos celestes. Las medidas se realizan en bandas fotométricas que seleccionan el intervalo espectral. Es una técnica menos exigente que la espectroscopía en cuanto a tiempo de exposición porque se integra el flujo en un intervalo espectral. Las bandas fotométricas están caracterizadas por la combinación de la transmisión de los filtros y la respuesta espectral de los detectores (y por todos los elementos ópticos en el telescopio). 

Con la fotometría astronómica realizada mediante detectores de imagen se pueden obtener las magnitudes de todos los objetos del campo registrados de manera simultánea. Esto es muy útil si observaos un cúmulo de estrellas o un campo cosmológico lleno de galaxias. La combinación de observaciones en diferentes bandas fotomçetricas nos ayuda a determinar las propiedades de estos objetos celestes. Con los datos de magnitudes y colores podemos, por ejemplo, clasificar las estrellas usando un diagrama color-color. El análisis de las de curvas de luz (variación temporal de su magnitud) informa sobre la naturaleza de las estrellas variables y sobre parámetros de las binarias. La fotomería se emplea también para determinar distancias y tamaños. 

```{figure} /_static/lecture_specific/fotometria/foto_00_spectra-color.png
---
height: 600px
name: spectra-color-fig
---
(Izquierda) Bandas U, B, y V de Johnson (abajo) junto a espectros de estrellas de fiferentes tipos espectrales. (Derecha) Las estrellas de diferentes tipos espectrales aparecen en diferentes lugares del diagrama color-color  (U-B) versus (B-V). 
```

Como ejemplo de cómo se buscan y encuentran objetos a alto redshift usando técnicas fotométricas se muestra el trabajo de Esther Hu y colaboradores (["An Extremely Luminous Galaxy at z = 5.74" Esther M. Hu, Richard G. McMahon, & Lennox L. Cowie 1999, ApJ Letters, 522, L9)](https://iopscience.iop.org/article/10.1086/312205)

```{figure} /_static/lecture_specific/fotometria/foto_05_Hu_images.png
---
width: 800px
name: images-Hu-fig
---
 Keck image of the field around a luminous galaxy at redshift 5.74 in the Constellation of Aquarius. Deep exposures at far red and infrared wavelengths were combined to make this picture. An image taken in a narrowband filter which captures light from the redshifted 1216 Å Hydrogen Lyman alpha line excited by star formation is responsible for the green halo around the faint, distant galaxy at the center, and shows that substantial star formation is taking place. (Derecha) Imágenes individuales en diferentes bandas fotométricas incluyendo la banda estrecha en 8185 Å (anchura 115 Å). 
```
```{figure} /_static/lecture_specific/fotometria/foto_04_Hu_SED.png
---
width: 800px
name: SED-Hu-fig
---
Distribución espectral de energía (SED) del candidato a galaxia a z=5.74 mostrando un exceso de emisión en el filtro estrecho sintonizado a Ly alpha a ese desplazamiento al rojo. 
```
```{figure} /_static/lecture_specific/fotometria/foto_06_Hu_spectrum.png
---
width: 800px
name: spectrum-Hu-fig
---
Una vez tomado el espectro de la candidata ('folow-up observations') se comprueba que efectivamente tiene Ly alpha en emisión al z esperado. 1216 x (1+z) = 1216 x 6.8 = 8269 Å  
```


[Más información](http://www.ifa.hawaii.edu/faculty/hu/redshift_5.7.html)




### Sistemas fotométricos

Una información completa sobre los sistemas fotométricos se puede encontrar en la revisión Bessel 2005ARA&A..43..293B. El enlace al documento en [Standard Photometric Systems by Michael S Bessel ](http://www.mso.anu.edu.au/~bessell/araapaper.pdf)

Los sistemas fotométricos surgen de la necesidad de estudiar diferentes tipos de objetos celestes. Se caracterizan por un conjunto de bandas fotométricas. Las bandas fotométricas están definidas por la transmisión del filtro y la respuesta espectral de los detectores. 

Tal vez el más conocido es el sistema de Johnson-Cousins UBVRI que nos sirve como ejemplo de fotometría de banda ancha. Este sistema usa en su origen fotomultiplicadores que permite mediante diferentes combinaciones de filtros definir las bandas espectrales mencionadas. Se aprovechó la mejor tecnología de detectores del momento y filtros comerciales. Para defiir la banda V original, por ejemplo, Johnson(1955) usó en principio filtros Schott GG14 que ahora se llaman GG495 (corte azul de la banda) y la caída de respuesta espectral del fotocátofo S4 del fotomultiplicador 1P21. Véase, por ejemplo, ['UBVRI passbands' by Bessell, M. S. 1990PASP..102.1181B](http://adsabs.harvard.edu/full/1990PASP..102.1181B)

Los sistemas fotométricos deben ser definidos con ayuda de observaciones de estrellas en esas bandas de forma que se establece una lista de magnitudes y colores estándar para un conjunto de estrellas que sirven de referencia. Los astrónomos que quieran medir objetos celestes en un sistema estándar deben usar la instrumentación adecuada y transformar sus observaciones a ese sistema estándar mediante observaciones de estrellas de la lista original o de estrellas bien calibradas en ese sistema (estrellas estándar). Las magnitudes observadas deben ser corregidas de extinción atmosférica (magnitudes fuera de la atmósfera). Para ello se necesitan observaciones de fotometría absoluta como se verá más adelante.

De acuerdo al ancho de banda los sistemas fotométricos se clasifican 
Banda ancha    |    Δλ < 100 nm     | (broad-band)
Banda media    |  7 nm < Δλ< 40 nm  | (intermediate-band)
Banda estrecha |    Δλ < 7 nm       | (narrow-band)

Existen versiones modernas de los sistemas fotométricos más antiguos que se han ido desarrollando según se disponía de detectores más sensibles y, en particular de detectores panorámicos como los CDs.

Se pueden citar algunos ejemplos de sistemas fotométricos: Johnson-Cousins-Glass UBVRIJHKLM, Strömgen u v b y bn bw, Sloan u’ g’ r’ i’ z’. Los astrónomos aficionados suelen observar con filtros de colores que definen bandas RGB similares a las que producen los sistemas de cámaras de color que usamos en nuestra vida diaria. 


```{figure} /_static/lecture_specific/fotometria/foto_10_UBVRI.gif
---
width: 800px
name: Girardi-UBVRI-fig
---
```
```{figure} /_static/lecture_specific/fotometria/foto_12_sloan.png
---
width: 800px
name: Girardi-sloan-fig
---
Representación de las bandas de diversos sistemas fotométricos junto al espectro del sol y de una estrella azul y otra roja. Fuente: Girardi, L. et al. "Theoretical isochrones in several photometric systems
I. Johnson-Cousins-Glass, HST/WFPC2, HST/NICMOS, Washington, and ESO Imaging Survey filter sets" A&A 391, 195-212 (2002) and Girardi, L. et al. “Theoretical isochrones in several photometric systems. II. The Sloan Digital Sky Survey ugriz system.” A&A 422 (2004): 205-215.
```


### Sistemas Vega, AB y ST

Una importante fuente de confusión, incluso dentro de la literatura publicada por
astrómos profesionales, es la clara definición del sistema fotométrico utilizado. Esto incluye 3 ingredientes. El primero lo define la curva de sensibilidad espectral del filtro (en la gráfica se representan los tradicionales filtros de Johnson-Cousins UBVRI, usando las curvas actualizadas por Bessell & Murphy 2012). El segundo es el parámetro físico a integrar dentro de cada filtro. Aquí hay varias opciones: i) energía (en unidades FLAM erg s-1 cm-2 Å-1, o FNU erg s-1 cm-2 Hz-1), o ii) fotones (en unidades PHOTLAM photon s-1 cm-2 Å-1, o PHOTNU photon s-1 cm-2 Hz-1).
 
El tercer ingrediente es el espectro de referencia que determina el cero en la escala de magnitudes: sistema VEGA, sistema AB (Oke & Gunn, 1983, referencia constante en densidad de flujo por unidad de frecuencia), o sistema ST (Koornneef et al., 1986, referencia constante en densidad de flujo por unidad de longitud de onda). 

```{figure} /_static/lecture_specific/fotometria/foto_13_Vega_AB_ST.png
---
width: 800px
name: Cardiel-Vega-AB-ST-fig
---
Representación de los tres espectros de referencia (en unidades PHOTLAM).
```

La magnitud en una cierta banda fotométrica S(λ) de un objeto celeste de disrtribución espectral de energía F(λ) se determina como,

$$
  m(\lambda) =  -2.5 log_{10} \int_0^\infty \frac{F(\lambda) S(\lambda) d\lambda }{F_o(\lambda) S(\lambda) d\lambda }
$$

donde $F_o(\lambda)$ es la distribución espectral de energía de la fuente de referencia para fijar el punto cero de la fotometría. Por ejemplo para la banda V de Johnson-Cousins V band podemos usar el espectro de Vega ($\alpha$ Lyrae) y fijar V(Vega) = 0 (como en su definición original, aunque luego resulta que V(Vega) = 0.03) o, la referencia absoluta (AB) de 3631 definido por Oke (1974) $F_o(\lambda)  = 3631 \times (c/\lambda^2) \times 10^{-26} W/m^2/m$ donde   $𝑐 = 2.99792458 × 10^8 m s^{-1}$ es la velocidad de la luz en el vacío, $\lambda$ es la longitud de onda en m y Jy (jansky) es una unidad fuera del sistema internacional SI de irradiancia espectral Jy = $10^{-26}
W m^{-2} Hz^{-1}$. Puede verse un análisis completo en [Bará et al (2020)](https://eprints.ucm.es/60386/19/zamorano143postprint.pdf).



Los sistemas fotométricos usaban tradicionalmente a Vega como estrella de referencia y el problema es la dificultad de obtener una calibración absoluta precisa de esta estrella. Por eso actualmente se prefiere usar magnitudes AB.

### Fotometría visual y fotográfica
La clasificación de estrellas de acuerdo a su brillo aparente que realizó el astrónomo griego Hiparcos está basada en la comparación de sus observaciones a simple vista sin ninguna instrumentación óptica. Estableció una escala de magnitudes siendo las estrellas en la categoría de primera magnitud las más brillantes. Esta 'fotometría visual' utiliza el ojo humano como detector y no emplea filtros. Por lo tanto la banda de paso viene definida por la respuesta espectral del ojo. Todavía hoy en día se utiliza la fotometría visual en observaciones de astrónomos aficionados que pueden observar y medir (por comparación) las magnitudes de estrellas más débiles que el límite impuesto por la sensibilidad del ojo.

Con el desarollo de la fotografía a mediados del siglo XIX se dispuso de un detector que colocado en el foco de un telescopio permitía registrar estrellas más débiles y en un rango espectral diferente a la banda visual. Con emulsiones fotográficas sensibles en diferentes intervalos espectrales (detector) y filtros se podían tomar imágenes de campos estelares o de objetos extensos (al ser un detector de imagen o panorámico) en difrentes bandas fotométricas. Estas observaciones de 'fotometría fotográfica', a diferencia de las visuales, dejan una placa fotográfica  que, correctamente almacenada, puede volver a medirse  las veces que se desee incluso después de muchos años. aunque su formato no es digital, las placas pueden ser escaneadas para producir un fichero tratable con ordenadores.

### Fotometría fotoeléctrica
Los astrónomos utilizaton en sus observaciones los fotodetectores más sencillos en cuanto éstos estuvieron disponibles. La 'Fotometría Fotoeléctrica' supuso un gran avance en sensibilidad permitiendo observar y medir objetos más débiles. Los fotómetros fotoeléctricos tienen como detector una célula fotoeléctrica o mejor un fotomultiplicador. Este dispositivo 
electrónico transforma los fotones incidentes en corriente eléctrica que puede ser medida. Las ventajas principales son su linealidad, de la que carece la emulsión fotográfica, y su mayor eficiencia cuántica.
- Stebbins, Whitford & Kron  (ca. 1940)         fotocélulas
- Johnson, Morgan, Whitford et al. (ca. 1950)   fotomultiplicadores
  - RCA 1P21 (fotomultiplicador sensible al azul)
  - Sistema de Johnson  bandas U B V con RCA 1P21
- Sistema de Strömgren ubvy
- Kron (1958)    Fotocátodo S1  (sensible al rojo)
- Johnson et al. (1966)   bandas R I
   - Fotocátodo S25 y GaAs (mucho más sensibles que 1P21)
- Bessel (1976) U B V R I con el mismo fotomultiplicador
   - Aumento de la lista de estándars primarias y secundarias
       Cousins (1976-1980)     Cousins UBVRI
       Landolt (1973-1983)     Landolt UBVRI

Desgraciadamente estos sistemas son algo diferentes por usar filtros distintos.


### Fotometría CCD
La fotometría fotoeléctrica sólo permite observar una estrella cada vez o una parte de un objeto extenso, es decir que no tiene la capacidad de un detector de imagen con resolución espacial. La 'Fotometría CCD' (casi la única que se usa en la actualidad) desplazó a la fotometría fotoeléctrica ya que tiene como gran ventaja el uso de un detector panorámico. Las imágenes obtenidas con un detector CCD contienen información de los objetos celestes contenidos en el campo de visión del sistema. Estas observaciones simultáneas de múltiples objetos tienen la gran ventaja del ahorro de tiempo de observación y la garantía de observación en el mismo lapso de tiempo lo que es ideal para fotometría diferencial.

Por citar algunos inconvenientes tenemos los propios de la observación con CCDs (tiempos muertos leyendo el detector, por ejemplo) y el procesado de las imágenes CCD. Con la fotometría fotoeléctrica se obtenían mejor precisión fotométrica en menos tiempo de observación. También existen problemas relacionados con la variación de la transmisión de los filtros interferenciales con el ángulo de llegada de la luz, lo que se traduce en diferencias de banda de paso en zonas de la imagen según te alejas del eje óptico. También existe una gran variedad de CCDs en el mercado con diferencias considerables en la respuesta espectral en el azul que no facilitan la calibración de la banda U, por ejemplo.

Todos estos inconvenientes quedan en un segundo plano con la facilidad de uso de los CCDs y de su procesado posterior. Los CCDs se sitúan en criostatos que mantienen la temperatura del chip a temperatiras bajas (-120ºC típicamente) para evitar ruido térmico y con estabilización de temperatura para mantener su sensibilidad constante a lo largo de la observación.

### Fotometría absoluta
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

#### Ecuaciones fundamentales
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
name: Bouguer_2-fig
---
Las observaciones auxiliares de estrellas estándar nos permiten determinar las constantes instrumentales y el coeficiente de exrtinción de esa noche.  
```


```{figure} /_static/lecture_specific/fotometria/foto_20_absoluta_calibracion.png
---
width: 600px
name: Bouguer_2-fig
---
Con el flujo en c/s de nuestro objeto de interés podemos determinar la magnitud instrumental y luego corregirla del efecto de la atmósfera gracias a que hemos determinado previamente $C_\lambda$ y $K_\lambda$ 
```

#### Observaciones de calibración para fotometría absoluta
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

### Transformación al sistema estándar 
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

#### Pasos en la reducción de las observaciones:

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


### Fotometría diferencial
La fotometría diferencial es un método menos exigente que la fotometría absoluta ya que no requiere de noches fotométricas. La idea es comparar las diferencias de magnitud de objetos problema con otros de magnitud conocida. Es el método que se usa en la fotometría visual en donde se comparan los brillos de las estrellas variables con cartas donde se marcan estrellas de referencia. De esta forma se obtienen curvas de luz. También sirve para salir del paso cuando no se ha podido hacer fotometría absoluta pero disponemos  de estrellas de referencia en el campo de las imágenes de los objetos problema.


```{figure} /_static/lecture_specific/fotometria/foto_25_AAVSO_Beta_Per.jpg
---
width: 400px
name: Beta-Per-fig
---
Carta de la [AAVSO](https://www.aavso.org/variable-star-charts) de Beta Persei.
```

```{figure} /_static/lecture_specific/fotometria/foto_26_diferencial_1.png
---
width: 600px
name: Foto-diferencial-1-fig
---
Observaciones consecutivas en diferentes instantes del objeto problema (estrella variable en este caso) y la estrella de referencia en el mismo campo.
```
```{figure} /_static/lecture_specific/fotometria/foto_27_diferencial_2.png
---
width: 600px
name: Foto-diferencial-2-fig
---
Medidas de las estrellas problema y de referencia y determinación de la dirferencia de magnitud en el instante de la observación.
```

Es importante notar que en las dos ecuaciones el valor de $C_\lambda$ es el mismo ya que están siendo observadas en la misma imagen CCD con la misma instrumentación y que el coeficiente de extinción ($K_\lambda$ que tampoco conocemos) es también el mismo ya que se observan simultáneamente.

### Fotometría de objetos extensos
Las medidas fotométricas de objetos puntuales como las estrellas se realizan sumando la señal registrada en la imagen en una abertura generalmente circular que contenga toda la estrella. Para restar el brillo de fondo de cielo (sky background) y obtener el flujo neto se mide y promedia en aberturas similares en posiciones cercanas a la estrella o en un anillo cercano centrado en la imagen de la estrella. 

#### magnitud integrada
En el caso de objetos extensos como galaxias podemos realizar la misma operación para obtener la magnitud integrada (integrated magnitude). En este caso la abertura tiene que contener la imagen de la galaxia. Para estimar el brillo de fondo de cielo podemos utilizar aberturas más pequeñas y escalar por el área de las mismas.

```{figure} /_static/lecture_specific/fotometria/foto_28_extensos.png
---
width: 400px
name: Foto-extensos-1-fig
---
Medida del flujo total de una galaxia para obtener la magnitud integrada. Se observan aberturas en la imagen donde se ha medido para estimar el brillo de fondo de cielo. Como se aprecia se seleccionan zonas libres de imágenes de otros objetos del campo.
```

Flujo neto   $F = (F+S) - S  $

Magnitud instrumental $m = -2.5 log F(c/s)$

#### brillo superficial
El brillo superficial es una medida de la magnitud por unidad de área y se expresa en $mag/arcsec^2$ (magnitudes por segundo de arco cuadrado). Como la escala de magnitudes es logarítmica:

Brillo superficial  $S = -2.5 log F(c/s/A) = m -2.5 log(A)$

con el área $A$ expresada en $arcsec^2$.

#### isofotas
Son las líneas que unen los puntos de la imagen con igual brillo superficial. Son curvas de nivel en los plots de contornos.

```{figure} /_static/lecture_specific/fotometria/foto_29_extensos_2.png
---
width: 400px
name: Foto-extensos-2-fig
---
Imagen de una galaxia espiral en codificación de falso color con azul en el nivel más bajo y rojo en el más alto.
```

```{figure} /_static/lecture_specific/fotometria/foto_30_extensos_3.png
---
width: 400px
name: Foto-extensos-2-fig
---
Plot de contornos de la galaxia espiral con niveles desde $24.5\;mag/arcsec^2$ y pasos de 
$0.5\;mag/arcsec^2$
```

#### brillo de fondo de cielo
El cielo libre de objetos celestes brilla. En realidad lo que brilla es la atmósfera terrestre que dispersa la luz que le llega. El mayor contribuyente al brillo de cielo es la Luna (espectro solar reflejado por la Luna) en sitios de poca contaminación lumínica. Las noches de observación se llaman oscuras cuando la Luna no está presente y no aumenta el brillo de cielo. Las noches brillantes tienen brillo de cielo mayor por causa de la Luna. Noches grises tendría parte de noche oscura. 

```{figure} /_static/lecture_specific/fotometria/foto_34_Brillo_Luna.png
---
width: 400px
name: Foto-brillo_luna-fig
---
Aumento del brillo de cielo con la presencia de la Luna durante las observaciones astronómicas. [Benn & Ellison (2007)](http://www.ing.iac.es/Astronomy/observing/conditions/skybr/skybr.html).
```

Además tenemos otros contribuyentes como la Luz zodiacal (luz solar difundida por polvo interplanetario) que sólo es posible apreciar en cielos muy oscuros, la radiación estelar difundida por granos de polvo interestelar y las auroras.

Airglow: Es la luminiscencia nocturna del cielo emitida por átomos y moléculas de la alta atmósfera que son excitados por la radiación solar UV durante el día.
- OI 5577/6300/6363Å  (como en las auroras)
- NaD 5890/6 Å 
- OH Bandas vibro-rotacionales de Meinel (en el rojo e infrarrojo)
- O2 8645Å 	O2 bandas de Herzberg

El airglow depende de la actividad solar y es 1000x más brillante de día. Su intensidad varía de forma errática en escalas de tiempo de minutos y en un factor 2 durante la noche (en especial las bandas de OH). La emisión no depende de la latitud terrestre (salvo zonas de auroras) y tiene su máximo en distancias cenitales z≈80° (cerca del horizonte). Se origina en una capa fina a h=100-300 km.

```{figure} /_static/lecture_specific/fotometria/foto_31_espectro_cielo_oscuro.png
---
width: 800px
name: Foto-espectro_cielo-fig
---
Espectro del cielo en una noche sin luna en el Observatorio del Roque de los Muchachos. La Palma night-sky brightness, Benn & Ellison 1998, ING Technical Note 115.
```

Luminiscencia de la alta atmósfera: Las observaciones desde satélites en órbitas cercanas se ven afectadas por:
- $Ly_\alpha$ geocoronal (difusión resonante múltiple de la luz solar en la geocorona).
- Luminiscencia producida por el propio satélite que en su movimiento excita átomos y moléculas (en especial O2).



```{figure} /_static/lecture_specific/fotometria/foto_32_brillo_contribuyentes.png
---
width: 800px
name: Foto-brillo_contribuyentes-fig
---
Contribuyentes al brillo de cielo nocturno. $S10 = 27.78 mag/arcsec^2$
 $220 S10 = 21.9 mag/arcsec^2$. S10, a unit of measurement of surface brightness used in astronomy and defined as the surface brightness of a star whose visual magnitude is 10 and whose light is smeared over one square degree.
```

Por desgracia un contribuyente importante es la contaminación lumínica. Por eso los observatorios se situan en lugares alejados de la actividad humana. El brillo de cielo nocturno es un factor de calidad a la hora de elgir la localización de un observatorio astronómico.

```{figure} /_static/lecture_specific/fotometria/foto_33_sand_Madrid.png
---
width: 800px
name: Foto-espectro-brillo-cielo-Madrid-fig
---
El espectro del cielo nocturno de Madrid presenta las líneas del espectro de las  lámparas del alumbrado público.
```

> En los estudios de contaminación lumínica se usa el **Brillo de cielo nocturno** (*Night Sky Brightness*) que contiene la contribución de los objetos celestes en el área muestreada. No se debe confundir con el **Brillo de fondo de cielo** (*Night sky background*) que se mide en zonas sin contribución de estrellas.

>**Ejemplo de cálculo de Brillo de fondo de cielo**
Supongamos que se miden 30 c/s/pixel en una imagen CCD  obtenida con un telescopio de distancia focal f=2m y píxeles de 50 micras de lado con un sistema de constante instrumental C=20 en una cierta banda.
>
>$m = C – 2.5 log F(c/s/pixel)$   -->  $m = 20 -  2.5 x log10(30) = 16.31 mag/pixel$
>
> Escala de placa $P = 206265 / f(mm) = 206265 / 2000 = 103.13 arcsec/mm = 0.10313 arcsec/\mu m$
>
>Área de 1 pixel sobre el cielo    $50 micras \times 0.10313 arcsec/\mu m = 6.19 arcsec$
área de cielo en cada pixel                $6.19 \times 6.19 = 38.3 arcsec^2$
>
> $m = C – 2.5 log F(c/s/arcsec2) =16.31 + 2.5 log 38.3 = 16.31 + 3.96 = 20.27 mag/arcsec^2$  

#### perfiles de brillo ####
Se puede obtener la variación del brillo superficial de un objeto extenso con la distancia al centro mediante el ajuste de las isofotas a elipses. Los perfiles de brillo superficial de las galaxias (por ejemplo) promediados acimutalmente sirven para su clasificación morfológica y para determinar alguna de sus propiedaes.

```{figure} /_static/lecture_specific/fotometria/foto_36_Vitores_perfiles.png
---
width: 800px
name: Foto-Vitores_perfiles-fig
---
Representación gráfica en escala de grises, en contornos (isofotas) y perfil de brillo ajustado a un bulbo y un disco para galaxias de la exploración UCM (UCM survey) de la tesis de Álvaro Vitores.
```
```{figure} /_static/lecture_specific/fotometria/foto_37_Vitores_perfiles_2.png
---
width: 800px
name: Foto-Vitores_perfiles-2-fig
---
Representación gráfica en escala de grises, en contornos (isofotas), perfil de brillo ajustado a un bulbo y un disco y variación del ángulo de posición y elipticidad de elipses ajustadas a las isofotas para galaxias de la exploración UCM (UCM survey) de la tesis de Álvaro Vitores.
```


### Fotometría sintética a partir de espectros
Se pueden determinar las magnitudes en un cierto sistema fotométrico de los objetos cuyas densidades espectrales de energía sean conocidas siempre que se disponga de las respuestas espectrales de las bandas fotométricas.

$S(\lambda)$  Paso de banda del sistema. Convolución de la atmósfera, reflectividad de los espejos del telescopio, transmisión del filtro, eficiencia cuántica del detector (todas dependientes de la longitud de onda).

$F(\lambda)$ Flujo de la fuente en $erg/cm^2/s/Å$

$$
  N_{fotones} =  \int_0^\infty (F(\lambda)/h\nu) S(\lambda) d\lambda 
  = \int_0^\infty (\lambda F(\lambda)/hc) S(\lambda) d\lambda 
$$

La densidad de flujo media pesada por la respuesta de la banda

$$
  <\lambda F(\lambda)> =  \int_0^\infty \frac{\lambda F(\lambda) S(\lambda) d\lambda }{\lambda S(\lambda) d\lambda }
$$

A. Pickles and É. Depagne (2010) PASP 122,898   
Bessel 2005, Annu. Rev Astron. Astrophys., 43, 293


## Observaciones de fotometría CCD

Los intrumentos  empleados para fotometría son cámaras CCD que disponen de una rueda de filtros seleccionables. Estas cámaras se elige en base a los requerimientos del proyecto de investigación y a su disponibilidad. Los parámetros importantes son el campo de visión que depende de la escala de placa del telescopio, de la amplificación de la cámara y del tamaño del CCD que se coloca en el plano focal de la cámara.

La lista de intrumentos para realizar fotometría de imagen y sus características se pueden consultar en los portales de los observatorios. Con la ayuda de los astrónomos de apoyo se configura de manera óptima a nuestras necesidades.

Como detector se emplea un CCD. Si el CCD es muy grande o la óptica de la cámara instrumento no es suficiente, sólo se usa parte de la imagen que proporciona el CCD. En ese caso se selecciona una región del mismo (ventana) en el momento de la observación  para no archivar ficheros innecesariamente grandes. Se ahorra espacio y tiempo de lectura del CCD.

Por ejemplo para las observaciones de CAFOS que proporciona un campo de visión de diámetro 16 arcmin y con un CCD tiene dimensiones de $2048 \times 2048$ píxeles se suele usar la parte central de $11 \times 11 \; arcmin^2$ que no está viñeteada y que corresponde a una ventana de $1024 \times 1024$ píxeles en el centro del CCD.  

```{figure} /_static/lecture_specific/fotometria/foto_39_CAFOS_window.png
---
width: 800px
name: Foto-CAFOS_window-fig
---
Recorte de la imagen CCD de CAFOS para seleccionar la zona central de $11 \times 11 \; arcmin^2$.
```
```{figure} /_static/lecture_specific/fotometria/foto_40_CAFOS_FoV.png
---
width: 600px
name: Foto-CAFOS_FoV-fig
---
Imagen completa de CAFOS mostrando la región útil y la ventana cuadrada que suele recortarse.
```

Las observaciones de fotometría de imagen incluyen 

- Las imágenes usadas para calibración del CCD: los BIAS y DARK para medir el nivel de pedestal y la corriente de oscuridad si la hubiera. De esta manera podemos retirar la parte aditiva de la señal.
Los Flat Field (bien con imágenes de lámparas en la cúpula ('Dome flats') o imágenes de cielo en crepúsculo (Sky flats') para determinar la variación espacial de la sensibilidad del CCD.

- Imágenes de los campos que contienen los objetos motivo de nuestro proyecto científico.

- Idem de estrellas estándar para calibración fotométrica. El flujo en las bandas fotométricas de estas estándares fotométricas es conocido y por comparación entre el resultado de la observación podemos determinar las constantes instrumentales y los coeficientes de extinción (véase fotometría absoluta).
