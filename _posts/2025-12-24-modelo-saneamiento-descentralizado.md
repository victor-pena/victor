---
title: "Modelo descentralizado de saneamiento"
author: "Victor Peña Guillen, PhD"
date: "December 24, 2025"
output:
  html_document: default
---

> El modelo de saneamiento corresponde a un modelo agregado basado en balances de masa y eficiencias de remoción, calibrado mediante datos de laboratorio y orientado al análisis de escenarios en sistemas descentralizados. Su objetivo es apoyar la planificación, el diseño y la integración con soluciones basadas en la naturaleza dentro de un marco de gemelo digital.

---

## 1. Base teórica

### 1.1 Modelo descentralizado basado en procesos con parámetros agregados

El modelo de saneamiento propuesto corresponde a un modelo basado en procesos con parámetros agregados (lumped-parameter model), adecuado para sistemas de tratamiento de aguas residuales descentralizados.

Sus características principales son:

* Cada unidad de tratamiento se representa como un **volumen de control**.
* No se resuelve explícitamente la variabilidad espacial interna.
* El desempeño del tratamiento se representa mediante **balances de masa** y **eficiencias de remoción**.
* El tiempo se considera en régimen **cuasi-estacionario** (promedios diarios), incorporando la variabilidad a través de escenarios.

Este tipo de modelos es ampliamente aceptado para:

* Planificación y diseño preliminar,
* Análisis comparativo de alternativas,
* Apoyo a la toma de decisiones en sistemas descentralizados
  (véase Wastewater Engineering: Treatment and Resource Recovery).

---

### 1.2 Adecuación de modelos agregados a sistemas descentralizados

Los sistemas de saneamiento descentralizados se caracterizan por:

* Escalas reducidas de operación,
* Alta variabilidad en caudales y cargas,
* Fuerte dependencia del contexto territorial, climático y operativo.

En estos sistemas, la **incertidumbre asociada a las condiciones de entrada y a la operación** suele ser mayor que la incertidumbre asociada a los parámetros cinéticos finos. Por ello, el uso de **envolventes de desempeño basadas en escenarios** resulta metodológicamente más robusto que la simulación detallada de procesos microbiológicos.

Este enfoque es consistente con las recomendaciones de la Organización Mundial de la Salud en materia de saneamiento seguro y gestión de riesgos, así como con los manuales de saneamiento descentralizado promovidos por organismos internacionales.

---

## 2. Formulación matemática

### 2.1 Balance de masa (ecuación fundamental)

Para cada unidad de tratamiento *i* y cada contaminante *p*, se aplica el siguiente balance:

$$
C_{p,i}^{\text{salida}} = C_{p,i}^{\text{entrada}} \cdot \left(1 - \eta_{p,i}\right)
$$

donde:

* ( \( C_{p,i}^{\text{entrada}} \) ) es la concentración de entrada del contaminante *p*,
* ( \( C_{p,i}^{\text{salida}} \) ) es la concentración de salida,
* ( \( \eta_{p,i} \) ) es la eficiencia de remoción adimensional (0–1).

Esta ecuación constituye el **núcleo del modelo**, y se fundamenta en principios clásicos de ingeniería sanitaria (Wastewater Engineering: Treatment and Resource Recovery).

---

### 2.2 Continuidad de caudales

En primera aproximación, se asume:

\( Q^{\text{salida}} = Q^{\text{entrada}} \)

salvo que se introduzcan explícitamente pérdidas por evaporación, infiltración o almacenamiento. Para la mayoría de sistemas descentralizados a escala de barrio o parque, esta hipótesis es válida en fase de planificación.

---

### 2.3 Tratamiento secuencial

Para un tren de tratamiento compuesto por *n* unidades:

\( C_p^{\text{final}} = C_p^{\text{influyente}} \cdot \prod_{i=1}^{n} (1 - \eta_{p,i}) \)

Esta formulación:

* Representa la remoción acumulada,
* Permite evaluar el efecto incremental de cada unidad,
* Es transparente y fácilmente interpretable por equipos multidisciplinarios.

---

### 2.4 Restricciones de capacidad hidráulica

Cada unidad está sujeta a una restricción de diseño:

\( Q^{\text{entrada}} \leq Q_{\text{max},i} \)

El incumplimiento de esta condición indica:

* Riesgo de fallo hidráulico,
* Pérdida de eficiencia,
* O inviabilidad de la configuración propuesta.

Este aspecto es crítico en sistemas descentralizados, donde los picos de carga pueden ser determinantes.

---

### 2.5 Tratamiento de patógenos (enfoque categórico)

Dada la elevada incertidumbre asociada a la dinámica de patógenos y su fuerte dependencia del contexto, estos se modelan de forma **categórica** (alta, media, baja), siguiendo un enfoque de gestión de riesgos recomendado por la Organización Mundial de la Salud.

Este enfoque evita una falsa precisión y es coherente con los lineamientos de saneamiento seguro y reutilización.

---

### 2.6 Estimación del consumo energético

El consumo energético se estima en orden de magnitud:

\( E = Q \cdot e_u \)

donde:

* ( \( Q \)
Q ) es el caudal tratado,
* ( \( e_u \)
 ) es un factor energético característico de la unidad (kWh/m³).

Estos valores se emplean exclusivamente para **comparaciones relativas entre alternativas**, no para optimización detallada.

---

## 3. Base experimental y rol de los laboratorios DOTyC de la UNALM

### 3.1 Filosofía de calibración

Los datos experimentales se utilizan para:

* Delimitar rangos de eficiencia de remoción,
* Validar **clases de calidad de salida**, no valores puntuales,
* Identificar sensibilidades operativas.

