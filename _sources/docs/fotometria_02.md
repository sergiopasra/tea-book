# Instrumentos y métodos
 

```{note}
Este capítulo asume conocimientos básicos de fotometría astronómica 
explicados en la signaturas de Astrofísica previas al Máster. 
En particular de Astrofísica y de Astronomía Observacional del Grado en Física 
y de Instrumentación Astronómica del máster en Astrofísica.  
```

## Fotometría visual y fotográfica
La clasificación de estrellas de acuerdo a su brillo aparente que realizó el astrónomo griego Hiparcos está basada en la comparación de sus observaciones a simple vista sin ninguna instrumentación óptica. Estableció una escala de magnitudes siendo las estrellas en la categoría de primera magnitud las más brillantes. Esta 'fotometría visual' utiliza el ojo humano como detector y no emplea filtros. Por lo tanto la banda de paso viene definida por la respuesta espectral del ojo. Todavía hoy en día se utiliza la fotometría visual en observaciones de astrónomos aficionados que pueden observar y medir (por comparación) las magnitudes de estrellas más débiles que el límite impuesto por la sensibilidad del ojo.

Con el desarollo de la fotografía a mediados del siglo XIX se dispuso de un detector que colocado en el foco de un telescopio permitía registrar estrellas más débiles y en un rango espectral diferente a la banda visual. Con emulsiones fotográficas sensibles en diferentes intervalos espectrales (detector) y filtros se podían tomar imágenes de campos estelares o de objetos extensos (al ser un detector de imagen o panorámico) en difrentes bandas fotométricas. Estas observaciones de 'fotometría fotográfica', a diferencia de las visuales, dejan una placa fotográfica  que, correctamente almacenada, puede volver a medirse  las veces que se desee incluso después de muchos años. aunque su formato no es digital, las placas pueden ser escaneadas para producir un fichero tratable con ordenadores.

## Fotometría fotoeléctrica
Los astrónomos utilizaton en sus observaciones los fotodetectores más sencillos en cuanto éstos estuvieron disponibles. La 'Fotometría Fotoeléctrica' supuso un gran avance en sensibilidad permitiendo observar y medir objetos más débiles. Los fotómetros fotoeléctricos tienen como detector una célula fotoeléctrica o mejor un fotomultiplicador. Este dispositivo 
electrónico transforma los fotones incidentes en corriente eléctrica que puede ser medida. Las ventajas principales son su linealidad, de la que carece la emulsión fotográfica, y su mayor eficiencia cuántica.
- Stebbins, Whitford & Kron  (ca. 1940)         fotocélulas
- Johnson, Morgan, Whitford et al. (ca. 1950)   fotomultiplicadores
  - RCA 1P21 (fotomultiplicador sensible al azul)
  - Sistema de Johnson  bandas U B V con RCA 1P21
- Sistema de Strömgren ubvy
- Kron (1958)    Fotocátodo S1  (sensible al rojo)
- Johnson et al. (1966)   bandas R I
   - Fotocátodo S25 y GaAs (mucho más sensibles que 1P21)
- Bessel (1976) U B V R I con el mismo fotomultiplicador
   - Aumento de la lista de estándars primarias y secundarias
       Cousins (1976-1980)     Cousins UBVRI
       Landolt (1973-1983)     Landolt UBVRI

Desgraciadamente estos sistemas son algo diferentes por usar filtros distintos.


## Fotometría CCD
La fotometría fotoeléctrica sólo permite observar una estrella cada vez o una parte de un objeto extenso, es decir que no tiene la capacidad de un detector de imagen con resolución espacial. La 'Fotometría CCD' (casi la única que se usa en la actualidad) desplazó a la fotometría fotoeléctrica ya que tiene como gran ventaja el uso de un detector panorámico. Las imágenes obtenidas con un detector CCD contienen información de los objetos celestes contenidos en el campo de visión del sistema. Estas observaciones simultáneas de múltiples objetos tienen la gran ventaja del ahorro de tiempo de observación y la garantía de observación en el mismo lapso de tiempo lo que es ideal para fotometría diferencial.

