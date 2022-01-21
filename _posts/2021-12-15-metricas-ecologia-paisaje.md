---
layout: post
title: "Calculo de las metricas de ecologia del paisaje"
author: "Victor Peña Guillen"
#date:   2021-12-15 16:52:30 +0900
#permalink: /hello-world/
categories: updates
---

## Resumen

Los indicadores de ecologia del paisaje cuantifican las caracteristicas geometricas de los componentes del mosaico heterogeneo. Los valores resultantes proveen informacion acerca de la configuracion espacial y composicion de los fragmentos y clases. El analisis de estos datos permite inferir las funciones ecosistemicas resultantes. Estos indicadores fundamentan la evaluacion de la condicion del mosaico y sustentan las propuestas de diseño.

## Metodo

El proceso para el calculo de la metricas, emplea el programa R y paquetes que se indican dentro de la secuencia. Se requiere un archivo vectorial en formato shape representando la capa de vegetacion (o ecosistema).

## Procedimiento

## 1. Cargar el shape

### 1.1 Folder de trabajo

Identificar la direccion

```{r}
getwd()

```

### 1.2 Cargar el paquete rgdal

```{r}
library(rgdal)
```

### 1.3 Leer el shape

```{r}
bosques <- readOGR(dsn="/Users/victorpena/Documents/work/unalm/courses/pyr/taller/maps/Bm-oca_tres.shp")
```

### 1.4 Mostrar shape

(Datos)

```{r}
bosques
```

Tabla de atributos

```{r}
tabla_atributos <- bosques@data
tabla_atributos
class(tabla_atributos)
```

Grafico

```{r}
plot(bosques)
```

## 2. Rasterizar

### 2.1 Paquetes raster y maptools

```{r}
install.packages("remotes")
remotes::install_github("rspatial/terra")

#install.packages('terra', repos =' http://cran.mirror.garr.it/mirrors/CRAN/')

#install.packages('terra', repos='https://rspatial.r-universe.dev')

#install.packages("raster", repos = 'https://mac.R-project.org')

#install.packages("rtools")

#remotes::install_github("rspatial/terra")

install.packages("terra")
```

```{r}
library(terra)
library(raster)
library(maptools)
```

### 2.2 Creacion de la malla en blanco

```{r}
blank_raster <- raster(nrow = 1000, ncol = 1000, extent(bosques))
values(blank_raster) <- 1
plot(blank_raster)
```

### 2.3 Conversion al formato raster

```{r}
bosques_raster <- rasterize(bosques, blank_raster)
bosques_raster[!(is.na(bosques_raster))] <- 1
plot(bosques_raster, legend=FALSE)
```

### 2.4 Guardar con un nombre

```{r}
writeRaster(bosques_raster, "bosques_raster1000.tif", overwrite=TRUE)
```

## 3. Calculo de indicadores

### 3.1 Paquetes landscapemetrics, sf y dplyr

Referencia paquete "landscapemetrics": <https://r-spatialecology.github.io/landscapemetrics/index.html>

```{r}
library(landscapemetrics)     # landscape metrics calculation
library(landscapetools)
#library(raster)               # spatial raster data reading and handling
library(sf)                   # spatial vector data reading and handling
library(dplyr)                # data manipulation
library(rgeos)
```

#### Lista de las metricas

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

#### Verificacion del archivo raster

```{r}
check_landscape(bosques_raster)
show_patches(bosques_raster) 
```

### 3.2 Crear grid de referencia

```{r}
my_grid_geom = st_make_grid(st_as_sfc(st_bbox(bosques_raster)), cellsize = 25000)
my_grid = st_sf(geom = my_grid_geom)
```

### 3.3 Superponer capas raster

```{r}
plot(bosques_raster)
plot(my_grid, add = TRUE)
```

#### Referencia para la descripcion de los indices (FRAGSTATS Metrics)

<http://www.umass.edu/landeco/research/fragstats/documents/Metrics/Metrics%20TOC.htm>
Fuente: Landscape Ecology Lab at UMass Amherst (McGarigal). El Dr. McGarigal no trabaja actualmente en UMass Amherst.

