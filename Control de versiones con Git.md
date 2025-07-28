# Git- Control de versiones

## 1. Descripción del sistema actual del control de versiones

Hasta ahora he gestionado el control de versiones cambiando el nombre del documento y añadiéndole sufijos. Por ejemplo, `documento v1`, `documento v2`, `documento v3`. La nomenclatura permite diferenciar cambios menores de mayores. Así: `documento v2.1` -cambios menores respecto de la v2- `documento v3` -cambios mayores respecto de la v2.1 y la v2- y así sucesivamente.

Siendo un enfoque práctico, se pierde información respecto a los cambios introducidos en cada versión. Eso sí, se puede volver perfectamente a una versión anterior. Además, podría definir un documento explicativo `versiones.txt` para describir los cambios realizados de una versión respecto de otra.

## 2. Reflexión sobre el sistema actual de control de versiones

Tu enfoque actual es muy lógico y, de hecho, es el primer sistema de control de versiones que casi todos hemos utilizado de forma intuitiva. Llamémoslo "Versionado por Nomenclatura". Es simple, directo y, permite volver a una versión anterior sin problemas. El fichero `versiones.txt` es un añadido inteligente para mitigar una de sus grandes debilidades: la falta de contexto sobre los cambios.

## 3. Las limitaciones del sistema actual ("Versionado por Nomenclatura")

Tu sistema funciona, pero tiene "fugas de información" y genera trabajo manual que, con el tiempo, se vuelve pesado.

1. **El "Qué" es ambiguo:** Tu `versiones.txt` dice: "v2.1: Corregidos errores tipográficos y mejorada la introducción". Es útil, pero... ¿qué errores exactamente? ¿Cómo era la introducción *antes* y cómo es *ahora*? Para saberlo, tendrías que abrir la v2 y la v2.1 y compararlas a ojo. Esto es lento y propenso a errores.

2. **El espacio se multiplica:** Si tu "documento" es en realidad una carpeta con varios ficheros (imágenes, textos, hojas de cálculo), cada vez que creas una nueva versión (`proyecto_v2`, `proyecto_v3`), estás duplicando *todos* los archivos, incluso los que no han cambiado. Esto consume mucho espacio innecesariamente.
3. **El riesgo de la "versión final definitiva (ahora sí)":** Todos hemos caído en la trampa de `informe_final.docx`, `informe_final_entregar.docx`, `informe_final_corregido_por_jefe.docx`. El sistema de nombres se rompe fácilmente y genera confusión. ¿Cuál es el bueno?
4. **Experimentar es arriesgado:** Quieres probar un cambio radical en la estructura del documento. Lo lógico es hacer un "Guardar como..." y llamarlo `documento_v3_prueba_estructura.docx`. Si la idea funciona, tienes que copiar y pegar manually los cambios al documento "oficial". Si no funciona, simplemente dejas ese archivo abandonado. Con el tiempo, tu directorio se llena de ramas muertas, de experimentos olvidados.
En definitiva este sistema derive en un caos.  Es difícil saber qué cambios hay en cada versión, es imposible colaborar con otra persona, y restaurar una versión antigua es una trabajo de adivinanza.

## 4. Presentando a Git: Tu Asistente de Versiones Personal

Un Sistema de Control de Versiones (VCS) como Git automatiza este proceso de forma inteligente.

* **No guarda copias completas del archivo**, sino que registra los "cambios" (o "instantáneas") a lo largo del tiempo.
* **Añade un mensaje a cada cambio**, explicando qué se hizo y por qué.
* **Crea un historial lineal y claro**, permitiéndote viajar en el tiempo a cualquier punto del historial de tu proyecto.

Git funciona principalmente con tres "áreas" o "árboles":

* **Directorio de Trabajo (Working Directory):** La carpeta con tus archivos, donde trabajas y editas. Es tu "escritorio desordenado".
* **Área de Preparación (Staging Area):** Un área intermedia. Aquí colocas los cambios que has revisado y que quieres incluir en tu próxima "foto" oficial. Es como seleccionar los documentos que vas a meter en un sobre para enviar.
* **Repositorio (.git):** La base de datos donde Git guarda de forma permanente todas las "fotos" (commits) de tu proyecto. Es el archivo histórico seguro.

El flujo básico es siempre: Modificar en el Directorio de Trabajo -> Preparar en el Staging Area -> Confirmar en el Repositorio.
Ahora, olvida por un momento que Git es una herramienta para programadores. Piensa en Git como un asistente increíblemente meticuloso que observa tu trabajo. No guarda copias enteras de tu proyecto una y otra vez (copias completas del archivo). En su lugar, hace algo mucho más inteligente: **registra únicamente los cambios**.

Vamos a comparar directamente tu flujo de trabajo con el que tendrías con Git.

| Característica | Tu Flujo Actual ("Versionado por Nomenclatura") | El Flujo con Git y GitHub |
| :--- | :--- | :--- |
| **Estructura de archivos** | Múltiples copias del mismo archivo/carpeta: `doc_v1`, `doc_v2`, `doc_v2.1`... | **Un único archivo/carpeta**: `documento`. Git gestiona el historial de forma invisible en una subcarpeta oculta llamada `.git`. Tu directorio de trabajo está siempre limpio. |
| **Guardar un cambio** | Guardas el archivo. Creas una copia con un nuevo nombre (`doc_v3`). Abres `versiones.txt` y anotas el cambio. | Guardas el archivo. Le dices a Git: "Oye, registra este cambio". Git te pide una descripción (un "mensaje de commit"). Por ejemplo: `"Se añade el párrafo sobre impacto económico en la introducción"`. Este mensaje es tu `versiones.txt`, pero integrado, obligatorio y ligado a ese cambio exacto. |
| **Ver qué ha cambiado** | Abres `doc_v2.1` y `doc_v3` y los comparas visualmente. | Le pides a Git: "Muéstrame las diferencias entre la versión actual y la anterior". Git te mostrará, línea por línea, qué texto has añadido (en verde) y cuál has borrado (en rojo). **Tienes una precisión quirúrgica sobre el cambio.** (Esto funciona de maravilla con archivos de texto plano, como .txt, .md, .html, etc.). |
| **Volver a una versión** | Al disponer de un historial lineal y claro te permite viajar en el tiempo a cualquier punto del historial de tu proyecto. Borras el archivo actual y renombras una copia antigua. | Le dices a Git: "Quiero volver al estado de hace tres días a las 5 de la tarde". Y ¡listo! Tu archivo vuelve a ser exactamente como era en ese momento. Y no te preocupes, el historial más reciente no se borra, simplemente has "viajado en el tiempo". |
| **Experimentar** | Creas una copia (`doc_prueba_loca.docx`). Si funciona, copias y pegas. Si no, la abandonas. | Le dices a Git: "Crea una línea de tiempo paralela (una 'rama') para probar una idea". Trabajas en ella sin afectar a tu versión principal. ¿La idea fue buena? Le dices a Git: "Fusiona este experimento con la línea principal". Git lo hace automáticamente. ¿Fue mala? "Borra esta línea de tiempo". Sin desorden, sin archivos huérfanos. |
| **Seguridad / Backup** | Tu disco duro. Si falla, pierdes todas las versiones. Quizás una copia en un disco externo o en Google Drive, que sincroniza la versión actual. | Tu disco duro **Y** un repositorio remoto como GitHub. GitHub no es solo una copia de la última versión; es una **copia de seguridad completa de todo el historial de tu proyecto**. Si tu ordenador explota, clonas el repositorio desde GitHub en uno nuevo y tienes absolutamente todo de vuelta, cada cambio, cada mensaje, cada versión. |

## 5. El Beneficio Esperado de la Inversión

La inversión de tiempo no consiste en aprender un centenar de comandos, sino en interiorizar un flujo de trabajo nuevo y mucho más potente. Para tus necesidades, solo necesitas conocer 4 o 5 comandos básicos.

**El retorno de la inversión es inmediato y se manifiesta en:**

* **Claridad Mental:** Tu carpeta de trabajo estará siempre limpia. Un solo `documento`, no diez.
* **Confianza Absoluta:** Puedes hacer cualquier cambio, por drástico que sea, sabiendo que puedes volver al estado anterior en segundos con total precisión. Se acabó el miedo a "romper" algo.
* **Un Diario de Proyecto Automático:** Cada "commit" es una entrada en el diario de tu proyecto. Dentro de seis meses, podrás ver no solo *qué* cambiaste, sino *por qué* lo hiciste (gracias a tus mensajes de commit).
* **Profesionalización:** Estarás usando la herramienta estándar de la industria para la gestión de cualquier tipo de proyecto digital. Es una habilidad valiosa.

