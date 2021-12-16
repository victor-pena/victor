---
layout: post
title: "Calculo de las metricas de ecologia del paisaje"
#date:   2021-12-15 16:52:30 +0900
#permalink: /hello-world/
categories: updates
---

# Resumen
Los indicadores de ecologia del paisaje cuantifican las caracteristicas geometricas de los componentes del mosaico heterogeneo. Los valores resultantes proveen informacion acerca de la configuracion espacial y composicion de los fragmentos y clases. El analisis de estos datos permite inferir las funciones ecosistemicas resultantes. Estos indicadores fundamentan la evaluacion de la condicion del mosaico y sustentan las propuestas de diseño.

# Metodo

A continuacion se presenta el proceso para el calculo de algunas metricas, empleando el programa R y paquetes que se indican dentro de la secuencia. Se requiere un archivo vectorial en formato shape representando la capa de vegetacion (o ecosistema).

# Procedimiento

# 1. Cargar el shape

## 1.1 Folder de trabajo

Identificar la direccion

```{r}
getwd()

```

## 1.2 Cargar el paquete rgdal

```{r}
library(rgdal)
```

## 1.3 Leer el shape

```{r}
bosques <- readOGR(dsn="/Users/victorpena/Documents/work/unalm/courses/pyr/taller/maps/Bm-oca_tres.shp")
```
## 1.4 Mostrar shape

(Datos)
```{r}
bosques
```
