# Introducción a la Fotometría 

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


## Sistemas fotométricos

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


## Sistemas Vega, AB y ST

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
