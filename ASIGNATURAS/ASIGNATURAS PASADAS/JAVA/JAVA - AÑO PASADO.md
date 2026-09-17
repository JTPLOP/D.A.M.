***
# Guía de Contenidos y Router Semántico: Java SE (Temas 1 al 5)

Esta guía e índice estructurado de contenidos está diseñada para que cualquier modelo o agente de IA pueda realizar una **recuperación de información precisa (router semántico)** y localizar de inmediato la sintaxis, reglas y conceptos explicados en los apuntes.

---

## 🧭 Matriz de Enrutamiento Rápido para la IA (Quick Router)

| Si la necesidad o consulta trata sobre... | Tema / Documento | Apartado clave |
| :--- | :--- | :--- |
| Configuración de proyecto, tipos primitivos, `printf`, lectura por teclado (`Leer`), Git/GitHub | **Tema 1** (`APUNTES TEMA 1.pdf`) | Tipos de datos, I/O, Git |
| Condicionales (`if`, `switch`), bucles (`for`, `while`, `do-while`), `equals()`, arrays simples, `Random` | **Tema 2** (`APUNTES TEMA 2.pdf`) | Control de flujo, Vectores, Aleatorios |
| Clases, objetos, constructores, `this`, getters/setters, relaciones (asociación, composición), arrays de objetos, borrado lógico | **Tema 3** (`APUNTES TEMA 3.pdf` / `REPASO`) | POO, Relaciones, Algoritmos en arrays de objetos |
| Herencia (`extends`), `final`, clases y métodos abstractos (`abstract`), interfaces | **Tema 4** (`APUNTES TEMA 4.pdf`) | Herencia, Modificadores, Abstracción |
| `List`, `ArrayList`, `Set`, `HashSet`, `Map`, ordenación (`Comparable` vs `Comparator`), genéricos | **Tema 5 (Parte 1)** (`APUNTES TEMA 5.pdf`) | API Collections, Criterios de ordenación |
| Lambdas, clases anónimas, interfaces funcionales (`Predicate`, `Function`, etc.), `Stream`, `Optional`, `::` | **Tema 5 (Parte 2)** (`STREAM Y EXPRESIONES LAMBDA.pdf`, `STREAMS.pdf`) | Programación Funcional, Pipeline de Streams |

---

## 📚 Índice Estructurado y Resumen Detallado por Temas

---

### TEMA 1: Fundamentos del Lenguaje, Tipos Primitivos, I/O y Control de Versiones
* **Archivo de referencia:** `APUNTES TEMA 1.pdf`
* **Propósito:** Base de sintaxis en Java SE 21, entorno de desarrollo, manejo de variables elementales y flujo de trabajo con Git.

#### 1. Entorno y Estructura de Proyectos Java
* **Herramientas:** JDK 21, Eclipse EE, configuración de Workspace.
* **Jerarquía del proyecto:**
  * **Proyecto:** Notación *UpperCamelCase*.
  * **Paquete (`package`):** En minúsculas y descriptivo.
  * **Clase:** *UpperCamelCase*. Debe existir una clase principal con el método de arranque: `public static void main(String[] args)`.
* **Comentarios y terminación:** Comentarios con `//` y `/* ... */`. Toda instrucción finaliza con `;`.

#### 2. Tipos de Datos Primitivos y Variables
* **Tipos numéricos enteros:** `byte` (1 byte), `short` (2 bytes), `int` (4 bytes), `long` (8 bytes).
* **Tipos numéricos decimales:** `float` (4 bytes, decimal simple), `double` (8 bytes, decimal doble).
* **Carácter y lógico:** `char` (2 bytes, comillas simples `'a'`), `boolean` (1 byte, `true`/`false`).
* **Declaración e inicialización:** Diferencia entre reservar espacio (`int x;`) y asignar valor (`int x = 5;`). El operador `+` concatena texto en cadenas y suma valores numéricos.

#### 3. Operadores, Conversión de Tipos y Librería Math
* **Aritmética:** División `/`, producto `*`, resto/módulo `%`.
* **Casting:** Conversión forzada explícita (ej. `(float) num / den`).
* **Clase `Math`:** Uso de funciones matemáticas estándar.

