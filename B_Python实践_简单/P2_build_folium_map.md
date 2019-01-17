## Prepare
```
pip3 install folium
pip3 install pandas
```

## Step1 - Create a Base Map
``` python
#Import Library
import folium

#Create base map
map = folium.Map(location=[37.296933,-121.9574983], zoom_start = 8)

#Save the map
map.save("map1.html")
```
After you execute this code, you should have a map1.html generated under current work directory. Drag that .html file into your browser and you should get something like:
<img src="https://i.ibb.co/J2pFLnR/Step1.png" width="100%">

## Step 2 — Add Marker
``` python
#Import Library
import folium

#Create base map
map = folium.Map(location=[37.296933,-121.9574983], zoom_start = 8, tiles = "Mapbox bright")

#Add Marker
folium.Marker(location=[37.4074687,-122.086669], popup = "Google HQ", icon=folium.Icon(color = 'gray')).add_to(map)

#Save the map
map.save("map1.html")
```
<img src="https://i.ibb.co/chHm1wM/Step2.png" width="100%">

## Step 3 — Add Multiple Markers
``` python
#Import Library
import folium

#Create base map
map = folium.Map(location=[37.296933,-121.9574983], zoom_start = 8, tiles = "Mapbox bright")

#Multiple Markers
for coordinates in [[37.4074687,-122.086669],[37.8199286,-122.4804438]]:
    folium.Marker(location=coordinates, icon=folium.Icon(color = 'green')).add_to(map)


#Save the map
map.save("map1.html")
```
<img src="https://i.ibb.co/VNFvpq6/Step3.png" width="100%">
## Step 4 — Adding Markers from Data
``` python
#Import Library
import folium
import pandas as pd

#Load Data
data = pd.read_csv("Volcanoes_USA.txt")
lat = data['LAT']
lon = data['LON']
elevation = data['ELEV']

#Create base map
map = folium.Map(location=[37.296933,-121.9574983], zoom_start = 5, tiles = "Mapbox bright")

#Plot Markers
for lat, lon, elevation in zip(lat, lon, elevation):
    folium.Marker(location=[lat, lon], popup=str(elevation)+" m", icon=folium.Icon(color = 'gray')).add_to(map)

#Save the map
map.save("map1.html")
```
<img src="https://i.ibb.co/FzNcfvT/Step4.png" width="100%">
## Step 5 — Add Colors to Markers
``` python
#Import Library
import folium
import pandas as pd

#Load Data
data = pd.read_csv("Volcanoes_USA.txt")
lat = data['LAT']
lon = data['LON']
elevation = data['ELEV']

#Function to change colors
def color_change(elev):
    if(elev < 1000):
        return('green')
    elif(1000 <= elev <3000):
        return('orange')
    else:
        return('red')

#Create base map
map = folium.Map(location=[37.296933,-121.9574983], zoom_start = 5, tiles = "Mapbox bright")

#Plot Markers
for lat, lon, elevation in zip(lat, lon, elevation):
    folium.Marker(location=[lat, lon], popup=str(elevation), icon=folium.Icon(color = color_change(elevation))).add_to(map)

#Save the map
map.save("map1.html")
```
<img src="https://i.ibb.co/bNMZPmk/Step5.png" width="100%">
## Step 6 — Change Icons
``` python
#Import Library
import folium
from folium.plugins import MarkerCluster
import pandas as pd

#Load Data
data = pd.read_csv("Volcanoes_USA.txt")
lat = data['LAT']
lon = data['LON']
elevation = data['ELEV']

#Function to change colors
def color_change(elev):
    if(elev < 1000):
        return('green')
    elif(1000 <= elev <3000):
        return('orange')
    else:
        return('red')

#Create base map
map = folium.Map(location=[37.296933,-121.9574983], zoom_start = 5, tiles = "Mapbox bright")

#Plot Markers
for lat, lon, elevation in zip(lat, lon, elevation):
    folium.CircleMarker(location=[lat, lon], radius = 9, popup=str(elevation)+" m", fill_color=color_change(elevation), color="gray", fill_opacity = 0.9).add_to(map)

#Save the map
map.save("map1.html")
```
<img src="https://i.ibb.co/F8DNYmq/Step6.png" width="100%">
## Step 7 — Cluster all Markers
``` python
#Import Library
import folium
from folium.plugins import MarkerCluster
import pandas as pd

#Load Data
data = pd.read_csv("Volcanoes_USA.txt")
lat = data['LAT']
lon = data['LON']
elevation = data['ELEV']

#Function to change colors
def color_change(elev):
    if(elev < 1000):
        return('green')
    elif(1000 <= elev <3000):
        return('orange')
    else:
        return('red')

#Create base map
map = folium.Map(location=[37.296933,-121.9574983], zoom_start = 5, tiles = "CartoDB dark_matter")

#Create Cluster
marker_cluster = MarkerCluster().add_to(map)

#Plot Markers and add to 'marker_cluster'
for lat, lon, elevation in zip(lat, lon, elevation):
    folium.CircleMarker(location=[lat, lon], radius = 9, popup=str(elevation)+" m", fill_color=color_change(elevation), color="gray", fill_opacity = 0.9).add_to(marker_cluster)

#Save the map
map.save("map1.html")
```
<img src="https://i.ibb.co/t2ddMv8/Step7.png" width="100%">
