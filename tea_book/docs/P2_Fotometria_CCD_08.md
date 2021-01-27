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


# Procesado segunda noche
Se incluyen en esta sección algunas ayudas para realizar la misma tarea de reducción de observaciones que se ha descrito con detalle para la primera noche. 

La primera tarea sería bajarse los ficheros correspondientes a las observaciones de la segunda noche a un directorio de nombre N2 en este caso. Los cuadernos de jupyter se pueden usar teniendo en cuenta este cambio de nombre del directorio de trabajo. 

Se trata de realizar todo el proceso de reducción y obtener la calibración fotométrica. El cuaderno de observaciones tiene registrado que la noche aparentemente fue buena ("¡Noche preciosa!") con humedad H=0%, temperatura 5.3C, viento 0.7 m/s y presión 769 HPa.

## Listado de las observaciones disponibles
Para ganar tiempo se listan las observaciones de la segunda noche con información adicional sacada del cuederno de observaciones.

<pre>
AL13001 - AL13010		BIAS afternoon			# BIAS
AL13011 - AL13015		Sky Flat NB#78			# FLATS al anochecer
AL13016 - AL13022		Sky Flat NB#49
AL13023 - AL13027		Sky Flat B
AL13028 - AL13032		Sky Flat V
AL13033 - AL13039		Sky Flat R
AL13040 - AL13046		HZ44 foco			# Imágenes para obtener foco
AL13047 - AL13054		Feige34 foco			# interesan poco

AL13058 - AL13060		NGC3395 V 3x400s	
AL13061 - AL13063		NGC3982 V 3x400s
AL13064 - AL13066		NGC3982 B 3x600s
AL13067 - AL13069		NGC5668 R 3x300s
AL13070 - AL13072		NGC5668 #49 3x900s
AL13073 - AL13075		NGC5669 R 3x300s
AL13076 - AL13078		NGC5669 #78 3x900s
AL13079 - AL13081		NGC5669 B 3x600s
AL13082 - AL13084		NGC5669 V 3x400s
AL13085 - AL13087		NGC5668 V 3x400s
AL13088 - AL13090		NGC5668 B 3x600s
AL13091 - AL13093		NGC4941 B 3x600s
AL13094 - AL13096		NGC4941 V 3x400s

AL13097	  BD+33d2642	V 	2s	sec z = 1.02		# Estrellas estándar
AL13098	  BD+33d2642	V	0.5	4h25m
AL13099	  BD+33d2642	B	1s
AL13100	  BD+33d2642	R	1s
AL13101	  BD+33d2642	#49	25s	4h29m
AL13102	  BD+33d2642	#78	25s	4h31m

AL13103	  HR7001	#78	1s	Vega !
AL13104	  HZ44		#78	20s	4h36m 1.4
AL13105	  HZ44		#49	30s	4h38m
AL13106	  HZ44		V	1s
AL13107	  HZ44		B	2s	4h41m
AL13108	  HZ44		R	2s	4h43m

AL13109	  HZ21		R	5s	4h44m 2.05
AL13110	  HZ21		R	20s	
AL13111	  HZ21		B	30s	4h47m
AL13112	  HZ21		V	30s	4h49m

AL13113	  			NGC3982 R 300s			# Imágenes de ciencia
AL13114				NGC5363 R 300s
AL13115				NGC5668 R 300s
AL13116				NGC5669 R 300s
AL13117 - AL13121		GRB R 200s			# GRB (Target of Oportunity)

AL13122	  BD+33d2642	R	0.5s  5h45m sec z = 1.13	# Estrellas estándar
AL13123	  BD+33d2642	B	0.5s  5h46m
AL13124	  BD+33d2642	V	0.5s  5h47.5m
AL13125	  BD+33d2642	#49	25s   5h49m
AL13126	  BD+33d2642	#78	25s   

AL13127	  BD+28d4211	#78	25s   5h53m sec z = 1.47
AL13128	  BD+28d4211	#49	25s   5h54m
AL13129	  BD+28d4211	V	1s
AL13130	  BD+28d4211	B	1s
AL13131	  BD+28d4211	R	1s

