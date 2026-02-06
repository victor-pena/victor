---
title: "Dimensionando el humedal artificial"
author: "Victor Peña Guillen, PhD"
date: "January 29, 2026"
output:
  html_document: default
---

### Herramientas para ativar el gemelo digital: el Asset Register y el IFC

En proyectos para la gestión de las aguas residuales y los lodos en pequeñas comunidades periurbanas, mediante el uso de soluciones basadas en la naturaleza (SbN), el dimensionamiento de humedales es una consideración para optimizar el diseño de este tipo de SbN.  
El empleo de tecnología BIM dentro de un sistema de tratamiento y reuso, busca que este se represente a través de una infraestructura de datos para que funcione el **gemelo digital**.
El gemelo digital demuestra su valor, no como una tecnología sofisticada, sino como una **infraestructura de aprendizaje y planificación**.

---

### 1. La secuencia del pipeline: Asset Register + estandar IFC

El Asset Register (en formato CSV) es el punto de partida:

- Cada **fila** representa un **objeto BIM real**
- Cada **columna** representa un **atributo que el gemelo digital necesita**
- Todo lo que no está en el Asset Register **no existe para el gemelo**

Desde el BIM se exporta un **IFC**, que cumple una función clave:

- Es **estable**
- Es **auditable**
- Es **independiente del software**
- Se convierte en una **infraestructura de datos**, no solo en un modelo gráfico

Aquí el BIM deja de ser “dibujo” y pasa a ser **base objetiva del sistema**.

---

### 2. ¿Qué significa “dimensionamiento” en términos operativos?

En un gemelo digital de **planificación y validación**, el proceso iterativo de “dimensionamiento” requiere de un diagnóstico técnico bajo criterios explícitos.

Al menos tres dimensiones son posibles de evaluar, a partir de un escenario de sobredimensionamiento:

#### a) Sobredimensionamiento hidráulico
El área del humedal es mayor de lo necesario para el caudal real que recibe.

#### b) Sobredimensionamiento por desempeño
El sistema cumple los objetivos de calidad con amplia holgura, incluso en escenarios exigentes.

#### c) Sobredimensionamiento territorial o económico
La mejora marginal por unidad de área ya no justifica ocupar más suelo (especialmente en parques públicos).

El gemelo digital permite distinguir entre estas tres situaciones, en lugar de tratarlas como una sola.

---

### 3. El test mínimo que puede hacer el gemelo digital

Sin recurrir a modelos dinámicos complejos, el gemelo puede ejecutar verificaciones simples y replicables en el modelo físico, empleando conceptos y formulas de diseño.

#### 3.1 Carga hidráulica superficial (HLR)

Una relación básica es la siguiente:

\[
HLR = \frac{Q}{A}
\]

Donde:
- `Q` es el caudal que llega al humedal
- `A` es el área efectiva del humedal

Lectura operativa:
- **HLR muy baja** → posible sobredimensionamiento
- **HLR muy alta** → riesgo de subdimensionamiento

En este caso, el empleo de la formula no busca necesariamente un valor “universal”, sino una comparacion de dos situaciones:
- rangos de referencia,
- entre escenarios del propio proyecto.

---

#### 3.2 Análisis por escenarios (la lógica de la propuesta de tratamiento y reuso)

El gemelo digital simula escenarios simples, dentro del sistema humedal-SbN:

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

Cuando el desempeño real es muy holgado y el uso hidráulico es bajo, el gemelo confirma el criterio de dimensionamiento que el modelo anticipaba.

---

### 5. Qué decisiones habilita el gemelo digital

Detectar sobredimensionamiento no significa “error de diseño”.  
Significa tener opciones abiertas para corregir las condiciones presentes en la realidad, como por ejemplo:

- Reducir área en futuros diseños
- Mantener el área como **margen de resiliencia** para absorver cargas no contempladas o inciertas
- Reasignar parte del espacio a:
  - otra SbN,
  - gestión de lodos,
  - almacenamiento,
  - biodiversidad urbana

Aquí el gemelo digital conecta **ingeniería, territorio y política pública**.

---

### 6. Ideas clave para sistematizar el esquema humedal-SbN

> El BIM define los activos físicos presentes en la realidad, el Asset Register los vuelve operables, el IFC los estabiliza como infraestructura de datos y el gemelo digital les permite simular el comportamiento bajo ciertos escenarios.  
> De este modo se sistematiza el dimensionamiento del humedal, alejando las decisiones intuitivas o arbitrarias y permitiendo realizar decisiones informadas que ademas se registran para futuras evaluaciones.

---