Por citar algunos inconvenientes tenemos los propios de la observación con CCDs (tiempos muertos leyendo el detector, por ejemplo) y el procesado de las imágenes CCD. Con la fotometría fotoeléctrica se obtenían mejor precisión fotométrica en menos tiempo de observación. También existen problemas relacionados con la variación de la transmisión de los filtros interferenciales con el ángulo de llegada de la luz, lo que se traduce en diferencias de banda de paso en zonas de la imagen según te alejas del eje óptico. También existe una gran variedad de CCDs en el mercado con diferencias considerables en la respuesta espectral en el azul que no facilitan la calibración de la banda U, por ejemplo.

Todos estos inconvenientes quedan en un segundo plano con la facilidad de uso de los CCDs y de su procesado posterior. Los CCDs se sitúan en criostatos que mantienen la temperatura del chip a temperatiras bajas (-120ºC típicamente) para evitar ruido térmico y con estabilización de temperatura para mantener su sensibilidad constante a lo largo de la observación.



### Observaciones de fotometría CCD

Los intrumentos  empleados para fotometría son cámaras CCD que disponen de una rueda de filtros seleccionables. Estas cámaras se elige en base a los requerimientos del proyecto de investigación y a su disponibilidad. Los parámetros importantes son el campo de visión que depende de la escala de placa del telescopio, de la amplificación de la cámara y del tamaño del CCD que se coloca en el plano focal de la cámara.

La lista de intrumentos para realizar fotometría de imagen y sus características se pueden consultar en los portales de los observatorios. Con la ayuda de los astrónomos de apoyo se configura de manera óptima a nuestras necesidades.

Como detector se emplea un CCD. Si el CCD es muy grande o la óptica de la cámara instrumento no es suficiente, sólo se usa parte de la imagen que proporciona el CCD. En ese caso se selecciona una región del mismo (ventana) en el momento de la observación  para no archivar ficheros innecesariamente grandes. Se ahorra espacio y tiempo de lectura del CCD.

Por ejemplo para las observaciones de CAFOS que proporciona un campo de visión de diámetro 16 arcmin y con un CCD tiene dimensiones de $2048 \times 2048$ píxeles se suele usar la parte central de $11 \times 11 \; arcmin^2$ que no está viñeteada y que corresponde a una ventana de $1024 \times 1024$ píxeles en el centro del CCD.  

```{figure} /_static/lecture_specific/fotometria/foto_39_CAFOS_window.png
---
width: 800px
name: Foto-CAFOS_window-fig
---
Recorte de la imagen CCD de CAFOS para seleccionar la zona central de $11 \times 11 \; arcmin^2$.
```
```{figure} /_static/lecture_specific/fotometria/foto_40_CAFOS_FoV.png
---
width: 600px
name: Foto-CAFOS_FoV-fig
---
Imagen completa de CAFOS mostrando la región útil y la ventana cuadrada que suele recortarse.
```

Las observaciones de fotometría de imagen incluyen 

- Las imágenes usadas para calibración del CCD: los BIAS y DARK para medir el nivel de pedestal y la corriente de oscuridad si la hubiera. De esta manera podemos retirar la parte aditiva de la señal.
Los Flat Field (bien con imágenes de lámparas en la cúpula ('Dome flats') o imágenes de cielo en crepúsculo (Sky flats') para determinar la variación espacial de la sensibilidad del CCD.

- Imágenes de los campos que contienen los objetos motivo de nuestro proyecto científico.

- Idem de estrellas estándar para calibración fotométrica. El flujo en las bandas fotométricas de estas estándares fotométricas es conocido y por comparación entre el resultado de la observación podemos determinar las constantes instrumentales y los coeficientes de extinción (véase fotometría absoluta).