AL13132	  HZ44		R	2s	06h01m	sec z = 2.1
AL13133	  HZ44		B	2s
AL13134	  HZ44		V	2s	06h04m
AL13135	  HZ44		#78	30s	06h05.5m
AL13136	  HZ44		#49	30s	06h07m

AL13137 - AL13141	Sky Flats R				# FLATs al amanecer
AL13142 - AL13147	Sky Flats V
AL13148 - AL13150	Sky Flats B
AL13151 - AL13153	Sky Flats #49
AL13154 - AL13156	Sky Flats #78

AL13157 - AL13170	BIAS					# BIAS
</pre>

Vamos a retirar las imágenes que no necesitamos para acelerar el proceso antes de hacer el listado de todas las imágenes. Son las correspondientes al enfoque del telescopio  (AL13040 - AL13054) y las observaciones del GRB (AL13117 - AL13121). Simplemente las borramos del directorio para no arrastrarlas en la reducción.

## Reducción paso a paso
Exactamente igual que en la primera noche.
Este listado de tareas nos sirve de resumen:

###   Recortar
###   Preparar el BIAS maestro
<pre>
AL13001 - AL13010		BIAS afternoon			# BIAS
AL13157 - AL13170		BIAS					# BIAS
</pre>

###   Corregir de BIAS
###   Preparar FF maestro (para cada filtro)
Podemos empezar usando los Flats del anochecer    
<pre>
AL13011 - AL13015		Sky Flat NB#78			# FLATS al anochecer
AL13016 - AL13022		Sky Flat NB#49
AL13023 - AL13027		Sky Flat B
AL13028 - AL13032		Sky Flat V
AL13033 - AL13039		Sky Flat R
</pre>
Que debemos inspeccionar para retirar los de baja señal o imágenes estrellas, por ejemplo.
Combinados debemos obtener los flats de cada filtro 
<pre>
N2_flat_49.fits 		N2_flat_78.fits 		
N2_flat_B.fits  		N2_flat_R.fits  		N2_flat_V.fits
</pre>
###   Preparar las listas de las observaciones en cada filtro.
    
<pre>
sci_lista_49
	AL13070 - AL13072	NGC5668 #49 3x900s
	AL13101	  BD+33d2642		 #49	25s	4h29m
	AL13105	  HZ44			 #49	30s	4h38m
	AL13125	  BD+33d2642		 #49	25s    5h49m
	AL13128	  BD+28d4211		 #49	25s    5h54m
	AL13136	  HZ44			 #49	30s	06h07m
	sci_lista_78
	AL13076 - AL13078		NGC5669 #78 3x900s
	AL13102	  BD+33d2642		#78	25s	4h31m
	AL13103	  HR7001		#78	1s	Vega !
	AL13104	  HZ44			#78	20s	4h36m 1.4
	AL13126	  BD+33d2642		#78	25s   
	AL13127	  BD+28d4211		#78	25s    5h53m sec z = 1.47
	AL13135	  HZ44			#78	30s	06h05.5m
	sci_lista_B
	AL13055 - AL13057		NGC3395 B 3x600s		
	AL13064 - AL13066		NGC3982 B 3x600s
	AL13079 - AL13081		NGC5669 B 3x600s
	AL13088 - AL13090		NGC5668 B 3x600s
	AL13091 - AL13093		NGC4941 B 3x600s
	AL13099	  BD+33d2642			 B	1s
	AL13107	  HZ44				 B	2s	4h41m
	AL13111	  HZ21				 B	30s	4h47m
	AL13123	  BD+33d2642			 B	0.5s   5h46m
	AL13130	  BD+28d4211			 B	1s
	AL13133	  HZ44				 B	2s
	sci_lista_V
	AL13058 - AL13060		NGC3395 V 3x400s	
	AL13061 - AL13063		NGC3982 V 3x400s
	AL13082 - AL13084		NGC5669 V 3x400s
	AL13085 - AL13087		NGC5668 V 3x400s
	AL13094 - AL13096		NGC4941 V 3x400s
	AL13097	  BD+33d2642			 V 	2s	sec z = 1.02	
	AL13098	  BD+33d2642			 V	0.5	4h25m
	AL13106	  HZ44				 V	1s
	AL13112	  HZ21				 V	30s	4h49m
