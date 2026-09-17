# GUÍA RÁPIDA Y SISTEMA DE ÍNDICE: BASES DE DATOS Y SQL (TEMAS 2, 3 Y TEORÍA RELACIONAL)

Este documento funciona como un **índice de acceso rápido y base de conocimiento estructurada** para consultas de Inteligencia Artificial y desarrolladores. Permite identificar de inmediato reglas conceptuales, diseño relacional, sintaxis SQL, funciones avanzadas y resolución de ejercicios prácticos.

---

## 🗺️ 1. Matriz de Enrutamiento Rápido ("¿Qué necesitas resolver?")

| Si necesitas saber sobre... | Consulta la Sección | Conceptos Clave Implicados |
| :--- | :--- | :--- |
| **Diseño Conceptual (E/R)** | Sección 2 | Entidades fuertes/débiles, atributos derivados/compuestos, reflexividad. |
| **Especialización / Generalización** | Sección 2.5 | Criterios (Total/Parcial, Exclusiva/Solapada) y simbología de triángulos/círculos. |
| **Conceptos del Modelo Relacional** | Sección 3.1 - 3.3 | Grado, cardinalidad, tuplas, dominios, tablas base, vistas y vistas materializadas. |
| **Teoría de Claves (Keys)** | Sección 3.4 | Superclave (SK), Clave Candidata (CK), Clave Primaria (PK), Clave Foránea (FK). |
| **Restricciones y Borrado** | Sección 3.5 - 3.6 | Restricciones inherentes vs semánticas, Integridad referencial, CASCADE, SET NULL. |
| **Clasificación de Comandos SQL** | Sección 4.1 | DDL (CREATE, ALTER...), DML (SELECT, INSERT...), DCL, TCL. |
| **Estructura y Orden de Ejecución SQL** | Sección 4.2 | Prioridad: `FROM` → `WHERE` → `GROUP BY` → `HAVING` → `ORDER BY`. |
| **Operadores y Filtros de Texto** | Sección 4.3 | `=`, `<>`, `BETWEEN`, `IN`, `LIKE` vs `ILIKE`, comodines (`%`, `_`). |
| **Agrupaciones y Cálculos** | Sección 4.4 | `GROUP BY`, `HAVING` vs `WHERE`, `COUNT(*)` vs `COUNT(col)`, `ROUND`. |
| **Lógica Condicional en SQL** | Sección 4.5 | `CASE WHEN ... THEN ... ELSE ... END`, compatibilidad de tipos. |
| **Manejo de Fechas y Textos** | Sección 4.6 | `make_date()`, `to_char()`, `extract()`, casteos `::text`, rangos temporales. |
| **Combinación de Tablas (JOINs)** | Sección 4.7 | `JOIN ... USING`, `JOIN ... ON`, auto-uniones (Self-Join). |
| **Snippets y Ejercicios Resueltos** | Sección 5 | Plantillas de demografía, meteorología, cálculo de descuentos y vuelos. |

---

## 📐 2. Modelo Conceptual (Diagrama Entidad-Relación y Jerarquías)

### 2.1. Entidades
*   **Entidad Fuerte:** Objeto del mundo real representado mediante rectángulos con existencia propia (ej. `Empleado`).
*   **Entidades Débiles:** Dependen de una entidad fuerte. Se dividen en:
    *   **Débil por Identificación:** No tiene atributos suficientes para formar su propia clave primaria; su identificador se compone de su clave parcial más la clave primaria de la entidad fuerte (comparten identificador).
    *   **Débil por Existencia:** Su existencia en el sistema carece de sentido si desaparece la entidad fuerte; no obstante, la clave de la fuerte no forma parte de su identificador.

### 2.2. Atributos
*   **Atributo Simple:** Característica elemental e indivisible (ej. `DNI`, `nombre`).
*   **Atributo Compuesto:** Agrupación jerárquica con fines organizativos (ej. `dirección` compuesta por `calle`, `número` y `ciudad`).
*   **Atributo Calculado / Derivado:** Valor que no se almacena físicamente en la base de datos para evitar redundancia e inconsistencias; se calcula dinámicamente a partir de otros datos (ej. `edad` derivada de `fecha_nacimiento`). Representado gráficamente con un **óvalo de trazo discontinuo**.

