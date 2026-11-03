---
title: "Modelo de Cambio: del diseño espacial al funcionamiento ecológico del paisaje"
author: "Victor Peña Guillen, PhD"
date: "November 3, 2026"
output:
  html_document: default
---

## 1. ¿Qué es el Modelo de Cambio?

En el proceso de planificación del paisaje, el **Modelo de Cambio** permite formular alternativas de intervención territorial mediante la modificación deliberada de la composición y configuración espacial del paisaje.

Su propósito no consiste simplemente en modificar la geometría de un mosaico, sino en construir **escenarios espaciales que expresen decisiones sobre el territorio**, sustentados en principios ecológicos y en hipótesis sobre sus posibles consecuencias.

Siguiendo el marco metodológico de Steinitz, el Modelo de Cambio responde a una pregunta fundamental:

**¿Cómo podría modificarse el paisaje para alcanzar determinados objetivos ecológicos y territoriales?**

Las alternativas diseñadas deberán ser posteriormente examinadas mediante el Modelo de Impacto, que evalúa las consecuencias de las transformaciones propuestas.

## 2. Fundamentos de la ecología del paisaje

La ecología del paisaje estudia las relaciones entre tres dimensiones fundamentales:

- **Estructura:** distribución espacial de los elementos que componen el paisaje.
- **Procesos:** movimientos y flujos de organismos, agua, energía y materiales entre esos elementos.
- **Cambio:** transformaciones de la estructura y los procesos a través del tiempo.

Forman (1995) plantea principios generales que permiten comprender cómo la organización espacial del paisaje influye sobre los procesos ecológicos.

El modelo de **parche–corredor–matriz** proporciona una representación conceptual de esta organización:

- Los *parches* son superficies relativamente homogéneas que se distinguen de su entorno.
- Los *corredores* son elementos lineales que pueden facilitar o restringir determinados flujos.
- La *matriz* constituye el contexto territorial dentro del cual se distribuyen los parches y corredores.

Sin embargo, una determinada configuración espacial no garantiza por sí misma un funcionamiento ecológico específico. La relación entre estructura y procesos debe establecerse mediante hipótesis verificables.

## 3. Principios ecológicos para diseñar cambios en el paisaje

Dramstad, Olson y Forman (1996) sistematizan principios de diseño que permiten orientar intervenciones espaciales.

| Principio | Intervención posible | Pregunta ecológica |
|---|---|---|
| Tamaño del parche | Ampliar fragmentos existentes | ¿Qué superficie requiere el organismo o proceso de interés? |
| Forma y bordes | Modificar la geometría de los parches | ¿Qué efectos produce la exposición al borde? |
| Corredores | Restaurar conexiones entre fragmentos | ¿Qué especies o flujos pueden utilizar la conexión? |
| Matriz | Mejorar la compatibilidad de los usos circundantes | ¿Qué condiciones facilitan o restringen los procesos ecológicos? |
| Configuración espacial | Redistribuir parches y conexiones | ¿Qué disposición permite alcanzar los objetivos de restauración? |

Estos principios no constituyen reglas universales. Su aplicación depende de la escala, las características del ecosistema, las especies consideradas y los objetivos de la intervención.

Por ejemplo, aumentar el tamaño de un parche puede incrementar su superficie interior, mientras que crear corredores puede favorecer la continuidad espacial. Ambas estrategias pueden tener resultados diferentes según el proceso ecológico que se pretenda restaurar.

## 4. Composición, configuración y métricas del paisaje

Botequilha Leitão y Ahern (2002) muestran cómo las métricas del paisaje pueden utilizarse para caracterizar mosaicos, comparar escenarios y apoyar decisiones de planificación.

Es necesario distinguir dos dimensiones:

**Composición:** cuánto existe de cada tipo de cobertura o uso del suelo.

**Configuración:** cómo están distribuidos espacialmente los elementos del paisaje.

Entre las métricas más utilizadas se encuentran:

| Métrica | Qué permite evaluar |
|---|---|
| PLAND | Porcentaje del paisaje ocupado por una clase |
| AREA_MN | Tamaño medio de los parches |
| PD | Densidad de parches |
| SHAPE | Complejidad de la forma |
| ENN | Distancia euclidiana al parche más cercano |
| PROX | Proximidad espacial considerando distancia y área |
| COHESION | Continuidad o conectividad física de una clase |

La selección de métricas debe responder a preguntas concretas y evitar redundancias.

También es indispensable mantener constantes la escala, la resolución espacial y los criterios de clasificación cuando se comparan escenarios.

**Una métrica del paisaje describe una propiedad estructural; no constituye necesariamente una medición de un proceso ecológico.**

Por ejemplo, una reducción de ENN indica que los parches están espacialmente más próximos, pero no demuestra que haya aumentado el desplazamiento efectivo de organismos.

## 5. Del Modelo de Cambio al Modelo de Impacto

El diseño de escenarios requiere distinguir entre las transformaciones propuestas y sus consecuencias.

| Modelo de Cambio | Modelo de Impacto |
|---|---|
| ¿Qué intervenciones espaciales se proponen? | ¿Qué consecuencias pueden producirse? |
| ¿Dónde cambiarán las coberturas o usos del suelo? | ¿Cómo cambiarán la superficie y configuración de los hábitats? |
| ¿Qué áreas serán restauradas o protegidas? | ¿Cómo podrían modificarse los procesos ecológicos? |
| ¿Qué reglas orientan las intervenciones? | ¿Qué beneficios, riesgos e incertidumbres presentan las alternativas? |