AL13124	  BD+33d2642			 V	0.5s  5h47.5m
AL13129	  BD+28d4211			 V	1s
AL13134	  HZ44				 V	2s	06h04m
sci_lista_R
AL13067 - AL13069		NGC5668 R 3x300s
AL13073 - AL13075		NGC5669 R 3x300s
AL13100	  BD+33d2642			 R	1s
AL13108	  HZ44				 R	2s	4h43m
AL13109	  HZ21				 R	5s	4h44m 2.05
AL13110	  HZ21				 R	20s	
AL13113	  			NGC3982 R 300s			# Imágenes de ciencia
AL13114				NGC5363 R 300s
AL13115				NGC5668 R 300s
AL13116				NGC5669 R 300s
AL13122	  BD+33d2642			 R	0.5s  5h45m sec z = 1.13
AL13131	  BD+28d4211			 R	1s
AL13132	  HZ44				 R	2s	06h01m	sec z = 2.1
</pre>

###   Corregir de FlatField
Para ganar tiempo, vamos a centranos en los filtros anchos de forma que procesaremos las observaciones en B, V y R. 

###   Fotometría
Para las observaciones de las estrellas estándar realizaremos fotometría de apertura.
Para la banda B debemos obtener:

<pre>
# File	  Star 	       texp   	R    	MAG    FLUX     SKY     PEAK   
AL13099	  BD+33d2642	1s    	12.78  10.27 776991.    8.36   26576.
AL13107	  HZ44		2s    	21.10  10.34 733935.    7.40    9127.	
AL13111	  HZ21		30s	23.33  10.54 610342.   24.93    6243.
AL13123	  BD+33d2642	0.5s	19.37  11.06 378236.    7.61    5782. 
AL13130	  BD+28d4211	1s	16.86   9.96 1.041E6   61.34   19862.
AL13133	  HZ44		2s	18.41  10.52 620666.   199.7   10489.
</pre>

En el resultado aparece R que es el radio usado en la fotometría después del ajuste y MAG que es una magnitud instrumental obtenida como MAG = ZP - 2.5 log10(Flux).  
No conocemos todavía el valor del punto cero (ZP) de la fotometría. En este caso al no conocer ZP hemos usado ZP=25. La magnitud instrumental debe calcularse con el flujo expresado en cuentas/s, es decir la expresión correcta es cualquiera de estas dos:
<pre>
	m(instrumental)  =  ZP - 2.5 * log10( F [c]    )     + 2.5 * log10 (texp))
	m(instrumental)  =  ZP - 2.5 * log10( F [c/s] ) 
</pre>

Para las observaciones de la banda B podemos preguntar el nombre de la estrella observada ('OBJECT'), el tiempo de exposición ('EXPTIME') y la masa de aire ('AIRMASS', secZ) de las cabeceras FITS y tenemos

<pre>
# Fichero         objeto          	sec Z            T expo(s)
fztAL13099.fits   BD+33d2642      	1.0223799944     1.000
fztAL13107.fits   BD+33d2642      	1.4269499779     2.000
fztAL13111.fits   HZ21    		2.0890600681     30.000
fztAL13123.fits   BD+33d2642      	1.1395900249     0.500
fztAL13130.fits   BD+28d4211      	1.4480500221     1.000
fztAL13133.fits   HZ44    		2.1041800976     2.000
</pre>

Hay que ser cuidadoso en el nombre correcto del parámetro (keyword) de la cabecera. 
Si en la cabecera no se almacena la masa de aire tendríamos que determinarla con la localización geográfica del observatorio, la fecha y hora de observación y las coordenadas de la estrella.

En la tabla final de la fotometría debemos incorporar la magnitud de la estrella estándar y el flujo medido. Podemos trabajar con un programa en el entorno que más nos guste (Python, MatLab, Excel etc). Vamos simplemente a ajustar rectas a resultados de observaciones. En los primeros capítulos se ofrece un ejemplo de cómo hacerlo con cuadernos de Jupyter.

