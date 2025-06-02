---
title: "Hands-on R Workshop"
author: "Victor Peña Guillen, PhD"
date: "June 2, 2025"
output:
  html_document: default
---

Class overview: <https://victor-pena.github.io/victor/updates/2025/05/30/metrics-r.html>

## 1. Load and visualize raster/landscape data

### File address

```{r}
getwd()
```

## Upload Terra and sf packages

```{r}
library(terra)
```

```{r}
library(sf)
```

### Import shapefile parks

```{r}
parks <- st_read("/Users/victorpena/Documents/work/unalm/courses/ap/semesters/2021/workshop/taller_unalm/distritos 2/AREAS VERDES PUBLICAS.shp")
```


```{r}
parks
```

```{r}
plot(parks)
```

## Rasterize


```{r}
library(raster)
#library(maptools)
```


```{r}
blank_raster <- raster(nrow = 500, ncol = 500, extent(parks))
values(blank_raster) <- 1
plot(blank_raster)
```


```{r}
parks_raster <- rasterize(parks, blank_raster)
parks_raster[!(is.na(parks_raster))] <- 1
plot(parks_raster, legend=FALSE)
```


```{r}
terra::writeRaster(parks_raster, "parks_raster.tif", filetype = "GTiff", overwrite = TRUE)
```


### Import shapefile Mosaic La Molina

```{r}
lm <- st_read("/Users/victorpena/Documents/work/unalm/courses/ap/semesters/2021/workshop/taller_unalm/distritos 2/lamolina.shp")
```

```{r}
blank_raster <- raster(nrow = 500, ncol = 500, extent(lm))
values(blank_raster) <- 1
plot(blank_raster)
```



```{r}
lm_raster <- rasterize(lm, blank_raster)
lm_raster[!(is.na(lm_raster))] <- 1
plot(lm_raster, legend=FALSE)
```


```{r}
terra::writeRaster(lm_raster, "lm_raster.tif", filetype = "GTiff", overwrite = TRUE)
```



### funcion shp2raster

```{r}
shp2raster <- function(shp, mask.raster, label, value, transform = FALSE, proj.from = NA,
    proj.to = NA, map = TRUE) {
    require(raster, rgdal)

    # use transform==TRUE if the polygon is not in the same coordinate system as
    # the output raster, setting proj.from & proj.to to the appropriate
    # projections
    if (transform == TRUE) {
        proj4string(shp) <- proj.from
        shp <- spTransform(shp, proj.to)
    }

    # convert the shapefile to a raster based on a standardised background
    # raster
    r <- rasterize(shp, mask.raster)
    # set the cells associated with the shapfile to the specified value
    r[!is.na(r)] <- value
    # merge the new raster with the mask raster and export to the working
    # directory as a tif file
    r <- mask(merge(r, mask.raster), mask.raster, filename = label, format = "GTiff",
        overwrite = T)

    # plot map of new raster
    if (map == TRUE) {
        plot(r, main = label, axes = F, box = F)
    }

    names(r) <- label
    return(r)
}
```


```{r}
LH.mask <- raster("/Users/victorpena/Documents/work/unalm/courses/ap/semesters/2024_1/taller/lm_raster.tif")
# set the background cells in the raster to 0
LH.mask[!is.na(LH.mask)] <- 1

parks <- readShapePoly("/Users/victorpena/Documents/work/unalm/courses/ap/semesters/2021/workshop/taller_unalm/distritos 2/AREAS VERDES PUBLICAS.shp")

# convert the NPWS.reserves polygon data for Parks
# Parks to a raster
NPWS.raster <- shp2raster(shp = parks,
    mask.raster = LH.mask, label = "Parks La Molina", value = 3)

```

```{r}
terra::writeRaster(lm_raster, "lm_raster2.tif", filetype = "GTiff", overwrite = TRUE)
```

## 2. Calculate landscape metrics

```{r}
library(landscapemetrics) # landscape metrics calculation

```

Source: <https://r-spatialecology.github.io/landscapemetrics/>

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
check_landscape(NPWS.raster)
```


```{r}
show_patches(NPWS.raster)
```


### Practice


#### Class area (mean)

```{r}
lsm_c_area_mn(NPWS.raster)
```

#### Euclidean nearest neighbor (mean)

```{r}
lsm_c_enn_mn(NPWS.raster)
```

#### Shape (mean)

```{r}
lsm_c_shape_mn(NPWS.raster)
```

#### Cohesion (mean)

```{r}
cohesion <- lsm_c_cohesion(NPWS.raster)
cohesion
```

```{r}
write.csv(cohesion,"/Users/victorpena/Documents/work/unalm/courses/ap/semesters/2024_1/taller/areas.csv", row.names = FALSE)
```
