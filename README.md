
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8" />
<title>Population density changes</title>
<meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no" />
<script src="https://api.mapbox.com/mapbox-gl-js/v1.11.0/mapbox-gl.js"></script>
<link href="https://api.mapbox.com/mapbox-gl-js/v1.11.0/mapbox-gl.css" rel="stylesheet" />
<style>

	body { margin: 0; padding: 0; }
	#map { position: absolute; top: 0; bottom: 0; width: 100%;  }
	#tytul {position: absolute; top: 10px; left: 10px;  background-color: white; font-size: 18px; opacity: 80%; padding: 10px; }
	

    .map-overlay {
    position: absolute;
    bottom: 0;
    right: 0;
    background-color: #d4dce6;

    margin-right: 10px;
    font-family: Arial, sans-serif; font-size: 14px;
    overflow: auto;
    border-radius: 3px;
    
    padding: 10px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
    line-height: 24px;
    
    margin-bottom: 25px;
    width: 100px;}

    

    .legend-key {
    display: inline-block;
    border-radius: 20%;
    width: 10px;
    height: 10px;
    margin-right: 5px;}

    #autor {position: absolute; bottom: 0; left: 100px;  background-color: white; font-family: Arial, sans-serif; font-size: 12px; opacity: 80%; padding: 10px;}

</style>

</head>

<body>
    <style>
    .mapboxgl-popup {
    max-width: 400px;
    font: 12px/20px 'Helvetica Neue', Arial, Helvetica, sans-serif;
    }
        
    #menu {
    background: #fff;
    position: absolute;
    z-index: 1;
    top: 10px;
    right: 50px;
    border-radius: 3px;
    width: none;
    border: 1px solid rgba(0, 0, 0, 0.4);
    font-family: 'Open Sans', sans-serif;
    }
     
    #menu a {
    font-size: 13px;
    color: #404040;
    display: block;
    margin: 0;
    padding: 0;
    padding: 10px;
    text-decoration: none;
    border-bottom: 1px solid rgba(0, 0, 0, 0.25);
    
    }
     
    #menu a:last-child {
    border: none;
    }
     
    #menu a:hover {
    background-color: #f8f8f8;
    color: #404040;
    }
     
    #menu a.active {
    background-color: #3887be;
    color: #ffffff;
    }
     
    #menu a.active:hover {
    background: #3074a4;
    }


</style>
<nav id="menu">  </nav>


<div id="map"></div>

<div class="map-overlay" id="legendd" style="visibility: visible">

    <div  id="legenda1" style="line-height: 18px; font-size: 12px;">Dynamika zmian gęstości zaludnienia w okresie 2002 - 2019. <br/> 2002 = 100%<br/></div>

    <div><span class="legend-key" style="background-color: #fef0d9;"></span><span>0-99</span></div>
    <div><span class="legend-key" style="background-color: #fdcc8a;"></span><span>100-112</span></div>
    <div><span class="legend-key" style="background-color: #fc8d59;"></span><span>113-138</span></div>
    <div><span class="legend-key" style="background-color: #e34a33;"></span><span>139-190</span></div>
    <div><span class="legend-key" style="background-color: #b30000;"></span><span>191-248</span></div>

</div>


<div class="map-overlay" id="legend2002" style="visibility: hidden">

    <div  id="legenda2002" style="line-height: 20px;" >Gęstość zaludnienia w 2002r. [osób/km2] </div>

    <div><span class="legend-key" style="background-color: #ffffb2;"></span><span>0-67</span></div>
    <div><span class="legend-key" style="background-color: #fecc5c;"></span><span>68-141</span></div>
    <div><span class="legend-key" style="background-color: #fd8d3c;"></span><span>142-369</span></div>
    <div><span class="legend-key" style="background-color: #f03b20;"></span><span>370-1844</span></div>
    <div><span class="legend-key" style="background-color: #bd0026;"></span><span>1845-2209</span></div>

</div>

<div class="map-overlay" id="legend2019" style="visibility: hidden">

    <div  id="legenda2019" style="line-height: 20px;">Gęstość zaludnienia w 2019r. [osób/km2] </div>

    <div><span class="legend-key" style="background-color: #ffffb2;"></span><span>0-86</span></div>
    <div><span class="legend-key" style="background-color: #fecc5c;"></span><span>87-160</span></div>
    <div><span class="legend-key" style="background-color: #fd8d3c;"></span><span>161-335</span></div>
    <div><span class="legend-key" style="background-color: #f03b20;"></span><span>336-589</span></div>
    <div><span class="legend-key" style="background-color: #bd0026;"></span><span>590-2364</span></div>

</div>


<div id="tytul">Zmiany gęstości zaludnienia <br/>w Poznaniu i gminach powiatu poznańskiego <br/>w okresie 2002-2019. </div>