Nuestro fichero de datos podría parecerse a éste
<pre>
# NOT_2008_04_12-14/N2
# Fotometria estrellas B
# Fichero		Estrella	sec Z	    texp    Flujo      Sky   V   B-V    
fztAL13099.fits, BD+33d2642, 1.0223799944 , 1. ,776991. ,  8.36  , 10.83 , -0.17 
fztAL13107.fits, BD+33d2642, 1.4269499779 , 2. ,733935. ,  7.40  , 10.83 , -0.17 
fztAL13111.fits, HZ21      , 2.0890600681 , 30.,610342. , 24.93 , 14.69 , -0.33
fztAL13123.fits, BD+33d2642, 1.1395900249 , 0.5,378236. , 7.61  , 10.83 , -0.17 
fztAL13130.fits, BD+28d4211, 1.4480500221 , 1. ,1.041E6 , 61.34 , 10.51 , -0.34
fztAL13133.fits, HZ44      , 2.1041800976 , 2. ,620666. , 199.7 , 11.67 , -0.29 
</pre>

donde los datos V y B-V los hemos buscado en Simbad o en listas de estrellas estándar de las páginas de los observatorios. La recomendación es usar el artículo:

"Optical Multicolor Photometry of Spectrophotometric Standard Stars"  
Arlo U. Landolt1,3,4 and Alan K. Uomoto2,3  
The Astronomical Journal, Volume 133, Issue 3, pp. 768-790.  
[https://ui.adsabs.harvard.edu/link_gateway/2007AJ....133..768L/doi:10.1086/510485](https://ui.adsabs.harvard.edu/link_gateway/2007AJ....133..768L/doi:10.1086/510485)

Recordemos las ecuaciones de fotometría absoluta ($F$ es el flujo neto, sin fondo de cielo)

$$ m_\lambda = C_\lambda -2.5 log_{10}(F_\lambda [c/s]) - K_\lambda sec z $$

Por lo tanto si ajustamos 

$$ B + 2.5 log_{10}(F_B [c/s]) = C_B - K_B sec z$$

se obtiene la constante instrumental C y el coeficiente de extinción para el filtro B

```{figure} /_static/lecture_specific/p2_fotometria/p2_10_bouger_1.png
---
width: 800px
name: bouger-1-fig
---
Primer intento de ajuste de la recta de Bouger para el filtro B.
```
Apreciamos por una parte que el número de observaciones es pequeño. Además uno de los puntos se sale de la tendencia. Estamos sesgados a revisar los puntos raros y a dejar sin comprobar los que parecen que está bien. Somos humanos, así que miremos qué está pasando. 

La estrella que falla parece ser 
<pre>
fztAL13107.fits, BD+33d2642 , 1.4269499779,  2. ,733935., 7.40 , 10.83 , -0.17
</pre>
y si revisamos el cuaderno nos damos cuenta de que en realidad esta observación corresponde a HZ44 y el nombre de la estrella fue mal escrito en la cabecera del fichero.


```{figure} /_static/lecture_specific/p2_fotometria/p2_10_bouger_2.png
---
width: 600px
name: bouger-1-fig
---
Extraído del cuaderno de observaciones.
```
luego tenemos que corregir esa línea en el fichero ya que la estrella observada es en realidad HZ44.
<pre>
fztAL13107.fits, HZ44 , 1.4269499779 , 2.,733935. , 7.40  , 11.67 , -0.29
</pre>
Con ese cambio (después de revisar que lo demás está bien) obtenemos un nuevo ajuste, con menos dispersión,


```{figure} /_static/lecture_specific/p2_fotometria/p2_10_bouger_3.png
---
width: 800px
name: bouger-3-fig
---
Ajuste de la recta de Bouger para el filtro B una vez corregido el error.
```

El resultado final es $C_B = 25.62$ y $K_B = 0.243$. En este caso no hemos determinado erroes en estos parámetros pero deberíamos hacerlo. 

Repetiremos el proceso para el resto de los filtros y determinaremos las constantes instrumentales y coeficientes de extinción de esta noche en todos los filtros empleados. Como entregable se esperan las gráficas de Bouger y los valores de los ajustes.



