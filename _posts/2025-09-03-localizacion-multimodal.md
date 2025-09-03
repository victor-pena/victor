---
title: "Guía de Análisis Espacial para la Localización de un Nodo Logístico Multimodal"
author: "Victor Peña Guillen, PhD"
date: "September 3, 2025"
output:
  html_document: default
---

**Objetivo:** Identificar las zonas óptimas para establecer un nodo logístico multimodal en una zona costera, integrando criterios de accesibilidad, valor del suelo, riesgo e interferencia urbana.

---

### ** Criterios Técnicos Aplicados**

| Capa                                   | Criterio aplicado                               | Función                                                        |
| -------------------------------------- | ----------------------------------------------- | -------------------------------------------------------------- |
| **Carreteras (lineal)**                | Crear un buffer (100–500 m)                     | Representa la **unidad económica de accesibilidad**            |
| **Uso/agrología del suelo (polígono)** | Seleccionar zonas de **menor valor agrológico** | Representa la **unidad ecológica de menor conflicto agrícola** |
| **Área urbana (polígono)**             | Excluir o alejar zonas urbanizadas              | Minimiza conflictos con zonas consolidadas                     |

---

# 🛰️ Secuencia para la localización de un Nodo Logístico Multimodal

**Software:** QGIS (v. 3.x)

---

## 🧩 1. Datos requeridos (en formato shapefile)

| Capa                   | Tipo     | Descripción                             |
| ---------------------- | -------- | --------------------------------------- |
| `carreteras.shp`       | Línea    | Red vial existente o planificada        |
| `valor_agrologico.shp` | Polígono | Clasificación de uso o aptitud de suelo |
| `area_urbana.shp`      | Polígono | Límite de urbanización consolidada      |
| `inundacion.shp`       | Polígono | Áreas inundables   |

---

## 🔧 2. Pre-procesamiento de capas

### A. Revisar proyecciones

* Asegúrate de que todas las capas estén en la **misma proyección (CRS)**. Usa el sistema WGS84 en la zona correspondiente (por ejemplo: EPSG:4326 para Perú central).
* Si es necesario:
  `Clic derecho sobre capa` → `Exportar` → `Guardar como…` → seleccionar CRS unificado.

### B. Filtrar suelo de bajo valor agrológico

* Ir a: `Capa` → `Filtrar…`
* Ejemplo: `"clase" IN ('D', 'E')` → selecciona suelos con baja aptitud agrícola.
* Exportar resultado como: `suelo_bajo_valor.shp`

---

## 🛣️ 3. Crear unidad económica: buffer de accesibilidad vial

1. Ir a: `Vector` → `Herramientas de geoprocesamiento` → `Buffer`
2. Seleccionar `carreteras.shp`
3. Distancia sugerida: `500 metros`
4. Resultado: `buffer_acceso.shp`

---

## 🌍 4. Crear unidad ecológico-económica (intersección)

1. Ir a: `Vector` → `Geoprocesamiento` → `Intersección`
2. **Capa A**: `buffer_acceso.shp`
   **Capa B**: `suelo_bajo_valor.shp`
3. Salida: `unidad_eco_econ.shp`

---

## 🏘️ 5. Excluir zonas urbanas

1. Ir a: `Vector` → `Geoprocesamiento` → `Diferencia`
2. **Capa de entrada**: `unidad_eco_econ.shp`
   **Capa de resta**: `area_urbana.shp`
3. Resultado: `zona_sin_urbano.shp`

---

## 🌊 6. Excluir zonas de inundación

1. Repetir el paso de diferencia:

   * Entrada: `zona_sin_urbano.shp`
   * Resta: `inundacion.shp`
2. Resultado final: `area_sugerida_nodo.shp`

---

## 📐 7. Verificar y calcular atributos espaciales

* Abre la tabla de atributos de `area_sugerida_nodo.shp`
* Abre el **Calculador de campos**:

  * Nuevo campo: `area_ha`
  * Tipo: Decimal
  * Expresión: `area($geometry)/10000` → para obtener hectáreas
* Puedes añadir también:

  * `centroid($geometry)` para coordenadas
  * `perimeter($geometry)` si deseas perímetros

---

## 📤 8. Exportar resultados y elaborar mapa final

* Exporta la capa final como shapefile o geopackage.
* Usa el **Diseñador de impresión** (`Proyecto` → `Nuevo diseño de impresión`) para generar tu mapa final:

  * Incluir norte, escala, leyenda y títulos.
  * Añadir áreas urbanas y red vial como contexto.

---

## 📌 Sugerencias adicionales

* Verifica que las áreas candidatas cumplan con un **mínimo de superficie** (e.g., >5 ha).
* Si hay múltiples polígonos: usa `Multipart to Singleparts` para separarlos.
* Ordena o clasifica candidatos por tamaño o cercanía a puertos u otras infraestructuras.

---

### ✅ **Resultado Final:**

Una capa de polígonos que representa zonas:

* Con **acceso vial cercano**
* En **suelo poco productivo agrícola**
* **Fuera de zonas urbanas consolidadas**

---

### 📌 Observaciones y recomendaciones:

* Si quieres afinar aún más el análisis, podrías:

  * Agregar análisis de **riesgo por inundación** como capa de exclusión adicional.
  * Calcular **área mínima funcional** para el nodo (por ejemplo, >5 ha).
  * Evaluar **distancia a puertos o zonas industriales existentes**.
  * Agregar un **análisis de pendientes** si el terreno tiene topografía variable.

---