#### 4. Entrada y Salida (I/O)
* **Salida estándar:**
  * `System.out.println()`: Salida sin formateo con salto de línea.
  * `System.out.printf()`: Formateo de texto sin salto de línea automático (requiere `\n`).
    * Especificadores: `%d` (enteros), `%.Nf` (decimales con redondeo a $N$ cifras), `%c` (char), `%s` (String).
* **Entrada por teclado (Clase propia `utilidades.Leer`):** Métodos estáticos auxiliares para lectura por terminal: `Leer.dato()` (String), `Leer.datoInt()`, `Leer.datoDouble()`, `Leer.datoChar()`.

#### 5. Integración Eclipse + Git/GitHub
* **Flujo de trabajo:** Conectar proyecto local a repositorio remoto.
* **Fases:** `Share Project` $\rightarrow$ Repositorio local $\rightarrow$ Mover cambios de *unstaged* a *staged* (`git add` / `++`) $\rightarrow$ `Commit` $\rightarrow$ `Push` hacia la rama principal (`main`).
* **Autenticación:** Uso de HTTPS con nombre de usuario y Personal Access Token (PAT) de GitHub.
* **Clonado:** `Import Projects from Git` $\rightarrow$ `Clone URI`.

> **Tags para IA:** `JDK21`, `Eclipse`, `Primitivos`, `Casting`, `printf`, `Clase Leer`, `Git`, `GitHub`, `Commit`, `Push`, `Tokens`.

---

### TEMA 2: Control de Flujo, Bucles, Arrays y Números Aleatorios
* **Archivo de referencia:** `APUNTES TEMA 2.pdf`
* **Propósito:** Lógica condicional, algoritmos repetitivos e indexación de datos en vectores fijos.

#### 1. Estructuras Condicionales y de Selección
* **`if` / `if...else` / anidados:** Bifurcaciones lógicas según condición booleana.
* **Operadores lógicos:** Conjunción (`&&`), disyunción (`||`) y precedencia de evaluación.
* **`switch`:** Selección de múltiples casos por valor de variable.
  * Cláusulas `case`, obligatoriedad de `break` para evitar caída en cascada (*fall-through*), y rama `default`.
  * Uso prioritario con tipos enteros.
* **Comparación de Strings:** Advertencia crítica sobre el uso erróneo de `==` (compara posición en memoria) frente al uso mandatorio de `.equals()` para comparar contenido de cadenas.

#### 2. Estructuras Iterativas (Bucles)
* **`while`:** Bucle pre-condición. Requiere control de incremento (`++`, `+=`) para evitar bucles infinitos.
* **`do...while`:** Bucle post-condición. Asegura al menos una primera ejecución antes de evaluar la condición (ideal para menús interactivos).
* **`for`:** Bucle definido con tres secciones: inicialización (`int i = 0`), condición de parada (`i < limite`) y paso (`i++`).

#### 3. Arrays Unidimensionales (Vectores)
* **Características:** Tamaño fijo inmutable una vez instanciado, tipo de dato homogéneo, indexación basada en cero ($0$ a $length - 1$).
* **Declaración e instanciación:** `tipo[] nombre = new tipo[tam];` o asignación directa `{v1, v2, ...}`.
* **Acceso y recorrido:** Acceso mediante corchetes `array[indice]`. Iteración utilizando la propiedad inmutable `array.length` (nunca variables desacopladas de tamaño).
* **Separación de responsabilidades:** Separar los bucles de captura de datos de los bucles de visualización.

#### 4. Generación de Números Aleatorios
* **Método estático `Math.random()`:** Genera números en el rango $[0.0, 1.0)$. Fórmula de escalado a enteros: `(int) Math.floor(Math.random() * (N - M + 1) + M)`.
* **Clase `java.util.Random`:** Generación pseudoaleatoria basada en semilla temporal:
  * Inicialización: `Random r = new Random(System.nanoTime());`.
  * Rango entero: `r.nextInt(hasta - desde + 1) + desde`.

> **Tags para IA:** `Control de Flujo`, `if-else`, `switch`, `equals vs ==`, `while`, `do-while`, `for`, `Arrays`, `Array.length`, `Random`, `Math.random`.

---

### TEMA 3: Programación Orientada a Objetos (POO), Encapsulamiento, Relaciones y Gestión de Arrays de Objetos
* **Archivos de referencia:** `APUNTES TEMA 3.pdf`, `TEMA 3_ REPASO EXTENSO.pdf`
* **Propósito:** Diseño de clases, encapsulamiento, instanciación, relaciones estructurales y manipulación algorítmica de colecciones de objetos mediante arrays.