### 2.3. Relaciones y Cardinalidad
*   **Relación:** Asociación semántica entre dos o más entidades, representada con un rombo y etiquetada con un verbo. **Las relaciones pueden contener atributos propios**.
*   **Relación Reflexiva (Recursiva):** Una entidad se relaciona consigo misma (ej. un `Empleado` es responsable/jefe de otros `Empleado`s).
*   **Cardinalidad:** Rango de instancias mínimas y máximas asociadas `(min, max)` utilizando `0`, `1` o `N`.
    *   Tipos: Uno a uno (`1:1`), Uno a muchos (`1:N`), Muchos a muchos (`N:M`).
    *   *Regla de lectura:* Se lee proyectando la condición hacia la entidad opuesta.

### 2.4. Jerarquías de Especialización y Generalización
Relación jerárquica vertical: hacia arriba se generaliza (superclase/padre), hacia abajo se especializa (subclase/hijo). Se clasifica según dos ejes ortogonales:

1.  **Exclusividad:**
    *   **Exclusiva (Disjunta):** Una instancia padre solo puede pertenecer como máximo a una subclase hija.
    *   **Solapada:** Una instancia padre puede pertenecer simultáneamente a varias subclases hijas.
2.  **Cobertura:**
    *   **Total:** Toda instancia de la superclase debe pertenecer obligatoriamente a alguna de las subclases hijas.
    *   **Parcial:** Existen instancias de la superclase que no pertenecen a ninguna subclase hija.

### 2.5. Código Gráfico de Representación (Triángulos)
*   **Solapada y Parcial (Menos restrictiva):** Triángulo simple apuntando a las subclases hijas.
*   **Solapada y Total:** Triángulo con un **círculo sobre el vértice superior**.
*   **Exclusiva y Parcial:** Triángulo con un **arco/semicírculo inferior** que une las ramas que descienden a las hijas.
*   **Exclusiva y Total (Más restrictiva):** Triángulo con un **círculo en el vértice superior Y un arco/semicírculo inferior**.

---

## 🗄️ 3. Modelo Lógico-Relacional (Estructura y Reglas)

### 3.1. Elementos Estructurales
*   **Relación (Tabla):** Conjunto bidimensional de datos con nombre unívoco.
*   **Tupla (Fila):** Registro individual correspondiente a un hecho del mundo real.
*   **Atributo (Columna):** Característica nombrada de la relación.
*   **Dominio:** Conjunto finito de valores atómicos admisibles para un atributo (definido por nombre, tipo lógico y formato).
*   **Grado:** Número total de columnas (atributos) de una tabla.
*   **Cardinalidad:** Número total de filas (tuplas) de una tabla.

### 3.2. Tipos de Tablas
1.  **Tablas Persistentes:**
    *   **Tablas Base:** Tablas físicas primarias donde se insertan, actualizan y consultan los datos.
    *   **Vistas (Views):** Consultas guardadas con interfaz de tabla; no almacenan datos propios, sino que ejecutan la consulta sobre las tablas base subyacentes.
    *   **Vistas Materializadas:** Almacenan físicamente el resultado de la consulta además de la definición lógica, requiriendo refrescos periódicos.
2.  **Tablas Temporales:** Tablas volátiles activas durante la sesión o ejecución de cálculos transitorios.

### 3.3. Propiedades Fundamentales del Modelo
*   No pueden existir dos tuplas idénticas en la misma tabla.
*   El orden de las filas no es significativo.
*   El orden de las columnas no es significativo.
*   Atomicidad: cada celda (intersección fila-columna) almacena un único valor escalar.

### 3.4. Jerarquía y Tipos de Claves (Keys)
*   **Superclave (SK):** Cualquier atributo o conjunto de atributos que identifica unívocamente cada tupla en una tabla.
*   **Clave Candidata (CK):** Superclave mínima (irreducible); superclave de menor grado a la que si se le retira un atributo pierde la unicidad.
*   **Clave Primaria (PK):** Clave candidata seleccionada oficialmente para identificar registros. **Propiedades: inmutable, no anulable (NOT NULL) y única**.
*   **Clave Externa / Foránea (FK):** Atributo(s) en una tabla cuyos valores deben coincidir con la clave primaria de otra tabla (o ser nulos).