### 3.4 Indices - escala de fragmento

#### 3.4.1 Areas (ha), en la escala de fragmento

```{r}
a1 = sample_lsm(bosques_raster, my_grid, level = "patch", metric = "area")
a1
```

#### 3.4.2 Perimetros (m), en la escala de fragmento

```{r}
perimetro <- lsm_p_perim(bosques_raster)
perimetro
```

### 3.5 Indices, en la escala de clase

#### 3.5.1 area

```{r}
ca = sample_lsm(bosques_raster, my_grid, level = "class", metric = "ca")
ca
```

#### 3.5.2 perimetro total a

```{r}
te = sample_lsm(bosques_raster, my_grid, level = "class", metric = "te")
te
```

#### 3.5.3 Perimetro total b

```{r}
lsm_c_te(bosques_raster)
```

#### 3.5.4 Vecino cercano

```{r}
 lsm_c_enn_mn(bosques_raster)
```

```{r}
lsm_l_enn_cv(bosques_raster)
```

#### 3.5.5 densidad de fragmentos

```{r}
pd = sample_lsm(bosques_raster, my_grid, level = "class", metric = "pd")
pd
```

#### 3.5.6 indice de forma

```{r}
lsi = sample_lsm(bosques_raster, my_grid, level = "class", metric = "lsi")
lsi
```

#### 3.5.7 cohesion

```{r}
lsm_c_cohesion(bosques_raster)
```

### 3.6 Indices, en la escala de paisaje

#### 3.6.1 Area Total

```{r}
lsm_l_ta(bosques_raster)
```

#### 3.6.2 Numero de fragmentos

```{r}
lsm_l_np(bosques_raster)
```

#### 3.6.3 Densidad de fragmentos

```{r}
lsm_l_pd(bosques_raster)
```

## 4. Edicion de los datos

```{r}
write.csv(a1,"/Users/victorpena/Documents/work/unalm/courses/pyr/taller/notebooks/area_esc_frag.csv", row.names = FALSE)
```

```{r}
library(openxlsx)
write.xlsx(a1,"/Users/victorpena/Documents/work/unalm/courses/pyr/taller/notebooks/area_esc_frag_hc.xlsx", overwrite=TRUE)
```

### 4.1 Distribucion

#### 4.1.1 Cantidad

```{r}
# library
library(ggplot2)
 
# dataset:
data=data.frame(a1)

# basic histogram
p <- ggplot(data, aes(x=value)) + 
  geom_histogram()

p
```

#### 4.1.2 Tamaño

```{r}
# A really basic boxplot.
ggplot(data, aes(x=as.factor(layer), y=value)) + 
    geom_boxplot(fill="slateblue", alpha=0.2) + 
    xlab("area bosque")
```

#### Histogramas y curva de densidad


```{r}
df <- data[order(data$value,decreasing = TRUE),]
 barplot(df$value,names.arg = df$id, col="orange", 
          xlab="id fragmentos", 
          ylab="superficie (ha)")
```

```{r}
df <- data[order(data$value,decreasing = TRUE),]
 barplot(df$value,names.arg = df$id, col="orange", 
          xlab="id fragmentos", 
          ylab="superficie (ha)")
```

```{r}
x.gen <- data$value
hist(x.gen, prob = TRUE) 

library(MASS)
x.est <- fitdistr(x.gen, "exponential")$estimate

curve(dexp(x, rate = x.est), add = TRUE, col = "red", lwd = 2)
```

#### Normalidad

```{r}
### normality qq plot

x <- qnorm(seq(0,1,l=34))  # Theoretical normal quantiles
x <- x[-c(1, length(x))]  # Drop ends because they are -Inf and Inf
y <- data$value  # Actual data. 1000 points drawn from a normal distribution
l.1 <- lm(sort(y)~sort(x))
qqplot(x, y, xlab="Theoretical Quantiles", ylab="Actual Quantiles")
abline(coef(l.1)[1], coef(l.1)[2])
```