#### 1. Principios de la POO y Estructura de Clases
* **Conceptos:** Objeto (instancia con estado y comportamiento), Clase (plantilla/molde).
* **Estructura del archivo:** Una clase pública por archivo `.java`.
* **Convención y visibilidad:** Atributos siempre `private`; métodos operativos `public`.
* **Modificadores de acceso:** `public` (accesible en todo el proyecto), `default` (accesible dentro del mismo paquete), `private` (restringido a la propia clase).

#### 2. Ciclo de Vida del Objeto y Constructores
* **Instanciación:** `Clase objeto = new Clase(argumentos);`.
* **Constructores:**
  * Mismo nombre que la clase, sin tipo de retorno.
  * Uso de la palabra clave `this` para diferenciar el atributo del parámetro homónimo (`this.campo = campo`).
  * Sobrecarga: Constructor con todos los campos, constructor por defecto/vacío y constructores parciales.
  * Reinstanciación: Capacidad de sobreescribir una referencia existente con una nueva llamada a `new Constructor(...)` para actualizar o ampliar atributos.

#### 3. Encapsulamiento y Métodos
* **Getters y Setters:** Acceso y mutación controlada de atributos privados desde el exterior. Actúan funcionalmente como "variables expuestas" desde otras clases.
* **Diseño de métodos:** Un método debe retornar datos con `return` y no imprimir directamente con `System.out.println` salvo que sea explícitamente un método de visualización/reporte.
* **Paso de parámetros:**
  * **Por valor:** Tipos primitivos (se copia el valor).
  * **Por referencia:** Objetos (se comparte la referencia en memoria; el objeto debe instanciarse previamente antes de consumirse).

#### 4. Relaciones entre Clases
* **Asociación:** Conexión estructural entre clases.
  * **Unidireccional:** Solo una clase conoce a la otra.
  * **Bidireccional:** Ambas clases mantienen referencias cruzadas.
  * **Agregación:** Relación Todo-Partes donde las partes tienen ciclo de vida independiente del contenedor.
  * **Composición:** Relación fuerte donde la existencia de las partes está sujeta y controlada por la clase contenedora.
* **Dependencia:** Relación puntual de tipo "Cliente-Servidor" (un método recibe o invoca un objeto transitorio como servicio).

#### 5. Arrays de Objetos y Algoritmia Básica
* **Declaración e instanciación:** `Clase[] lista = new Clase[tam];`. Requiere instanciar cada posición de manera individual: `lista[i] = new Clase(...)`.
* **Representación en texto:** Sobreescritura del método `toString()` para evitar la impresión de direcciones de memoria.
* **Algoritmo de Búsqueda Secuencial por ID/Clave Primaria:** Recorrido con bucle `while` deteniéndose en cuanto se encuentra la coincidencia.
* **Modificación de datos:** Búsqueda previa del objeto por ID y posterior aplicación de su método `set` correspondiente.
* **Borrado lógico en arrays:** Dado que los arrays en Java no se pueden redimensionar ni eliminar posiciones físicamente, se implementa un atributo de estado booleano (ej. `activo` o `eliminado`) para marcar bajas lógicas.

> **Tags para IA:** `POO`, `Clases`, `Constructores`, `this`, `Getters y Setters`, `Asociación`, `Agregación`, `Composición`, `Arrays de Objetos`, `Búsqueda por ID`, `Borrado Lógico`, `toString`.

---

### TEMA 4: Herencia, Polimorfismo y Clases/Métodos Abstractos
* **Archivo de referencia:** `APUNTES TEMA 4.pdf`
* **Propósito:** Reutilización de código mediante jerarquías, contratos de abstracción y sellado de clases.

#### 1. Herencia en Java
* **Sintaxis:** `public class Subclase extends Superclase`.
* **Reglas:**
  * Java soporta herencia simple (una subclase solo hereda de su clase directa superior).
  * Se heredan atributos y métodos visibles; **los constructores no se heredan** (deben invocarse o redefinirse).
  * Las subclases pueden ampliar la clase madre agregando nuevos atributos y métodos.

#### 2. Modificador `final`
* **Aplicado a clases (`final class`):** Declara que la clase es la última de la jerarquía; no permite ser extendida (prohíbe subclases).
* **Aplicado a métodos (`final método()`):** Impide que el método sea reescrito/sobreescrito (`@Override`) en las clases hijas.

