# Práctica 2 – Generar y usar clave **SSH** con Git y GitHub (Java + Eclipse)

> **Contexto:** En esta práctica aprenderás a configurar una conexión **segura** entre tu ordenador y GitHub usando **SSH**, para evitar introducir usuario y contraseña cada vez que subas o descargues código.

---

## 1) ¿Qué es una clave SSH?

SSH (Secure Shell) es un protocolo que permite conectarte de forma **segura y cifrada** con servidores remotos.
GitHub permite usar claves SSH para **autenticarte automáticamente**, sin tener que escribir tu usuario ni contraseña.

Una clave SSH se compone de dos partes:

* 🔑 **Clave privada**: se queda en tu ordenador. **No se comparte nunca.**
* 🪪 **Clave pública**: se sube a GitHub para que reconozca tu equipo.

Cuando haces `git push` o `git pull`, Git usa la clave privada para comprobar que eres tú.

[Aquí tienes una explicación más detallada de cómo funcionan las claves SSH](3_git_practica2_SSH_detalle.md)

---

## 2) Verificar si ya tienes una clave SSH

Antes de generar una nueva, comprueba si ya existe:

```bash
ls -al ~/.ssh
```

Si ves archivos como `id_ed25519.pub` o `id_rsa.pub`, ya tienes una clave.
Si no aparecen, continúa con el siguiente paso.

---

## 3) Generar una nueva clave SSH

Ejecuta en tu terminal o **Git Bash (Windows)**:

```bash
ssh-keygen -t ed25519 -C "tu_usuario@g.educaand.es"
```

**Explicación:**

* `-t ed25519` → tipo de clave moderna y segura (recomendada por GitHub).
* `-C` → comentario identificador (usa tu correo de EducaAnd para saber de qué equipo es la clave).

Cuando te pregunte la ubicación, presiona **Enter** para aceptar la ruta por defecto:

```
/home/tu_usuario/.ssh/id_ed25519
```

Puedes dejar la contraseña vacía (solo si es tu equipo personal) o añadir una para mayor seguridad.

---

## 4) Iniciar el agente SSH y añadir la clave

El **agente SSH** mantiene tus claves activas durante la sesión. En Git Bash o terminal, escribe:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
ssh-add -l   # Verifica que está cargada
```

> 💡 Si usas **Windows** y `ssh-agent` no se inicia, ejecuta:
>
> ```bash
> start-ssh-agent
> ```
>
> o reinicia Git Bash como administrador.

---

## 5) Copiar la clave pública al portapapeles

### Según tu sistema operativo:

**Windows:**

```bash
clip < ~/.ssh/id_ed25519.pub
```

**macOS:**

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

**Linux:**

```bash
xclip -sel clip < ~/.ssh/id_ed25519.pub
```

Si no tienes utilidades de portapapeles, también puedes mostrarla y copiarla manualmente:

```bash
cat ~/.ssh/id_ed25519.pub
```

---

## 6) Añadir la clave SSH a GitHub

1. Entra en [GitHub](https://github.com/) y accede con tu cuenta de EducaAnd.
2. Haz clic en tu foto de perfil → **Settings**.
3. En el menú lateral, entra en **SSH and GPG keys**.
4. Haz clic en **New SSH key**.
5. Escribe un título identificativo (por ejemplo, *Clave portátil DAM*).
6. Pega la clave copiada y haz clic en **Add SSH key**.

---

## 7) Probar la conexión SSH con GitHub

Para comprobar que la configuración funciona correctamente:

```bash
ssh -T git@github.com
```

La primera vez aparecerá una advertencia de autenticidad del host (`The authenticity of host 'github.com'...`).
Escribe **yes** y presiona **Enter**.

Deberías ver un mensaje como:

```
Hi tu_usuario! You've successfully authenticated, but GitHub does not provide shell access.
```

Eso significa que la conexión está configurada correctamente.

---

## 8) Configurar tu repositorio local para usar SSH

Si ya tenías tu repositorio configurado con HTTPS, cambia su dirección remota:

```bash
git remote set-url origin git@github.com:tu_usuario/nombre_repositorio.git
```

Comprueba la nueva URL:

```bash
git remote -v
```

Deberías ver algo como:

```
origin  git@github.com:tu_usuario/nombre_repositorio.git (fetch)
origin  git@github.com:tu_usuario/nombre_repositorio.git (push)
```

---

## 9) Usar Git con SSH

A partir de ahora, tus comandos de Git funcionarán sin pedir usuario ni contraseña:

```bash
git push origin main

git pull origin main
```

Git autenticará automáticamente usando tu clave SSH.

> ⚙️ Si tu rama principal se llama `master` en lugar de `main`, reemplázala en los comandos anteriores.

---

## 10) Uso desde Eclipse (EGit)

1. Abre **Eclipse** → *Window → Preferences → Team → Git → Configuration*.
2. Verifica que en tu sistema existe la carpeta `.ssh` en tu usuario.
3. Al hacer *Team → Push to Upstream*, Eclipse detectará tu clave SSH automáticamente si la URL remota del proyecto empieza por `git@github.com:`.
4. Si no la detecta, revisa en *Window → Preferences → General → Network Connections → SSH2* que el **Private Key** apunta a:

```
C:\Users\tu_usuario.ssh\id_ed25519
```

5. Una vez guardado, podrás **push** y **pull** sin autenticación manual.

---

## 11) Ejercicio práctico

[Sigue las siguientes instrucciones para realizar el ejercicio con tu clave SSH](3_git_practica2_ejercicio.md)

---

## 12) Seguridad y mantenimiento

* Nunca compartas tu **clave privada** (`id_ed25519`).
* Puedes añadir varias claves SSH si trabajas desde diferentes dispositivos.
* Si pierdes o cambias de equipo, elimina la clave antigua desde GitHub → *Settings → SSH and GPG Keys*.
* Usa `ssh-add -l` para listar las claves cargadas actualmente.

---

## 13) Recursos útiles

* [GitHub Docs – Conectar con SSH](https://docs.github.com/es/authentication/connecting-to-github-with-ssh)
* [Git – Manual SSH](https://git-scm.com/book/es/v2/Git-en-el-Servidor-Generaci%C3%B3n-de-Tu-Clave-P%C3%BAblica-SSH)
* [EGit User Guide](https://www.eclipse.org/egit/documentation/)
* [Comandos de Git más usados](https://training.github.com/downloads/es_ES/github-git-cheat-sheet/)
