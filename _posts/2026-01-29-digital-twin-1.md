---
title: "Dimensionando el humedal artificial"
author: "Victor Peña Guillen, PhD"
date: "January 29, 2026"
output:
  html_document: default
---

En proyectos para el tratamiento y el reuso de las aguas residuales y los lodos, mediante el uso de soluciones basadas en la naturaleza (SbN), el dimensionamiento de los humedales es una consideración para optimizar el diseño de este tipo de esquemas complementarios.  
El empleo de tecnología BIM dentro de un sistema de tratamiento y reuso, busca que este se represente a través de una infraestructura de datos.

---

### 1. El modelo digital del sistema de tratamiento

El registro del sistema se realiza empleando un protocolo llamado Asset Register (en formato CSV), el cual es el punto de partida para el modelamiento:

- Cada **fila** representa un **objeto real (en formato BIM)**
- Cada **columna** representa un **atributo que el modelo necesita**
- Todo lo que no está en el Asset Register **no existe para el modelo**

Desde el BIM se exporta un archivo (denominado protocolo IFC), que cumple las siguientes funciones clave:

- Es estable
- Es auditable
- Es independiente del software
- Se convierte en una **infraestructura de datos**, no solo en un modelo gráfico

Aquí el BIM deja de ser un "dibujo" y pasa a ser la **base objetiva del sistema**.

---

### 2. Diseño y dimensionamiento operativos

En un modelo digital de **validación**, el proceso iterativo de “dimensionamiento” requiere criterios explícitos para facilitar  el diagnóstico técnico de los resultados de cada escenario.

Al menos tres dimensiones son posibles de evaluar, a partir de un escenario de sobredimensionamiento:

#### a) Sobredimensionamiento hidráulico
El área del humedal es mayor de lo necesario para el caudal real que recibe.

#### b) Sobredimensionamiento por desempeño
El sistema cumple los objetivos de calidad con amplia holgura, incluso en escenarios exigentes.

#### c) Sobredimensionamiento territorial o económico
La mejora marginal por unidad de área ya no justifica ocupar más suelo (especialmente util en parques públicos).

El modelo digital permite distinguir entre estas tres situaciones, en lugar de tratarlas como una sola.

---

### 3. El test mínimo que puede hacer el modelo digital

Sin recurrir a modelos dinámicos complejos, el gemelo puede ejecutar verificaciones simples y replicables en el modelo físico, empleando conceptos y formulas de diseño.

#### 3.1 Carga hidráulica superficial (HLR)

Una formula básica que uede emplearse es la siguiente:

\[
HLR = \frac{Q}{A}
\]

Donde:
- `Q` es el caudal que llega al humedal
- `A` es el área efectiva del humedal

Lectura operativa:
- **HLR muy baja** → posible sobredimensionamiento
- **HLR muy alta** → riesgo de subdimensionamiento

En este caso, el empleo de la formula no busca necesariamente un valor "universal", sino una comparacion de dos situaciones:
- rangos de referencia,
- escenarios de funcionamiento en el propio proyecto.

---

#### 3.2 Análisis por escenarios (la lógica de la propuesta de tratamiento y reuso)

El modelo digital simula escenarios simples, dentro del sistema humedal-SbN:

- Caudal bajo (uso reducido, estacionalidad)
- Caudal típico
- Caudal alto (picos, crecimiento, eventos)

Si el humedal cumple objetivos en todos los escenarios y la HLR se mantiene baja incluso en caudal alto, entonces existe **evidencia técnica de sobredimensionamiento** (o de un margen de resiliencia deliberado frente a sobrecargas).

---

### 4. El cierre del ciclo: datos reales

El diagnóstico se consolida cuando se incluyen datos obtenidos a través del monitoreo de la realidad:

- **Sensores**: ¿el caudal real es menor que el de diseño?
- **Laboratorio**: ¿la calidad del efluente supera ampliamente lo exigido?
- **Operación**: ¿hay zonas secas, baja saturación, tiempos muertos?

Cuando el desempeño o eficiencia real de tratamiento es muy holgado y el uso hidráulico es bajo, el modelo confirma el criterio de dimensionamiento que el criterio de diseño anticipaba.

---

### 5. Qué decisiones habilita el modelo digital

Detectar sobredimensionamiento, en el ejemplo anterior, no significa necesariamente u "error de diseño". Podria significar tomar en cuenta un rango de opciones  para corregir las condiciones presentes en la realidad, como por ejemplo:

- Reducir área en futuros diseños
- Mantener el área como **margen de resiliencia** para absorver cargas no contempladas o inciertas
- Reasignar parte del espacio a:
  - otra SbN,
  - gestión de lodos,
  - almacenamiento,
  - biodiversidad urbana

Aquí el modelo digital conecta **ingeniería, territorio y política pública**.

---

### 6. Ideas clave para sistematizar el esquema humedal-SbN

> El BIM define los activos físicos presentes en la realidad, el Asset Register los vuelve operables, el IFC los estabiliza como infraestructura de datos y el modelo digital les permite simular el comportamiento bajo ciertos escenarios.  
> De este modo se sistematiza el dimensionamiento del humedal, alejando las decisiones intuitivas o arbitrarias y permitiendo realizar decisiones informadas que ademas se registran para futuras evaluaciones.

---
