# Repaso Final — Programación II
*Basado únicamente en tus apuntes a mano, tu resumen Word y la teoría del aula virtual (Unidad 1 y 2). No se usó ninguna fuente externa.*

> ⚠️ **Aviso:** no tenía capturas del parcial anterior para calibrar el estilo exacto de las preguntas, así que este repaso está armado 100% en base al contenido teórico. El nivel de detalle apunta a lo que un multiple choice suele preguntar (definiciones, símbolos, diferencias, "qué NO es X").

---

## PARTE 1 — ESQUEMAS DE REPASO FLASH (repaso en 5 minutos)

### 🔹 A. Los 10 patrones de diseño permitidos (según TUS apuntes)

| Categoría | Patrón | Qué resuelve (en una frase) |
|---|---|---|
| **Creacional** | **Singleton** | Que exista **una única instancia** de un objeto determinado |
| **Creacional** | **Factory Method** | Simplifica la creación de objetos de una familia, definiendo una **interfaz estándar** para construirlos |
| **Creacional** | **Abstract Factory** | **Centraliza** la fabricación de objetos de **distintas familias** en un solo lugar |
| **Estructural** | **Adapter** | Adapta un objeto/interfaz para que **pueda ser usado por otro** que de otro modo no podría usarlo |
| **Estructural** | **Composite** | Trata a objetos **simples y compuestos de la misma forma** |
| **Estructural** | **Proxy** | Da un **sustituto** de otro objeto y **controla el acceso** a él (hace algo antes/después de la solicitud) |
| **Comportamiento** | **State** | Un objeto **cambia su comportamiento** cuando cambia su **estado interno** |
| **Comportamiento** | **Strategy** | Dispone **varios métodos** para resolver un problema y permite elegir **cuál usar en tiempo de ejecución** |
| **Comportamiento** | **Observer** | Un sujeto avisa a **muchos observadores** cuando cambia su estado, y estos se **actualizan solos** |
| **Comportamiento** | **Command** | **Encapsula una operación** en un objeto, permitiendo ejecutarla sin conocer su contenido |

**Truquito para no confundir categorías:**
- **Creacional** → tiene que ver con **cómo se crea/instancia** un objeto
- **Estructural** → tiene que ver con **cómo se componen/relacionan** objetos entre sí
- **Comportamiento** → tiene que ver con **cómo se comunican/interactúan** en tiempo de ejecución

**Dato extra de tus apuntes (relación Singleton–Strategy):**
- Si un Strategy concreto tiene un **estado interno no compartido** por toda la app, puede ser Singleton.
- Singleton puede reducir la proliferación de objetos con Strategy **solo si** la estrategia no requiere una instancia por consumidor.
- Cómo implementar Singleton: constructor **privado** + atributo **estático y privado** + método **estático y público** para `getInstance()`.

---

### 🔹 B. Diagrama de Clases vs. Diagrama de Secuencia

| | **Diagrama de Clases** | **Diagrama de Secuencia** |
|---|---|---|
| **Tipo de vista** | Estructural / estática | De comportamiento / dinámica |
| **Qué muestra** | Las clases de un sistema, sus atributos, métodos y relaciones | Cómo interactúan los objetos entre sí en un escenario particular, a través del tiempo |
| **Analogía** | Es "una foto" del sistema | Es "el diagrama de clases en movimiento" |
| **Se arma a partir de** | El análisis de responsabilidades de los objetos | La descripción de un **caso de uso** |
| **Elementos clave** | Nombre, atributos, métodos, visibilidad, relaciones | Rol de la clase, activación, mensajes, líneas de vida, destrucción, loops, selección |

---

### 🔹 C. Relaciones UML — cuadro resumen

