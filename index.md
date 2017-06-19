## Peer graded assignment: R Markdown and Leaflet

In 2016 I backpacked along the Trans-Siberian railway with two friends. This map shows the main stops I did along the way!
library(leaflet)

my_map <- leaflet() 

#Create Data Frame with markers

Places <- c('Lisbon', 
            'Saint Petersburg', 'Moscow', 'Krasnoyarsk', 'Irkutsk', 
            'Ulaanbaatar', 
            'Beijing', 'Xi\'an', 'Chengdu')

lat <- c(38.777818,
         59.940255, 55.729272,56.013978,52.283808,
         47.918922,
         39.908863,34.218746,30.699796)

lng <- c(-9.135511,
         30.314659,37.601295,92.894328,104.259728,
         106.917742,
         116.397491,108.964087,104.070858)

mapData <- data.frame(Places,lat,lng)
#Load special markers
myIcons <- icons(
        iconUrl = ifelse(mapData$Places == "Lisbon",
        "https://cdn2.iconfinder.com/data/icons/jetflat-vehicles/90/001_037_plane_takeoff_travel_start-512.png",
        "http://icons.iconarchive.com/icons/paomedia/small-n-flat/1024/map-marker-icon.png"
        ),
        iconWidth = 33*215/230, iconHeight = 33, iconAnchorX = 15, iconAnchorY = 30
)

#Generate map with Carto DB Tiles, markers and lines
my_map <- my_map %>% addProviderTiles(providers$CartoDB.Positron) %>% 
        addMarkers(icon=myIcons, lat = mapData$lat, lng = mapData$lng, label = mapData$Places,
        labelOptions = labelOptions(textsize = "14px")) %>%
        addPolylines(mapData, lng=mapData$lng,lat=mapData$lat,smoothFactor=3,color="#000")





###### Page creation date: 18 June 2017. 