### 3.5. Restricciones de Integridad
*   **Restricciones Inherentes:** Intrínsecas al modelo relacional (unicidad de tuplas, atomicidad de datos, irrelevancia del orden).
*   **Restricciones Semánticas (Reglas de negocio):**
    1.  **Unicidad (`UNIQUE`):** Impide valores repetidos en atributos secundarios.
    2.  **Obligatoriedad (`NOT NULL`):** Prohíbe valores nulos en el campo.
    3.  **Integridad Referencial:** Prohíbe la existencia de claves foráneas huérfanas que apunten a registros padres inexistentes.
    4.  **Validación (`CHECK`):** Evaluación de condiciones booleanas sobre las columnas.
    5.  **Disparadores (`TRIGGERS`):** Procedimientos automáticos disparados por eventos de base de datos.

### 3.6. Políticas de Borrado Referencial
Determinan la acción sobre las filas hijas cuando se elimina la fila padre referenciada:
*   `CASCADE` (Cascada): Si se borra el padre, se eliminan automáticamente todos los registros hijos asociados (útil para detalles dependientes o tablas débiles).
*   `SET NULL`: Si se borra el padre, la clave foránea en la tabla hija pasa a valor `NULL` (adecuado cuando el registro hijo debe preservarse por motivos históricos, ej. un préstamo donde el bibliotecario cesa).
*   `RESTRICT` / `NO ACTION`: Se prohíbe la eliminación del padre mientras existan filas hijas asociadas.

---

## ⚡ 4. SQL en PostgreSQL: Manual Técnico de Referencia

### 4.1. Taxonomía de Comandos
*   **DDL (Data Definition Language):** Creación y modificación de esquemas (`CREATE`, `ALTER`, `DROP`, `TRUNCATE`).
*   **DML (Data Manipulation Language):** Manipulación y consulta de datos (`SELECT`, `INSERT`, `UPDATE`, `DELETE`).
*   **DCL (Data Control Language):** Permisos y control de seguridad (`GRANT`, `REVOKE`).
*   **TCL (Transaction Control Language):** Gestión de transacciones atómicas (`COMMIT`, `ROLLBACK`, `SAVEPOINT`).

### 4.2. Estructura y Prioridad de Ejecución de Cláusulas
Una sentencia SQL sigue un orden estricto de resolución lógica interna:
```
FROM  →  WHERE  →  GROUP BY  →  HAVING  →  ORDER BY
```
1.  **`FROM`**: Identifica las tablas base y resuelve los `JOIN`.
2.  **`WHERE`**: Filtra filas individuales antes de cualquier agregación.
3.  **`GROUP BY`**: Agrupa las filas resultantes en función de campos de agrupación.
4.  **`HAVING`**: Filtra los grupos calculados en base a condiciones sobre funciones agregadas.
5.  **`ORDER BY`**: Ordena el conjunto final de registros (`ASC` por defecto, `DESC` para descendente).

### 4.3. Operadores de Comparación, Filtros y Lógica
*   Comparación estándar: `=`, `<>`, `>`, `<`, `>=`, `<=`.
*   Rangos y pertenencia: `BETWEEN valor1 AND valor2`, `IN (val1, val2, ...)`.
*   Coincidencia de patrones:
    *   `LIKE`: Sensible a mayúsculas/minúsculas. Comodines: `%` (múltiples caracteres), `_` (un único carácter).
    *   `ILIKE`: Específico de PostgreSQL; insensible a mayúsculas y minúsculas (insensitivo).
*   **Trampa del Lenguaje Natural:** Enunciados como *"artículos de la sección deporte y cerámica"* requieren el operador lógico `OR` en SQL (`WHERE seccion = 'Deportes' OR seccion = 'Ceramica'`), ya que un único campo no puede tener dos valores a la vez.

### 4.4. Consultas de Agrupación y Funciones de Agregado
Requiere dos tipos de columnas en el `SELECT`:
1.  **Campo de agrupación:** Indicado explícitamente en la cláusula `GROUP BY`.
2.  **Campo de cálculo:** Envuelto en funciones de agregación (`AVG`, `SUM`, `MAX`, `MIN`, `COUNT`).
*   *Comportamiento de NULLs:* `COUNT(columna)` ignora los valores nulos; `COUNT(*)` cuenta todas las filas.
*   *Redondeo numérico:* `ROUND(AVG(precio), 2)` redondea a dos cifras decimales.
*   *Diferencia Clave:*
    *   `WHERE`: Descarta filas antes de agrupar.
    *   `HAVING`: Descarta grupos después de computar las funciones de agregado.

