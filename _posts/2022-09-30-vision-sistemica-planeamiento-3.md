---
layout: post
title: "Una vision sistémica del planeamiento (3)"
author: "Victor Peña Guillen"
date:   2022-09-30 09:35:30 +0900
#permalink: /hello-world/
categories: updates
---

---

**Prefacio.**
Tercera parte del comentario al libro de G.F. Chadwick [^1].

---

## Los modelos de representación

La utilidad de la modelística reside en el entendimiento de los sistemas que estudia y en el esclarecimiento que ofrece acerca de las decisiones posibles y los resultados probables de estas decisiones.
Hay diversos métodos de modelamiento y simulación de basados en algoritmos, probabilidades y sobretodo en criterios relacionados con el proposito buscado con el plan.

En la descripción de los modelos generamente empleados se elige un modelo que para el autor (en 1968) sería de gran utilidad en el futuro.
Este es el modelo de Lowry, que es un algoritmo de ubicación de actividades en un espacio, de modo que esta localización sea la mejor.
Este modelo ha sido perfeccionado y complementado, siendo la mejor de estas inclusiones aquella realizada por Garin.

Este modelo es bastante complejo e incluye variables agrupadas en grandes grupos, tales como vivienda, población, accesibilidad, etc. los cuales forman todo un sistema que es representado por modelos matemáticos y algoritmos que simulan su comportamiento para cada uno de los cambios en las variables.
Este proceso necesita de la ayuda de la computadora.

## Modelos lineales a escala del sistema

El modelo anterior y los demás son una mera representación del sistema, lo cual no le quita ningún mérito como herramientas.
De este modo se requerirá una modelística "a escala del sistema" que permita la planificación de estaen el sentido de alterar su trayectoria (y probablemente también su estructura), en un esfuerzo para conseguir, si no la optimización, al menos la satisfacción de una serie de criterios derivados de ciertos objetivos.

La modelística a escala del sistema implica la modelación de diversos sub--sistemas en interacción, mas que la precisión del análisis en un solo subsistema importante, y esto a su vez, entraña la satisfacción simultánea (o intento de optimización), de los criterios que se relacionan a la realización de dichos sub-sistemas.

Esta es la filosofía de la modelística del sistema total, y la principal herramienta que utiliza es la programación lineal, útil para optimizar modelos económicos y aplicable al planeamiento.

Schlager parte de la idea que "el diseño y no la explicación o la predicción se convierte en el problema primario a resolver"; de acuerdo a esto este autor plantea dos condiciones de diseño: primero, las variables de calidad, cantidad y localización; y en segundo lugar, los requisitos comparando el uso en zonas distintas, y a la vez determinando los rangos en las variables para el uso del suelo.

En ambos casos el requisito de diseño es susceptible de una expresión matemática, por medio de una igualdad o desigualdad algebraica haciendo viable, de este modo, una formulación mediante la programación lineal.