#### 3. Abstracción: Clases y Métodos Abstractos
* **Definición de Clase Abstracta (`abstract class`):**
  * Representa conceptos genéricos no instanciables directamente (`new Superclase()` está prohibido).
  * Su instanciación se delega exclusivamente a las clases hijas concretas.
  * Sí puede y debe tener constructores para permitir inicializar el estado común heredado por las hijas.
  * Sí permite la creación de colecciones/arrays basados en su tipo abstracto.
* **Métodos Abstractos (`abstract tipo metodo();`):**
  * Métodos que carecen de cuerpo/implementación `{}` en la clase madre.
  * **Obligatoriedad:** Toda subclase concreta está obligada a sobreescribirlos (`@Override`). Si una subclase no implementa un método abstracto heredado, debe declararse a su vez como `abstract`.
  * Una clase abstracta debe contener al menos un método abstracto.
* **Regla de incompatibilidad:** Una clase no puede ser simultáneamente `abstract` y `final`.

> **Tags para IA:** `Herencia`, `extends`, `final class`, `final method`, `Clases Abstractas`, `Métodos Abstractos`, `Sobreescritura`, `@Override`.

---

### TEMA 5 (Parte 1): API Collections, Genéricos y Mecanismos de Ordenación
* **Archivo de referencia:** `APUNTES TEMA 5.pdf`
* **Propósito:** Manejo de estructuras de datos dinámicas en memoria y algoritmos de comparación y ordenación.

#### 1. Convenciones de Genéricos en Java
* `<T>`: *Type* (Tipo principal).
* `<E>`: *Element* (Utilizado en colecciones).
* `<K>`: *Key* (Clave en mapas).
* `<V>`: *Value* (Valor en mapas).
* `<R>`: *Return* (Tipo de retorno).
* `<S>`, `<U>`: Segundo y tercer tipo de entrada/argumento.

#### 2. Interfaz `List<E>` e Implementaciones
* **Características:** Colección ordenada por índice posicional, admite duplicados y respeta orden de inserción.
* **Implementaciones:** `ArrayList<E>` y `LinkedList<E>`.
* **Métodos clave de `ArrayList`:**
  * `add(E elemento)`: Inserta al final.
  * `get(int index)`: Recupera por índice.
  * `set(int index, E elemento)`: Reemplaza en posición.
  * `remove(int index)`: Elimina por posición.
  * `clear()`: Vacía la lista.

#### 3. Interfaz `Set<E>`
* **Características:** Conjunto matemático sin duplicados y sin orden posicional garantizado (sin acceso por índice).
* **Implementación común:** `HashSet<E>`.
* **Consideraciones:** Para ordenar los datos de un `Set`, es necesario volcarlo previamente a una lista (`List`). Mención al método auxiliar inmutable `Collections.unmodifiableSet()`.

#### 4. Ordenación de Colecciones: `Comparable` vs `Comparator`
* **Orden Natural — Interfaz `Comparable<T>`:**
  * Se implementa directamente en la clase del objeto (*POJO*): `public class Alumno implements Comparable<Alumno>`.
  * Método a sobreescribir: `public int compareTo(Alumno o)`.
  * Retorno: Entero negativo ($< 0$), cero ($0$) o positivo ($> 0$).
  * Invocación: `Collections.sort(miLista);`.
* **Orden Alternativo / No Natural — Interfaz `Comparator<T>`:**
  * Se implementa en clases externas independientes por cada criterio de ordenación: `public class CompararPorMarca implements Comparator<Telefono>`.
  * Método a sobreescribir: `public int compare(Objeto o1, Objeto o2)`.
  * Invocación: `Collections.sort(miLista, new CompararPorMarca());`.

> **Tags para IA:** `Collections`, `List`, `ArrayList`, `Set`, `HashSet`, `Comparable`, `compareTo`, `Comparator`, `compare`, `Collections.sort`, `Generics`.

---

### TEMA 5 (Parte 2): Programación Funcional, Lambdas, Streams y Optional
* **Archivos de referencia:** `STREAM Y EXPRESIONES LAMBDA.pdf`, `STREAMS.pdf`
* **Propósito:** Paradigma declarativo, eliminación de clases anónimas repetitivas, canalización de datos y prevención de `NullPointerException`.