| Relación | Símbolo (según tus apuntes) | Frase clave | Regla de "vida" |
|---|---|---|---|
| **Herencia / Generalización-Especialización** | flecha vacía sólida `——▷` | "es un" | Ocurre en tiempo de diseño, no en ejecución |
| **Implementación / Realización** | flecha vacía punteada `- - -▷` | Clase implementa interfaz | — |
| **Asociación** | flecha simple `——>` | Colaboran entre sí | Si A deja de existir, B **no** |
| **Agregación** | diamante vacío `◇——>` | "tiene un" (parte-todo débil) | Si A deja de existir, B **no** |
| **Composición** | diamante lleno `◆——>` | "tiene un" (parte-todo fuerte) | Si A deja de existir, B **también** |
| **De Uso / Dependencia** | flecha punteada `- - ->` | A recibe, crea o devuelve un objeto de B | El objeto no se guarda en la clase que lo usa |

**Atributos de las relaciones:**
- **Navegabilidad** → dirección de la relación (unidireccional o bidireccional)
- **Multiplicidad** → cuántas instancias de una clase se relacionan con una instancia de otra (`1`, `0..1`, `M..N`, `*`, `0..*`, `1..*`)

---

## PARTE 2 — LISTA DE TEMAS CLAVE ("Menos es más")

## UNIDAD 1 — POO, Conceptos y Diseño

### Objetos y responsabilidades
- Los objetos se detectan al descubrir sus **responsabilidades** (lo que "saben hacer").
- Las responsabilidades se representan como **métodos**.
- Los métodos son como funciones: reciben parámetros de entrada y pueden devolver salida.
- Los métodos tienen una **firma**: nombre + parámetros que recibe y devuelve.

