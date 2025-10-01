
# 2. IDE: Eclipse.

## **1. Introducción**

El código en Java se puede escribir en cualquier editor de texto y, para compilarlo a **bytecodes**, basta con instalar la versión del **JDK** correspondiente. Sin embargo, escribir y compilar programas de esta forma resulta incómodo, ya que obliga a gestionar manualmente la compilación y la ejecución desde la línea de comandos.

Por ello surgieron los **IDE (Integrated Development Environment)** o entornos de desarrollo integrados, que consisten básicamente en un editor de código, un compilador y un depurador, además de otras herramientas.

**Ventajas principales de un IDE:**

* Facilidades para escribir código: coloreado de palabras clave, autocompletado, sugerencias de corrección, uso de abreviaturas.
* Herramientas de depuración, para detectar y corregir errores durante la ejecución.
* Facilidad de configuración del sistema y de integración con librerías externas.
* Organización estructurada de los proyectos y sus archivos.
* Exportación e importación sencilla de proyectos.

Algunos IDEs muy utilizados para programar en Java son **Eclipse**, **NetBeans** e **IntelliJ IDEA**.

En esta asignatura utilizaremos **Eclipse**, que puede descargarse desde la página oficial:  
👉 [https://www.eclipse.org/downloads/eclipse-packages/](https://www.eclipse.org/downloads/eclipse-packages/)

Se recomienda instalar la versión más reciente de **Eclipse IDE for Java Developers**, escogiendo la del sistema operativo correspondiente.

Una vez instalado, es importante definir en Eclipse la versión del compilador de Java:

* `Window → Preferences → Java → Compiler` → seleccionar la versión de JDK deseada.
* `Window → Preferences → Java → Installed JREs` → marcar la versión como predeterminada.

Además, el alumno puede personalizar la apariencia del entorno:

* `Window → Preferences → General → Appearance → Theme`, seleccionando un tema oscuro o claro según preferencias.

---

## **2. Workspace**

Al iniciarse, Eclipse solicita la selección de un **workspace**, es decir, el directorio que funcionará como área de trabajo donde se guardarán todos los proyectos.

* Se puede aceptar la ruta predeterminada o establecer otra distinta.
* Es posible mantener **varios workspaces** para proyectos de distinta naturaleza.

Para cambiar de área de trabajo:
👉 `File → Switch Workspace → Other`.

---

## **3. UTF-8**

**UTF-8** *(Unicode Transformation Format-8)* es un formato de codificación de caracteres en el que cada carácter se representa mediante una 
secuencia de entre **1 y 4 bytes**. Los caracteres ASCII básicos (como letras, números y símbolos comunes) se codifican con un único byte (8 bits), 
mientras que otros caracteres Unicode más complejos (acentos, símbolos especiales, alfabetos no latinos) pueden necesitar 2, 3 o 4 bytes.

También existen otras variantes como **UTF-16** y **UTF-32**. La ventaja de UTF-8 respecto a estas es que resulta más eficiente cuando se 
trabaja con textos que contienen principalmente caracteres ASCII y, además, es compatible con versiones anteriores de ASCII.

**Características principales de UTF-8:**

* Representa cualquier carácter Unicode.
* Longitud variable (1 a 4 bytes por carácter).
* Compatible con US-ASCII de 7 bits: cualquier texto ASCII se representa sin cambios.
* Evita ambigüedades: la secuencia de bytes de un carácter no puede confundirse con parte de otro carácter.

**Cómo configurar Eclipse en UTF-8:**

* `Window → Preferences → General → Workspace → Text file encoding → UTF-8`.
* También puede configurarse por proyecto en `Project → Properties → Resource → Text file encoding → UTF-8`.

**Ejemplos de codificación UTF-8**

| Carácter | Descripción            | Bytes en UTF-8 | Hexadecimal   | Binario (bits)                        |
| -------- | ---------------------- | -------------- | ------------- | ------------------------------------- |
| `A`      | Letra ASCII básica     | 1 byte         | `41`          | `01000001`                            |
| `ñ`      | Letra latina acentuada | 2 bytes        | `C3 B1`       | `11000011 10110001`                   |
| `€`      | Símbolo del euro       | 3 bytes        | `E2 82 AC`    | `11100010 10000010 10101100`          |
| 😀       | Emoji (cara sonriente) | 4 bytes        | `F0 9F 98 80` | `11110000 10011111 10011000 10000000` |

---

## **4. Editores, vistas y perspectivas**

La interfaz de usuario de **Eclipse** se organiza en torno a **editores**, **vistas** y **perspectivas**:

* Un **editor** es la parte de la interfaz que permite crear, modificar y guardar archivos (por ejemplo, el editor de código Java).
* Una **vista** es una ventana auxiliar que muestra información adicional o permite realizar tareas de apoyo (ejemplo: la consola, el explorador de paquetes, las variables en depuración).
* Una **perspectiva** es una disposición o agrupación de editores y vistas diseñada para apoyar una tarea completa del proceso de desarrollo.

### Perspectivas principales en Eclipse

* **Java**: diseñada para trabajar con proyectos Java (muestra el editor de código, el explorador de paquetes, la consola, etc.).
* **Debug**: enfocada en la depuración de programas (muestra vistas como Variables, Breakpoints, Consola, etc.).

Estas perspectivas se pueden abrir en:
👉 `Window → Perspective → Open Perspective`
o desde los botones de la **barra de perspectivas** en la esquina superior derecha de la interfaz.

Además, el usuario puede personalizar una perspectiva (añadir/quitar vistas, reorganizar paneles) y guardarla en:
👉 `Window → Perspective → Save Perspective As`.

Las vistas también se pueden abrir directamente en:
👉 `Window → Show View`.
Por ejemplo, la **Consola** se abre en `Window → Show View → Console`.

---

## **5. Package Explorer**

En la columna izquierda de la interfaz suele encontrarse la vista **Package Explorer** (Explorador de Paquetes).

Esta vista muestra la **estructura de proyectos, paquetes y clases Java** que forman parte del área de trabajo (workspace). Permite navegar fácilmente por los archivos de un proyecto, abrir clases en el editor y gestionar recursos.

Al ser una vista, puede abrirse también en:
👉 `Window → Show View → Package Explorer`.

---

## **6. CamelCase**

**CamelCase** es un estilo de escritura utilizado en programación para nombrar identificadores compuestos (clases, métodos, variables). Consiste en unir varias palabras y escribir la primera letra de cada palabra en mayúscula (excepto, en ocasiones, la primera).

El nombre se debe a que las mayúsculas intermedias recuerdan a las “jorobas” de un camello 🐪.

Existen dos variantes:

* **UpperCamelCase (PascalCase):** la primera letra de cada palabra va en mayúscula.
  👉 Ejemplo: `PrimerPrograma`, `EjemploDeUpperCamelCase`.
* **lowerCamelCase:** igual que la anterior, pero la primera palabra empieza en minúscula.
  👉 Ejemplo: `primerPrograma`, `ejemploDeLowerCamelCase`.

La notación CamelCase se usa en muchos lenguajes de programación, incluido **Java**:

* **Clases e interfaces** → `UpperCamelCase` (`MiClase`, `CalculadoraSimple`).
* **Variables y métodos** → `lowerCamelCase` (`contador`, `sumarNumeros()`).

---

## **7. Proyectos, paquetes y clases**

### Proyectos

Un **proyecto Java** en Eclipse puede considerarse como una carpeta organizada que contiene todo lo necesario para desarrollar una aplicación.
Un proyecto incluye:

* Archivos **.java** (código fuente).
* Archivos **.class** (código compilado en bytecode).
* Documentación y otros recursos asociados (imágenes, librerías, etc.).

Cuando se crea un proyecto Java en Eclipse, este se guarda en el **workspace** y genera por defecto dos subcarpetas:

* **src** (source): contiene los archivos `.java` organizados en paquetes.
* **bin** (binary): contiene los archivos `.class` generados al compilar el código.

---

### Paquetes

Los **paquetes** permiten organizar las clases dentro de la carpeta `src`.

* Un paquete se corresponde con una **subcarpeta** en `src`.
* Dentro de cada clase Java se debe indicar al inicio el paquete al que pertenece con la palabra clave `package`.

Ejemplo con clase en un paquete:

```java
package tema1_1_IntroduccionAlLenguajeJava; // Especificación del paquete

public class Integers {
    public static void main(String[] args) {
        // código...
    }
}
```

Si la clase está en el **paquete por defecto** (`default package`), se guarda directamente en `src` y no aparece ninguna declaración `package` en el código:

```java
// Clase en el default package
public class Integers {
    public static void main(String[] args) {
        // código...
    }
}
```

👉 Aunque Eclipse permite el default package, **no se recomienda** en proyectos grandes porque dificulta la organización.

---

### Clases

Las **clases** son los archivos `.java` que contienen el código fuente. Cada clase debe tener un nombre que siga la notación **UpperCamelCase** (primera letra de cada palabra en mayúscula).

Ejemplo: `PrimerPrograma`, `CalculadoraSimple`.

---

### Operaciones en Eclipse

**Crear un proyecto Java**

1. Menú `File → New → Java Project`.
2. En **Project name**, escribir el nombre del proyecto (conviene que empiece en mayúscula).
3. Desactivar la opción *Create module-info.java file* (no se usará en este módulo).
4. Pulsar *Finish*.

⚠️ Nota: si el proyecto ya existe en el workspace, Eclipse lo abrirá con todos los datos guardados previamente.

---

**Borrar un proyecto**

1. Seleccionar el proyecto en el **Package Explorer**.
2. Botón derecho → `Delete`.
3. Eclipse preguntará si quieres borrarlo solo del explorador o también físicamente del workspace.

---

**Crear un paquete**

1. En **Package Explorer**, situarse sobre el proyecto o sobre su carpeta `src`.
2. Botón derecho → `New → Package`.
3. Escribir el nombre (todo en minúsculas, se permiten números y `_` pero no caracteres especiales).

   * Ejemplo: `tema1_1`.
4. Pulsar *Finish*.

---

**Crear una clase**

1. En **Package Explorer**, situarse sobre el paquete donde se quiere crear.
2. Botón derecho → `New → Class`.
3. En **Name**, escribir el nombre de la clase (usar UpperCamelCase).
4. Si se quiere que sea ejecutable, marcar la casilla **public static void main(String[] args)**.
5. Pulsar *Finish*.

---

¡Perfecto, Diego! 🙌 He reescrito el apartado **8. Build Path** integrando todo lo que hemos hablado: la definición del Build Path, la importancia del JRE, la relación JDK–JRE–JVM y cómo configurarlo en Eclipse. Te lo dejo como un bloque completo para tu material:

---

## **8. Build Path**

El **Build Path** (ruta de compilación) en Eclipse define **qué necesita un proyecto para compilarse y ejecutarse correctamente**.
Incluye:

* La carpeta de **código fuente** (`src`, con los archivos `.java`).
* La carpeta de **clases compiladas** (`bin`, con los archivos `.class`).
* Las **librerías necesarias** (por ejemplo, el JRE de Java o archivos JAR externos).

### 8.1. ¿Qué es el JRE System Library?

Todo proyecto Java necesita tener asociada la librería básica del lenguaje: **JRE System Library**.
Esta librería contiene las clases fundamentales de Java, como:

* `String`
* `System`
* `ArrayList`
* `Scanner`
* …y muchas más de la API estándar.

👉 Si un proyecto no tiene asignada esta librería, Eclipse marcará errores incluso en instrucciones tan simples como `System.out.println()` porque no sabrá dónde encontrar esas clases.

### 8.2. Relación JDK – JRE – JVM

Cuando instalamos **Java** en nuestro ordenador, lo que realmente descargamos es el **JDK (Java Development Kit)**.

El JDK incluye:

* **Compilador** (`javac`), para traducir `.java` → `.class`.
* **Herramientas de desarrollo** (javadoc, jar, debugger, etc.).
* **JRE (Java Runtime Environment)**, que a su vez contiene:

  * La **JVM (Java Virtual Machine)**, que ejecuta el bytecode en cualquier sistema.
  * La **biblioteca estándar de clases de Java** (colecciones, E/S, utilidades, etc.).

Por tanto, cuando en Eclipse añadimos la **JRE System Library** al Build Path, en realidad le estamos diciendo:
👉 “Este proyecto usará la librería estándar incluida en el JDK que tienes instalado.”

### 8.3. Configurar el Build Path en Eclipse

1. Seleccionar el proyecto en el **Package Explorer**.
2. Botón derecho → `Build Path → Configure Build Path`.
3. En la pestaña **Libraries**, comprobar si ya aparece la **JRE System Library**.

   * Si no aparece o quieres cambiar la versión:

     * Clic en **Add Library → JRE System Library**.
     * Selecciona usar el **Workspace default JRE** (el que configuraste en `Window → Preferences → Java → Installed JREs`) o bien otro JDK instalado en tu equipo.
4. Pulsar *Finish*.

Además del JRE, en esta misma pestaña se pueden añadir **librerías externas** (Add External JARs) que el proyecto necesite, como frameworks o APIs adicionales.

---

## **9. Importar en Eclipse**

En Eclipse, **importar** significa traer al workspace elementos ya existentes (clases, paquetes o proyectos) para poder trabajar con ellos dentro del IDE.

### 🔹 Importar clases sueltas

Si tenemos archivos `.java` creados previamente y queremos añadirlos a un paquete existente:

1. En el **Package Explorer**, situarse encima del paquete donde se van a importar las clases.
2. Botón derecho → `Import`.
3. `General → File System → Next`.
4. En **From Directory**, pulsar *Browse* y seleccionar la carpeta donde están las clases.
5. Marcar las clases que se quieren importar → *Finish*.

👉 Nota:

* Si marcas la opción **Create top-level folder**, Eclipse crea también la carpeta de origen como paquete dentro de `src`. Esto es útil si quieres que las clases mantengan el mismo paquete original.

---

### 🔹 Importar paquetes completos

Si quieres traer paquetes ya creados (con sus clases dentro):

1. En el **Package Explorer**, situarse encima de `src`.
2. Botón derecho → `Import`.
3. `General → File System → Next`.
4. Seleccionar en **From Directory** la carpeta donde están los paquetes.
5. Marcar los paquetes deseados → *Finish*.

👉 Resultado: Eclipse creará esos paquetes dentro de `src` y colocará dentro las clases correspondientes.

---

### 🔹 Importar proyectos completos

Si ya existe un proyecto creado en otro workspace o en otra carpeta:

1. Si el proyecto no existe todavía en tu workspace, puedes crearlo primero con el mismo nombre (vacío).
2. En el **Package Explorer**, botón derecho → `Import`.
3. `General → File System → Next`.
4. En **From Directory**, seleccionar la carpeta raíz del proyecto.
5. Selecciona el proyecto entero y pulsa *Finish*.
6. Si Eclipse pregunta “¿Sobrescribir archivos?”, normalmente se elige **No to All** para evitar reemplazar lo que ya exista en el workspace.

👉 Consejo: en lugar de `File System`, para proyectos completos es más cómodo usar:

* `File → Import → Existing Projects into Workspace`.
  Así Eclipse detecta automáticamente el proyecto (con su `.project` y `.classpath`) y lo añade tal cual al workspace.

---

## **10. Mi primer programa en Java**

```java
package tema2_Eclipse;

public class MyFirstProgramme {

    public static void main(String[] args) {
        System.out.println("¡Mi primer programa!");
    }

}
```

Este programa muestra por pantalla el texto **¡Mi primer programa!**.

### Explicación del código:

* `public class MyFirstProgramme`: declara la clase pública llamada `MyFirstProgramme`.
  ⚠️ El nombre del archivo debe coincidir exactamente con el de la clase (`MyFirstProgramme.java`).
* `public static void main(String[] args)`: es el **método principal**. Todo programa en Java comienza su ejecución en el `main`.
* `System.out.println("¡Mi primer programa!");`: instrucción que escribe un texto en pantalla. Como se trata de una cadena, debe ir entre comillas.

👉 En Eclipse existen **plantillas de código** que facilitan escribir instrucciones repetitivas. La más común es:

* Escribir `sysout` → pulsar `Ctrl + Espacio` → Eclipse lo reemplaza por `System.out.println();`.
  Además de `sysout`, existen muchas otras plantillas e incluso se pueden crear nuevas.

---

## **11. Cambiar el nombre a los elementos de Java**

Al renombrar manualmente una clase, método o variable, podemos romper el programa si ese nombre aparece en varios lugares. Para evitarlo, Eclipse ofrece la herramienta de **refactorización**:

* Seleccionar el elemento (clase, variable, método, etc.).
* Botón derecho → `Refactor → Rename` (o pulsar **Alt+Shift+R**).
* Eclipse cambiará el nombre automáticamente en todos los sitios donde se use.

👉 Si se trata de una **clase**, también se renombra el archivo `.java` correspondiente y viceversa.

---

## **12. Escritura de programas en Java**

Al escribir programas en Java hay que tener en cuenta:

* Los archivos de código fuente terminan en `.java`.
* Java distingue entre **mayúsculas y minúsculas** (`Variable` ≠ `variable`).
* Cada instrucción debe terminar con `;`.
* Una instrucción puede ocupar varias líneas, y es válido usar espacios o tabuladores para mejorar la legibilidad.

### Comentarios en Java:

Los comentarios son anotaciones ignoradas por el compilador y sirven para explicar el código:

* **Una sola línea:**

  ```java
  // Comentario de una línea
  ```
* **Varias líneas:**

  ```java
  /* Comentario
     de varias líneas */
  ```

👉 Los comentarios deben aportar claridad, sobre todo en código complejo. La legibilidad es clave para el mantenimiento de una aplicación.

---

## **13. Comentarios en Eclipse**

Algunas configuraciones útiles:

* Cuando se crea una clase, Eclipse genera un comentario por defecto. Esto se configura en:
  `Window → Preferences → Java → Code Style → Code Templates → Code → Method Body → Edit`.
* Para desactivar la corrección ortográfica en los comentarios (que a veces subraya palabras técnicas):
  `Window → Preferences → General → Editors → Text Editors → Spelling → deshabilitar "Enable Spell Checking"`.
* Para comentar o descomentar rápidamente un bloque de código:

  * Seleccionarlo y pulsar **Ctrl + Shift + C** o **Ctrl + 7**.

---

## **14. Dar formato al código**

En Java, el código se organiza en **bloques** delimitados por llaves `{ ... }`. Para mejorar la legibilidad se utiliza la **indentación** (sangrado), moviendo el código hacia la derecha dentro de cada bloque.

Ejemplo sin formatear:

```java
public static void main(String[] args) {
        int x=3;
    System.out.print("Este código no está");
System.out.print(" muy bien ");
            System.out.print("tabulado");
  x=7;
}
```

Ejemplo formateado automáticamente en Eclipse:

```java
public static void main(String[] args) {
    int x = 3;
    System.out.print("Este código no está");
    System.out.print(" muy bien ");
    System.out.print("tabulado");
    x = 7;
}
```

### Cómo dar formato al código en Eclipse:

* Pulsar **Ctrl + Shift + F**.
* O bien: `Menú Source → Format` o `Botón derecho → Source → Format`.

Además, Eclipse permite configurar el estilo de formateo:

* `Window → Preferences → Java → Code Style → Formatter`.
* Crear un nuevo perfil y editar opciones como:

  * Desactivar *Enable block comment formatting* (para que no toque los comentarios de varias líneas).
  * Desactivar *Enable line comment formatting* (para que no toque los comentarios de una sola línea).

---

