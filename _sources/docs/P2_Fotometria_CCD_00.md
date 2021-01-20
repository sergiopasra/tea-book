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
# Práctica 2     Fotometría CCD

Reduciremos a continuación la primera noche de observación. Los pasos seguidos son idénticos para la segunda noche pero se prefiere construir los master BIAS y master FLATs para cada noche y usarlos para las observaciones correspondientes.

Estamos siguiendo en gran parte los pasos descritos en CCD Data Reduction Guide una guía muy completa escrita por Matt Craig and Lauren Chambers y editada por Lauren Glattly. En esa guía se dan detalles muy interesantes sobre cómo es una imagen CCD fabricando imágenes artificiales y procesándolas de diferentes maneras.

Se han escrito cuadernos de Jupyter para cada paso y se muestran sólo partes de los mismos en este documento. Se usa en preferencia ccdproc. “Ccdproc is is an Astropy affiliated package for basic data reductions of CCD images. It provides the essential tools for processing of CCD images in a framework that provides error propagation and bad pixel tracking throughout the reduction process.” (© Copyright 2020, Steve Crawford, Matt Craig, and Michael Seifert.)