### 4.5. Lógica Condicional: Expresión CASE WHEN
Estructura condicional evaluada en línea que genera un valor escalar:
```sql
CASE
    WHEN condicion_1 THEN resultado_1
    WHEN condicion_2 THEN resultado_2
    ELSE resultado_defecto
END
```
**Reglas Obligatorias:**
*   Todos los bloques `THEN` y el bloque opcional `ELSE` **deben retornar el mismo tipo de dato** (o compatibles mediante casteo).
*   No se pueden invocar alias definidos en la misma cláusula `SELECT` dentro de la expresión `CASE`.
*   Puede utilizarse en `SELECT`, `WHERE`, `ORDER BY` y en el interior de funciones de agregado.

### 4.6. Manejo Técnico de Fechas y Cadenas en PostgreSQL
*   Construcción segura de fechas: `make_date(año, mes, dia)` (ej. `make_date(2019, 4, 1)`).
*   Formateo de salida: `to_char(fecha, 'DD/MM/YYYY')` o `to_char(fecha, 'DAY, DD/MM/YYYY')`.
*   Extracción de partes temporales: `extract(month from hire_date)`.
*   Casteos directos: `fecha::text`, `substr(fecha::text, 1, 4)`.
*   *Mejor práctica para rangos mensuales:* Usar desigualdades semiabiertas (`fecha >= '2019-04-01' AND fecha < '2019-05-01'`) en lugar de calcular la duración exacta del mes.

### 4.7. Combinación de Tablas (JOINs)
*   **`JOIN ... USING (columna_clave)`:** Se utiliza cuando el atributo común de unión se llama exactamente igual en ambas tablas.
*   **`JOIN ... ON tablaA.id = tablaB.id_fk`:** Se utiliza cuando los nombres de columna difieren o se aplican condiciones lógicas compuestas.
*   **Self-Join (Auto-unión):** Unión de una tabla consigo misma mediante el uso obligatorio de alias distintos (típico para jerarquías como empleados y sus supervisores):
    ```sql
    SELECT e.first_name AS empleado, m.first_name AS manager
    FROM employees e
    JOIN employees m ON e.manager_id = m.employee_id;
    ```

---

## 🛠️ 5. Catálogo de Patrones SQL y Ejemplos de Examen

### Patrón 1: Clasificación de rangos y etiquetas de texto con `CASE WHEN`
```sql
SELECT id, desde, hasta, precio,
    CASE
        WHEN descuento IS NULL OR descuento = 0 THEN 'Sin_Descuento'
        WHEN descuento >= 30 THEN 'Descuento_Alto'
        ELSE 'Descuento_Bajo'
    END AS tipo_descuento
FROM vuelos
WHERE salida::text ILIKE '2020-03%'
  AND precio BETWEEN 60 AND 300;
```

### Patrón 2: Formateo con ceros a la izquierda (Zero Padding) y concatenación
```sql
SELECT CONCAT(
    SUBSTR(desde, 1, 3),
    SUBSTR(hasta, 1, 3),
    ' ',
    CASE
        WHEN id < 10 THEN CONCAT('000', id::text)
        WHEN id < 100 THEN CONCAT('00', id::text)
        WHEN id < 1000 THEN CONCAT('0', id::text)
        ELSE id::text
    END
) AS codigo_ruta
FROM vuelos;
```

### Patrón 3: Cálculo de porcentajes ponderados evitando división por cero
```sql
SELECT fecha, estacion, provincia, precipitacion_total,
    ROUND(
        CASE
            WHEN precipitacion_total > 0 THEN (precipitacion_0_a_6 / precipitacion_total * 100)
            ELSE 0
        END, 2
    ) AS porc_precipitacion_0_a_6
FROM climatologia
WHERE fecha >= '2019-03-21' AND fecha < '2019-06-21';
```

### Patrón 4: JOINs encadenados a través de múltiples niveles jerárquicos
```sql
SELECT d.first_name AS hijo, e.first_name AS padre, r.region_name AS region
FROM dependents d
JOIN employees e USING (employee_id)
JOIN departments dep USING (department_id)
JOIN locations l USING (location_id)
JOIN countries c USING (country_id)
JOIN regions r USING (region_id)
WHERE r.region_name = 'Americas'
ORDER BY c.country_name;