#### 1. Expresiones Lambda y SAM
* **Definición:** Funciones anónimas compactas equivalentes a clases que implementan un único método abstracto (SAM: *Single Abstract Method*). Marcadas con `@FunctionalInterface`.
* **Evolución:** Clase concreta $\rightarrow$ Clase Anónima $\rightarrow$ Lambda explícita `(Tipo x) -> { return res; }` $\rightarrow$ Lambda compacta `x -> res`.
* **Regla de variables locales:** Solo pueden leer variables externas si son declaradas como `final` o son *effectively final* (su valor no se altera tras inicializarse).

#### 2. Catálogo de Interfaces Funcionales (`java.util.function`)
* **`Supplier<T>`:** `() -> T`. Proveedor. No recibe argumentos y retorna un objeto de tipo $T$.
* **`Consumer<T>`:** `(T) -> void`. Consumidor. Recibe un objeto $T$ y no devuelve nada.
* **`Function<T, R>`:** `(T) -> R`. Transformador. Recibe un objeto $T$ y devuelve un resultado transformado $R$.
* **`Predicate<T>`:** `(T) -> boolean`. Filtro/Validador. Recibe un objeto $T$ y devuelve un booleano.
* **`BiFunction<T, U, R>`:** `(T, U) -> R`. Operación binaria con dos entradas y un retorno.

#### 3. Pipeline de Java Streams
* **Propiedades:** Flujos de elementos continuos, inmutables (no alteran la lista de origen) y de un solo uso (se cierran tras su consumo).
* **Generación:** `coleccion.stream()`.
* **Operaciones Intermedias (*Lazy*, retornan otro Stream):**
  * `filter(Predicate)`: Filtra elementos que cumplan la condición.
  * `map(Function)`: Aplica transformación elemento a elemento.
  * `mapToInt()` / `mapToDouble()`: Mapeo a flujos de datos primitivos para cálculos matemáticos.
  * `distinct()`: Elimina duplicados basándose en `.equals()`.
  * `sorted()`: Ordena por orden natural o comparator.
  * `limit(n)` y `skip(n)`: Paginación; toma o descarta los primeros $n$ elementos.
  * `peek(Consumer)`: Inspecciona elementos en tránsito para depuración.
* **Operaciones Terminales (Consumen y cierran el Stream):**
  * `forEach(Consumer)`: Itera ejecutando una acción sobre cada elemento.
  * `collect(Collectors.toList())` / `collect(Collectors.joining())`: Acumula el resultado en listas o cadenas estructuradas.
  * `count()`: Devuelve el número de elementos en formato `long`.
  * `anyMatch(Predicate)` / `allMatch(Predicate)`: Comprobaciones de existencia condicional (devuelven `boolean`).
  * `findFirst()`: Retorna el primer elemento envuelto en un `Optional`.
  * `reduce(...)`: Acumulación de todos los elementos en un único resultado escalar.
  * `min(...)` / `max(...)`: Obtiene los extremos según un comparador.

#### 4. Operador de Referencia a Método (`::`)
* Atajo sintáctico para enlazar métodos existentes a lambdas:
  * Métodos estáticos: `Clase::metodoEstatico`.
  * Métodos de instancia: `objeto::metodo` o `Tipo::metodo`.
  * Constructores: `Clase::new`.

#### 5. Clase `Optional<T>`
* **Propósito:** Manejo seguro de valores potencialmente nulos sin lanzar `NullPointerException` (actúa conceptualmente como una "caja contenedora").
* **Métodos principales:**
  * `Optional.ofNullable(valor)`: Crea el Optional con el valor o genera una caja vacía si es `null`.
  * `isPresent()`: Comprueba si contiene valor (`true`/`false`).
  * `ifPresent(Consumer)`: Ejecuta la acción solo si hay un valor presente.
  * `orElse(valorPorDefecto)`: Retorna el valor o una alternativa de respaldo.
  * `orElseThrow(...)`: Lanza una excepción si la caja está vacía.
  * `map(Function)`: Aplica una transformación sobre el valor si existe.
  * `Optional.empty()`: Retorna un contenedor vacío explícito.

> **Tags para IA:** `Lambdas`, `SAM`, `Effectively Final`, `Supplier`, `Consumer`, `Function`, `Predicate`, `Streams`, `filter`, `map`, `collect`, `reduce`, `Optional`, `Method Reference (::)`.