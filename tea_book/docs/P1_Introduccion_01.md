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

#  Introducción

## Recomendaciones previas

### Nombres de los ficheros
Aunque parezca de menor importancia se debe procurar que el nombre de los ficheros informe de su contenido no sólo al autor. Si enviamos un fichero a un colaborador o a un profesor para su evaluación, el destinatario tendrá la información básica si se la proporcionamos. Por ejemplo 

<pre>
Malos ejemplos a evitar:  
 - práctica 2.pdf     	(acentos, espacios, informa poco)
 - memoria_final.pdf 	(no informa nada)  
Mejor:  
 - TEA_G2_practica_3_v2.pdf
 - Grupo3_practica2_v1.pdf
</pre>

### Control de versiones y cabecera

La cabecera de las memorias  deben informar de sus autores, grupo, asignatura y fecha. La fecha puede servir de control de la versión. Más completo es añadir la versión y la fecha:

<pre>
TÉCNICAS EXPERIMENTALES EN ASTROFÍSICA 
Práctica 2      Fotometría CCD 
GRUPO 6: Carmelo de Castro, Felipe Paredes y Daniel Revilla
Versión 2. 12 abril 2020
</pre>

Cuando se comparte trabajo con colaboradores lo ideal es usar un control de versiones. Este libre se está realizando con ese método y los autores colaboran creando contenido localmente (en sus ordenadores) y subiendo su trabajo a un repositorio donde se unen las contribuciones. No tenemos tiempo en este curso para entrar en detalles pero puede verse una introducción a este método en las charlas de Dr. Ángel de Vicente (Instituto de Astrofísica de Canarias) [basics of Git](http://iactalks.iac.es/talks/view/1426) y [some intermediate concepts](http://iactalks.iac.es/talks/view/1428).



## Introducción básica a LINUX y transferencia de ficheros

[Linux](https://www.linux.org/) es el sistema operativo preferido por los investigadores en el campo de la Astronomía. Para usuarios que vengan del mundo de Windows es fácil aprender lo básico para empezar a trabajar como usuario e ir aprendiendo sobre la marcha.

Linux dispone de un escritorio con iconos que llevan a las carpeta de ficheros o a las aplicaciones. Su uso es intuitivo. Los ficheros se encuentar en una estructura de directorios y subdirectorios. Normalmente se usa la terminal para introducir comandos (cli, command line interface). El intérprete de comandos se encarga de realizar las operaciones solicitadas. Se pueden encontrar manuales para principiantes en muchos sitios. Por ejemplo redhat.com  [Linux 10-commands-terminal](https://www.redhat.com/sysadmin/10-commands-terminal) o de maker.pro [basic-linux-commands-for-beginners](https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners)

### Comandos básicos de Linux 
Haremos demostraciones en directo de estos comandos en clase.  
Mostramos aquí sólo lo más básico. 

- pwd (print working directory) muestra el directorio donde nos encontramos
<pre>
sidrax:Jupyter jzamorano@sidrax$ pwd  
/home/jzamorano/0_TEA/Jupyter
</pre>

Lo que se encuentra delante del símbolo $ es lo que se conoce como el 'prompt'. 
Contiene información del nombre del ordenador y del directorio donde nos encontramos. 
Si escribimos el comando pwd la respuesta sale en la siguiente línea que en este caso informa de que estamos en el subdirectorio Jupyter que cuelga de 0_TEA en el 'home' (directorio raíz) del usuario jzamorano. 

- ls (list) es el comando para lista el contenido del directorio donde nos encontramos
<pre>
sidrax:Jupyter jzamorano$ ls  
</pre>
La ayuda de los parámetros que podemos agregar a los comandos se obtiene  con 'man' de manual. Por ejemplo,

<pre>
sidrax:Jupyter jzamorano@sidrax$ man ls
</pre>

Podemos usar el asterisco  para listar sólo algunos ficheros etc.

<pre>
sidrax:Jupyter jzamorano$ ls *fits          # Para listar los ficheros con extensión fits de este directorio
sidrax:Jupyter jzamorano$ ls *2015*         # Para listar los ficheros cuyo nombre contenga 2015
</pre>

<pre>
sidrax:Jupyter jzamorano$ ls -la            # más información de los ficheros contenidos en el directorio 
</pre>

<pre>
sidrax:Jupyter jzamorano$ ls -larth         # con tamaño del fichero y listado en orden cronolócico inverso 
</pre>

- cd (current directory) sirve para cambiar de directorio

<pre>
sidrax:Jupyter jzamorano$ cd         # nos lleva al directorio /home/
sidrax:Jupyter jzamorano$ cd -       # al directorio anterior antes de movernos al actual
sidrax:Jupyter jzamorano$ cd ../     # al directorio por encima del actual 
sidrax:Jupyter jzamorano$ cd  pepe   # al subdirectorio pepe/ que cuelga del actual
</pre>


###  Manejo de ficheros y carpetas 
- mkdir (make directory)   crea un subdirectorio 
<pre>
sidrax:Jupyter jzamorano$ mkdir fits_files  # crea el subdirectorio fits_files colgando del actual
sidrax:Jupyter jzamorano$ cd fits_files     # nos movería a este nuevo directorio
</pre>

- cp (copy)  copia ficheros  
<pre>
sidrax:Jupyter jzamorano$ cp listado.txt mi_lista.txt  # el nuevo fichero mi_lista.txt es una copia de listado.txt
</pre>

- mv (move)  cambia el nombre y/o localización del fichero
<pre>
sidrax:Jupyter jzamorano$ mv listado.txt mi_lista.txt  # el nuevo fichero mi_lista.txt sustituye a listado.txt que ya no existe
sidrax:Jupyter jzamorano$ mv file_01.csv pepe/.  # mueve el fichero file_01.csv al subdirectorio pepe y ya no está en el directorio actual.
sidrax:Jupyter jzamorano$ mv file_01.csv pepe/fichero_1.csv  # mueve el fichero file_01.csv al subdirectorio pepe y le cambia el nombre a fichero_1.csv
</pre>

- more (more) muestra el contenido de los ficheros ascii
<pre>
sidrax:Jupyter jzamorano$ more file_005.txt  # muestra las líneas en la terminal hasta llenar el espacio disponible
</pre>

- head (head) muestra sólo las primeras líneas
<pre>
sidrax:Jupyter jzamorano$ head file_005        # Muestra las primeras líneas
sidrax:Jupyter jzamorano$ head file_005 -n 30  # Muestra las primeras 30 líneas
</pre>

- tail (tail) muestra sólo las últimas líneas
<pre>
sidrax:Jupyter jzamorano$ tail file_005        # Muestra las últimas líneas
sidrax:Jupyter jzamorano$ tail file_005 -n 30  # Muestra las últimas 30 líneas
</pre>

- touch(touch)  crea un fichero vacío 
<pre>
sidrax:Jupyter jzamorano$ touch test_file.txt  # el nuevo fichero test_file.txt está vacío
</pre>

###  Edición de ficheros ascii
Los ficheros de texto son legibles ya que están formados por caracteres ascii. Pueden tener extensión '.txt' para indicar su condición. El contenido de estos ficheros se puede mostrar con los comandos aprendidos (more, head, tail). Estos ficheros se pueden editar usando ele ditor de nuestra elección. Los editores más usados en Linux son

- vi o vim (vi improved) [vim en la UCM](https://www.ucm.es/pimcd2014-free-software/vim)
Este último está pensado para desarrollar programas.

- emacs [gnu emacs](https://www.gnu.org/software/emacs/)

- gedit [gnome gedit](https://help.gnome.org/users/gedit/stable/)

Cualquier editor que venga con la instalación de Linux nos vale. Lo importante es manejarlo con soltura y eso se aprende con el tiempo.

Hay un tipo de ficheros de texto que se usa para almacenar datos que tienen extensión '.csv' (comma separated values) y en su interior los datos se encuentran tabulados en columnas separadas por ',' o ';' o '\tab' tabuladores. 


###  Transferencia de ficheros entre ordenadores 
#### FTP
FTP es un protocolo estándar para transferencia de ficheros. Con esta utilidad podemos mover ficheros entre diferentes ordenadores (cliente y servidor) mediante comandos. Para que un servidor permita descargar ficheros es necesario autenticarse (username & password) salvo en el caso de servidores públicos donde se puede hacer una conexión anónima.

```{figure} /_static/lecture_specific/p1_intro/intro_01_ftp_1.png
---
height: 500px
name: ftp_1-fig
---
Comandos básicos de ftp.
```

```{figure} /_static/lecture_specific/p1_intro/intro_01_ftp_2.png
---
height: 800px
name: ftp_2-fig
---
```

```{figure} /_static/lecture_specific/p1_intro/intro_01_ftp_3.png
---
height: 800px
name: ftp_3-fig
---
```

```{admonition} ftp Ejercicio 1
Descargar la Tabla 1 del artículo Pérez-González et al. "Optical photometry of the UCM Lists I and II
I. The data" [Astron. Astrophys. Suppl. Ser. 141, 409-421 (2000)](https://aas.aanda.org/articles/aas/abs/2000/03/ds1775/ds1775.html) del repositorio ftp de A&A ftp://cdsarc.u-strasbg.fr/pub/ftp/aas/ 
```
```{figure} /_static/lecture_specific/p1_intro/intro_01_ftp_5.png
---
width: 400px
name: ftp_5-fig
---
```
```{figure} /_static/lecture_specific/p1_intro/intro_01_ftp_4.png
---
width: 400px
name: ftp_4-fig
---
Cabecera del artículo.
```

```{figure} /_static/lecture_specific/p1_intro/intro_01_ftp_6.png
---
width: 600px
name: ftp_6-fig
---
El principio de la tabla 1 tal como aparece en el artículo.
```
Y en formato digital tras descargarlo del ftp
<pre>
0000+2140  0.0238       HIIH        1.204   
0003+2200  0.0224 Sc+   DANS  16.16 0.867   
0003+2215  0.0223       SBN         1.008   
0003+1955  0.0278       Sy1                 
0005+1802  0.0187       SBN         1.244   
0006+2332  0.0159       HIIH        0.644   
0013+1942  0.0272 Sc+   HIIH  16.39 0.276   
0022+2049  0.0185 Sb    HIIH  14.45 0.901 
</pre>

```{tip}
Tambien se puede acceder al ftp del Centre de Données astronomiques de Strasbourg [CDS](http://cdsweb.u-strasbg.fr/) via navegador     
[FTP repository for Astronomical Catalogues & Tables](http://cdsarc.u-strasbg.fr/ftp/).
```
```{figure} /_static/lecture_specific/p1_intro/intro_01_ftp_7.png
---
width: 600px
name: ftp_7-fig
---
Acceso al ftp de A&A via navegador web
```

#### SSH
SSH (secure shell) es un protocolo encriptado que permite conexiones y transferencias seguras en redes que no lo son. En las conexiones podemos acceder a otro servidor y lanzar comandos o trabajar con ese ordenador remoto como si estuviéramos conectados en una terminal de él. 

[Ejemplos de uso de ssh y scp](http://nartex.hst.ucm.es/~ncl/AE2019/instrucciones_practica1a.html)

