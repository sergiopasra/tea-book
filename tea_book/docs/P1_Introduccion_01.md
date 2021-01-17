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

## Introducción básica a LINUX y transferencia de ficheros

[Linux](https://www.linux.org/) es el sistema operativo preferido por los investigadores en el campo de la Astronomía. Para usuarios que vengan del mundo de Windows es fácil aprender lo básico para empezar a trabajar como usuario e ir aprendiendo sobre la marcha.

Linux dispone de un escritorio con iconos que llevan a las carpeta de ficheros o a las aplicaciones. Su uso es intuitivo. Los ficheros se encuentar en una estructura de directorios y subdirectorios. Normalmente se usa la terminal para introducir comandos (cli, command line interface). El intérprete de comandos se encarga de realizar las operaciones solicitadas. Se pueden encontrar manuales para principiantes en muchos sitios. Por ejemplo redhat.com  [Linux 10-commands-terminal](https://www.redhat.com/sysadmin/10-commands-terminal) o de maker.pro [basic-linux-commands-for-beginners](https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners)

### Comandos básicos de Linux 

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
Podemos usar el asterisco  para listar sólo algunos ficheros etc.


###  Manejo de ficheros y carpetas 
Comandos touch, cd, mkdir, cp, mv, more, head, tail, etc

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
#### SSH
SSH (secure shell) es un protocolo encriptado que permite conexiones y transferencias seguras en redes que no lo son. En las conexiones podemos acceder a otro servidor y lanzar comandos o trabajar con ese ordenador remoto como si estuviéramos conectados en una terminal de él. 

Ejemplos de uso de ssh y scp. 