<div id="autor" > Adrian Linkowski. ZPRZI. 2020-13-07.</div>


<script>
	mapboxgl.accessToken = 'pk.eyJ1IjoiYWRybGluMTEiLCJhIjoiY2tiaTQwcnp0MGJpcjJybHNoMDg1cDJ5NiJ9.0MnPILggpy5L8KvQ65fEZQ';

           
       // Set bounds 
    var bounds = [
    [0.0, 30.68392799015035], // Southwest coordinates
    [39.91058699000139, 65.87764500765852] // Northeast coordinates
    ];
     
    var map = new mapboxgl.Map({
    container: 'map',
    style: 'mapbox://styles/adrlin11/ckc6gvsld05ob1ioo6hdks8k8',
    center: [16.924936581286488, 52.410275834952785], //starting center
    zoom: 8.79, //starting zoom,
    maxBounds: bounds // Sets bounds as max
    });

    
        // Add zoom and rotation controls to the map.
    map.addControl(new mapboxgl.NavigationControl());

    var scale = new mapboxgl.ScaleControl({
    maxWidth: 80,
    unit: 'imperial'
    });
    map.addControl(scale);
     
    scale.setUnit('metric');

    map.addControl(new mapboxgl.FullscreenControl({container: document.querySelector('body')}));

    // ograniczenie poziomu powiększenia
    map.setMinZoom(4.58);
    map.setMaxZoom(12);



// utworzenie popupów
map.on('click', 'Dynamika zmian gestosci zaludnienia', function(e) {


    var gestosc_zaludnienia=e.features[0].properties._2019
    var nazwa=e.features[0].properties._Nazwa
    var image=e.features[0].properties.image
    var dynamika=e.features[0].properties.dynamika
    var name=e.features[0].properties._Nazwa
    var zmiana=(dynamika-100);
    var zmianaZaokraglona = zmiana.toFixed(2);


       
new mapboxgl.Popup()
        .setLngLat(e.lngLat)
        .setHTML(image +'<br/> Wykres gęstości zaludnienia w gminie '+name+ '<br/> w okresie 2002 - 2019. <br/> Gęstość zaludnienia w badanym okresie w gminie '+name+ '<br/> zmieniła się o : <b>'+zmianaZaokraglona+ '% </b>') 
        .setMaxWidth("none")
        .addTo(map);
});
 
// Change the cursor to a pointer when the mouse is over the states layer.
map.on('mouseenter', 'Dynamika zmian gestosci zaludnienia', function() {
    map.getCanvas().style.cursor = 'pointer';
});
 
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'Dynamika zmian gestosci zaludnienia', function() {
    map.getCanvas().style.cursor = '';
});



// przełączanie warstw 

    // enumerate ids of the layers
const toggleableLayerIds = ['Gestosc zaludnienia 2002', 'Gestosc zaludnienia 2019','Dynamika zmian gestosci zaludnienia'];

const toggleableLegendsIds = ['legend2002', 'legend2019','legend2002'];


// set up the corresponding toggle button for each layer
for (var i = 0; i < toggleableLayerIds.length; i++) {
var id = toggleableLayerIds[i];
 
var link = document.createElement('a');
link.href = '#';
link.className = 'active';
link.textContent = id; 

 
    link.onclick = function(e) {
    var clickedLayer = this.textContent;
    e.preventDefault();
    e.stopPropagation();
    for (var j=0; j<toggleableLayerIds.length; j++) {
        if (clickedLayer===toggleableLayerIds[j]) {
            layers.children[j].className = 'active';
            map.setLayoutProperty(toggleableLayerIds[j], 'visibility', 'visible');
             }
            else {
                layers.children[j].className = '';
                map.setLayoutProperty(toggleableLayerIds[j], 'visibility', 'none')
            }
        }
    
 
    // ustawienie widoczności legend według widoczności odpowiedniej warstwy
    if (map.getLayoutProperty(toggleableLayerIds[0], 'visibility') === 'visible'){
    document.getElementById("legend2002").style.visibility = "visible"
    } 
    else {document.getElementById("legend2002").style.visibility = "hidden"};

     if (map.getLayoutProperty(toggleableLayerIds[1], 'visibility') === 'visible'){
    document.getElementById("legend2019").style.visibility = "visible"
    } 
    else {document.getElementById("legend2019").style.visibility = "hidden"};

     if (map.getLayoutProperty(toggleableLayerIds[2], 'visibility') === 'visible'){
    document.getElementById("legendd").style.visibility = "visible"
    } 
    else {document.getElementById("legendd").style.visibility = "hidden"};


    };


     var layers = document.getElementById('menu');
    layers.appendChild(link);

};

// uniemożliwienie obracania mapy

// disable map rotation using right click + drag
map.dragRotate.disable();
 
// disable map rotation using touch rotation gesture
map.touchZoomRotate.disableRotation();


</script>

</body>
</html>
