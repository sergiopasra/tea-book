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


# Pasos finales  



## Calibración fotométrica
Determinación de las constantes instrumentales y coeficientes de extinción para cada noche.


## Calibración astrométrica
Para ello se utilizará [Astrometry.net](http://astrometry.net/) y las herramientas disponibles en [AstrOmatic.net](http://www.astromatic.net/).

## Eliminación de rayos cósmicos
Los rayos cósmicos se eliminan mediante combinación de 3 o más imágenes similares (de existir), lo que precisa alineamiento previo. También, en caso necesario, se puede realizar una limpieza individual mediante proceso semi-interactivo con el programa [cleanest](https://cleanest.readthedocs.io/en/latest/).

