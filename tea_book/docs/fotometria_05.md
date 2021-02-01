
# Fotometría de objetos extensos
Las medidas fotométricas de objetos puntuales como las estrellas se realizan sumando la señal registrada en la imagen en una abertura generalmente circular que contenga toda la estrella. Para restar el brillo de fondo de cielo (sky background) y obtener el flujo neto se mide y promedia en aberturas similares en posiciones cercanas a la estrella o en un anillo cercano centrado en la imagen de la estrella. 

## magnitud integrada
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

## brillo superficial
El brillo superficial es una medida de la magnitud por unidad de área y se expresa en $mag/arcsec^2$ (magnitudes por segundo de arco cuadrado). Como la escala de magnitudes es logarítmica:

Brillo superficial  $S = -2.5 log F(c/s/A) = m -2.5 log(A)$

con el área $A$ expresada en $arcsec^2$.

## isofotas
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
name: Foto-extensos-3-fig
---
Plot de contornos de la galaxia espiral con niveles desde $24.5\;mag/arcsec^2$ y pasos de 
$0.5\;mag/arcsec^2$
```


## perfiles de brillo
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
## brillo de fondo de cielo
El cielo libre de objetos celestes brilla. En realidad lo que brilla es la atmósfera terrestre que dispersa la luz que le llega. El mayor contribuyente al brillo de cielo es la Luna (espectro solar reflejado por la Luna) en sitios de poca contaminación lumínica. Las noches de observación se llaman oscuras cuando la Luna no está presente y no aumenta el brillo de cielo. Las noches brillantes tienen brillo de cielo mayor por causa de la Luna. Noches grises tendría parte de noche oscura. 

```{figure} /_static/lecture_specific/fotometria/foto_34_Brillo_luna.png
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

