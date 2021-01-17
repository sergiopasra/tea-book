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

#  Redución de observaciones astronómicas
Las observaciones astronómicas que emplean detectores de imagen tipo CCD deben procesarse o reducirse para proporcionar imágenes o espectros calibrados. Sólo tras la reducción de las observaciones podemos medir en ellas para obtener la información que nuestro proyecto científico requiera. Este procesado debe ser cuidadoso porque de él depende la calidad final de nuestras medidas.

## Formato FITS de las imágenes astronómicas 
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


## Paquetes de reducción de datos
La reducción de las observaciones astronómicas con imágenes digitales al principio de estar disponibles era una tarea a la que los astrónomos se enfrentaban con sus propios medios. No sólo para leer los ficheros sino para calibrar y extraer la información de los mismos. De aquellos tiempos quedan astrónomos que prefieren desarrollar sus propios programas.  
Sin embargo aparecieron enseguida paquetes de reducción desarrollados por observatorios o centros de investigación que fueron de gran ayuda sobre todo para los astrónomos con menos conocimientos de programación. En cualquier caso supuso un avance ya que permitieron a los investigadores dedicar el tiempo a la reducción de los datos y no al desarrollo de software. Estas herramientas fundamentales se mantenían con ayuda de expertos cuyo cometido era fundamentalmente éste y también con la aportación de astrónomos.

### STARLINK 
Otro problema adicional era el acceso a ordenadores capaces de realizar este trabajo. Por ejemplo en el año 1978 se decidió en el Reino Unido establecer [STARLINK](http://starlink.eao.hawaii.edu/starlink) con una red de 6 ordenadores (superminicomputers DEC VAX 11/780) conectados entre sí. Resulta instructivo comprobar lo que se ha avanzado desde entonces (5000 Mbytes of disc space and 12 Mbytes of memory).

```{figure} /_static/lecture_specific/p1_intro/intro_02_starlink.png
---
height: 200px
name: starlink-fig
---
Source: [http://www.chilton-computing.org.uk/acd/starlink/p002.htm](http://www.chilton-computing.org.uk/acd/starlink/p002.htm)
```

Los primeros ordenadores VAX (sistema operativo VMS) dieron paso a los miniVAX y luego al sistema operativo Unix en estos ordenadores y otros de SUN y finalmente pudieron usar PCs con Linux.  El proyecto dejó de mantenerse en 2005 después de 25 años de funcionamiento. Por suerte para los nostálgicos el Joint Astronomy Centre siguió desarrollando software hasta 2015 y actualmente está mantenido por East Asian Observatory. El código es abierto ('open software').

### FIGARO
El paquete de software [FIGARO](http://star-www.rl.ac.uk/docs/sun86.htx/sun86.html) fue inicialmente desarrollado por Keith Shortridge  en los primeros 1980s para analizar los datos del observatorio de Monte Palomar. Escrito fundamentalmente en Fortran estaba compuesto de múltiples subrutinas para tareas de todo tipo en la reducción de observaciones astronómicas. Su uso se extendió rápidamente por los centros de investigación de todo el mundo. Era relativamente sencillo desarrolar rutinas propias para tareas diferentes e incorporarlas en el paquete.

### MIDAS
[ESO-MIDAS](https://www.eso.org/sci/software/esomidas/) fue desarrollado por el European Southern Observatory siguiendo los pasos de STARLINK en 1980 y usaba ordenadores VAX con sistema operativo VMS que posteriormente migró a UNIX. Su estructura es modular con rutinas accesibles por comandos que admiten parámetros siguiendo la filosofía del sistema de procesado de imagen 'Image handling and Processing system' [IHAP](https://link.springer.com/chapter/10.1007%2F0-306-48080-8_4) que estaba basado en ordenadores Hewlett-Packard. Se pueden desarrollar procedimientos que combinan varios comandos sucesivos para crear cadenas de procesado ('pipelines') con su sistema MCL ('MIDAS control language'). Su uso fue muy popular y aun hoy continua empleándose.  
En sus orígenes se necesitaba también un ordenador grande y una serie de periféricos para interaccionar con el sistema escribir los comandos y lanzar las aplicaciones (terminal o monitor) y otras terminales gráficas para mostrar imágenes o espectros, por ejemplo. Las rutinas de graficado de MIDAS se escribieron con el estándard de AGL (ASTRONET Graphic Library) desarrrolado por ASTRONET. Más tarde se las rutinas de Image Display Interface desarrolladas en colaboración con ST ScI, UK STARLINK, KPNO y Trieste Observatory.  Actualmente todo es más acesible ya que puede instalarse en ordenadores personales con sistemas operativos Linux y también sistemas Mac OSX. Las diferentes terminales gráficas aparecen como ventanas en el escritorio.

### IDL
[IDL](https://www.l3harrisgeospatial.com/Software-Technology/IDL) ('Interactive Data Language') es un lenguage de programación para análisis de datos que se usa entre otros campos en astronomía, ciencias de la atmósfera o análisis de imágenes en medicina.

### IRAF
[IRAF](http://ast.noao.edu/data/software) 'Image Reduction and Analysis Facility' es un software desarrollado en NOAO con el fin de procesar observaciones astronómicas. Escrito para sistema operativo Unix originalmente se usa en la actualidad en plataformas Linux o mac OS. IRAF está estructurado en tareas ('tasks') que están incluidas en paquetes. Dentro del proyecto IRAF existen desarrollos especiales como STSDAS ('Space Telescope Science Data Analysis System') para procesar datos de los instrumentos de HST (Hubble Space Telescope). IRAF ha sido tal vez el software más popular ya que algunos desarrolladores de instrumentación astronómica para grandes telescopios han escrito paquetes de procesado y tareas especiales para la reducción de las observaciones como nuevos paquetes.

### Astropy
[Astropy](https://www.astropy.org/)   
Las observaciones realizadas con modernos intrumentos astronómicos pueden ser reducidas por cadenas de procesado ('pipelines') sobre la marcha. De esta forma el investigador dispone de los datos reducidos inmediatamente. La exigencia de proporcionar esta utilidad es habitual en el desarrollo de instrumentación de primer nivel para asegurar el rendimiento científico de la inversión realizada. Para procesados más delicados o con mayor detalle en algún aspecto es normal que el investigador desee hacer una reducción más manual usando sus propios métodos y usando, generalmente, las herramientas disponibles. El proyecto Astropy es un esfuerzo conjunto (comunitario) de desarrollo de software para astronomía en Python [Astropy: A community Python package for astronomy](https://www.aanda.org/articles/aa/full_html/2013/10/aa22068-13/aa22068-13.html)