---

## 6. ¡Manos a la Obra! Preparando el Terreno en GitHub

 Necesitamos dos cosas de GitHub antes de poder tocar la terminal o la línea de comandos en tu ordenador: un **repositorio** donde vivirá nuestro proyecto en la nube, y un **token** para que tu ordenador tenga permiso para hablar con ese repositorio.

### 6.1. Paso 1: Crear el Repositorio Remoto en GitHub

Piensa en el repositorio como la "caja" o el "contenedor" central de tu proyecto.

1. Inicia sesión en [GitHub.com](https://github.com).
2. En la esquina superior derecha, haz clic en el icono `+` y selecciona **New repository**.
3. **Repository name:** Elige un nombre corto y descriptivo. Como vamos a usarlo para tus apuntes, algo como `mis-apuntes-git` o `primer-repositorio` es perfecto.
4. **Description (optional):** Escribe una frase corta que describa el proyecto. Ej: "Mis primeros pasos con Git y control de versiones".
5. **Public / Private:** Puedes elegir si quieres que cualquiera vea tu proyecto (Público) o solo tú y quien tú invites (Privado). Para empezar, **te recomiendo seleccionar Privado**.
6. **IMPORTANTE: No marques ninguna de estas casillas:**
    * `Add a README file`
    * `Add .gitignore`
    * `Choose a license`
    * **¿Por qué?** Queremos crear un repositorio completamente vacío. Si GitHub añade estos archivos, crea un historial inicial en la nube. Nosotros queremos crear el historial primero en nuestro ordenador y luego subirlo. Conectar un proyecto local a un repositorio que ya tiene historial es un poco más complejo, y queremos mantenerlo simple.
7. Haz clic en el botón verde **Create repository**.

¡Listo! Ahora verás una página con instrucciones y una URL. La que nos interesa es la que empieza por `https://...`. Cópiala, la necesitaremos en un momento.

### 6.2. Paso 2: Generar un Token de Acceso Personal (PAT)

Estás totalmente en lo cierto, esta es la forma moderna y segura de autenticarse. Antes usábamos nuestra contraseña de GitHub, pero eso era poco seguro. Un token es como una contraseña de un solo uso o para una aplicación específica.

1. En GitHub, haz clic en tu foto de perfil (esquina superior derecha) y ve a **Settings**.
2. En el menú de la izquierda, baja del todo y haz clic en **Developer settings**.
3. En el nuevo menú de la izquierda, haz clic en **Personal access tokens** y luego en **Tokens (classic)**.
4. Haz clic en el botón **Generate new token** y selecciona **Generate new token (classic)**.
5. **Note:** Dale un nombre que te recuerde para qué es. Por ejemplo: `Token para Git en mi PC`.
6. **Expiration:** Por seguridad, los tokens caducan. 30 o 90 días es una buena opción. Siempre puedes generar otro.
7. **Select scopes:** Esta es la parte más importante. Aquí defines qué permisos le das a este token. Para lo que queremos hacer (subir y bajar cambios de nuestros repositorios), solo necesitas marcar **la casilla principal que dice `repo`**. Al marcarla, se seleccionarán automáticamente todos sus permisos secundarios. Es todo lo que necesitas.
8. Baja hasta el final y haz clic en **Generate token**.

**¡¡MÁXIMA ATENCIÓN!!**
GitHub te mostrará el token **una sola vez**. En cuanto abandones o refresques la página, desaparecerá para siempre.

* **Copia la cadena de letras y números (empieza por `ghp_...`) inmediatamente.**
* **Pégala en un lugar seguro y temporal.** Un bloc de notas, un gestor de contraseñas... donde sea, pero que no se te pierda en los próximos 10 minutos.

Cuando tu ordenador te pida la contraseña para conectar con GitHub, no pondrás tu contraseña real, sino que pegarás este token.

---

**Tu Misión (si decides aceptarla):**

Completa estos dos pasos. Cuando tengas la **URL de tu repositorio vacío** y el **token copiado y a buen recaudo**, avísame.

Entonces, pasaremos a la parte más emocionante: abrir una terminal en tu ordenador y ejecutar los 3-4 comandos que darán vida a tu control de versiones local y lo conectarán con la nube.

Ya hemos superado la parte "administrativa" y tenemos todo lo necesario para construir el puente entre tu ordenador y la nube de GitHub. Ahora viene la parte divertida, donde vemos la magia en acción.

---

## 7. Dando Vida al Repositorio Local y Conectándolo a GitHub

Aquí es donde tu directorio local se convierte en un repositorio de Git "inteligente" y aprende a hablar con su gemelo en GitHub. Asumiré que ya tienes Git instalado en tu ordenador. Si no es así, puedes descargarlo desde [git-scm.com].

Todo lo que sigue lo haremos desde una **terminal** o **línea de comandos**.

### 7.0 Configuración Global de identidad Git en una máquina

`git --version``
`git config --global user.name "Tu Nombre"`
`git config --global user.email [tu@email.com] `
Esto es necesario para los commits tenga autor.

Git almacena configs en tres niveles: local (por repo), global (para tu usuario) y system (para toda la máquina). Como configuraste global, nos enfocamos ahí, es el 80% de lo que usarás.

1. Ver Toda la Configuración Global
**Por qué?** Te da una vista completa, incluyendo user.name, user.email y otras settings (como editor predeterminado).
**Comando clave: git config --global --list
Paso práctico:
Abre iTerm con Fish.
Escribe git config --global --list y presiona Enter.
Busca líneas como:
user.name=Tu Nombre
user.email= tu@email.com
Si la lista es larga, usa la búsqueda de iTerm (Cmd + F) para encontrar "user.name" o "user.email".

Paso práctico:
Abre iTerm con Fish.
Escribe git config --global --list y presiona Enter.
Busca líneas como:
user.name=fglguevara
user.email=fgonzal@omp.upv.es
gui.recentrepo=/Users/fglguevara/ownCloud/SuperdiskTesis/Tools/git/Vanity
init.defaultbranch=main

Si la lista es larga, usa la búsqueda de iTerm (Cmd + F) para encontrar "user.name" o "user.email"

### 7.1. Paso 1: Preparar el Directorio Local

1. **Crea una carpeta para tu proyecto.** Se recomienda llamarla igual que tu repositorio en GitHub para mantener la coherencia. Por ejemplo, `mis-apuntes-git`.
2. **Mete tus archivos dentro.** Coge ese archivo Markdown donde estás tomando notas y ponlo dentro de esta nueva carpeta.
3. **Abre una terminal DENTRO de esa carpeta.** Este paso es crucial.
    * En Windows: Navega hasta la carpeta, haz clic derecho en un espacio en blanco y selecciona "Abrir en Terminal" o "Git Bash Here" (si lo instalaste con Git).
    * En Mac/Linux: Abre la aplicación de Terminal, escribe `cd ` (con un espacio al final), y arrastra la carpeta de tu proyecto desde el Finder/explorador de archivos a la ventana de la terminal. Esto pegará la ruta correcta. Luego presiona Enter.
No es necesario **desactivar el control de versiones `Git`** si simplemente dejas de trabajar en un directorio o te mueves a otro subdirectorio; Git seguirá funcionando únicamente en la carpeta(s) donde lo hayas inicializado. Si quieres dejar de usar Git en un directorio, simplemente no ejecutes más comandos de Git allí. Si deseas eliminar el control de versiones, puedes borrar la carpeta oculta `.git` dentro del directorio.

### 7.2. Paso 2: El Bautizo (`git init`)

Ahora le diremos a Git que empiece a "observar" esta carpeta.

Escribe el siguiente comando en tu terminal y presiona Enter:

```fish
git init
```

* **¿Qué hace esto?** Este comando crea una subcarpeta oculta llamada `.git`. Ahí es donde nuestro "asistente meticuloso" (Git) guardará todo el historial, todas las versiones y     toda la información del proyecto. No necesitas tocar nada dentro de esa carpeta, pero es el cerebro de tu repositorio.
* No es necesario desactivar el control de versiones Git si simplemente dejas de trabajar en un directorio o te mueves a otro subdirectorio; Git seguirá funcionando únicamente en la carpeta (y subcarpetas) donde se encuentra el repositorio inicializado (es decir, donde existe el directorio oculto .git).
* Si ya no quieres que una carpeta en particular esté bajo control de versiones, puedes eliminar el directorio oculto `.git` dentro de esa carpeta. Esto eliminará todo el historial de versiones, pero los archivos seguirán ahí como estaban. O bien eliminar solo ciertos archivos/carpetas del cotrol sin borrar el historial completo.  Se puete utilizar .gitignore para excluir archivos específicos del control de versiones, o bien eliminar el control de versiones de un archivo específico con el comando `git rm --cached nombre_del_archivo`.

### 7.3. Paso 3: La Lista de Ignorados (`.gitignore`)

Como te comenté, hay ciertos archivos que no queremos guardar en nuestro historial (archivos temporales, secretos, archivos de configuración del sistema operativo, etc.). Le diremos a Git que los ignore creando un archivo especial.

1.  **Crea un archivo de texto** dentro de tu carpeta de proyecto y nómbralo exactamente así: `.gitignore` (sí, empieza con un punto).
2.  **Ábrelo con un editor de texto** y añade contenido. Para un proyecto de documentación, un buen punto de partida es ignorar los archivos de sistema comunes:

    ```fish 
    # Archivos de sistema operativo
    .DS_Store
    Thumbs.db

    # Archivos temporales de editores
    *.tmp
    *.swp
    ```

* **¿Qué hace esto?** Cualquier archivo o patrón que escribas en `.gitignore` será completamente invisible para Git. Es como darle a tu asistente una lista de cosas en las que no debe fijarse.

### 7.4. Paso 4: Tu Primer "Guardado" (`add` y `commit`)

Este es el flujo de trabajo que repetirás cada vez que quieras guardar un punto de control. Consta de dos pasos:

1. **Preparar los archivos para la "foto" (`git add`)**: Le dices a Git qué cambios específicos quieres incluir en el próximo punto de guardado.
  ` git add . `

2. **Tomar la "foto" y describirla (`git commit`)**: Guardas permanentemente esos cambios en el historial con un mensaje que explica qué hiciste.

En tu terminal, ejecuta estos dos comandos, uno después del otro:

```fish
# 1. Añade TODOS los archivos nuevos o modificados de la carpeta (excepto los ignorados)
git add .

# 2. Guarda los cambios en el historial con un mensaje descriptivo
git commit -m "Commit inicial: Creación del proyecto y notas iniciales"
```

* **¿Qué hemos hecho?** Acabas de crear la **primera versión oficial** de tu proyecto en tu historial local. El mensaje `"Commit inicial..."` es tu nuevo `versiones.txt`, pero ligado de forma precisa e imborrable a este momento exacto.

### 7.5. Paso 5: Conectar con la Nube y Subir tu Trabajo (`remote` y `push`)

Ya tienes el historial en tu ordenador. Ahora vamos a conectarlo con esa "caja fuerte" vacía que creamos en GitHub y a subirle una copia.

1. **Enseña a tu repositorio local la dirección del remoto:**
    * Coge la URL de tu repositorio que copiaste de GitHub (la que termina en `.git`).
    * Ejecuta este comando, **reemplazando `URL_DE_TU_REPOSITORIO`** con tu URL:

    ```fish
    git remote add origin URL_DE_TU_REPOSITORIO
    ```
    * *Explicación*: `remote add` añade un control remoto. `origin` es el nombre corto que, por convención, le damos a nuestra URL principal.

2. **Renombra tu línea de tiempo principal a `main`:** Es una buena práctica moderna.
    ```fish
    git branch -M main
    ```

3. **Sube tu historial a GitHub (`git push`):**
    ```fish
    git push -u origin main
    ```
    * *Explicación*: 
  Al realizar un commit, tu repositorio en la carpeta .git está actualizado y se disponde de un punto de restauración seguro en tu máquina. Pero si el disco duro fallara se perdería el trabajo. Para sincronizar la historia local con el directorio en remotoen Github, asegurando una **copia de seguridad completa** se utiliza el comando `push` que significa "empujar" o "subir". Le estás diciendo a Git: "sube el contenido de mi línea de tiempo local `main` al destino `origin`". Continuando con la analogía, es el "camión de reparto" que lleva tus cajas selladas ('commits') desde tu almacén local a la fortaleza segura de GitHub.
  La bandera `-u` es especial para la primera vez, y crea un enlace para que en el futuro solo necesites escribir `git push`.

**¡Aquí es donde usarás tu Token!**

Al ejecutar `git push`, es muy probable que se abra una ventana o que la terminal te pida tu usuario y contraseña de GitHub.
*   **Usuario:** Tu nombre de usuario de GitHub.
*   **Contraseña:** **NO escribas tu contraseña de GitHub.** Pega aquí el **TOKEN** que generaste (`ghp_...`).

### ¡Verificación Final!

Si todo ha ido bien, la terminal te mostrará un mensaje confirmando que los objetos se han subido.

Ahora, ve a la página de tu repositorio en GitHub y **refréscala**. ¡Tus archivos (`notas.md`, `.gitignore`) deberían estar ahí! Has completado el ciclo.

---

**Resumen de tu flujo de trabajo diario a partir de ahora:**

A partir de este momento, tu rutina para guardar cambios y tener una copia de seguridad será increíblemente simple:

1.  Modificas tus archivos como siempre.
2.  Cuando llegues a un punto de control lógico, abres la terminal en la carpeta y ejecutas:

    ```fish
    # 1. Preparas los cambios
    git add .

    # 2. Guardas los cambios con un mensaje claro
    git commit -m "He añadido la sección 7 a mis apuntes"

    # 3. Subes la copia de seguridad a GitHub
    git push
    ```

¡Y ya está! Tres comandos para tener un control de versiones robusto, un historial claro y una copia de seguridad remota. ¡Enhorabuena, has dado tus primeros y más importantes pasos con Git

Ahora llegas a la pregunta más importante para el trabajo diario: **"¿Y ahora qué? ¿Cómo sé en qué estado está mi proyecto?"**

Aquí es donde conocerás al que se convertirá en tu comando más utilizado en Git, tu mejor amigo, tu panel de control: `git status`.

---

## 8. El Panel de Control: Verificando Cambios (`git status`, `git diff` y `git log`)

Una vez que el repositorio está conectado, necesitas una forma de saber qué ha cambiado desde tu último punto de guardado (tu último `commit`). Git te ofrece tres comandos principales para esto: uno te da una vista general, otro una vista detallada, y el último te muestra la historia completa.

### 8.1. La Vista General: `git status`

Piensa en `git status` como preguntarle a tu asistente: **"¿Cuál es la situación actual del proyecto?"**. Te dirá si hay cambios, si hay archivos nuevos, si todo está guardado y limpio, etc. Es el primer comando que debes ejecutar cuando vuelves a un proyecto después de un tiempo.

**Vamos a probarlo ahora mismo.** Ve a tu terminal, asegúrate de estar en la carpeta de tu proyecto, y ejecuta:

```fish
git status
```

Como acabas de subir todo y no has tocado nada desde entonces, deberías ver un mensaje muy tranquilizador:

```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

*   **`On branch main`**: Te confirma que estás en tu línea de tiempo principal.
*   **`Your branch is up to date...`**: Tu versión local es idéntica a la que hay en GitHub (`origin/main`).
*   **`nothing to commit, working tree clean`**: Esta es la frase clave. Significa que no hay ninguna modificación en tus archivos desde el último `commit`. Tu directorio está "limpio", en un estado conocido y guardado.

---

**Ahora, vamos a ensuciarlo para ver qué pasa.**

1.  **Abre tu archivo de notas** (el `.md`).
2.  **Añade una nueva línea de texto.** Por ejemplo, al final del todo, añade el título de esta misma sección: `## 8. El Panel de Control: Verificando Cambios`.
3.  **Guarda el archivo.**

Tu directorio de trabajo ahora es **diferente** a tu último commit. Volvamos a preguntarle a Git por la situación. Ejecuta de nuevo:

```fish
git status
```

Ahora, el resultado será muy distinto y mucho más interesante:

```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   tus-apuntes.md

no changes added to commit (use "git add" and/or "git commit -a")
```

*   **`Changes not staged for commit`**: Git te avisa: "¡Ojo! Hay cambios que no has preparado para el próximo guardado".
*   **`modified: tus-apuntes.md`**: Y aquí te dice exactamente **qué archivo** ha cambiado. El nombre del archivo aparecerá en rojo.

### 8.2. La Vista Detallada: `git diff`

`git status` te dice **QUÉ** archivos han cambiado. Pero `git diff` (de "diferencia") te muestra **EXACTAMENTE QUÉ LÍNEAS** han cambiado dentro de esos archivos. Es tu herramienta para resolver la duda que tenías con tu sistema antiguo: "¿Qué cambié exactamente entre la v2 y la v2.1?".

Con los cambios que acabas de hacer, ejecuta este comando:

```fish
git diff
```

La salida será algo así:

```diff
diff --git a/tus-apuntes.md b/tus-apuntes.md
index 1234567..abcdefg 100644
--- a/tus-apuntes.md
+++ b/tus-apuntes.md
@@ -95,3 +95,5 @@
 ¡Y ya está! Tres comandos para tener un control de versiones robusto, un historial claro y una copia de seguridad remota. 
+
+## 8. El Panel de Control: Verificando Cambios
```

*   Las líneas que empiezan con `---` y `+++` son información para Git.
*   La línea que empieza con `+` (normalmente en verde) es el texto que has **añadido**.
*   Si hubieras borrado texto, aparecería una línea empezando con `-` (normalmente en rojo).

### 8.3. La Vista Histórica: `git log` y `git log --oneline`

Mientras `status` y `diff` te muestran el presente, `git log` te muestra el pasado. Es tu máquina del tiempo para ver todo el historial de commits que has creado.

Ejecuta el comando básico:
```fish
git log
```
Verás una lista detallada de cada commit: su identificador largo (hash), el autor, la fecha y el mensaje completo. Es útil, pero a menudo es demasiada información.

El `hash`del commit (técnicamente un hash SHA-1) es la "huella digital del comit". Se calcula a partir de todo lo que define a ese commit: los archivos que contiene, el mensaje, el autor, la fecha y, muy importante, el hash del commit anterior "padre". 
 Esto significa que cada commit está vinculado al anterior, formando una cadena inmutable. Si cambias cualquier cosa en un commit, su hash cambia completamente, lo que invalida todos los commits posteriores. Es como un sello de seguridad: si alguien intenta modificar un commit antiguo, todo el historial se rompe.


Para una vista mucho más práctica, usa la opción `--oneline`:
```fish
git log --oneline
```
La salida se transforma en un resumen perfecto:
```
a1b2c3d (HEAD -> main) Añadida la sección sobre git status y diff
f1e2d3c Reestructura el capítulo de 'Primeros Pasos'
1a2b3c4 Commit inicial: Creación del proyecto y notas iniciales
```
* **`a1b2c3d`**: El identificador corto y único de cada commit.
* **`(HEAD -> main)`**: Te indica dónde estás ahora mismo (en la punta de la rama `main`).
* **`Añadida la sección...`**: El mensaje de commit, tu titular del cambio.

### Resumen Práctico

* **¿Quiero saber si he cambiado algo?** -> `git status`
* **¿Quiero saber qué he cambiado exactamente?** -> `git diff`
* **¿Quiero ver el historial de cambios?** -> `git log --oneline`

Ahora que has visto los cambios, el siguiente paso lógico sería guardarlos. ¿Recuerdas el ciclo?

1. `git add .` (para preparar los cambios que te mostró `git status`)
2. `git commit -m "Añadida la sección sobre git status y diff"` (para guardar la "foto")
3. `git push` (para subir la nueva versión a tu copia de seguridad en GitHub)

Este ciclo (`modificar -> status/diff/log -> add -> commit -> push`) es el 90% del uso diario de Git para un usuario individual. ¡Lo estás haciendo genial!

## 9. La Tríada Mágica: `add`, `commit` y `push`

Imagina que tu proyecto no es una carpeta en tu ordenador, sino que estás organizando un envío de paquetes desde tu casa a un almacén central seguro (que sería GitHub).

En este escenario, tienes tres áreas de trabajo:

1. **Tu Mesa de Trabajo (El Directorio de Trabajo):** Aquí es donde tienes todos los documentos y herramientas. Modificas los archivos, escribes, borras, creas... es tu zona de "caos" creativo.
2. **La Caja de Envío (El "Staging Area"):** Es una caja de cartón vacía que tienes al lado de la mesa. Antes de sellarla, decides qué documentos de tu mesa vas a meter dentro para este envío en particular.
3. **Tu Almacén Local (El Repositorio Local, la carpeta `.git`):** Es una estantería en tu garaje. Aquí guardas todas las cajas que ya has sellado y etiquetado, listas para que el camión de reparto se las lleve. Están a salvo dentro de tu casa.
4. **El Almacén Central (El Repositorio Remoto en GitHub):** Es el almacén de alta seguridad al que envías tus paquetes para tener una copia perfecta y accesible desde cualquier lugar.

Ahora, veamos qué hace cada comando en esta analogía.

### 1. `git add` - "Meter cosas en la caja"

*   **Qué haces:** Coges un documento modificado de tu mesa de trabajo y lo metes **dentro de la caja de envío**.
*   **Comando:** `git add mi-archivo.md` (mete ese archivo específico) o `git add .` (mete todos los archivos que hayas modificado en la mesa).
*   **Propósito:** Este es un paso intermedio y es **útil**. Te permite ser selectivo. Imagina que has modificado 5 archivos en tu mesa, pero solo 3 de ellos pertenecen a la misma "idea" o "tarea". Con `git add`, puedes meter solo esos 3 archivos en la caja, dejando los otros 2 en la mesa para un envío posterior. Es como decir: "De todo lo que he modificado, esto es lo que quiero incluir en mi próximo paquete". Es el acto de meter las cosas en la "caja de envío" antes de precintarla Permite crear "puntos de guardado" limpios y lógicos.

En **resumen**: `git add` no guarda nada de forma permanente. Solo prepara los cambios para el siguiente guardado.

### 2. `git commit` - "Precintar y etiquetar la caja"

*   **Qué haces:** Coges la caja de envío (que ya tiene dentro los archivos que seleccionaste con `git add`), la cierras con cinta adhesiva y le escribes una etiqueta clara en el exterior que describe su contenido. Por ejemplo: "Contiene el borrador del capítulo 5 y la corrección de la introducción".
*   **Comando:** `git commit -m "Este es el mensaje de mi etiqueta"`
*   **Propósito:** Este es el **verdadero acto de guardar**. Creas un punto de control permanente y seguro en tu historial. La caja (el "commit") se mueve desde la zona de preparación a tu **almacén local** (tu garaje). El cambio ya está registrado para siempre en tu ordenador. **Importante:** en este punto, GitHub todavía no sabe nada de esta nueva caja.
    *   `git commit -a -m "Mensaje"`: Este comando es un atajo que añade automáticamente todos los archivos modificados al commit, sin necesidad de hacer `git add` primero. Es útil si estás seguro de que quieres incluir todos los cambios en el commit.

**En resumen: `git commit` crea un punto de guardado permanente en el historial de TU ordenador.**

#### `stash` alternativa temporal a `commit`
`git stash` ofrece una alternativa a `git commit` para guardar cambios temporalmente sin modificar el historial de commits. 
Mientras que git commit guarda los cambios de forma permanente en el repositorio, `git stash` los "esconde" en un espacio aparte, permitiéndote limpiar tu directorio de trabajo o cambiar de rama sin perder tu progreso. 
Puedes recuperar los cambios guardados con git stash pop o git stash apply cuando los necesites. Es ideal para situaciones donde no quieres commitar cambios incompletos o cuando necesitas cambiar de contexto rápidamente.

### 3. `git push` - "Enviar el paquete al almacén central"

*   **Qué haces:** Llamas al camión de reparto para que venga a tu garaje, recoja todas las cajas nuevas que has precintado y etiquetado, y se las lleve al **almacén central (GitHub)**.
*   **Comando:** `git push`
*   **Propósito:** Sincroniza tu historial local con el historial remoto. Es el paso que hace que tu trabajo esté respaldado en la nube y, si trabajaras en equipo, sería el paso que permite que otros vean tus cambios.

**En resumen: `git push` sube tus commits (tus cajas guardadas) desde tu ordenador a GitHub.**

### Tabla Resumen

| Comando | Analogía | Propósito Técnico | ¿Dónde ocurre? |
| :--- | :--- | :--- | :--- |
| `git add` | Meter archivos en la caja de envío. | Añade los cambios al "Staging Area". | En tu ordenador. |
| `git commit` | Precintar y etiquetar la caja. | Guarda una "instantánea" permanente de los cambios en el historial local. | En tu ordenador. |
| `git push` | Enviar la caja al almacén central. | Sube los commits locales al repositorio remoto (GitHub). | Entre tu ordenador y GitHub. |

### El Flujo Visual

```
[Tu Mesa (Directorio)] --> git add --> [La Caja (Staging Area)] --> git commit --> [Tu Garaje (Repo Local)] --> git push --> [Almacén Central (GitHub)]
```

Por eso el ciclo es siempre `add` -> `commit` -> `push`. No puedes enviar una caja que no has precintado, y no puedes precintar una caja que está vacía.

Para aumentar ese 90% y acercarte al 95-98% del uso real, te sugiero que nos centremos en tres áreas que cubren las situaciones más comunes que encontrarás a partir de ahora:

1.  **Corregir errores y viajar en el tiempo:** ¿Qué pasa si te equivocas?
2.  **Experimentar sin miedo (el verdadero superpoder de Git):** El uso de ramas.
3.  **Sincronizar el trabajo de otros (o el tuyo desde otro ordenador):** El complemento de `push`.

Añadamos estas secciones a tus notas.

---

## 10. Viajar en el Tiempo: Cómo Corregir Errores Comunes

Tarde o temprano, cometerás un error. Guardarás algo que no debías, escribirás un mensaje incorrecto o simplemente querrás deshacer un cambio. Git es tu red de seguridad. Git ofrece varias herramientas para "deshacer" cosas y cada una sirve para un propósito distinto: Vamos a verlas en detalle y ordenadas de menor a mayor "potencia" (o carácter más destructivo o inevitable): `git commit --amend`, `git restore`(<archivo>, --staged), `git revert` y `git revert --soft`, git reset, `git reset --soft`, `git reset --hard`.

### 1. `git commit --amend` Corregir el último commit.
* **Problema que resuelve**: "He hecho un commit, pero me he dado cuenta de que he olvidado añadir un archivo o he escrito un mensaje incorrecto. Quiero corregirlo".
* **Analogía**: Es como si hubieras enviado un paquete, pero luego te das cuenta de que olvidaste incluir un documento importante. En lugar de enviar un nuevo paquete, abres el paquete original, metes el documento que faltaba y vuelves a sellarlo con una etiqueta corregida. Es una forma elegante de arreglar errores menores en el último commit sin complicar el historial. Es la opción menos destructiva. 
  * `git commit --amend -m "Mensaje corregido"`. Permite cambiar el mensaje del último commit sin abrir el editor de texto.
  * `git commit --amend --no-edit`. No modifica el mensaje del commit. Es útil para añadir o quitar archivos del último commit sin cambiar el mensaje. 


### 2. `git restore <archivo>` Descartar cambios en el Directorio de Trabajo
* **Problema que resuelve**: "He modificado un archivo, pero no me gusta lo que he hecho. Quiero volver a la versión que está en mi último commit y descartar todos mis cambios locales en ese archivo".
* **Analogía**: Es como arrugar una hoja de papel en la que estabas escribiendo y luego desarrugarla para volver a su estado original.
  * `git restore .` Descarta todos los cambios en todos los archivos del directorio de trabajo. Similar al anterior, pero afecta a todos los archivos.


### 3. `git restore --staged <archivo>` Deshacer los cambios en un archivo específico del área de trabajo, restaurando la última versión confirmada
* **Problema que resuelve**: "He añadido un archivo al Staging Area con `git add`, pero me he dado cuenta de que no quiero incluirlo en el próximo commit".
* **Analogía**: Es como meter un documento en una caja de envío, pero luego decides que no quieres enviarlo. Lo sacas de la caja sin cambiar el documento en sí. Mantiene los cambios en el directorio de trabajo. Es útil para quitar archivos que se añadieron accidentalmente con `git add`. 
  * `git restore --staged .`Des-escenifica todos los archivos del Staging area.
  * `git restore --source:<commit> <archivo>` Restaura un archivo a la versión de un commit específico. Permite volver a una versión anterior sin afectar al historial de commits.


* ### 4. `git revert <hash_del_commit>`Revertir un commit público de forma segura
* **Problema que resuelve**: "He subido un commit a GitHub, pero me he dado cuenta de que contiene un error grave. Quiero deshacer ese commit sin perder el historial".
* **Analogía**: Enviar un email con un error y, en lugar de intentar hackear el servidor para borrarlo, enviar un segundo email que dice "Corrección: Por favor, ignoren el contenido del email anterior y usen esta nueva información". Es transparente y no reescribe la historia.
  * `git revert --no-commit <hash_del_commit>` Deshace el commit pero no lo guarda inmediatamente. Permite revisar los cambios antes de hacer el commit de reversión.
  * `git revert --no-edit <hash_del_commit>` Deshace el commit sin abrir el editor de texto para modificar el mensaje. Es útil cuando quieres revertir un commit sin cambiar el mensaje original.

--- 
Los cambios siguientes reescriben el historial de commits, por lo que **debes tener cuidado** al usarlos, son potencialmente destructivos, especialmente si ya has compartido tus commits con otros (por ejemplo, si ya has hecho `git push`).

* ### 5. `git reset --soft <hash_del_commit>` Deshacer commits locales sin perder cambios.
* **Problema que resuelve**: "He hecho varios commits, pero me he dado cuenta de que debería haber hecho uno solo. Quiero combinar esos commits sin perder los cambios".
* **Analogía**: Es como si hubieras escrito varios borradores de un documento y decides que todos esos borradores deberían ser un solo documento final. Los borradores siguen ahí, pero ahora están en una sola versión.
  * `git reset --mixed <commit>` Combina el último commit con el anterior, manteniendo los cambios en el área de staging. Mueve el puntero de la rama al commit esepcificado, des-escenificando los cambios pero manteniéndolos en el directorio de trabajo.
* 
* ### 6. `git reset --hard <hash_del_commit>` Deshacer commits y perder cambios.
* **Problema que resuelve**: "He hecho varios commits, pero me he dado cuenta de que todo lo que he hecho es un desastre. Quiero volver a un estado anterior y perder todos los cambios desde entonces".
* **Analogía**: Es como si hubieras estado trabajando en un proyecto de construcción y decides que todo lo que has hecho hasta ahora es un error. Llamas a la excavadora y le pides que derribe todo lo construido desde el último plano aprobado. Ahora estás de vuelta al punto anterior, pero todo lo que hiciste en el medio se ha perdido.
  * `git reset --hard HEAD~1` Deshace el último commit y todos los cambios asociados. Es como si nunca hubieras hecho ese commit. **¡Cuidado!** Los cambios se pierden para siempre.
Ejemplos de <commit> pueden ser HEAD~1 (el commit anterior al actual), HEAD~2 (dos commits antes), o un hash de commit específico.

Recuerda que las opciones de reset que modifican el historial `(--mixed y --hard)` no deben usarse en commits que ya se han compartido con otros desarrolladores, ya que esto puede causar problemas de sincronización y pérdida de trabajo. En esos casos, `revert` es la opción más segura.


### Regla nemotécnica
**A.R.R.H. (Amend, Restore, Revert, Rebase -i, Hard Reset)**

* `Amend` (Ajustar): Modifica el último commit. El cambio más superficial. Piensa en ajustar una tuerca.

* `Restore` (Recuperar): Descarta cambios en archivos. Puede ser local o del staging area. Piensa en recuperar un archivo borrado accidentalmente.

* `Revert` (Revertir): Crea un nuevo commit que deshace cambios anteriores. Seguro para el historial. Piensa en dar marcha atrás a un coche.

* `Rebase -i` (Reescribir): Modifica el historial de commits. Permite reorganizar, combinar o editar commits. Piensa en reescribir un capítulo de un libro.

* `Hard` (reset --hard): El más destructivo. Descarta todos los cambios y mueve el HEAD. Piensa en formatear un disco duro.

Esta nemotecnia (A.R.R.H.) ordena los comandos correctamente según su potencia destructiva: amend (menor impacto), restore, revert, rebase -i y reset --hard (mayor impacto). Recuerda que debes usar reset --hard con extrema precaución.

### Escenarios Prácticos de uso 
Vamos a ver ahora una serie de escenarios prácticos para aplicar estas herramientas. Imagina que estás trabajando en un proyecto y te encuentras con diferentes situaciones donde necesitas deshacer o corregir algo. Aquí van algunos ejemplos comunes:

### Escenario 1: "Me equivoqué en el mensaje de mi ÚLTIMO commit"

Acabas de hacer un `commit` y te das cuenta de que el mensaje tiene una errata o no es claro. **Si aún no lo has subido con `git push`**, la solución es elegantísima.

```fish
git commit --amend
```

Este comando abrirá tu editor de texto para que puedas reescribir el mensaje del último commit. Si solo quieres cambiar el mensaje en una línea sin abrir el editor, puedes hacer:

```fish
git commit --amend -m "Este es el mensaje corregido"
```

### Escenario 2: "¡Olvidé añadir un archivo al último commit!"

Similar al anterior. Haces un commit y al segundo te das cuenta de que un archivo relacionado con ese cambio se quedó fuera. No necesitas hacer un nuevo commit que diga "ahora sí, el archivo que faltaba".

1.  Añade el archivo olvidado al Staging Area:
    ```fish
    git add el-archivo-olvidado.md
    ```
2.  Ahora, usa el mismo comando de antes para "enmendar" el commit anterior, añadiendo este nuevo archivo:
    ```fish
    git commit --amend --no-edit
    ```
    *   La opción `--no-edit` es un truco útil: realiza la enmienda sin abrir el editor de texto, ya que el mensaje del commit original ya era correcto.
    *   `--amend` destruye el commit antiguo y crea uno nuevo -se abre el editor de texto- que lo reemplaza. Por eso es vital usarlo solo en commits que no has subido con `git push`. Si ya lo has hecho, es mejor evitarlo para no causar conflictos.
*   Escenaro 2b: Quieres cambiar el mensaje del último commit.
    ```fish
    git commit --amend -m "Mensaje corregido del último commit"
    ```

### Escenario 3: "Quiero deshacer completamente los cambios de mi último commit"

Hiciste un commit, pero los cambios que contiene son un desastre y quieres volver exactamente al estado del commit anterior, pero sin perder el trabajo que hiciste (por si quieres reusarlo).

```fish
git reset --soft HEAD~1
```

Desglosemos este comando:
*   `git reset`: Es el comando para "resetear" tu estado a un punto anterior.
*   `HEAD~1`: `HEAD` es un puntero a tu commit actual. `~1` significa "un commit antes de `HEAD`".
*   `--soft`: Esta es la clave. Le dice a Git: "deshaz el commit, pero deja todos los cambios que contenía en el Staging Area (la 'caja de envío')". De esta forma, no pierdes el código, solo el punto de guardado.

### Escenario 4: "Quiero descartar TODOS mis cambios locales que NO he guardado"

Has modificado varios archivos, pero no has hecho `git add` ni `git commit`. Te das cuenta de que todo lo que has hecho es basura y quieres volver a la versión limpia de tu último commit. Este es tu "botón de pánico".

```fish
git restore .
```

Este comando restaura todos los archivos de tu directorio de trabajo a la versión exacta en la que estaban en el último commit. **¡Cuidado! A diferencia de `reset --soft`, estos cambios se pierden para siempre.**

---

## 11. El Superpoder de Git: Ramas para Experimentar (`branch` y `merge`)

Hasta ahora, has trabajado en una única línea de tiempo, llamada `main`. La rama `main`es la versión "oficial" y funcional de tu proyecto. Es la que enseñarías a un cliente o la que desplegarías en un servidor. No quieres hacer experimentos ni añadir funcionalidades a medio terminar directamente ahí, porque podrías romperlo todo. 

Aquí es donde entran las **ramas (branches)**
```
**Analogía Clave**: Una rama es una copia de tu proyecto en un punto concreto en el tiempo. Es un universo paralelo donde puedes trabajar en una nueva funcionalidad o corregir un error de forma segura, sin afectar a la línea de tiempo principal (main). Si el trabajo sale bien, fusionas ese universo paralelo de vuelta al principal. Si sale mal, simplemente lo abandonas sin que haya afectado en nada al original.

```
Las **ramas** (`branches`) son líneas de tiempo paralelas que nacen de un punto de tu historia. Son, sin duda, la característica más potente de Git.

**¿Por qué son útiles incluso si trabajas solo?**
Imagina que estás escribiendo tus notas y se te ocurre una idea para reestructurar todo el documento. Es un cambio grande y no sabes si funcionará.

*   **Sin ramas:** Harías una copia de seguridad manual, trabajarías en el archivo original y, si no te gusta, tendrías que restaurar la copia. Un lío.
*   **Con ramas:** Creas una rama llamada `experimento-estructura`. El universo `main` se queda congelado y seguro, y tú saltas al universo `experimento-estructura` para hacer todos los cambios que quieras.
    *   **¿La idea funciona?** Fusionas (`merge`) la rama de experimento con `main`, y la línea de tiempo principal ahora incluye tu gran idea.
    *   **¿La idea es un desastre?** Simplemente borras la rama de experimento y vuelves a `main` como si nada hubiera pasado.

### El Flujo de Trabajo con Ramas

1.  **Ver tus ramas actuales:**
    ```fish
    git branch
    ```
    *(Verás solo `* main`, indicando que estás en la rama `main`)*.

2.  **Crear una nueva rama:**
    ```fish
    git branch nueva-funcionalidad
    ```

3.  **Moverte a tu nueva rama:**
    ```fish
    git switch nueva-funcionalidad
    ```
    *(El comando moderno es `switch`. También verás mucho el antiguo `git checkout nueva-funcionalidad`)*.
    Para generar una nueva rama y cambiarte a ella al mismo tiempo, puedes usar:
    ```fish
    git switch -c nueva-funcionalidad
    ```
    *(El `-c` significa "crear")*.

4.  **Trabajar como siempre:** Ahora estás en la rama `nueva-funcionalidad`. Puedes hacer `add` y `commit` aquí. Estos commits **solo existen en esta rama** y no afectan a `main`.



5. ¿Qué pasa la primera vez que subimos una rama nueva? Cuando creamos una rama y queremos subirla por primera vea a GitHub, necesitamos decirle a Git dos cosas: a qué repositorio remoto queremos subirla (`origin`) y cómo queremos que se llame en el remoto (normalmente, con el mismo nombre).

Además, podemos crear un "vínculo" o "seguimiento" entre nuestra rama local y la remota. Para hacer todo esto en un solo paso, usamos el comando:

`git push --set-upstream origin <nombre-de-la-rama>`

O su versión corta, que es mucho más común:

`git push -u origin <nombre-de-la-rama>`

**¿Qué hace el parámetro `-u` o `--set-upstream`?**

Establece una conexión permanente. Le dice a Git: "A partir de ahora, cada vez que yo haga `git push` en esta rama, ya sabes que tienes que enviarlo a `origin` y a la rama con este mismo nombre".

Gracias a esto, la primera vez es un comando largo, pero todas las siguientes veces que queramos subir cambios en esta misma rama, solo necesitaremos escribir:

`git push`


6.  **Volver a la rama principal:** Cuando hayas terminado tu trabajo en la rama.
    ```fish
    git switch main
    ```

7.  **Fusionar los cambios:** Ahora que estás de vuelta en `main`, le dices a Git que traiga todo el trabajo que hiciste en la otra rama.
    ```fish
    git merge nueva-funcionalidad
    ```
    Git inteligentemente integrará todos los commits de `nueva-funcionalidad` en `main`.

8.  **(Opcional) Borrar la rama:** Una vez que el trabajo está fusionado y ya no la necesitas.
    ```fish
    git branch -d nueva-funcionalidad
    ```

---

### 12. De la Rama al Tronco: Proponiendo Cambios con Pull Requests

Ya sabes crear ramas, trabajar en ellas y fusionarlas en tu máquina (`git merge`). Este es el flujo de trabajo local. Pero cuando tu código vive en GitHub, introducimos un paso intermedio crucial y colaborativo: el **Pull Request (PR)**.

Piénsalo con esta analogía:
*   `git merge` es el acto de **casarse**. Es la acción técnica que une dos historiales.
*   Un **Pull Request** es la **petición de mano**. Es la propuesta, la discusión, la revisión y la aprobación que ocurre *antes* de la boda.

Un Pull Request es una **característica de GitHub** (no un comando de Git) que inicia una discusión formal sobre los cambios que has hecho en una rama. Es tu forma de decir: "He terminado mi trabajo en la rama `docs/actualizar-con-flujo-remoto`. Por favor, revisad mis cambios antes de integrarlos en `main`".

**El Flujo de Trabajo con Pull Request:**

1.  **Termina tu trabajo en la rama:** Haz tus commits como siempre.
    ```fish
    git add .
    git commit -m "Docs: Añade la sección sobre Pull Requests"
    ```

2.  **Sube tu rama a GitHub:** La primera vez que subes una rama nueva, usas la bandera `-u` para establecer un seguimiento.
    ```fish
    git push -u origin docs/actualizar-con-flujo-remoto
    ```

3.  **Abre el Pull Request en GitHub:**
    *   Ve a la página de tu repositorio en GitHub. Verás un aviso en amarillo sugiriéndote crear un Pull Request para la rama que acabas de subir. ¡Hazle caso!
    *   Dale un título descriptivo y un comentario si es necesario.
    *   Asegúrate de que la fusión sea desde tu rama (`docs/actualizar...`) hacia la rama base (`main`).
    *   Haz clic en "Create pull request".

4.  **Revisión y Fusión:**
    *   En esta nueva pantalla, puedes ver todos los cambios, añadir comentarios y, si trabajaras en equipo, esperar la aprobación de tus compañeros.
    *   Una vez que todo está correcto, verás un gran botón verde: **"Merge pull request"**. Al pulsarlo, GitHub ejecutará el `git merge` por ti en sus servidores.

5.  **Limpieza:**
    *   Después de la fusión, GitHub te ofrecerá un botón para **"Delete branch"**. Es una buena práctica borrar la rama remota, ya que su trabajo ha terminado.

### 13. Manteniendo la Sincronía: `git pull` y la Limpieza Post-Fusión

¡Felicidades! Tus cambios están en la rama `main`... **pero en GitHub**. Tu repositorio local aún no lo sabe. Tu rama `main` local está ahora desactualizada.

Aquí es donde entra el comando `git pull`, el complemento de `git push`.

```fish
# 1. Vuelve a tu rama principal
git switch main

# 2. "Tira" de los cambios del remoto para actualizar tu local
git pull origin main
```

Este comando descarga el "commit de fusión" que GitHub creó y lo integra en tu `main` local, dejándola perfectamente sincronizada con el remoto.

Ahora solo queda un paso de limpieza: borrar la rama en tu máquina local.

```fish
# -d es seguro, solo funciona si la rama ya fue fusionada
git branch -d docs/actualizar-con-flujo-remoto
```

Has completado el ciclo profesional completo: **rama -> commit -> push -> pull request -> merge -> pull -> limpieza**.

---

### **Siguientes Pasos (¡Ahora mismo!)**

Una vez que hayas pegado este texto y guardado el archivo, estás en medio del flujo de trabajo. ¿Qué toca ahora?

1.  **Verifica tus cambios** con `git status` y `git diff`. Verás las modificaciones que acabas de hacer.
2.  **Guarda tu trabajo en un commit** en la rama `docs/actualizar-con-flujo-remoto`. Un buen mensaje sería:
    ```fish
    git add .
    git commit -m "Docs: Añade secciones sobre Pull Requests y flujo remoto"
    ```
3.  **Sube la rama a GitHub** como se describe en el texto que acabas de pegar:
    ```fish
    git push -u origin docs/actualizar-con-flujo-remoto
    ```


---
## 14. Sincronización Bidireccional: Trayendo Cambios (`pull`)

`git push` envía tus cambios a GitHub. Pero, ¿qué pasa si los cambios están en GitHub y no en tu ordenador? Esto puede ocurrir por dos razones:
*   Hiciste un cambio directamente desde la interfaz web de GitHub.
*   Estás trabajando en otro ordenador (ej. el del trabajo), subiste cambios desde allí, y ahora estás en casa.

El comando para traer los cambios remotos a tu repositorio local es `git pull`.

```fish
git pull
```

**¿Qué hace `git pull` exactamente?**
Es la combinación de dos comandos:
1.  `git fetch`: Descarga toda la información del repositorio remoto (nuevos commits, nuevas ramas) pero **no la integra** en tu trabajo local. Solo "baja el catálogo".
2.  `git merge`: Fusiona los cambios que se acaban de descargar en tu rama local actual.

Por lo tanto, `git pull` es el equivalente a `git push`, pero en la dirección opuesta. Es el comando que usarás cada mañana al empezar a trabajar para asegurarte de que tienes la última versión del proyecto.

### Resumen de las Nuevas Habilidades

*   **Para corregir:** `git commit --amend`, `git reset`
*   **Para experimentar:** `git branch`, `git switch`, `git merge`
*   **Para sincronizar hacia abajo:** `git pull`

Con estos comandos, ya no solo eres alguien que guarda versiones, sino que puedes gestionar un historial complejo, trabajar en múltiples ideas a la vez de forma segura y mantener tu trabajo sincronizado en múltiples lugares. Has pasado del 90% a, probablemente, el 98%. El 2% restante son casos muy específicos que ya resolverás cuando te los encuentres.

---

## 15. Poniendo Todo en Práctica: Un Caso Real de Actualización

La teoría está clara, pero la práctica presenta desafíos. ¿Qué ocurre cuando nos enfrentamos a una tarea cotidiana?

**El Escenario:** Tenemos una versión de nuestro archivo de notas. Recibimos una versión más nueva y completa.

**El Impulso "Viejuno":** Nuestro primer instinto es renombrar el archivo actual a `notas_v1.md` y guardar el nuevo contenido en `notas_v2.md`. Esto nos devuelve al sistema de "Versionado por Nomenclatura", justo lo que queremos evitar.

**La Pregunta Clave:** "Pero... ¿y si me gustara más la versión anterior? ¿La pierdo si la sobreescribo?" Esta pregunta es la razón de ser de Git. La respuesta es: **nunca pierdes nada que hayas guardado en un commit.**

Veamos el curso de acción correcto, paso a paso, usando nuestro nuevo framework.

### Paso 1: Verificar el Punto de Partida

Antes de hacer nada, confirmamos que nuestro trabajo previo está a salvo.
```fish
git status
```
El mensaje "nothing to commit, working tree clean" nos da luz verde. Nuestro último commit es nuestro punto de restauración seguro.

### Paso 2: Realizar el Cambio sin Miedo

Procedemos a actualizar el archivo directamente.
1.  Abrimos `Control de versiones con Git.md`.
2.  Borramos todo el contenido antiguo.
3.  Pegamos el nuevo contenido completo.
4.  Guardamos el archivo.

### Paso 3: Observar con las Herramientas de Git

No estamos a ciegas. Le pedimos a Git que nos informe de la situación.
```fish
# Primero, vemos QUÉ archivo ha cambiado
git status

# Luego, vemos EXACTAMENTE QUÉ líneas han cambiado
git diff
```
`status` nos dirá que el archivo fue `modified`. `diff` nos mostrará todas las líneas eliminadas (rojo) y añadidas (verde), dándonos una visión precisa de la actualización.

### Paso 4: Preparar el Nuevo Contenido (`add`)

Estamos conformes con la actualización. La preparamos para ser guardada en el historial.
```fish
git add .
```
Ahora el cambio está en el "Staging Area", listo para la "foto".

### Paso 5: Crear un Nuevo Punto en la Historia (`commit`)

Guardamos esta nueva versión como un nuevo punto seguro en nuestra línea de tiempo, con una descripción clara.
```fish
git commit -m "Incorpora el contenido actualizado del manual"
```
¡Listo! Hemos creado una nueva versión oficial del proyecto.

### Paso 6: La Prueba de Fuego - ¿Dónde está mi versión antigua?

Aquí calmamos nuestro miedo. La versión antigua no ha desaparecido. Está en el commit anterior.
Primero, vemos el historial:
```fish
git log --oneline
```
Veremos nuestro nuevo commit en la cima, y el commit anterior justo debajo. Copiamos el código (hash) del commit anterior y ejecutamos:
```fish
git show HASH_DEL_COMMIT_ANTIGUO:"Control de versiones con Git.md"
```
Git nos mostrará en la terminal el contenido íntegro del archivo en esa versión pasada, demostrando que sigue ahí, intacta y accesible.
`git show HASH_DEL_COMMIT_ANTIGUO`nos permite ver la información del commit (has, autor, fecha, mensaje y dun diff detallado, línea por línea de los cambiso exactos que se introdujeron en ese commit: en verde las adiciones, en rojo, las eliminaciones).

### Paso 7: Sincronizar con la Nube (`push`)

Contentos con nuestra nueva versión y sabiendo que la antigua está a salvo en el historial, subimos una copia de seguridad de nuestro trabajo a GitHub.
```fish
git push
```

**Conclusión de la práctica:** Hemos sustituido el **miedo a sobreescribir** por la **confianza de tener un historial**. No creamos desorden con múltiples archivos, sino que construimos una línea de tiempo limpia y robusta sobre un único archivo. Este es el verdadero cambio de mentalidad que nos ofrece Git.

---
### 16. Git Avanzado

Una vez dominados los fundamentos del ciclo `add -> commit -> push` y el trabajo con ramas, es hora de abrir la caja de herramientas avanzadas. Los comandos de esta sección te otorgan un poder inmenso para manipular y limpiar el historial de tu proyecto. Son como bisturís de cirujano: increíblemente precisos en manos expertas, pero peligrosos si no se comprende bien su función.

En esta sección exploraremos tres de las herramientas más potentes:

*   **`git rebase`**: Para reescribir la historia y crear un registro de cambios lineal y limpio.
*   **`git cherry-pick`**: Para seleccionar y aplicar un commit específico de una rama a otra.
*   **`git reflog`**: Tu red de seguridad definitiva, un registro de todos tus movimientos que puede salvarte incluso de los errores más graves.

---
#### 16.1 Git Rebase: El Arte (poder y peligro) de Reescribir la Historia

El comando `git rebase` es la alternativa a `git merge` para integrar cambios de una rama en otra. Mientras `merge` une dos historiales creando un nuevo "commit de fusión" que los ata, `rebase` lo hace de una forma radicalmente diferente 're-escribiendo la historia'.

**La Analogía:**
Imagina que los commits de tu rama son piezas de Lego que has ido apilando.
*   **`git merge`** coge tu torre de Lego y la torre principal, y construye una nueva pieza grande encima que une las dos. El resultado es funcional, pero tienes una historia con dos caminos que convergen.
*   **`git rebase`** coge tu torre de Lego, la desmonta pieza por pieza, se mueve a la cima de la torre principal y vuelve a montar tus piezas, una por una, en el nuevo sitio. El resultado es una única torre alta y recta, como si hubieras construido tus piezas directamente sobre las últimas de la torre principal.

**La Diferencia Visual:**

Un `merge` produce un historial así (con una "burbuja" de fusión):

```
      A---B---C feature/mi-idea
     /         \
D---E---F-------G main  (G es el commit de fusión)
```

Un `rebase` produce un historial lineal y limpio:

```
D---E---F---A'--B'--C' main (A', B', C' son tus commits, reconstruidos)
```

Su función principal es tomar una serie de commits de una rama y "re-aplicarlos" encima de otra. Esto resulta en un historial de commits lineal y mucho más limpio, como si todo el trabajo se hubiera hecho en secuencia directa sobre la rama principal.

**Ventajas de `git rebase`:**

1.  **Historial Lineal:** El resultado es una historia de proyecto fácil de leer, sin los commits de fusión que pueden añadir ruido.
2.  **Facilita la Búsqueda de Errores:** Un historial lineal es perfecto para usar herramientas como `git bisect` para encontrar cuándo se introdujo un bug.
3.  **Commits Limpios:** Es una oportunidad para limpiar y ordenar tus commits antes de proponer su integración a la rama principal.

### La Regla de Oro: No Cambies el Pasado de los Demás

El comando `git rebase` es una herramienta para cirujanos del historial, y como tal, viene con una advertencia crítica que nunca debe ser ignorada.

> **La Regla de Oro:** Usa `rebase` solo en ramas que viven exclusivamente en tu máquina. Nunca lo uses en ramas públicas o compartidas (`main`, `develop`, etc.).

¿Por qué esta regla es tan estricta? Porque `rebase` no reordena el pasado, lo **re-escribe**. Destruye los commits originales y los reemplaza por copias nuevas.

Piénsalo así: es como si un historiador decidiera que la Batalla de Waterloo ocurrió en 1816 en lugar de 1815. Él publica sus nuevos libros, pero todos los demás historiadores del mundo, que trabajan con la fecha original, de repente tienen una versión de la historia incompatible. Intentar poner en común sus trabajos sería una pesadilla. Eso es exactamente lo que `git rebase` le hace a un equipo si se usa en una rama compartida.

La conclusión es simple: si la rama solo la has usado tú, en tu ordenador, haz `rebase` para limpiarla. Si ya la has "publicado" con `git push` y otros pueden estar usándola, usa `git merge` para integrarla.

**Caso de Uso Práctico:**

Estás trabajando en tu rama `feature/mi-idea`. Mientras tanto, la rama `main` ha recibido nuevos commits. Quieres actualizar tu rama con lo último de `main` antes de proponer un Pull Request.

```fish
# 1. Asegúrate de que tu rama main está actualizada
git switch main
git pull

# 2. Vuelve a tu rama de trabajo
git switch feature/mi-idea

# 3. Ejecuta el rebase. Le dices a Git: "Coge mis commits y ponlos encima de lo último que hay en main"
git rebase main
```

#### 16.2 Git Cherry-Pick: Seleccionando Cambios Específicos

#### 16.3 Git reflog: Tu Red de Seguridad

#### 16.4 Alias: Atajos para tus Comandos Favoritos
Git permite crear alias para acortar comandos. Si te cansas de escribir `git status` o `git log --oneline --graph`, puedes crear atajos.

- `git config --global alias.st status` crea un alias `st` para `status`.
- `git config --global alias.loga "log --oneline --graph"` crea un alias `loga` para un log gráfico simplificado.
- `git config --global alias.cm "commit -m"` crea un alias `cm` para  `commit -m`, permitiéndote escribir el mensaje de confirmación directamente. Por ejemplo, `git cm "Mensaje de confirmación"`.
- `git config --global alias.br branch` crea un alias `br` para `branch`.
- `git config --global alias.last 'log -1 HEAD'` crea un alias `last` para ver el último commit.
- `git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)'"` crea un alias `lg` para un log con formato mejorado, incluyendo hash abreviado, fecha relativa, autor y colores.
- `git config --global alias.aac "add . && commit -m"`. Este alias te permite añadir todos los archivos modificados y crear un commit con un solo comando.  Recuerda que esta práctica puede ser peligrosa si no revisas los cambios antes de confirmarlos, así que úsala con precaución. Un ejemplo de uso sería: `git aac "Mensaje del commit"`.
- `git config --global alias.undo "reset HEAD~1"`. Este comando deshace el último commit, manteniendo los cambios en tu directorio de trabajo.
- `git config --global alias.empty-commit "commit --allow-empty -m"`. Permite crear un commit vacío con un mensaje específico, útil para marcar puntos en la historia del repositorio sin cambios en los archivos. Ejemplo: `git empty-commit "Marca de inicio de la fase 2"`.


Ahora, simplemente puedes escribir `git st` o `git loga`, `git co`, `git cm`, etc. en lugar de los comandos completos.

---
## Apéndice A: El Arte de Escribir un Buen Mensaje de Commit

La línea de asunto de un commit es, posiblemente, la pieza de documentación más leída de todo un proyecto. Un buen historial de commits es una de las marcas de un desarrollador profesional y cuidadoso.

Aunque existen convenciones formales como los "Conventional Commits", podemos aplicar una regla del 80/20 que nos dará la mayor parte del beneficio con el mínimo esfuerzo.

### La Regla de Oro: Escribe el Asunto como si dieras una Orden

Piensa que tu mensaje de commit completa la frase: **"Si se aplica, este commit va a..."**

*   "...**Añadir** el capítulo sobre `git log`."
*   "...**Corregir** el error tipográfico en la introducción."
*   "...**Reestructurar** la sección de instalación."

Esto te obliga a seguir tres sencillas directrices:

1.  **Empieza siempre con un verbo de acción en imperativo:** `Añade`, `Corrige`, `Elimina`, `Modifica`, `Actualiza`, `Mejora`, `Simplifica`, `Implementa`, `Reestructura`.
2.  **Sé específico sobre el "qué":** No escribas "Arreglos". Escribe "Corrige el enlace roto a la política de privacidad".
3.  **Sé conciso:** Intenta que la línea no supere los 50-70 caracteres. Es el titular de una noticia, no la noticia entera.

### El Cuerpo del Mensaje: Explicando el "Porqué"

Si tu cambio es complejo y la línea de asunto no es suficiente, puedes añadir un cuerpo para explicar el **"porqué"** del cambio, no el "cómo" (para eso está el código o el `diff`).

Cuando estés en la pantalla de `git commit` (o `git commit --amend`), sigue esta estructura:

1.  Escribe tu línea de asunto (el titular) siguiendo la regla de oro.
2.  Deja una línea completamente en blanco.
3.  Escribe uno o dos párrafos cortos explicando el contexto y la motivación.

**Ejemplo de un mensaje de commit completo:**
```
El mensaje no es solo una nota sino más bien una entrada de diario estructurada. Obliga a pensar en el cambio de forma concisa y a documentar no solo lo que se hizo, sino la intención detrás de ello. Se facilita que un futuro lector pueda entender la naturaleza del cambio. 
El mensaje está ligado al `hash` del commit. Mediante el hash del `commit` se puede entender con precisión los cambios realizados (el `diff`) y su contexto.
Reestructura el capítulo de 'Primeros Pasos' para facilitar la lectura

La versión anterior del capítulo mezclaba los conceptos de instalación,
configuración y primer uso, lo que generaba tickets de soporte
recurrentes.

Este cambio divide el contenido en tres secciones distintas y numeradas,
siguiendo un flujo lógico para guiar al nuevo usuario desde cero hasta
tener el programa funcionando.
```
* **Titular:** Claro, imperativo, dice el *qué* y el *porqué* superficial.
* **Línea en blanco:** Crucial para separar asunto y cuerpo.
* **Cuerpo:** Explica el *contexto* (problema) y la *solución* (por qué fue necesario el trabajo).
