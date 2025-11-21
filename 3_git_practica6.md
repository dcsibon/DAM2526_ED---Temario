
# Práctica 6: Entendiendo `git revert` (deshacer cambios sin borrar historia)

## 🎯 Objetivo

Comprender cómo funciona el comando:

```bash
git revert <id_commit>
```

y ver que:

* **no borra** commits antiguos,
* crea un **nuevo commit** que “deshace” otro,
* se puede revertir el **último commit** o uno **más antiguo**,
* puede producir conflictos si el código ha cambiado mucho.

Todo se realiza **en local**, en una única rama (`main`).

---

## 0️⃣ Preparación inicial – Crear el repositorio

1. Crea una carpeta para la práctica y entra en ella:

```bash
mkdir pruebaRevert
cd pruebaRevert
```

2. Inicializa el repositorio Git:

```bash
git init
```

3. Comprueba el estado:

```bash
git status
```

---

## 1️⃣ Crear 3 versiones del fichero `notas.txt` (commits A, B y C)

Vamos a crear un archivo de texto y hacer **3 commits** que lo vayan modificando.

---

### 🔹 Commit A — Versión inicial

Crea el fichero `notas.txt` con este contenido:

```text
Línea 1: Versión inicial
Línea 2: Texto original
```

Confirma:

```bash
git add notas.txt
git commit -m "A: Versión inicial"
```

---

### 🔹 Commit B — Modificar la línea 2

Edita `notas.txt` para que quede:

```text
Línea 1: Versión inicial
Línea 2: Texto modificado en B
```

Confirma:

```bash
git add notas.txt
git commit -m "B: Cambiada la línea 2"
```

---

### 🔹 Commit C — Añadir una línea nueva

Edita `notas.txt`:

```text
Línea 1: Versión inicial
Línea 2: Texto modificado en B
Línea 3: Añadida en el commit C
```

Confirma:

```bash
git add notas.txt
git commit -m "C: Añadida la línea 3"
```

---

### 🔍 Ver historial inicial

```bash
git log --oneline --graph --all
```

Deberías ver algo parecido a:

```text
* cccccc C: Añadida la línea 3
* bbbbbb B: Cambiada la línea 2
* aaaaaa A: Versión inicial
```

Y el archivo actual:

```bash
cat notas.txt
```

Debe mostrar las 3 líneas.

---

## 2️⃣ Revertir el último commit (revert de C)

Vamos a deshacer el último commit **C**, pero sin borrar su existencia del historial.

### 2.1 Ejecutar `git revert C`

1. Localiza el identificador de C (`cccccc`) con:

```bash
git log --oneline
```

2. Ejecuta:

```bash
git revert cccccc
```

Git abrirá el editor de mensajes de commit (o usará uno por defecto) y creará un nuevo commit que “deshace” C.

---

### 2.2 Analizar el resultado

#### a) Historial

```bash
git log --oneline --graph --all
```

Deberías ver algo como:

```text
* dddddd Revert "C: Añadida la línea 3"
* cccccc C: Añadida la línea 3
* bbbbbb B: Cambiada la línea 2
* aaaaaa A: Versión inicial
```

👉 Fíjate:
C **sigue existiendo** en el historial, pero ahora hay un commit nuevo (“Revert C”) que deshace sus cambios.

---

#### b) Contenido del archivo

```bash
cat notas.txt
```

Deberías ver ahora:

```text
Línea 1: Versión inicial
Línea 2: Texto modificado en B
```

👉 El archivo ha vuelto al estado anterior a C,
pero **el historial no ha desaparecido**, solo hemos añadido un commit que “revierte” C.

---

## 3️⃣ Revertir un commit antiguo (revert de B)

Ahora vamos a deshacer un commit que **no es el último**: el commit B.

### 3.1 Localizar el commit B

```bash
git log --oneline
```

Identifica el SHA de B (`bbbbbb`).

En este momento:

* El archivo está así (después de revertir C):

  ```text
  Línea 1: Versión inicial
  Línea 2: Texto modificado en B
  ```

