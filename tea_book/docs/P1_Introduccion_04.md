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


# Python, cuadernos de Jupyter, astropy
Python es un lenguaje de programación abierto que puede se aprende a utilizar rápido y que está siendo cada vez más utilizado en la investigación. También en astronomía ha desplazado a otros lenguajes.
La mayor parte de los astrónomos han usado paquetes como ``IRAF`` para el procesado o reducción de observaciones astronómicas. aunque ``IRAF`` sigue usándose nosotros trabajaremos con Python y las utilidades de [''astropy''](https://www.astropy.org/) para procesar los datos de las observaciones astronómicas. De esta forma es más fácil desarrollar nuestros propios programas y lo aprendido servirá para cualquier tipo de investigación en el futuro aunque no esté relacionada con la astronomía.

## Python
Guías de iniciación de la página oficial de [Python](https://www.python.org/)  
- [Python for programmers ](https://wiki.python.org/moin/BeginnersGuide/Programmers)
- [Python for non programers](https://wiki.python.org/moin/BeginnersGuide/NonProgrammers)
- [Downloading Python](https://wiki.python.org/moin/BeginnersGuide/Download)

## Cuadernos de Jupyter
Un taller de introducción a los cuadernos de Jupyter se puede encontrar en  
[Taller Jupyter](https://github.com/sergiopasra/taller-jupyter) by Sergio Pascual (UCM)

## astropy 
Aunque podríamos hacer toda la reducción de observaciones usando sólo [``python``] es conveniente hacerlo usando los paquetes que pone a nuestra disposición [``astropy``](https://docs.astropy.org/en/stable/index.html) ya que fure desarrollado precisamente para ayudar a las tareas de la comunidad de astrónomos. Además incorpora otros paquetes afiliados desarrollados por investigadores que han resuleto problemas de reducción que no estaban originalmente en el núcleo de ``astropy``.

[Astropy: A community Python package for astronomy](https://www.aanda.org/articles/aa/full_html/2013/10/aa22068-13/aa22068-13.html)

- Instalar ``astropy`` [https://docs.astropy.org/en/stable/install.html](https://docs.astropy.org/en/stable/install.html)

Resumiendo (es mejor consultar la página de instrucciones enlazada), si tienes una instalación de Linux realizada con ``conda``

<pre>
conda install astropy
</pre>
y después para actualizar a la última versión
<pre>
conda update astropy
</pre>

También puedes usar [``pip``](https://pypi.org/) si estás usando este instalador de paquetes. 

<pre>
pip install astropy
</pre>

o si se quiere uno asegurar de que se cargan todas las dependencias
<pre>
pip install astropy[all]
</pre>

Segun avancemos en las clases surgirán paquetes nuevos que se usan. Se enlaza en cada caso las instrucciones de instalación aunque es fácil encontrarlas en las páginas de los paquetes. 

## (Importancia de la utilización de un sistema de control de versiones)
Introducción a [Git](https://git-scm.com/)

No tenemos tiempo en este curso para entrar en detalles pero puede verse una introducción a este método en las charlas de Dr. Ángel de Vicente (Instituto de Astrofísica de Canarias) [basics of Git](http://iactalks.iac.es/talks/view/1426) y [some intermediate concepts](http://iactalks.iac.es/talks/view/1428).


## (Acceso a catálogos on line desde Python)
Realización de queries a [Vizier](https://vizier.u-strasbg.fr/viz-bin/VizieR)
 y [Aladin](https://aladin.u-strasbg.fr/).
Utilización del paquete [PyVO](https://pypi.org/project/pyvo/) para acceder a datos astronómicos en archivos que siguen los estándares definidos por el IVOA (International Virtual Observatory Alliance).

