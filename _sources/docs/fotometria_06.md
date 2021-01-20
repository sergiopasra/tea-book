
# Fotometría sintética 

## Fotometría sintética a partir de espectros
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
