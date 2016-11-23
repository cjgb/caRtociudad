# caRtociudad

R package to query [Cartociudad](http://www.cartociudad.es) API. The API is documented [here](http://www.cartociudad.es/recursos/Documentacion_tecnica/CARTOCIUDAD_ServiciosWeb.pdf).

## Installation

```
library(devtools)
install_github("cjgb/caRtociudad")
```

## Geocoding

```
# using full address
my.address <- cartociudad_geocode("plaza de cascorro 11, 28005 madrid")
print(my.address)

# using address chunks
my.address <- cartociudad_geocode(road_type = "plaza", road_name = "cascorro",
    zip = "28012", municipality = "madrid", province = "madrid")
print(my.address)
```

## Reverse geocoding

Function `cartociudad_reverse_geocode` returns the address details of a location.

```
cartociudad_reverse_geocode(40.45332, -3.69442)
```

## Mapping

Function `get_cartociudadmap` downloads static maps from Cartociudad servers and tries to imitate the behaviour of `ggmap::get_googlemap`.

```
soria <- cartociudad_geocode("soria")
mapa_soria <- get_cartociudadmap(c(soria$latitude, soria$longitude), 1)
ggmap(mapa_soria)
```

Cartociudad maps can include different kinds of layers. The full list of available layers can be consulted in the API reference manual (see above). 

## Area

Function `get_cartociudad_area` calculates the area given a point and a radius in meters. E.g.,

```
vallecas.lat <- 40.3930144
vallecas.lon <- -3.6596683
map <- get_cartociudadmap(c(vallecas.lat, vallecas.lon), 1)
polygon <- get_cartociudad_area(vallecas.lat, vallecas.lon, 500)
ggmap(map) + geom_polygon(data = polygon, aes(x = longitude, y = latitude), colour = "red", fill = NA)
```

draws a polygon around the given center in a map.

## Location info

Function `get_cartociudad_location_info` provides administrative information on a point indicated by its coordinates. E.g.,

```
get_cartociudad_location_info(40.473219,-3.7227241)
```
indicates the reverse geocoding details, censal section, censal district, cadastral information and the url to the spanish cadastre website associated to the point.


## TODO

Add extra API functionalities to the package.

## Help wanted!

If you want to help extend the package, do write to the maintainer and submit your code. It will be reviewed you will be added to the list of authors.