* Y el historial contiene A, B, C y el revert de C.

---

### 3.2 Ejecutar `git revert B`

```bash
git revert bbbbbb
```

Git creará **otro commit nuevo** que deshace los cambios del commit B.

---

### 3.3 Analizar el resultado

#### a) Historial

```bash
git log --oneline --graph --all
```

Verás algo similar a:

```text
* eeeeee Revert "B: Cambiada la línea 2"
* dddddd Revert "C: Añadida la línea 3"
* cccccc C: Añadida la línea 3
* bbbbbb B: Cambiada la línea 2
* aaaaaa A: Versión inicial
```

👉 Observa:

* Ni B ni C han desaparecido.
* Simplemente hemos creado commits nuevos que “los deshacen”.

---

#### b) Contenido del archivo

```bash
cat notas.txt
```

Debería volver a:

```text
Línea 1: Versión inicial
Línea 2: Texto original
```

Es decir, prácticamente el estado del commit A, **pero A no se ha repetido**, y B y C siguen estando en la historia.

---

## 4️⃣ Comparación con reset (reflexión guiada)

Puedes comentar en clase (o poner como reflexión escrita):

1. Con `reset`, movíamos la rama hacia atrás y **podíamos borrar commits de la historia**.
2. Con `revert`, **no se borra nada**:

   * La historia se mantiene,
   * solo se añaden commits que deshacen cambios anteriores.

Pregunta tipo:

> ¿Por qué `revert` es más seguro que `reset --hard` cuando ya hemos hecho `push` a GitHub?

Respuesta orientativa:

* Porque `revert` no reescribe la historia, solo añade commits nuevos.
* Los demás compañeros no pierden su referencia de la historia.
* Se puede usar después de hacer `push` sin romper el repositorio remoto.

---

## 5️⃣ (Opcional avanzado) Ver un revert con conflicto

Este bloque es **opcional** y sirve para ver que `revert` también puede generar conflictos.

### 5.1 Preparar la situación

Partimos de este estado en el archivo (después de los reverts anteriores):

```text
Línea 1: Versión inicial
Línea 2: Texto original
```

Haz ahora un nuevo commit D modificando otra vez la línea 2:

1. Edita `notas.txt`:

```text
Línea 1: Versión inicial
Línea 2: Texto cambiado en el commit D
```

2. Confirma:

```bash
git add notas.txt
git commit -m "D: Cambio nuevo en la línea 2"
```

---

### 5.2 Intentar revertir otra vez B

Ahora intenta esto:

```bash
git revert bbbbbb
```

(Si B está muy atrás y sus cambios no se encuentran tal cual, es posible que Git **no pueda aplicar el parche inverso sin ayuda**.)

Si se produce un conflicto, Git lo indicará:

```text
CONFLICT (content): Merge conflict in notas.txt
```

El archivo contendrá algo como:

```text
<<<<<<< HEAD
Línea 1: Versión inicial
Línea 2: Texto cambiado en el commit D
=======
Línea 1: Versión inicial
Línea 2: Texto modificado en B
>>>>>>> bbbbbb B: Cambiada la línea 2
```

Tendrás que:

1. Editar el archivo y dejar la versión correcta.
2. Ejecutar:

```bash
git add notas.txt
git revert --continue
```

---

### 🧠 Mensaje clave

> `revert` es seguro a nivel de historia (no borra commits),
> pero también puede producir conflictos si los cambios que intenta deshacer han sido modificados en commits posteriores.

---

## 6️⃣ Resumen final

* `git revert <id_commit>`:

  * **NO borra** el commit indicado.
  * Crea un **nuevo commit** que aplica el “contracambio”.
* Se puede revertir:

  * el último commit (HEAD),
  * o uno más antiguo del historial.
* Es seguro usarlo después de hacer `push` a GitHub.
* Puede generar conflictos si el código ha cambiado mucho desde el commit que queremos revertir.
* En caso de conflicto:

  * resolver en el archivo,
  * `git add`,
  * `git revert --continue`.

---
