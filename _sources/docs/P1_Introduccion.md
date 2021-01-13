# P1_Introducción 

## Introducción al software de procesado de observaciones astronómicas
Para paliar el problema de la heterogénea formación inicial con la que ingresan los estudiantes del Máster en el ámbito de la utilización de un sistema operativo en Linux (o similar), así como en el manejo de lenguajes de programación, se comienzan las clases prácticas con un repaso sobre el uso de terminales y comandos básicos de Linux. Esto permite al estudiante organizar y manejar un gran volumen de ficheros, algo esencial para esta asignatura. 

Por otro lado, como las prácticas propuestas durante el resto del curso están pensadas para poder ser llevadas a cabo utilizando el lenguaje de programación [Python](https://www.python.org/) a través de cuadernos de [Jupyter](https://jupyter.org/) (conocidos como Jupyter notebooks), se utiliza este sistema desde el primer instante de ejecución de esta práctica de demostración inicial. Se explican los pasos a seguir para obtener imágenes y espectros de objetos astronómicos reducidos, destacando la importancia de adquirir el número suficiente de imágenes de calibración de diferentes tipos (dependiendo del tipo de observación). Finalmente se discuten distintas alternativas para la estimación de incertidumbres en las medidas finales realizadas sobre las imágenes reducidas. 

Los alumnos podrán entregar los Jupyter notebooks generados por ellos mismos como material evaluable de las Prácticas 2, 3 y 4, lo que evita la necesidad de generar informes independientes.

### Recomendaciones previas

#### Nombres de los ficheros
Aunque parezca de menor importancia se debe procurar que el nombre de los ficheros informe de su contenido no sólo al autor. Si enviamos un fichero a un colaborador o a un profesor para su evaluación, el destinatario tendrá la información básica si se la proporcionamos. Por ejemplo 

<pre>
Malos ejemplos a evitar:  
 - práctica 2.pdf     	(acentos, espacios, informa poco)
 - memoria_final.pdf 	(no informa nada)  
Mejor:  
 - TEA_G2_practica_3_v2.pdf
 - Grupo3_practica2_v1.pdf
</pre>

#### Control de versiones y cabecera

La cabecera de las memorias  deben informar de sus autores, grupo, asignatura y fecha. La fecha puede servir de control de la versión. Más completo es añadir la versión y la fecha:

<pre>
TÉCNICAS EXPERIMENTALES EN ASTROFÍSICA 
Práctica 2      Fotometría CCD 
GRUPO 6: Carmelo de Castro, Felipe Paredes y Daniel Revilla
Versión 2. 12 abril 2020
</pre>

### Introducción básica a LINUX y transferencia de ficheros: 

[Linux](https://www.linux.org/) es el sistema operativo preferido por los investigadores en el campo de la Astronomía. Para usuarios que vengan del mundo de Windows es fácil aprender lo básico para empezar a trabajar como usuario e ir aprendiendo sobre la marcha.

Linux dispone de un escritorio con iconos que llevan a las carpeta de ficheros o a las aplicaciones. Su uso es intuitivo. Los ficheros se encuentar en una estructura de directorios y subdirectorios. Normalmente se usa la terminal para introducir comandos (cli, command line interface). El intérprete de comandos se encarga de realizar las operaciones solicitadas. Se pueden encontrar manuales para principiantes en muchos sitios. Por ejemplo redhat.com  [Linux 10-commands-terminal](https://www.redhat.com/sysadmin/10-commands-terminal) o de maker.pro [basic-linux-commands-for-beginners](https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners)

#### Comandos básicos de Linux 

- pwd (print working directory) muestra el directorio donde nos encontramos
sidrax:Jupyter jzamorano@sidrax$ pwd  
/home/jzamorano/0_TEA/Jupyter

Lo que se encuentra delante del símbolo $ es lo que se conoce como el 'prompt'. 
Contiene información del nombre del ordenador y del directorio donde nos encontramos. 
Si escribimos el comando pwd la respuesta sale en la siguiente línea que en este caso informa de que estamos en el subdirectorio Jupyter que cuelga de 0_TEA en el 'home' (directorio raíz) del usuario jzamorano. 


- ls (list) es el comando para lista el contenido del directorio donde nos encontramos
sidrax:Jupyter jzamorano$ ls  

Podemos usar el asterisco  para listar sólo algunos ficheros etc.


####  Manejo de ficheros y carpetas 
Comandos touch, cd, mkdir, cp, mv, more, head, tail, etc

####  Transferencia de ficheros entre ordenadores 
##### FTP
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
##### SSH
SSH (secure shell) es un protocolo encriptado que permite conexiones y transferencias seguras en redes que no lo son. En las conexiones podemos acceder a otro servidor y lanzar comandos o trabajar con ese ordenador remoto como si estuviéramos conectados en una terminal de él. 

Ejemplos de uso de ssh y scp. 


### Redución de observaciones astronómicas
Las observaciones astronómicas que emplean detectores de imagen tipo CCD deben procesarse o reducirse para proporcionar imágenes o espectros calibrados. Sólo tras la reducción de las observaciones podemos medir en ellas para obtener la información que nuestro proyecto científico requiera. Este procesado debe ser cuidadoso porque de él depende la calidad final de nuestras medidas.

#### Formato FITS de las imágenes astronómicas 
Los primeros instrumentos que usaron CCDs grababan sus imágenes en cintas magnéticas en ficheros con formatos particulares (proprietary format), es decir que cada observatorio proporcionaba al final de las observaciones los ficheros y las instrucciones de cómo estaba almacenada y codificada la información. El investigador debía usar los programas de procesado en el propio observatorio (si disponían de ellos) o preparar los suyos propios en su lugar de trabajo. El primer paso consistía en lograr traspasar la información de la cinta magnética a un fichero en tu propio ordenador y crear una matriz de datos organizada en píxeles X,Y con la intensidad de cada pixel.

Para paliar esta pérdida de tiempo se diseñó el formato digital estándar abierto FITS [Flexible Image Transport System](https://fits.gsfc.nasa.gov/fits_primer.html) que es de uso común en la comunidad astronómica. Tanto la NASA como la IAU lo avalan y promueven. 

El formato FITS se usa tanto para imágenes como para tablas. La cabecera de una imagen FITS está escrita en ASCII y es por ello fácilmente legible. Contiene los metadatos, es decir, la información descriptiva que debe acompañar a los datos de la imagen. Por ejemplo el tamaño del fichero, su origen , la fecha de creación, el observador, el filtro utilizado etc. Estos parámetros son conocidos como los 'keywords' (descriptor).

Se han desarrollado paquetes de software para visualizar ficheros FITS como  Image Software [SAOImage DS9](http://ds9.si.edu/site/Home.html) y [ALADIN](http://aladin.u-strasbg.fr/) y para transformar entre FITS y otros formatos de imagen como, GIMP o ImageMagick.

La cabecera ('heeader') está escrita en líneas de 80 caracteres en ASCII sencillo y cada línea contiene el Nombre del descriptor + Valor + Comentario. 

KEYNAME = value / comment string
<pre>
SIMPLE = T        / file conforms to FITS standard 
BITPIX = 16       / number of bits per data pixel 
NAXIS  = 2        / number of data axes 
NAXIS1 = 440      / length of data axis 1 
NAXIS2 = 300      / length of data axis 2
</pre>
Algunos descriptores básicos son obligatorios. Otros descriptores pueden verse en el ejemplo siguiente de una observación de un arco de calibración con el IDS en el INT.

<pre>
SIMPLE  =                    T /                                                
BITPIX  =                   16 /                                                
NAXIS   =                    2 /                                                
NAXIS1  =                 1124 /                                                
NAXIS2  =                  400 /                                                
BSCALE  =             1.000000 /                                                
BZERO   =         32768.000000 /                                                
RUN     =               115135 / Run number                                     
IRAFNAME= 'r115135           ' / rfits should use this name                     
SYSVER  = 's6-1              ' / Version of observing system                    
ORIGIN  = 'ING La Palma      ' / Name of observatory                            
OBSERVAT= 'LAPALMA           ' / Name of observatory (IRAF style)               
OBJECT  = 'cune ucm1443+2844 ' / Title of observation                           
OBSTYPE = 'ARC               ' / Type of observation, eg. ARC                   
IMAGETYP= 'ARC               ' / Type of observation, eg. ARC                   
LATITUDE=            28.762000 / Telescope latitude  (degrees), +28:45:43.2     
LONGITUD=            17.877639 / Telescope longitude (degrees), +17:52:39.5     
HEIGHT  =                 2348 / [m] Height above sea level.                    
SLATEL  = 'LPO2.5  '           / Telescope name known to SLALIB                 
TELESCOP= 'INT     '           / 2.5m Isaac Newton Telescope                    
TELSTAT = 'TRACKING'           / Telescope status: TRACKING or GUIDING normally.
RA      = ' 14:43:46.201'      / RA  (220.9425040722087500 degrees)             
DEC     = '+28:44:07.02'       / DEC ( 28.7352839821988330 degrees)             
EQUINOX = 'B1950.00'           / Equinox of coordinates                         
RADECSYS= 'FK4     '           / mean place old (before the 1976 IAU) system    
XAPNOM  =         0.0000000000 / nominal aperture in x (0.00 arcsec)            
YAPNOM  =         0.0000000000 / nominal aperture in y (0.00 arcsec)            
XAPOFF  =         0.0000000000 / total aperture offset in x (0.00 arcsec)       
YAPOFF  =         0.0000000000 / total aperture offset in y (0.00 arcsec)       
MJD-OBS =        51039.8602077 / Modified Julian Date of midtime of observation 
JD      =      2451040.3602077 / Julian Date of midtime of observation          
STSTART = ' 16:59:24.0'        / Local sidereal time at start of observation    
ST      = ' 16:59:24.0'        / Local sidereal time at start of observation    
AZIMUTH =           277.778480 / Mean azimuth of observation (degrees)          
ZD      =            29.200487 / Mean zenith-distance of observation (degrees)  
FSTATION= 'CASSEGRAIN'         / Focal station of observation                   
PLATESCA=             1.502645 / [d/m] Platescale (  5.41arcsec/mm)             
TELFOCUS=             0.014303 / Telescope focus (metres)                       
ROTTRACK=                    T / Rotator always tracks sky on equatorial mount  
ROTSKYPA=           129.998198 / Turntable position angle (degrees)             
PARANGLE=            81.606581 / Parallactic angle at observation midpoint      
VIGNETTE=                    F / Can we see out?                                
DOMEAZ  =           282.618912 / Mean dome azimuth during observation           
AIRMASS =             1.145286 / Effective mean airmass                         
TEMPTUBE=            17.440534 / Truss Temperature (degrees Celsius)            
CAT-NAME= 'UCM1443+2844'       / Target input-catalogue name                    
CAT-RA  = ' 14:43:46.200'      / Target Right Ascension                         
CAT-DEC = '+28:44:07.00'       / Target Declination                             
CAT-EQUI= 'B1950.00'           / Equinox of target coordinates                  
CAT-EPOC=              1950.00 / Target epoch of proper motions                 
PM-RA   =             0.000000 / Target proper-motion RA (sec time/year)        
PM-DEC  =             0.000000 / Target proper-motion (sec arc/year)            
PARALLAX=             0.000000 / Target Parallax (arcsec)                       
RADVEL  =             0.000000 / Target radial velocity (km/s)                  
RATRACK =             0.000000 / Differential-tracking rate RA (arcsec/sec)     
DECTRACK=             0.000000 / Differential-tracking rate Dec (arcsec/sec)    
AGTVPOSX= 0.499996             / TV X position in meters                        
AGTVPOSY= 0.500027             / TV Y position in meters                        
AGTVFILT= 'F0 Clear          ' / TV filter name                                 
AGTVSHUT= 'SHUT              ' / State of TV shutter                            
AGPOSX  = 0.521599             / Autoguider X position in meters                
AGPOSY  = 0.408291             / Autoguider Y position in meters                
ASNDFILT= 'F0 Clear          ' / ND filter name in beam above the slit          
ASCFILT = 'F2 GG495          ' / Colour filter name in beam above the slit      
AGARCLMP= ' CuNe             ' / Arc lamps in use                               
COMPMPOS= 'IN                ' / Comparison mirror position                     
AUTOFILT= 'F3 RED            ' / Autoguider filter name                         
AGCFILNA= 'F0 Clear          ' / Comparison ND filter A name                    
AGCFILNB= 'F0 Clear          ' / Comparison ND filter B name                    
INSTRUME= 'IDS              '  / Name of the instrument                         
CAMERA  = '500               ' / Focal length of camera in use                  
SLITWID =         1.450000E-04 / Slit width in meters                           
PSLITWID=                0.046 / Slit width projected onto detector in mm       
SLTWDSKY=                0.784 / Slit width projected onto sky in arcseconds    
DEKKERID= 'D-IPCS            ' / Dekker slide name                              
DEKPOS  = 'P0 Clear          ' / Name of Dekker position in the beam            
BSCFILT = 'F0 Clear          ' / Name of colour filter in beam below the slit   
BSNDFILT= 'F0 Own            ' / Name of ND filter in beam below the slit 
COLLNAME= 'Ag-red            ' / Collimator name                                
COLLFOC =                  206 / Collimator focus in encoder units              
HARTMANR= 'OPEN              ' / State of right Hartmann shutter                
HARTMANL= 'OPEN              ' / State of left  Hartmann shutter                
GRATNAME= 'R1200Y            ' / Grating name                                   
GLINESMM=                 1200 / Grating rulings in lines/mm                    
GRATBLAZ=             6000.000 / Grating blaze in Angstroms                     
GRATANGL=              127.000 / Grating angle in degrees                       
GRATSHUT= 'OPEN              ' / State of grating shutter                       
CENWAVE =             6761.062 / Central wavelength in Angstroms                
DATE-OBS= '1998-08-14        '          / Date of start of observation          
UTSTART = '20:38:43.0        '          / UTC of start of observation hh:mm:ss  
ELAPSED =                2.000          / Time from end of CLR to shutter close 
DARKTIME=                1.000          / Time from end of CLR to start of r/o  
EXPOSED =                1.000          / Exposure time excluding pauses,in secs
EXPTIME =                1.000          / Exposure time excluding pauses,in secs
DETECTOR= 'TEK5              '          / Name of the detector                  
PREFLASH=                0.000          / Length of Preflash in seconds         
BUNIT   = 'ADU               '          / Unit of the array of image data       
GAIN    =                1.530          / Electrons per ADU                     
READNOIS=                4.820          / Readout noise in electrons per pix    
CCDSPEED= 'QUICK             '          / Readout speed of the CCD              
CCDNCHIP=                    1          / Number of CCDs in this head           
CCDCHIP =                    1          / Head number of this CCD               
CCDTYPE = 'TEK1024AR         '          / Type of CCD used in this detector     
CCDXSIZE=                 1124          / X Size in pixels of digitised frame   
CCDYSIZE=                 1124          / Y Size in pixels of digitised frame   
CCDXIMSI=                 1024          / X Size of useful imaging area         
CCDYIMSI=                 1024          / Y Size of useful imaging area         
CCDXIMST=                   50          / X Start pixel of useful imaging area  
CCDYIMST=                    0          / Y Start pixel of useful imaging area  
CCDWMODE=                    T          / True is windows are enabled           
CCDWXO1 =                    0          / Offset of window 1 in X               
CCDWYO1 =                  405          / Offset of window 1 in Y               
CCDWXS1 =                 1124          / Size of window 1 in X                 
CCDWYS1 =                  400          / Size of window 1 in Y                 
CCDWXO2 =                    0          / Offset of window 2 in X               
CCDWYO2 =                    0          / Offset of window 2 in Y               
CCDWXS2 =                    0          / Size of window 2 in X          
CCDWYS2 =                    0          / Size of window 2 in Y                 
CCDWXO3 =                    0          / Offset of window 3 in X               
CCDWYO3 =                    0          / Offset of window 3 in Y               
CCDWXS3 =                    0          / Size of window 3 in X                 
CCDWYS3 =                    0          / Size of window 3 in Y                 
CCDWXO4 =                    0          / Offset of window 4 in X               
CCDWYO4 =                    0          / Offset of window 4 in Y               
CCDWXS4 =                    0          / Size of window 4 in X                 
CCDWYS4 =                    0          / Size of window 4 in Y                 
CCDXPIXE=         2.400000e-05          / Size in meters of the pixels, in X    
CCDYPIXE=         2.400000e-05          / Size in meters of the pixels, in Y    
CCDXBIN =                    1          / Binning factor, in X                  
CCDYBIN =                    1          / Binning factor, in Y                  
CCDSTEMP=                  173          / Required temperature of CCD, in Kevlin
CCDATEMP=                  173          / Actual temperature of CCD, in Kevlin  
CHIPNAME= 'A5506-4           ' / Name of CCD chip                               
DASCHAN =                    1 / DAS channel                                    
TRIMSEC = '[51:1074,1:400]   ' / Illuminated region of image                    
BIASSEC = '[1:50,1:400]      ' / Bias region of image                           
WINSEC1 = '[1:1124,1:400]    ' / Readout window 1                               
WINSEC2 = '[0:0,0:0]         ' / Readout window 2                               
WINSEC3 = '[0:0,0:0]         ' / Readout window 3                               
WINSEC4 = '[0:0,0:0]         ' / Readout window 4                               
COMMENT This is padding to correct for missing descriptors earlier in the header
COMMENT This is padding to correct for missing descriptors earlier in the header
COMMENT This is padding to correct for missing descriptors earlier in the header
COMMENT This is padding to correct for missing descriptors earlier in the header
HISTORY This is the end of the header written by the ING observing-system.      
END                                                                                            </pre>


En los ejemplos de las prácticas veremos que estas cabeceras pueden contener información con la historia de su procesado previo.


#### Paquetes de reducción de datos
La reducción de las observaciones astronómicas con imágenes digitales al principio de estar disponibles era una tarea a la que los astrónomos se enfrentaban con sus propios medios. No sólo para leer los ficheros sino para calibrar y extraer la información de los mismos. De aquellos tiempos quedan astrónomos que prefieren desarrollar sus propios programas.  
Sin embargo aparecieron enseguida paquetes de reducción desarrollados por observatorios o centros de investigación que fueron de gran ayuda sobre todo para los astrónomos con menos conocimientos de programación. En cualquier caso supuso un avance ya que permitieron a los investigadores dedicar el tiempo a la reducción de los datos y no al desarrollo de software. Estas herramientas fundamentales se mantenían con ayuda de expertos cuyo cometido era fundamentalmente éste y también con la aportación de astrónomos.

##### STARLINK 
Otro problema adicional era el acceso a ordenadores capaces de realizar este trabajo. Por ejemplo en el año 1978 se decidió en el Reino Unido establecer [STARLINK](http://starlink.eao.hawaii.edu/starlink) con una red de 6 ordenadores (superminicomputers DEC VAX 11/780) conectados entre sí. Resulta instructivo comprobar lo que se ha avanzado desde entonces (5000 Mbytes of disc space and 12 Mbytes of memory).

```{figure} /_static/lecture_specific/p1_intro/intro_02_starlink.png
---
height: 200px
name: starlink-fig
---
Source: [http://www.chilton-computing.org.uk/acd/starlink/p002.htm](http://www.chilton-computing.org.uk/acd/starlink/p002.htm)
```

Los primeros ordenadores VAX (sistema operativo VMS) dieron paso a los miniVAX y luego al sistema operativo Unix en estos ordenadores y otros de SUN y finalmente pudieron usar PCs con Linux.  El proyecto dejó de mantenerse en 2005 después de 25 años de funcionamiento. Por suerte para los nostálgicos el Joint Astronomy Centre siguió desarrollando software hasta 2015 y actualmente está mantenido por East Asian Observatory. El código es abierto ('open software').

##### FIGARO
El paquete de software [FIGARO](http://star-www.rl.ac.uk/docs/sun86.htx/sun86.html) fue inicialmente desarrollado por Keith Shortridge  en los primeros 1980s para analizar los datos del observatorio de Monte Palomar. Escrito fundamentalmente en Fortran estaba compuesto de múltiples subrutinas para tareas de todo tipo en la reducción de observaciones astronómicas. Su uso se extendió rápidamente por los centros de investigación de todo el mundo. Era relativamente sencillo desarrolar rutinas propias para tareas diferentes e incorporarlas en el paquete.

##### MIDAS
[ESO-MIDAS](https://www.eso.org/sci/software/esomidas/) fue desarrollado por el European Southern Observatory siguiendo los pasos de STARLINK en 1980 y usaba ordenadores VAX con sistema operativo VMS que posteriormente migró a UNIX. Su estructura es modular con rutinas accesibles por comandos que admiten parámetros siguiendo la filosofía del sistema de procesado de imagen 'Image handling and Processing system' [IHAP](https://link.springer.com/chapter/10.1007%2F0-306-48080-8_4) que estaba basado en ordenadores Hewlett-Packard. Se pueden desarrollar procedimientos que combinan varios comandos sucesivos para crear cadenas de procesado ('pipelines') con su sistema MCL ('MIDAS control language'). Su uso fue muy popular y aun hoy continua empleándose.  
En sus orígenes se necesitaba también un ordenador grande y una serie de periféricos para interaccionar con el sistema escribir los comandos y lanzar las aplicaciones (terminal o monitor) y otras terminales gráficas para mostrar imágenes o espectros, por ejemplo. Las rutinas de graficado de MIDAS se escribieron con el estándard de AGL (ASTRONET Graphic Library) desarrrolado por ASTRONET. Más tarde se las rutinas de Image Display Interface desarrolladas en colaboración con ST ScI, UK STARLINK, KPNO y Trieste Observatory.  Actualmente todo es más acesible ya que puede instalarse en ordenadores personales con sistemas operativos Linux y también sistemas Mac OSX. Las diferentes terminales gráficas aparecen como ventanas en el escritorio.

##### IDL
[IDL](https://www.l3harrisgeospatial.com/Software-Technology/IDL) ('Interactive Data Language') es un lenguage de programación para análisis de datos que se usa entre otros campos en astronomía, ciencias de la atmósfera o análisis de imágenes en medicina.

##### IRAF
[IRAF](http://ast.noao.edu/data/software) 'Image Reduction and Analysis Facility' es un software desarrollado en NOAO con el fin de procesar observaciones astronómicas. Escrito para sistema operativo Unix originalmente se usa en la actualidad en plataformas Linux o mac OS. IRAF está estructurado en tareas ('tasks') que están incluidas en paquetes. Dentro del proyecto IRAF existen desarrollos especiales como STSDAS ('Space Telescope Science Data Analysis System') para procesar datos de los instrumentos de HST (Hubble Space Telescope). IRAF ha sido tal vez el software más popular ya que algunos desarrolladores de instrumentación astronómica para grandes telescopios han escrito paquetes de procesado y tareas especiales para la reducción de las observaciones como nuevos paquetes.

##### Astropy
- [Astropy](https://www.astropy.org/)   
Las observaciones realizadas con modernos intrumentos astronómicos pueden ser reducidas por cadenas de procesado ('pipelines') sobre la marcha. De esta forma el investigador dispone de los datos reducidos inmediatamente. La exigencia de proporcionar esta utilidad es habitual en el desarrollo de instrumentación de primer nivel para asegurar el rendimiento científico de la inversión realizada. Para procesados más delicados o con mayor detalle en algún aspecto es normal que el investigador desee hacer una reducción más manual usando sus propios métodos y usando, generalmente, las herramientas disponibles. El proyecto Astropy es un esfuerzo conjunto (comunitario) de desarrollo de software para astronomía en Python [Astropy: A community Python package for astronomy](https://www.aanda.org/articles/aa/full_html/2013/10/aa22068-13/aa22068-13.html)


### Visualización e inspección de imágenes 
Existen visualizadores de las imágenes procedentes de observaciones astronómicas en formato FITS. Incluso pueden estar incluidos en programas de manejo de imágenes de uso general. Por supuesto los paquetes de reducción mencionados anteriormente disponen de sus comandos para visualización. 

#### SAOimageDS9
[SAOimageDS9](https://sites.google.com/cfa.harvard.edu/saoimageds9)
es uno de los programas favoritos que, por ejemplo, funciona dentro de IRAF como como su sistema de visualización. Pero una de las características más importantes de este software que permite cargar y ver varias imágenes FITS (y tablas binarias) a la vez es que funciona independientemente (stand-alone application) de otros paquetes de software y no necesita instalación o ficheros adicionales. Funciona con menús desde su GUI (graphical user interface) o por medio de comandos. SAOimageDS9 tiene su origen en SAOimage desarrollado por Mike Van Hilst en el Smithsonian Astrophysical Observatory, Center for Astrophysics, Harvard University en 1990. Unos años después Eric Mandel desarrolla SAOtng (SAOImage, The Next Generation) y a finales de los 1990s William Joye empezó a reescribir el software que se llama desde entonces SAOimageDS9 (Deep Space 9). 

El programa se descarga desde [http://ds9.si.edu](http://ds9.si.edu) y existen versiones para Windows, Mac y Linux. Los manuales, guía y tutoriales se encuentran en la página de [documentación SAOimageDS9](https://sites.google.com/cfa.harvard.edu/saoimageds9/documentation). 

- [SAOImageDS9 Reference Manual](http://ds9.si.edu/doc/ref/index.html)
- [SAOImageDS9 Users Manual](http://ds9.si.edu/doc/user/index.html)
- [Introduction to the ds9 Interface](http://ds9.si.edu/doc/user/gui/index.html)
- [Introduction to Astronomy Images and the DS9 Image Viewer](http://www.jb.man.ac.uk/~gbendo/Sci/Pict/DS9guide.pdf) tutorial de George J. Bendo
- [IPAC introduction to DS9, en cuatro videos](https://www.youtube.com/watch?v=C8QBwrKbEtc) by [Luisa Rebull](https://www.ipac.caltech.edu/science/staff/luisa-rebull) si tienes más tiempo y te gustan los tutoriales en video.  

La recomendación es ir aprendiendo poco a poco usando la herramienta y encontrando las funcionalidades a medida que las necesitamos. Se puede añadir a DS9 [Funtools](https://github.com/ericmandel/funtools) que es una librería FITS y paquete con utilidades.  
##### Ejemplo 
Como una primera introducción podemos descargarnos imágenes FITS del par de galaxias NGC274-NGC275 en las bandas u, g y r de la exploración [SDSS](https://www.sdss.org/) del [DR12 Science Archive Server (SAS)](https://dr12.sdss.org/fields)

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_1.png
---
width: 500px
name: ds9_1-fig
---
Imagen del par de galaxias en interación e la página de descarga de SDSS 
[https://dr12.sdss.org/fields/name?name=NGC274](https://dr12.sdss.org/fields/name?name=NGC274)
```
Tras descargarlas tenemos las tres imágenes como ficheros FITS frame-u-008067-4-0054.fits, frame-g-008067-4-0054.fits, frame-r-008067-4-0054.fits. Empecemos mostrando la imagen en banda g. Para ello en DS9 usamos los menús 'file' + 'open' y selecionamos el directorio y fichero. Se mostrará en la ventana. 

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_2.png
---
width: 500px
name: ds9_2-fig
---
Tras cargar la primera imagen.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_3.png
---
width: 500px
name: ds9_3-fig
---
No se ve la imagen completa sino un trozo. Arriba a la derecha vemos una miniatura y un cuadrado verde con al zona recortada que vemos en la ventana. El cuadro de más a la derecha muestra una ampliación del punto donde tenemos el cursor.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_4.png
---
width: 500px
name: ds9_4-fig
---
Tras hacer zoom para imagen completa. Nótese que aparecen arriba a la izquierda el nombre del fichero y las coordenadas de imagen (píxeles) y celestes (WCS world coordinate system) ya que en este caso es una imagen completamente procesada incluyendo astrometría.
```

Las imágenes de las galaxias aparecen saturadas porque la escala empleada para mostrar la imagen se queda corta y hay valores en los píxeles de las galaxias por encima de 0.12 que es el límite superior elegido automáticamente (abajo a la derecha). Con el menú de escala y colocando nuestros límites a mano entre 0 y 5 unidades se obtiene una representación que permite ver las variaciones en la galaxia.

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_5.png
---
width: 500px
name: ds9_4-fig
---
Diálogo de límites para la escala de la representación gráfica que muestra un histograma de los valores de los píxeles de la imagen. Se pueden cambiar con el cursor o escribiendo los valores deseados.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_6.png
---
width: 500px
name: ds9_6-fig
---
Tras hacer zoom y centrar las galaxias usando una tabla de color ('lookup table') de tipo arcoiris.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_7.png
---
width: 500px
name: ds9_7-fig
---
Tras hacer zoom y centrar las galaxias usando una tabla de color ('lookup table') de tipo arcoiris.
```

Podemos cargar otra imagen en otro canal o 'frame' usando el menú 'frame'+'new' y eligiendo el fichero.


```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_8.png
---
width: 500px
name: ds9_8-fig
---
Nuevo fichero cargado en el canal ('frame') 2. De momento usa el mismo zoom que el canal 1 pero no está centrado en las galaxias.
```
```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_9.png
---
width: 500px
name: ds9_9-fig
---
Usando el menu de 'frame'+'match'+'image'+'WCS' centramos las dos imágenes en el mismo sitio. Se usa de referencia la imagen seleccionada. En este caso la primera.
```
Podemos ver las dos imágenes porque estamos en modo tejar ('tile') pero podemos seleccionar para ver sólo una ('single') o incluso hacer parpadeo entre las cargadas. Cargemos la última imagen correspondiente a la banda u.

```{figure} /_static/lecture_specific/p1_intro/intro_03_ds9_10.png
---
width: 500px
name: ds9_10-fig
---
Vemos las tres imágenes cargadas en 3 canales diferentes. Para que se vean así en columnas hay que elegirlo en el menu de 'frame'+'farme parameters'+'tile'.
```


- NED buscar y cargar cargar imagen
- Regiones y Fotometría sencilla

#### ALADIN
[Aladin](https://aladin.u-strasbg.fr/), etc.

### Programación en Python y cuadernos de Jupyter
Ventajas e inconvenientes frente a los paquetes tradicionales.

#### Importancia de la utilización de un sistema de control de versiones
Introducción a [Git]https://git-scm.com/)

#### Acceso a catálogos on line desde Python
Realización de queries a [Vizier](https://vizier.u-strasbg.fr/viz-bin/VizieR)
 y [Aladin](https://aladin.u-strasbg.fr/).
Utilización del paquete [PyVO](https://pypi.org/project/pyvo/) para acceder a datos astronómicos en archivos que siguen los estándares definidos por el IVOA (International Virtual Observatory Alliance).

### Cuaderno de observaciones
Importancia del logbook de observación para el procesado posterior de las imágenes.

### La llegada de fotones a un detector
Utilizando un array de pequeñas dimensiones, se simula la llegada poissoniana de fotones a un detector y la posterior conversión analógica-digital. Esta simulación permite ilustrar conceptos básicos de relación señal/ruido y propagación de incertidumbres.

### Imágenes de calibración
Bias, dark, flat fields de baja y alta frecuencia, arcos para calibración en longitud de onda. Se explican sus características y utilización. Definición de región útil del detector y regiones de under/overscan. Utilización de binning durante las observaciones para incrementar la relación señal/ruido y/o reducir el tiempo de lectura.

### Ejemplo de reducción de imágenes CCD
Utilizando un subconjunto de las imágenes disponibles para la Práctica 2, se ilustrará la aplicación de calibraciones básicas (corrección de cero, corrección de flat field, corrección de rayos cósmicos), la combinación de imágenes individuales y la calibración astrométrica.

### Ejemplo de reducción de espectros CCD
Utilizando un subconjunto de las imágenes disponibles para la Práctica 3, se ilustrará la aplicación de calibraciones básicas (corrección de cero, corrección de flat field, corrección de rayos cósmicos, calibración en longitud de onda, corrección de iluminación) y la combinación de imágenes individuales.

### Estrategias para la estimación de incertidumbres
Propagación analítica frente a la utilización de técnicas de bootstrapping y Monte Carlo.


