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
 ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen8.png )
  ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen9.png )
  Si decidiste etiquetar la línea con algún id para la tabla de atributos, llenas la información requerida
 ![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen10.png )
 
 
### 4. Nos dirigiremos al icono de herramientas, y buscaremos la herramienta “Drape” esta nos ayudará a asociar un dato de elevación para cada punto de la línea que dibujamos. Exportamos esta capa en formato geojson. Y hacemos el tratamiento correspondiente para poder agregar la capa vectorial al código. 
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen11.png )
 Seleccionamos la línea a la que queremos añadir la información de la elevación y la capa ráster de la que se obtendrá la elevación
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen12.png )
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen13.png )
 Obtendremos una nueva línea, en este caso con las alturas incluidas, para verificar esto asegurate de que la capa incluya la siguiente leyenda 
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen14.png )

### 5.  Declaramos el estilo de esta capa en la sección correspondiente. 

``` html
<script>
<!-- ------ ESTILOS PARA CAPAS VECTORIALES ------ -->

	var seccion_style = {
		    "color": "#000000",
		    "weight": 5,
		};
</script>
	
```

 Agregamos la capa al código verificamos que se haya cargado correctamente.

``` html
<script>
<!-- ------ ESTILOS PARA CAPAS VECTORIALES ------ -->

	var seccion_style = {
		    "color": "#000000",
		    "weight": 5,
		};
</script>
	
```

### 6. Para agregar el plugin
Te recomendamos vayas a esta liga https://github.com/jlgrandes/Example_Leaflet-Elevation descargues el proyecto, o si lo prefieres solamente los archivos que sean necesarios. Descomprimimos y abrimos la carpeta, Necesitamos guardar los archivos leaflet-elevation.css y
leaflet-elevation.js  en la carpeta de DATA, donde se encuentran los demás archivos auxiliares de nuestro proyecto.  Abrimos el archivo llamado ExampleLeafletElevation-geojson.html en nuestro procesador de textos, (en este caso Notepad++)  Hay que leer el código y analizar que líneas de código necesitamos incluir en nuestro proyecto. 

## De arriba hacia abajo necesitamos incluir las siguientes líneas en el head de nuestro proyecto

En <head>, Las librerías de d3, la hoja de estilos de estilos para la sección.
 
 ``` html
 	<script src="https://d3js.org/d3.v5.min.js"></script>
	<link rel="stylesheet" href="DATA/leaflet-elevation.css" />
	<script type="text/javascript" src="DATA/leaflet-elevation.js"></script>
 ```
  
En <body>, una etiqueta div que contenga la sección.

``` html
<div id="mapDIV"></div>
<div id="elevation-div"></div>
```

