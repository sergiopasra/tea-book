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


# Calibración fotométrica y astrométrica



## Calibración fotométrica
Se trata de construir las rectas de Bouger para cada filtro y determinar las constantes instrumentales y coeficientes de extinción para cada noche.  
Veremos un ejemplo en el procesado de la segunda noche.


## Calibración astrométrica

Para un calibrado astrométrico dentro de una cadena de procesado de imágenes se puede usar software desarrollado para este fin como las herramientas disponibles en [AstrOmatic.net](http://www.astromatic.net/).

De momento vamos a ver ejemplos de utilización de [Astrometry.net](http://astrometry.net/) que funciona muy bien y sirve para la calibración astrométrica de unas cuantas imágenes sueltas.

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_1.png
---
width: 600px
name: astrometria-1-fig
---
Portada de la página web de [Astrometry.net](http://astrometry.net)
```

Este software también puede ser usado dentro de programas o scripts en terminal pero su uso más sencillo es a través de la interfaz web [http://nova.astrometry.net/](http://nova.astrometry.net/)


```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_2.png
---
width: 600px
name: astrometria-2-fig
---
Portada de la interfaz web de  [http://nova.astrometry.net/](http://nova.astrometry.net/).
```

Veamos el proceso en un ejemplo usando una imagen de M51. 

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_3.png
---
width: 300px
name: astrometria-3-fig
---
Interfaz para seleccionar la imagen a procesar. Se puede usar una dirección html. En este caso hemos buscado el fichero en nuestro ordenador.
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_5.png
---
width: 600px
name: astrometria-5-fig
---
A esta tarea se le asigna un número de orden y comineza el procesado.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_4.png
---
width: 600px
name: astrometria-4-fig
---
Al cabo de un rato (dependiendo de las tareas en la cola) se muestra la imagen subida. 
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_6.png
---
width: 600px
name: astrometria-6-fig
---
Durante el procesado puede verse una pantalla como la mostrada.
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_8.png
---
width: 600px
name: astrometria-8-fig
---
Finalmente se muestran los resultados: Coordenadas del centro de la imagen, escala de placa, orientación etc.
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_7.png
---
width: 600px
name: astrometria-7-fig
---
Las estrellas identificadas en el campo.
```

Podemos bajarnos el resultados como una imagen FITS donde la astrometría está incluida con los descriptores WCS. 

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_11.png
---
width: 600px
name: astrometria-11-fig
---
Descriptores WCS en la cabecera del fichero creado por Astrometry.net
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_9.png
---
width: 600px
name: astrometria-9-fig
---
La imagen original mostrada en DS9. Al mover el cursor por encima sólo nos proporciona coordenadas de imagen (píxeles).
```

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_10.png
---
width: 600px
name: astrometria-10-fig
---
La imagen procesada por Astrometry.net mostrada en DS9. Al mover el cursor por encima se muestran las  coordenadas de imagen (píxeles) y las coordenadas ecuatoriales. Véase además el recuadro de arriba con las flechas de orientación de la imagen.
```

Astrometry.net no ha necesitado que le demos ninguna pista de escala, campo de visión etc. Si le proporcionamos indicaciones puede realizar la tarea mucho más rápido.


```{admonition} Astrometry.net Ejercicio 1
Use una imagen propia o descargada de internet para realizar la astrometría con esta herramienta. Nótese que la imagen puede ser una imagen profesional en formato FITS o una fotografía en formato jpeg o png etc.
```

Ejemplo con una fotografía del cometa [21P/Giacobini-Zinner [2018]](https://cometografia.es/021p-2018/) obtenida por Jaime Izquierdo. Se muestran el original (un fichero jpeg) y los resultados.

```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_12.png
---
width: 500px
name: astrometria-12-fig
---
Fotografía origional.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_13.png
---
width: 500px
name: astrometria-13-fig
---
Fotografía procesada. Se muestran los ejes de coordenadas.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_14.png
---
width: 500px
name: astrometria-14-fig
---
Se muestran las estrellas identificadas y las que deberían verse en el campo.
```
```{figure} /_static/lecture_specific/p2_fotometria/p2_11_astrometria_15.png
---
width: 500px
name: astrometria-15-fig
---
Se muestran las estrellas principales anotadas.
```



## Eliminación de rayos cósmicos
Los rayos cósmicos se eliminan mediante combinación de 3 o más imágenes similares (de existir), lo que precisa alineamiento previo. También, en caso necesario, se puede realizar una limpieza individual mediante proceso semi-interactivo con el programa [cleanest](https://cleanest.readthedocs.io/en/latest/).

