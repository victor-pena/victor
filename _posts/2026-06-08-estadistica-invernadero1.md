---
title: "Análisis de datos del invernadero"
author: "Victor Peña Guillen, PhD"
date: "June 8, 2026"
output:
  html_document: default
---

## Ejercicio 1: ¿La temperatura del aire difiere significativamente entre los periodos del día?

Se plantea usar 144 mediciones registradas cada 10 minutos, clasificadas en cuatro periodos: madrugada, mañana, tarde y noche; la variable respuesta es la temperatura del aire, y el factor de comparación es el periodo del día

### Librerias a emplear

```{r}
library(readxl)
library(dplyr)
library(ggplot2)
```

## A. Hipótesis

La prueba ANOVA parte de dos hipótesis:

### Hipótesis nula, H0:

*Las medias de temperatura son iguales en todos los periodos del día*

Temperatura madrugada = Temperatura mañana = Temperatura tarde = Temperatura noche

### Hipótesis alternativa, H1:

*Al menos una media de temperatura es diferente*

Esto no significa que todas sean diferentes, sino que por lo menos un periodo del día tiene una temperatura promedio distinta.

### 1. Cargar datos

```{r}
data <- read_excel("/Users/victorpena/Documents/work/unalm/research/invernadero/circulo/capacitacion/greenhouse_sensor_dataset_144.xlsx", sheet = "Data")
```

### 2. Convertir Timestamp a fecha-hora

```{r}
data$Timestamp <- as.POSIXct(data$Timestamp)
```

### 3. Crear variable Hora

```{r}
data$Hora <- as.numeric(format(data$Timestamp, "%H"))
```

### 4. Clasificar por periodo del día

```{r}
data <- data %>%
  mutate(
    Periodo = case_when(
      Hora >= 0  & Hora <= 5  ~ "Madrugada",
      Hora >= 6  & Hora <= 11 ~ "Mañana",
      Hora >= 12 & Hora <= 17 ~ "Tarde",
      Hora >= 18 & Hora <= 23 ~ "Noche"
    )
  )
```

### 5. Convertir Periodo a factor

```{r}
data$Periodo <- factor(data$Periodo,
                       levels = c("Madrugada", "Mañana", "Tarde", "Noche"))
```

### 6. Estadística descriptiva

```{r}
data %>%
  group_by(Periodo) %>%
  summarise(
    n = n(),
    media_temp = mean(Air_Temperature_C, na.rm = TRUE),
    sd_temp = sd(Air_Temperature_C, na.rm = TRUE),
    min_temp = min(Air_Temperature_C, na.rm = TRUE),
    max_temp = max(Air_Temperature_C, na.rm = TRUE)
  )
```

## B. ¿Por qué usar ANOVA?
Porque tenemos más de dos grupos:
- Madrugada
- Mañana
- Tarde
- Noche
Si solo comparáramos dos grupos, podríamos usar una prueba t. Pero como son cuatro grupos, usar muchas pruebas t aumentaría el riesgo de error. Por eso usamos ANOVA de un factor.

El factor es:
*Periodo del día*

La variable respuesta es:
Temperatura del aire (°C)

## C. ¿Qué evalúa ANOVA?

ANOVA compara dos tipos de variación:
Variación entre grupos:

Cuánto cambian las temperaturas promedio entre madrugada, mañana, tarde y noche.

Variación dentro de los grupos:
Cuánto varía la temperatura dentro de cada periodo.

La lógica es:
Si la variación entre periodos es mucho mayor que la variación interna,
entonces el periodo del día sí influye sobre la temperatura.


### 7. ANOVA de un factor

```{r}
anova_temp <- aov(Air_Temperature_C ~ Periodo, data = data)
summary(anova_temp)
```

## D. Interpretacion del resultado del ANOVA
El resultado principal aparece como:

summary(anova_temp)

Observar el valor:
$Pr(>F)$
Ese es el valor-p.

La regla es:

Si p < 0.05 → se rechaza H0

Si p ≥ 0.05 → no se rechaza H0

Entonces:
*Existen diferencias estadísticamente significativas en la temperatura promedio del aire entre los periodos del día.*


### 8. Prueba de Tukey

La prueba de Tukey compara todos los pares de periodos:

```{r}
TukeyHSD(anova_temp)
```
*observar el valor $p-adj$*

La regla es:

*Si p adj < 0.05 → ese par de periodos sí difiere significativamente*

Tarde - Madrugada: p adj < 0.05

Tarde - Mañana: p adj > 0.05

Noche - Tarde: p adj < 0.05

La tarde presenta temperaturas significativamente diferentes respecto a la noche y la madrugada, probablemente por el incremento de radiación solar y acumulación térmica dentro del invernadero. Pero no difiere de la Mañana, porque la temperatura aumenta casi inmediatamente.


```{r}
# 9. Gráfico boxplot
ggplot(data, aes(x = Periodo, y = Air_Temperature_C)) +
  geom_boxplot() +
  labs(
    title = "Temperatura del aire por periodo del día",
    x = "Periodo del día",
    y = "Temperatura del aire (°C)"
  ) +
  theme_minimal()
```

## E. Informe

Se aplicó un ANOVA de un factor para evaluar si la temperatura del aire difiere entre cuatro periodos del día: madrugada, mañana, tarde y noche. La hipótesis nula estableció que las medias de temperatura son iguales entre periodos.
Si el valor-p del ANOVA fue menor a 0.05, se rechazó la hipótesis nula, indicando diferencias significativas. Posteriormente, se aplicó la prueba de Tukey para identificar entre qué periodos se presentan dichas diferencias.


## F. Informacion agronomica

Este análisis permite entender el comportamiento térmico del invernadero:

- La madrugada puede mostrar enfriamiento.

- La mañana puede mostrar incremento progresivo.

- La tarde puede mostrar máxima acumulación térmica.

- La noche puede mostrar descenso.

La temperatura afecta:

- crecimiento del cultivo

- estrés térmico

- evapotranspiración

- eficiencia del riego

- calidad del fruto
