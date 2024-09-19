---
layout: post
title: "Calculo de las metricas de ecologia del paisaje (2)"
author: "Victor Peña Guillen"
date:   2024-09-06 00:52:30 +0900
#permalink: /hello-world/
categories: updates
---

## Resumen

Los indicadores de ecologia del paisaje cuantifican las caracteristicas geometricas de los componentes del mosaico heterogeneo. Los valores resultantes proveen informacion acerca de la configuracion espacial y composicion de los fragmentos y clases. El analisis de estos datos permite inferir las funciones ecosistemicas resultantes. Estos indicadores fundamentan la evaluacion de la condicion del mosaico y sustentan las propuestas de diseño.

## Metodo

El proceso para el calculo de la metricas, emplea el programa R y paquetes que se indican dentro de la secuencia. Se requiere un archivo vectorial en formato shape representando la capa de vegetacion (o ecosistema).

## Procedimiento

### Lectura del archivo vector en R

#### Libreria de trabajo

```{r}
setwd("/Users/victorpena/Documents/work/unalm/courses/pyr/taller/2024_2/shapes")
```

#### Paquetes terra y sf

```{r}
library(terra)
```

```{r}
library(sf)
```

#### Cargar shape en R

```{r}
cv <- st_read("/Users/victorpena/Documents/work/unalm/courses/pyr/taller/2024_2/shapes/cv_chh.shp")
```

```{r}
plot(cv)
```

```{r}
lomas <- st_read("/Users/victorpena/Documents/work/unalm/courses/pyr/taller/2024_2/shapes/lomas.shp")
```

```{r}
lomas
```

```{r}
plot(lomas)
```

### Rasterizar

```{r}
library(raster)
#library(maptools)
```

```{r}
blank_raster <- raster(nrow = 1000, ncol = 1000, extent(lomas))
values(blank_raster) <- 1
plot(blank_raster)
```

```{r}
terra::writeRaster(blank_raster, "blank_raster.tif", filetype = "GTiff", overwrite = TRUE)
```

```{r, fig.width=6, fig.height=4}
lomas_raster <- rasterize(lomas, blank_raster)
lomas_raster[!(is.na(lomas_raster))] <- 1
plot(lomas_raster, legend=FALSE)
```

### Calculo de las metricas de ecologia del paisaje

```{r}
library(landscapemetrics) # landscape metrics calculation
library(landscapetools)
```

Fuente: landscapemetrics[^1]
**[enlace](https://r-spatialecology.github.io/landscapemetrics/index.html "spatialecology's Homepage")**

```{r}
list_lsm(
level = NULL,
metric = NULL,
name = NULL,
type = NULL,
what = NULL,
simplify = FALSE,
verbose = TRUE
)
```

```{r}
check_landscape(parques_raster)
```

#### Mosaico de la cuenca

```{r}
cuenca <- st_read("/Users/victorpena/Documents/work/unalm/courses/pyr/taller/2024_2/shapes/cuenca_chancay_huaral.shp")
```

```{r}
blank_raster <- raster(nrow = 1000, ncol = 1000, extent(cuenca))
values(blank_raster) <- 1
plot(blank_raster)
```

```{r}
cuenca_raster <- rasterize(cuenca, blank_raster)
cuenca_raster[!(is.na(cuenca_raster))] <- 1
plot(cuenca_raster, legend=FALSE)
```

```{r}
terra::writeRaster(cuenca_raster, "cuenca_raster.tif", filetype = "GTiff", overwrite = TRUE)
```

#### Funcion shp2raster[^2]

```{r}
shp2raster <- function(shp, mask.raster, label, value, transform = FALSE, proj.from = NA, proj.to = NA, map = TRUE) {require(raster, rgdal)
    # use transform==TRUE if the polygon is not in the same coordinate system as the output raster, setting proj.from & proj.to to the appropriate projections
    if (transform == TRUE) {proj4string(shp) <- proj.from
    shp <- spTransform(shp, proj.to)
    }
    # convert the shapefile to a raster based on a standardised background
    # raster
    r <- rasterize(shp, mask.raster)
    # set the cells associated with the shapfile to the specified value
    r[!is.na(r)] <- value
    # merge the new raster with the mask raster and export to the working
    # directory as a tif file
    r <- mask(merge(r, mask.raster), mask.raster, filename = label, format = "GTiff", overwrite = T)
    # plot map of new raster
    if (map == TRUE) {plot(r, main = label, axes = F, box = F)}
    names(r) <- label
    return(r)
}
```

```{r}

LH.mask <- raster("/Users/victorpena/Documents/work/unalm/courses/pyr/taller/2024_2/shapes/cuenca_raster.tif")
# set the background cells in the raster to 0
LH.mask[!is.na(LH.mask)] <- 1
lomas <- st_read("/Users/victorpena/Documents/work/unalm/courses/pyr/taller/2024_2/shapes/lomas.shp")
# convert the NPWS.reserves polygon data for Parks
# Parks to a raster
NPWS.raster <- shp2raster(shp = lomas, mask.raster = LH.mask, label = "Lomas Chancay-Huaral", value = 3)

```

```{r}
lsm_p_area(NPWS.raster)
```

```{r}
p1 <- lsm_c_te(NPWS.raster)
p1
```

```{r}
lsm_c_ca(NPWS.raster)
```

```{r}
lsm_c_pd(NPWS.raster)
```

```{r}
lsm_c_shape_mn(NPWS.raster)
```

#### Referencias

[^1]: landscapemetrics 2.1.4 4 octubre 2023
**[enlace](https://r-spatialecology.github.io/landscapemetrics/index.html "spatialecology's Homepage")**

[^2]: Amy Whitehead 1 May 2014
<https://www.r-bloggers.com/2014/05/converting-shapefiles-to-rasters-in-r/>
