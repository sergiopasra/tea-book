# P2 Fotometría CCD

## Campaña de observación 
Se realiza la reducción de una campaña de observación de objetos extensos realizada
con el Nordic Optical Telescope (La Palma) en abril de 2008 (Fig. 4.5, izquierda). En particular, se trata del proyecto Calibrating the [OII]158 micron line as a star formation rate tracer (PI: A. Gil de Paz; Observadores: Pablo G. Pérez González & Jaime Zamorano). Los estudiantes deben seguir los pasos que se muestran a continuación.

### Descarga de los ficheros
Los ficheros de las observaciones se encuentran disponibles en un ftp anónimo, y el cuaderno de observación (logbook), ubicado en el Campus Virtual de la asignatura.

### Inspección de las imágenes
Examen de las cabeceras y clasificación de las imágenes por noche de observación y por
tipos: calibraciones e imágenes científicas.

### Examen visual de las imágenes
Determinación de la región útil del detector.

## Reducción de las observaciones.

### Generación del máster bias
### Corrección de bias 
### Generación de un máster flat field por filtro
### Procesado de las imágenes de estándares de flujo y científicas
Sustracción de bias, corrección de flat field (aplicando a cada imagen el obtenido con el mismo filtro).
### Eliminación de rayos cósmicos
mediante combinación de 3 o más imágenes similares (de existir), lo que precisa alineamiento previo, o limpieza individual mediante proceso semi-interactivo con el programa cleanest.

### Calibración astrométrica
Para ello se utilizará [Astrometry.net](http://astrometry.net/) y las herramientas disponibles en [AstrOmatic.net](15http://www.astromatic.net/).

### Calibración fotométrica
Determinación de las constantes instrumentales y coeficientes de extinción para cada noche.