El estudio de la cuenca del río Mill, discutido por Botequilha Leitão y Ahern (2002), ilustra la utilidad de comparar escenarios territoriales mediante métricas del paisaje para anticipar consecuencias sobre los hábitats.

La enseñanza principal es que **las decisiones de asignación espacial pueden producir configuraciones ecológicas muy diferentes**, incluso cuando las alternativas responden a objetivos generales semejantes.

## 6. Variables estructurales y funcionales

Una distinción esencial para evaluar las intervenciones es la diferencia entre variables estructurales y funcionales.

Las primeras describen propiedades espaciales del paisaje. Las segundas representan procesos ecológicos o su desempeño.

| Intervención | Variable estructural | Variable funcional |
|---|---|---|
| Conectar fragmentos de bosque | ENN, PROX, COHESION | Probabilidad de desplazamiento de una especie |
| Ampliar parches de vegetación | Área y superficie núcleo | Tasa de colonización o regeneración |
| Restaurar vegetación ribereña | Ancho y continuidad de la franja vegetal | Retención de sedimentos o regulación térmica |
| Recuperar áreas degradadas | Superficie restaurada | Infiltración o recuperación de funciones del suelo |

Las variables funcionales pueden estimarse mediante modelos o medirse mediante observaciones de campo.

Por tanto, conviene distinguir entre:

1. **Cambio estructural medido:** se modifica la superficie, forma o distribución de los parches.
2. **Cambio funcional estimado:** un modelo predice modificaciones en un proceso ecológico.
3. **Cambio funcional observado:** existen mediciones que evidencian la modificación del proceso.

Esta distinción evita atribuir beneficios ecológicos que todavía no han sido demostrados.

## 7. Taller de diseño: dos escenarios de restauración

El ejercicio de clase propone diseñar dos alternativas para un paisaje fragmentado, manteniendo constante la superficie total destinada a restauración.

**Escenario A: ampliación de parches existentes.**

Se concentra la restauración en incrementar la superficie de los fragmentos actuales. Esta estrategia puede aumentar el área núcleo y reducir la exposición relativa al borde, aunque no necesariamente resuelve el aislamiento entre fragmentos.

**Escenario B: creación de conexiones intermedias.**

Se distribuye la restauración mediante nuevos parches, corredores o elementos de conexión. Esta estrategia puede reducir distancias estructurales y aumentar la continuidad espacial, aunque sus resultados dependerán de la calidad de los nuevos hábitats y de la permeabilidad de la matriz.

Los equipos deberán comparar ambos escenarios mediante tres o cuatro métricas y seleccionar al menos una variable funcional vinculada al objetivo de restauración.

La evaluación deberá considerar tanto los beneficios esperados como las incertidumbres y posibles efectos no deseados.

## 8. Del impacto esperado a la decisión territorial

La selección de una alternativa no debería depender exclusivamente de cuál presenta mejores valores en determinadas métricas.

Es necesario considerar:

- **Eficacia ecológica:** relación plausible entre la intervención y la función que se busca restaurar.
- **Riesgos y compensaciones:** posibles efectos negativos sobre otros procesos, servicios o usuarios.
- **Viabilidad:** condiciones de tenencia, mantenimiento, costos y participación de actores.
- **Aprendizaje:** posibilidad de monitorear resultados y adaptar las intervenciones.

De este modo, el Modelo de Cambio forma parte de un proceso de planificación en el cual las alternativas espaciales se formulan, comparan, evalúan y someten a decisiones.

## 9. Reflexión final

El diseño ecológico del paisaje exige superar una interpretación exclusivamente geométrica de la restauración.

Una mayor superficie vegetal, una menor distancia entre parches o una mayor cohesión espacial pueden representar mejoras estructurales importantes, pero no constituyen por sí mismas evidencia de recuperación funcional.

El desafío consiste en establecer relaciones causales plausibles entre las intervenciones, los cambios en la estructura del paisaje y los procesos ecológicos que se busca recuperar.

**La pregunta central del Modelo de Cambio no es solamente dónde y cuánto restaurar, sino qué procesos ecológicos esperamos modificar mediante una determinada configuración espacial y cómo podremos evaluar sus resultados.**

---

## Referencias

Botequilha Leitão, A., & Ahern, J. (2002). Applying landscape ecological concepts and metrics in sustainable landscape planning. *Landscape and Urban Planning, 59*(2), 65–93. https://doi.org/10.1016/S0169-2046(02)00005-1

Dramstad, W. E., Olson, J. D., & Forman, R. T. T. (1996). *Landscape ecology principles in landscape architecture and land-use planning*. Island Press.

Forman, R. T. T. (1995). Some general principles of landscape and regional ecology. *Landscape Ecology, 10*(3), 133–142. https://doi.org/10.1007/BF00133027

Opdam, P., Steingröver, E., & van Rooij, S. (2006). Ecological networks: A spatial concept for multi-actor planning of sustainable landscapes. *Landscape and Urban Planning, 75*(3–4), 322–332. https://doi.org/10.1016/j.landurbplan.2005.02.015