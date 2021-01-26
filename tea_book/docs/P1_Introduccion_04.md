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
Ventajas e inconvenientes frente a los paquetes tradicionales.


## Python
## Cuadernos de Jupyter
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

## (Acceso a catálogos on line desde Python)
Realización de queries a [Vizier](https://vizier.u-strasbg.fr/viz-bin/VizieR)
 y [Aladin](https://aladin.u-strasbg.fr/).
Utilización del paquete [PyVO](https://pypi.org/project/pyvo/) para acceder a datos astronómicos en archivos que siguen los estándares definidos por el IVOA (International Virtual Observatory Alliance).

