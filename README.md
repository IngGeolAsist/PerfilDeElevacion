# Perfil de Elevación
Hasta ahora hemos visto las características básicas de Leaflet, sin embargo , ya que lo visto hasta ahora es algo que fácilmente puede ser desarrollado en cualquier Gis , te estarás preguntando ¿qué ventajas tiene Leaflet sobre un SIG?. Bueno, el mayor potencial de Leaflet proviene de todas las herramientas que se han desarrollado por la comunidad, ofreciendo características extendidas, por lo que si piensas que Leaflet no incluye una herramienta que estas buscando es muy posible que alguien ya haya desarrollado un Plugin que hace exactamente que estás buscando. 
###  Y a grandes rasgos eso es un plugin, una extensión de las características usuales de Leaflet que nos brinda herramientas nuevas, desarrolladas en por y para la comunidad.

El sitio oficial de Leaflet incluye un enorme catalogo de plugins disponibles, los cuales puedes revisar en https://leafletjs.com/plugins.html. Estos plugins incluyen herramientas para  medir  y digitalizar hasta buscar direcciones y calcular rutas.

Lamentablemente no podríamos hacer un tutorial para todos los plugins que hay, pero la información en la página es bastante detallada y seguramente podrás utilizar cualquier plugin sin problema. De manera paralela hay plugins que a pesar de no ser oficiales, son también desarrollos muy interesantes. En este tutorial veremos uno de ellos, que nos será útil para visualizar perfiles de elevación longitudinales. 

### 1.	Para comenzar, necesitaremos reunir toda la información necesaria para utilizar el plugin. 

Una vez mas utilizaremos QGIS para algunos procesamientos de capas vectoriales como lo hicimos en la Parte IV: Capas Vectoriales: GeoJSON con Estilos Simples. 

Necesitamos seleccionar la capa vectorial (cuya geometría sea de tipo línea) de la que deseamos obtener el perfil, también necesitamos una capa ráster con la información de las elevaciones, puede ser el DEM de la zona de estudio. Recuerda que toda la información debe estar en coordenadas geográficas.

![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen1.png )

### 2.	Ya con toda la información, dibujaremos una nueva línea, con un mayor número de iteraciones, ya que si tu sección es solo una línea recta, como sabrás, solo dos coordenadas son necesarias para dibujarla, y múltiples puntos de la línea son necesarios para representar ldiferentes elevaciones a lo largo del perfil.

 Para esto utilizaremos la herramienta de puntos aleatorios, seleccionaremos la cantidad que consideremos que es suficiente para nuestro perfil, a mayor cantidad el perfil será mas detallado. 

![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen2.png )

  Selecionamos el numero de puntos que deseamos agregar, yo elegí 300
  
  ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen3.png )

### 3. Creamos una nueva capa vectorial y con el sniping tool, uniremos los puntos. A partir de este momento solamente utilizaremos esta capa nueva. 

  ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen4.png )
  
  Guardamos la información en la carpeta correspondiente del proyecto
 ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen5.png )
 ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen6.png )
  Comenzamos a trazar la linea uniento los puntos que creamos en el paso anterior
 ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen7.png )
  Si decidiste etiquetar la línea con algún id para la tabla de atributos, llenas la información requerida
 ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen8.png )
 
 
### Nos dirigiremos al icono de herramientas, y buscaremos la herramienta “Drape” esta nos ayudará a asociar un dato de elevación para cada punto de la línea que dibujamos. Exportamos esta capa en formato geojson. Y hacemos el tratamiento correspondiente para poder agregar la capa vectorial al código. 
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen9.png )
Seleccionamos la línea ala que queremos añadir la información de la elevación y la capa ráster de la que se obtendrá la elevación
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen10.png )
Obtendremos una nueva línea, en este caso con las alturas incluidas, para verificar esto asegurate de que la capa incluya la siguiente leyenda 
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen11.png )