Este enfoque es coherente con manuales de saneamiento descentralizado y con prácticas recomendadas en contextos de alta variabilidad.

---

### 3.2 Laboratorio de Saneamiento

El Laboratorio de Saneamiento aporta:

* Rangos empíricos de eficiencia,
* Resultados bajo condiciones controladas,
* Identificación de umbrales operativos.

Estos datos se incorporan como:

\( \eta_{p,i} \in [\eta_{\text{min}}, \eta_{\text{max}}] \)

permitiendo análisis de escenarios (mejor caso, caso típico, peor caso).

---

### 3.3 Laboratorio de Prueba y Ensayo de Materiales

El Laboratorio de Prueba y Ensayo de Materiales contribuye a:

* Verificar la idoneidad de materiales constructivos,
* Validar la integridad de la estructura hidráulica,
* Ajustar parámetros del modelo en función del sistema construido.
* Elabora un modelo BIM para la construcción y operación.

Esto asegura coherencia entre el **gemelo digital** y la infraestructura real.

---

### 3.4 Lógica de validación

La validación del modelo se realiza mediante:

* Comparación entre clases de calidad modeladas y medidas,
* Verificación de la viabilidad hidráulica,
* Confirmación de compatibilidad constructiva.

Se trata de una **validación ingenieril**, no de una certificación regulatoria.

---

## 4. Posicionamiento epistemológico del modelo

### 4.1 Alcances

El modelo:

* Apoya la planificación y el diseño,
* Facilita la comparación de alternativas,
* Integra saneamiento y soluciones basadas en la naturaleza (SbN),
* Es transparente y reproducible.

---

### 4.2 Limitaciones explícitas

El modelo **no pretende**:

* Sustituir simuladores cinéticos detallados,
* Predecir concentraciones exactas en todo momento,
* Servir como herramienta de cumplimiento normativo final.

Esta delimitación es coherente con proyectos de investigación e innovación en saneamiento descentralizado.

---

## Referencias bibliográficas

### Ingeniería sanitaria y modelación de tratamientos

Metcalf & Eddy, Inc., Tchobanoglous, G., Stensel, H. D., Tsuchihashi, R., & Burton, F. L. (2014).
*Wastewater engineering: Treatment and resource recovery* (5th ed.). McGraw-Hill Education.
[https://www.mheducation.com](https://www.mheducation.com)

> **Referencia base** para balances de masa, eficiencias de remoción, trenes de tratamiento y principios de diseño. Es el anclaje clásico para justificar modelos agregados y aproximaciones de planificación.

---

### Saneamiento, salud pública y enfoque de riesgos

World Health Organization. (2019).
*WHO water, sanitation and hygiene strategy 2018-2025*. World Health Organization.
[https://www.who.int/publications/i/item/WHO-CED-PHE-WSH-18.03](https://www.who.int/publications/i/item/WHO-CED-PHE-WSH-18.03)

> Documento normativo clave que respalda el enfoque por clases de riesgo, el tratamiento categórico de patógenos y la planificación de saneamiento en contextos complejos.

---

World Health Organization. (2006).
*Guidelines for the safe use of wastewater, excreta and greywater* (Vols. 1–4). World Health Organization.
[https://www.who.int/publications/i/item/9241546859](https://www.who.int/publications/i/item/9241546859)

> Referencia fundamental para justificar **modelación orientada a reutilización**, evaluación por escenarios y control de riesgos en lugar de precisión cinética.

---

### Saneamiento descentralizado y enfoques modulares

Tilley, E., Ulrich, L., Lüthi, C., Reymond, P., & Zurbrügg, C. (2014).
*Compendium of sanitation systems and technologies* (2nd ed.). Eawag.
[https://www.eawag.ch/en/department/sandec/publications/compendium/](https://www.eawag.ch/en/department/sandec/publications/compendium/)

> **Referencia central** para saneamiento descentralizado, sistemas modulares, trenes de tratamiento y criterios de selección tecnológica.

---

Massoud, M. A., Tarhini, A., & Nasr, J. A. (2009).
Decentralized approaches to wastewater treatment and management: Applicability in developing countries.
*Journal of Environmental Management, 90*(1), 652–659.
[https://doi.org/10.1016/j.jenvman.2008.07.001](https://doi.org/10.1016/j.jenvman.2008.07.001)

> Sustenta la idoneidad de modelos simplificados para sistemas descentralizados y contextos de alta variabilidad.

---

### Enfoques de planificación y decisión (no cinéticos)

Gikas, P., & Tchobanoglous, G. (2009).
The role of satellite and decentralized strategies in water resources management.
*Journal of Environmental Management, 90*(1), 144–152.
[https://doi.org/10.1016/j.jenvman.2007.08.016](https://doi.org/10.1016/j.jenvman.2007.08.016)

> Apoya el uso de modelos orientados a decisión y planificación, más que a simulación detallada.

---

### Soluciones basadas en la naturaleza y tratamiento extensivo

Vymazal, J. (2011).
Constructed wetlands for wastewater treatment: Five decades of experience.
*Environmental Science & Technology, 45*(1), 61–69.
[https://doi.org/10.1021/es101403q](https://doi.org/10.1021/es101403q)

> Anclaje científico para la integración de humedales construidos y SbN, con desempeño evaluado por rangos y condiciones de contexto.

---

## Nota metodológica clave (puedes incluirla)

> El enfoque adoptado es coherente con la literatura clásica de ingeniería sanitaria y con las guías internacionales de la OMS, que recomiendan modelos transparentes, basados en balances de masa y evaluación de riesgos, para la planificación y el diseño de sistemas de saneamiento descentralizado.

---