### Visibilidad
- Clasifica el acceso a métodos y atributos: **público (+), privado (-), protegido (#), default/paquete (~)**.
- **Regla clave (típica pregunta de examen):** los **atributos siempre deben ser privados** (para asegurar el **encapsulamiento**). La visibilidad variable (pública/privada) aplica sobre todo a los **métodos**.
- Protegido (#): accesible en subclases, pero no desde afuera de ellas.
- Default (~): accesible por todos los objetos del **mismo paquete**.

### Atributos
- Se consideran **solo los necesarios** para cumplir la responsabilidad actual del objeto.
- **No** se deben modelar atributos "pensando a futuro" → genera riesgos y desvíos innecesarios.
- El objeto debe comportarse como una **caja negra** respecto a sus atributos (protege el encapsulamiento).

### Definición de una clase
- Una clase es un **molde (template)** para objetos del mismo tipo.
- Todos los objetos de una misma clase comparten la **misma definición** de métodos y atributos.
- Elementos de una clase: **Nombre, Atributos, Métodos, Visibilidad**.

### Reglas de nombres (clásica pregunta de detalle)
- **Clase:** empieza con **mayúscula**; si es compuesto, cada palabra siguiente en mayúscula, sin espacios.
- **Atributos/Métodos:** empiezan con **minúscula**; palabras compuestas siguientes en mayúscula (camelCase).
- **Atributos** que representan un único elemento → **singular**; si no, plural.
- **Métodos** que son verbos → **infinitivo** (ej: `ejecutar`, NO `ejecuto`).

### UML — generalidades
- UML = **Unified Modeling Language**, lenguaje **gráfico** para visualizar, especificar, construir y documentar sistemas.
- **UML NO se usa para describir algoritmos.**
- Diagramas se agrupan en **estructurales (estáticos)** y **de comportamiento (dinámicos)**.
- En este curso se usan: **Diagrama de Clases, Diagrama de Secuencia y Diagrama de Paquetes**.

### Diagrama de Paquetes
- Muestra las **dependencias entre paquetes** (agrupaciones lógicas de un sistema).
- Define un **espacio de nombres** (como `namespace` en C++ o `package` en Java).
- Relaciones entre paquetes: **Importación** (`<<import>>`), **Acceso** (`<<access>>`), **Combinación/merge** (`<<merge>>`), **Exportación** (implícita, por visibilidad pública), y **Generalización**.

### Clase Abstracta vs. Interfaz
- **Clase abstracta:** no puede instanciarse; puede tener métodos abstractos y **no abstractos**; puede tener atributos con cualquier modificador de acceso.
- **Interfaz:** solo tiene métodos **abstractos** (sin cuerpo); en Java, sus métodos son **implícitamente públicos y abstractos**; sus variables son **finales por defecto**.
- Una interfaz **solo puede extender otra interfaz**; una clase abstracta **sí puede implementar una interfaz**.
- Ambas se usan para **abstracción**, pero una interfaz "parece una clase, pero no es una clase".

### Principios SOLID (tal como los tenés en tus apuntes)
| Sigla | Nombre | Definición corta |
|---|---|---|
| **S** | Single Responsibility | Una clase debe tener **una única razón para cambiar** |
| **O** | Open/Closed | Abierta a **extensión**, cerrada a **modificación** |
| **L** | Liskov Substitution | Una **subclase** debe poder **reemplazar** a su superclase |
| **I** | Interface Segregation | Mejor **interfaces específicas** que una interfaz general |
| **D** | Dependency Inversion | Lo **concreto depende de lo abstracto**, no al revés |

> Nota: el material del aula agrega otros principios (Common Closure, Common Reuse, Acyclic Dependencies, Stable Dependencies, Stable Abstractions), pero **no están en tus apuntes a mano**, así que probablemente no sean el foco del examen — los menciono solo por si el profesor pregunta sobre "SOLID+".

### Cohesión y Acoplamiento
- **Cohesión:** grado de relación de las tareas/funciones de un módulo con su propósito. **Más cohesión = más calidad.** Se busca **maximizarla**.
- **Acoplamiento:** nivel de dependencia entre módulos. **Más acoplamiento = menos calidad.** Se busca **minimizarlo**.

### Arquitectura por capas
- Distribuye roles y responsabilidades **jerárquicamente**.
- Ejemplo típico: capa de **presentación**, capa de **negocio**, capa de **datos**.
- Principios: abstracción, encapsulamiento, funcionalidad claramente definida, **alta cohesión**, reutilizable, **bajo acoplamiento**.
- **N-capas/3-capas:** cada segmento vive en un **computador físicamente separado** (distinto del estilo por capas simple, donde pueden compartir la misma máquina).

---

## UNIDAD 2 — Patrones de Diseño

### ¿Qué es un patrón de diseño?
- **Solución descubierta** (no inventada) para un problema recurrente, ya probada en escenarios anteriores.
- Se inspiran en los **patrones de construcción de la arquitectura** (edilicia).
- El GoF documentó **~20 patrones** originales en C/C++ y Smalltalk.

### Clasificación GoF (pregunta muy típica)
- **Creacionales:** resuelven problemas de **creación/instanciación** de objetos.
- **Estructurales:** resuelven problemas de **estructura y composición interna** de objetos.
- **De Comportamiento:** resuelven problemas de **comunicación/interacción** entre objetos.

### Elementos de un patrón (según la teoría del aula)
Nombre, Clasificación, Intención, Motivación, Aplicabilidad, Segundo nombre, Estructura, Participantes, Colaboraciones, Consecuencias, Implementación, Código de ejemplo, Usos conocidos, Patrones relacionados.
- **Motivación** = explicación del problema recurrente, en un párrafo breve (3-6 líneas).
- **Consecuencias** = lo positivo y negativo de aplicar el patrón.

### Los 10 patrones permitidos (repaso en detalle — ver también tabla flash arriba)

**Creacionales**
- **Singleton:** única instancia de un objeto. Nivel de uso: **Muy Alto**.
- **Factory Method:** interfaz estándar para construir objetos de una familia. Nivel de uso: **Alto**. (Variante: *Simple Factory*.)
- **Abstract Factory:** centraliza la fabricación de objetos de **distintas familias**. Nivel de uso: **Bajo** (introducción).

**Estructurales**
- **Adapter:** adapta un objeto/interfaz para que otro pueda usarlo. Nivel de uso: **Muy Alto**.
- **Composite:** trata objetos simples y compuestos del mismo modo. Nivel de uso: **Medio**.
- **Proxy:** sustituto que controla el acceso al objeto original (según tus apuntes; nota: la teoría del aula no detalla Proxy explícitamente, así que esta definición viene de tu resumen).

**De Comportamiento**
- **State:** cambia comportamiento según su estado interno. Nivel de uso: **Alto**.
- **Strategy:** varios métodos intercambiables en tiempo de ejecución. Nivel de uso: **Alto**.
- **Observer:** un sujeto notifica automáticamente a sus observadores. Nivel de uso: **Alto**.
- **Command:** encapsula una operación en un objeto. Nivel de uso: **Medio**.

### Antipatrones (Anexo Unidad 2)
- Un antipatrón es una implementación que **invariablemente lleva a una mala solución**.
- **No** están en el libro original de *Design Patterns* (son posteriores, y contrapartida de los patrones).

**Antipatrones de Diseño General (los más "preguntables"):**
| Antipatrón | Qué es |
|---|---|
| Objeto todopoderoso (BLOB) | Toda la funcionalidad en un solo objeto |
| Clase Gorda (Fat Class) | Clase con demasiados atributos/métodos, responsable de lógica que no le corresponde |
| Botón mágico | Lógica de negocio metida en la pantalla/UI |
| Entrada chapuza | No validar los datos que entran al sistema |
| Gran bola de lodo | Sistema sin estructura definida |
| Interfaz inflada | Interfaz tan potente que es difícil de implementar |
| Re-dependencia | Dependencias innecesarias entre objetos |

**Antipatrones de Diseño Orientado a Objetos (los más "preguntables"):**
| Antipatrón | Qué es |
|---|---|
| Modelo de dominio Anémico | Objetos sin lógica de negocio, solo datos |
| Singletonitis | Abuso del patrón Singleton (o de cualquier patrón) en lugares innecesarios |
| Problema del círculo-elipse | Tipar pensando en subtipos, genera bifurcaciones lógicas impredecibles |
| Problema del yoyó | Estructuras de herencia difíciles de entender por exceso de fragmentación |
| YAFL | Agregar capas innecesarias a un sistema |

### Patrones asociados a capas — MVC
- **MVC (Model View Controller)** es el patrón precursor de los patrones asociados a capas.
- **Vista:** representa pantallas/elementos visuales.
- **Controlador:** atiende lo que pasa en la vista, dirige datos y flujo.
- **Modelo:** representa objetos del negocio, guarda/gestiona datos.

---

## ⚡ Chequeo relámpago final (los que más suelen trampear en multiple choice)

- ❌ UML **no** describe algoritmos.
- ❌ Los **atributos** no deberían tener visibilidad pública (siempre privados).
- ❌ Una **interfaz** no puede tener métodos con cuerpo (excepto default/static desde Java 8, que la teoría menciona como diferencia, pero no está en tus apuntes — probablemente no entra).
- ❌ **Builder** NO está en tu lista de patrones a estudiar (aparece en la teoría del aula, pero vos lo excluiste).
- ✅ Composición = diamante **relleno**; Agregación = diamante **vacío**. Es un error muy común confundirlos.
- ✅ Diagrama de secuencia se arma a partir de un **caso de uso**, no de la nada.
- ✅ Singleton = constructor **privado** + atributo **estático privado** + método **estático público**.

---

*Recordá: este documento cubre todo lo que aparece en tus apuntes + la teoría del aula. Si el profesor pregunta algo de Builder, Bridge, Decorator, Facade u otros patrones no mencionados en tus apuntes, no está cubierto acá a propósito, según tu instrucción original.*