Y al final del código agregaremos una nueva sección con las líneas de código que pertenecen al plugin en si
 
 ``` html
<!-- PLUGINS: PERFIL DE ELEVACIÓN LONGITUDINAL -->
 <script>
		var el = L.control.elevation({
  			position: "bottomleft",
            theme: "steelblue-theme", //default: lime-theme
            useHeightIndicator: true, //if false a marker is drawn at map position
            interpolation: d3.curveLinear, //see https://github.com/d3/d3/wiki/
            collapsed: false, //collapsed mode, show chart on click or mouseover
            detachedView: true, //if false the chart is drawn within map container
            elevationDiv: "#elevation-div", // (detached) elevation chart container
			});
		el.addTo(map);
		
		var seccion = L.geoJson(seccion,{
			style:seccion_style,
		    onEachFeature: el.addData.bind(el)
		}).addTo(map);
  </script>

```
### Asi debería verse tu codigo.
``` html
<html>
<head>
	<meta charset="utf-8">
	<title>Mapa E14C17_2</title>
	
	<!-- -----LIBRERIAS-------- -->
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"
	integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
	crossorigin=""/>
	<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"
	integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew=="
	crossorigin=""></script>
	
	
	<script src="https://d3js.org/d3.v5.min.js"></script>
	<link rel="stylesheet" href="DATA/leaflet-elevation.css" />
	<script type="text/javascript" src="DATA/leaflet-elevation.js"></script>
	
	<!-- -----CAPAS JSON------ -->
	
	
	<script type="text/javascript" src="DATA/json/Geología_PeñaDe Bernal_GCS.js"></script>
	<script type="text/javascript" src="DATA/json/contact.js"></script>
	<script type="text/javascript" src="DATA/json/seccion.js"></script>
	
	
	
	
	<!-- -----ESTILOS DEL MAPA------ -->
	<style>
	#mapDIV {
	height: 100%;
	width: 100%;
	border: solid 2px black;
	}
	</style>
</head>

<body>
<div id="mapDIV"></div>
<div id="elevation-div"></div>

 <script>	
 <!-- ------ CARACTERISTICAS DEL MAPA------ -->
 var map = L.map('mapDIV', {
		center:[20.83748 , -99.71396],
		zoom:11
	});
	
	
	var scale = L.control.scale({
		'imperial':false
	});
	scale.addTo(map);
	
<!-- ------ ESTILOS PARA CAPAS VECTORIALES ------ -->
	
	var contact_style = {
		color: "#000000",
		weight: 2,
		opacity: 1,
	};
	
	var seccion_style = {
		    "color": "#000000",
		    "weight": 5,
		};
	
<!-- ------CAPAS BASE------ -->
	
	var osm = L.tileLayer('http://a.tile.openstreetmap.org/{z}/{x}/{y}.png',
	{attribution: 'Map Data &copy; OpenStreetMap contributors'
	});
	osm.addTo(map);
	
	var topo = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
	maxZoom: 17,
	attribution: 'Map data: &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)'
	}); 
	topo.addTo(map);
	
	var sat = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
	attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
	});

<!-- ----- CONTROLADOR DEL MAPA------	 -->
	var basemaps = {
		"OSM": osm,
		"Topografía": topo,										
		"Satélite": sat
		};
	L.control.layers(basemaps).addTo(map);
	
<!-- ----- CAPAS VECTORIALES------	 -->
	var geology = L.geoJson(geology, {
	style:function(feature){
			switch (feature.properties.CLAVE){
				case 'Qhoal': return {color:'#fff5dd',fillOpacity: .5};
				case 'Qhoco': return {color:'#f7ece1',fillOpacity: .5};			
				case 'TplQptB': return {color:'#bf9487',fillOpacity: .5};
				case 'TplQptCgp-Ar': return {color:'#eedfb3',fillOpacity: .5};
				case 'TeGd-D': return {color:'#ed1c24',fillOpacity: .5};
				case 'TeoCgp': return {color:'#d8e9b9',fillOpacity: .5}; 
				case 'TmplA-B': return {color:'#fbc9bc',fillOpacity: .5};
				case 'TplA-Da': return {color:'#e4c19b',fillOpacity: .5};
				case 'TplR-TR': return {color:'#f9b6ac',fillOpacity: .5};
				case 'TplTR-TDa': return {color:'#f7b9d4',fillOpacity: .5};
				case 'ToR-TR': return {color:'#e1a49c',fillOpacity: .5};
				case 'KapceCz-Bro': return {color:'#00ac4e',fillOpacity: .5};	
				case 'KiCz-Lu': return {color:'#5f7641',fillOpacity: .5};
				case 'KsLu-Cz': return {color:'#698c42',fillOpacity: .5};
				case 'JtKvLu-Cz': return {color:'#76cdd6',fillOpacity: .5};	
			}}
			}).addTo(map);
	
	var contact = L.geoJson(contact,{
		style: contact_style
		}).addTo (map);
		
<!-- PLUGINS: PERFIL DE ELEVACIÓN LONGITUDINAL -->


		var el = L.control.elevation({
  			position: "bottomleft",
            theme: "steelblue-theme", //default: lime-theme
            useHeightIndicator: true, //if false a marker is drawn at map position
            interpolation: d3.curveLinear, //see https://github.com/d3/d3/wiki/
            collapsed: false, //collapsed mode, show chart on click or mouseover
            detachedView: true, //if false the chart is drawn within map container
            elevationDiv: "#elevation-div", // (detached) elevation chart container
			});
		el.addTo(map);
		
		var seccion = L.geoJson(seccion,{
			style:seccion_style,
		    onEachFeature: el.addData.bind(el)
		}).addTo(map);
	 
 </script>
</body>
</html>
```

### 7.Ejecutamos en el navegador, y deberíamos  visualizar algo como lo siguiente
![screenshot](https://raw.githubusercontent.com/sampach95/PerfilDeElevacion/master/img/Imagen18.png )


Haz click en el siguiente enlace para volver a la pagina inicial https://github.com/IngGeolAsist/ComoCrearMapasEnLaWebConLeaflet

