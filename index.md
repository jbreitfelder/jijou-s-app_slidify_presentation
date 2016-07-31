---
title       : Jijou's app
subtitle    : Find interesting places around you!
author      : Joanne Breitfelder
job         : Data Scientist
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, quiz, bootstrap]           
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

--- 
## Presentation of the application 

Jijou's app allows you to find interesting places around you. Looking for a good pizzeria, an aquarium, or the closest dentist? This app is for you! :) 

<img src="appli.pdf" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" width="1000" />

- *En tant qu'utilisateurs on est conquis!*
**Mélanie, France**
- *On aime beaucoup le design, le retour à la simplicité!*
**Damien, France**
- *Súper chévere y facil de usar! Aunque no encontré la pizzeria al lado de mi casa..* 
**Juan, Brazil**  

--- 
## General information 

- **The application:** <https://jijou.shinyapps.io/Jijou-s-app/>
- **My Github repository:** <https://github.com/jbreitfelder/Jijou-s-app>
- This application is based on [RStudio's Shiny](http://shiny.rstudio.com) and [Google Maps API](https://developers.google.com/maps/).

<img src="logos.pdf" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" width="600" />

### How to use the app?

- Enter the kind of place you are looking for.
- Enter your location
- Choose the radius in which you want to look for 
- Adjust the map zoom: from 3 (continent) to 21 (building).
- Actualize and enjoy! :)  

---
## Geocoding with Google Maps

The application is based on 2 functions using Google Maps API. The first one, `geoCode()`, allows to find the GPS coordinates of a given place. I found this function [here](https://gist.github.com/josecarlosgonz/6417633).

### Utilisation example:




```r
geoCode("Paris, France")
```

```
## [1] "48.856614"     "2.3522219"     "APPROXIMATE"   "Paris, France"
```

### Explanation of the result:

The first two items are the **latitude** and **longitude** coordinates, the third item is the **location type** ("ROOFTOP", "RANGE_INTERPOLATED", "GEOMETRIC_CENTER" or "APPROXIMATE") and the last one is the **formatted address**.

---
## Finding places of interest with Google Maps API

The second function, `close_places()` returns the 20 closest places of interest around a given position. 

### Utilisation example :




```r
results <- close_places("Johns Hopkins University", 1000, "school")
kable(head(results, 3))
```



|icon                                                                                                   |   rating|address                           |open_now       |name                           | idx|      lat|      long|
|:------------------------------------------------------------------------------------------------------|--------:|:---------------------------------|:--------------|:------------------------------|---:|--------:|---------:|
|<img src='https://maps.gstatic.com/mapfiles/place_api/icons/generic_business-71.png' width='50'></img> | 4.128571|701 East 34th Street, Baltimore   |No information |Baltimore City School District |   1| 39.32977| -76.60625|
|<img src='https://maps.gstatic.com/mapfiles/place_api/icons/school-71.png' width='50'></img>           | 4.500000|1300 Gorsuch Avenue #2, Baltimore |No information |The Stadium School             |   2| 39.32493| -76.59945|
|<img src='https://maps.gstatic.com/mapfiles/place_api/icons/school-71.png' width='50'></img>           | 4.100000|3400 Ellerslie Avenue, Baltimore  |No information |Waverly Elementary School      |   3| 39.33004| -76.60363|
