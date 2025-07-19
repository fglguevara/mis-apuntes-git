# Git- Control de versiones

## 1. Descripción del sistema actual del control de versiones.

Hasta ahora he gestionado el control de versiones cambiando el nombre del documento y añadiéndole sufijos. Por ejemplo, "documento v1", "documento v2", "documento v3". Como mucho me atrevo a utilizar una nomenclatura que diferencia cambios menores de mayores. Así: 'documento v2.1" -cambios menores respecto de la v2- 'documento v3' -cambios mayores respecto de la v2.1

Siendo un enfoque práctico pierdo información respecto a los cambios introducidos en cada versión. Eso sí puedo volver perfectamente a una versión anterior. Podría definir un documento explicativo `versiones.txt` que describiera los cambios realizados de una versión respecto de otra.

## 2. Reflexión sobre el sistema actual de control de versiones

Tu enfoque actual es muy lógico y, de hecho, es el primer sistema de control de versiones que casi todos hemos utilizado de forma intuitiva. Llamémoslo "Versionado por Nomenclatura". Es simple, directo y, como bien dices, te permite volver a una versión anterior sin problemas. El fichero `versiones.txt` es un añadido inteligente para mitigar una de sus grandes debilidades: la falta de contexto sobre los cambios.

Ahora, como tu gestor de proyectos y colega, quiero que reflexionemos juntos sobre este sistema. Imagina que no soy un programa, sino que estamos sentados con un café.

## 3. Las limitaciones del sistema actual ("Versionado por Nomenclatura")

Tu sistema funciona, pero tiene "fugas de información" y genera trabajo manual que, con el tiempo, se vuelve pesado.

1.  **El "Qué" es ambiguo:** Tu `versiones.txt` dice: "v2.1: Corregidos errores tipográficos y mejorada la introducción". Es útil, pero... ¿qué errores exactamente? ¿Cómo era la introducción *antes* y cómo es *ahora*? Para saberlo, tendrías que abrir la v2 y la v2.1 y compararlas a ojo. Esto es lento y propenso a errores.
2.  **El espacio se multiplica:** Si tu "documento" es en realidad una carpeta con varios ficheros (imágenes, textos, hojas de cálculo), cada vez que creas una nueva versión (`proyecto_v2`, `proyecto_v3`), estás duplicando *todos* los archivos, incluso los que no han cambiado. Esto consume mucho espacio innecesariamente.
3.  **El riesgo de la "versión final definitiva (ahora sí)":** Todos hemos caído en la trampa de `informe_final.docx`, `informe_final_entregar.docx`, `informe_final_corregido_por_jefe.docx`. El sistema de nombres se rompe fácilmente y genera confusión. ¿Cuál es el bueno?
4.  **Experimentar es arriesgado:** Quieres probar un cambio radical en la estructura del documento. Lo lógico es hacer un "Guardar como..." y llamarlo `documento_v3_prueba_estructura.docx`. Si la idea funciona, tienes que copiar y pegar manually los cambios al documento "oficial". Si no funciona, simplemente dejas ese archivo abandonado. Con el tiempo, tu directorio se llena de ramas muertas, de experimentos olvidados.

## 4. Presentando a Git: Tu Asistente de Versiones Personal

Ahora, olvida por un momento que Git es una herramienta para programadores. Piensa en Git como un asistente increíblemente meticuloso que observa tu trabajo. No guarda copias enteras de tu proyecto una y otra vez. En su lugar, hace algo mucho más inteligente: **registra únicamente los cambios**.

Vamos a comparar directamente tu flujo de trabajo con el que tendrías con Git.

| Característica | Tu Flujo Actual ("Versionado por Nomenclatura") | El Flujo con Git y GitHub |
| :--- | :--- | :--- |
| **Estructura de archivos** | Múltiples copias del mismo archivo/carpeta: `doc_v1`, `doc_v2`, `doc_v2.1`... | **Un único archivo/carpeta**: `documento`. Git gestiona el historial de forma invisible en una subcarpeta oculta llamada `.git`. Tu directorio de trabajo está siempre limpio. |
| **Guardar un cambio** | Guardas el archivo. Creas una copia con un nuevo nombre (`doc_v3`). Abres `versiones.txt` y anotas el cambio. | Guardas el archivo. Le dices a Git: "Oye, registra este cambio". Git te pide una descripción (un "mensaje de commit"). Por ejemplo: `"Se añade el párrafo sobre impacto económico en la introducción"`. **Este mensaje es tu `versiones.txt`, pero integrado, obligatorio y ligado a ese cambio exacto.** |
| **Ver qué ha cambiado** | Abres `doc_v2.1` y `doc_v3` y los comparas visualmente. | Le pides a Git: "Muéstrame las diferencias entre la versión actual y la anterior". Git te mostrará, línea por línea, qué texto has añadido (en verde) y cuál has borrado (en rojo). **Tienes una precisión quirúrgica sobre el cambio.** (Esto funciona de maravilla con archivos de texto plano, como .txt, .md, .html, etc.). |
| **Volver a una versión** | Borras el archivo actual y renombras una copia antigua. | Le dices a Git: "Quiero volver al estado de hace tres días a las 5 de la tarde". Y ¡listo! Tu archivo vuelve a ser exactamente como era en ese momento. Y no te preocupes, el historial más reciente no se borra, simplemente has "viajado en el tiempo". |
| **Experimentar** | Creas una copia (`doc_prueba_loca.docx`). Si funciona, copias y pegas. Si no, la abandonas. | Le dices a Git: "Crea una línea de tiempo paralela (una 'rama') para probar una idea". Trabajas en ella sin afectar a tu versión principal. ¿La idea fue buena? Le dices a Git: "Fusiona este experimento con la línea principal". Git lo hace automáticamente. ¿Fue mala? "Borra esta línea de tiempo". Sin desorden, sin archivos huérfanos. |
| **Seguridad / Backup** | Tu disco duro. Si falla, pierdes todas las versiones. Quizás una copia en un disco externo o en Google Drive, que sincroniza la versión actual. | Tu disco duro **Y** un repositorio remoto como GitHub. GitHub no es solo una copia de la última versión; es una **copia de seguridad completa de todo el historial de tu proyecto**. Si tu ordenador explota, clonas el repositorio desde GitHub en uno nuevo y tienes absolutamente todo de vuelta, cada cambio, cada mensaje, cada versión. |

## 5. El Beneficio Esperado de la Inversión

La inversión de tiempo no es en aprender un centenar de comandos, sino en interiorizar un flujo de trabajo nuevo y mucho más potente. Para tus necesidades, solo necesitas conocer 4 o 5 comandos básicos.

**El retorno de la inversión es inmediato y se manifiesta en:**

*   **Claridad Mental:** Tu carpeta de trabajo estará siempre limpia. Un solo `documento`, no diez.
*   **Confianza Absoluta:** Puedes hacer cualquier cambio, por drástico que sea, sabiendo que puedes volver al estado anterior en segundos con total precisión. Se acabó el miedo a "romper" algo.
*   **Un Diario de Proyecto Automático:** Cada "commit" es una entrada en el diario de tu proyecto. Dentro de seis meses, podrás ver no solo *qué* cambiaste, sino *por qué* lo hiciste (gracias a tus mensajes de commit).
*   **Profesionalización:** Estarás usando la herramienta estándar de la industria para la gestión de cualquier tipo de proyecto digital. Es una habilidad increíblemente valiosa.

---

## 6. ¡Manos a la Obra! Preparando el Terreno en GitHub

¡Excelente! Estás en lo cierto con los pasos a seguir. Necesitamos dos cosas de GitHub antes de poder tocar la terminal o la línea de comandos en tu ordenador: un **repositorio** donde vivirá nuestro proyecto en la nube, y un **token** para que tu ordenador tenga permiso para hablar con ese repositorio.

### 6.1. Paso 1: Crear el Repositorio Remoto en GitHub

Piensa en el repositorio como la "caja" o el "contenedor" central de tu proyecto.

1.  Inicia sesión en [GitHub.com](https://github.com).
2.  En la esquina superior derecha, haz clic en el icono `+` y selecciona **New repository**.
3.  **Repository name:** Elige un nombre corto y descriptivo. Como vamos a usarlo para tus apuntes, algo como `mis-apuntes-git` o `primer-repositorio` es perfecto.
4.  **Description (optional):** Escribe una frase corta que describa el proyecto. Ej: "Mis primeros pasos con Git y control de versiones".
5.  **Public / Private:** Puedes elegir si quieres que cualquiera vea tu proyecto (Público) o solo tú y quien tú invites (Privado). Para empezar, **te recomiendo seleccionar Privado**.
6.  **IMPORTANTE: No marques ninguna de estas casillas:**
    *   `Add a README file`
    *   `Add .gitignore`
    *   `Choose a license`
    *   **¿Por qué?** Queremos crear un repositorio completamente vacío. Si GitHub añade estos archivos, crea un historial inicial en la nube. Nosotros queremos crear el historial primero en nuestro ordenador y luego subirlo. Conectar un proyecto local a un repositorio que ya tiene historial es un poco más complejo, y queremos mantenerlo simple.
7.  Haz clic en el botón verde **Create repository**.

¡Listo! Ahora verás una página con instrucciones y una URL. La que nos interesa es la que empieza por `https://...`. Cópiala, la necesitaremos en un momento.

### 6.2. Paso 2: Generar un Token de Acceso Personal (PAT)

Estás totalmente en lo cierto, esta es la forma moderna y segura de autenticarse. Antes usábamos nuestra contraseña de GitHub, pero eso era poco seguro. Un token es como una contraseña de un solo uso o para una aplicación específica.

1.  En GitHub, haz clic en tu foto de perfil (esquina superior derecha) y ve a **Settings**.
2.  En el menú de la izquierda, baja del todo y haz clic en **Developer settings**.
3.  En el nuevo menú de la izquierda, haz clic en **Personal access tokens** y luego en **Tokens (classic)**.
4.  Haz clic en el botón **Generate new token** y selecciona **Generate new token (classic)**.
5.  **Note:** Dale un nombre que te recuerde para qué es. Por ejemplo: `Token para Git en mi PC`.
6.  **Expiration:** Por seguridad, los tokens caducan. 30 o 90 días es una buena opción. Siempre puedes generar otro.
7.  **Select scopes:** Esta es la parte más importante. Aquí defines qué permisos le das a este token. Para lo que queremos hacer (subir y bajar cambios de nuestros repositorios), solo necesitas marcar **la casilla principal que dice `repo`**. Al marcarla, se seleccionarán automáticamente todos sus permisos secundarios. Es todo lo que necesitas.
8.  Baja hasta el final y haz clic en **Generate token**.

**¡¡MÁXIMA ATENCIÓN!!**
GitHub te mostrará el token **una sola vez**. En cuanto abandones o refresques la página, desaparecerá para siempre.

*   **Copia la cadena de letras y números (empieza por `ghp_...`) inmediatamente.**
*   **Pégala en un lugar seguro y temporal.** Un bloc de notas, un gestor de contraseñas... donde sea, pero que no se te pierda en los próximos 10 minutos.

Cuando tu ordenador te pida la contraseña para conectar con GitHub, no pondrás tu contraseña real, sino que pegarás este token.

---

**Tu Misión (si decides aceptarla):**

Completa estos dos pasos. Cuando tengas la **URL de tu repositorio vacío** y el **token copiado y a buen recaudo**, avísame.

Entonces, pasaremos a la parte más emocionante: abrir una terminal en tu ordenador y ejecutar los 3-4 comandos que darán vida a tu control de versiones local y lo conectarán con la nube.

¡Fantástico! Ya hemos superado la parte "administrativa" y tenemos todo lo necesario para construir el puente entre tu ordenador y la nube de GitHub. Ahora viene la parte divertida, donde vemos la magia en acción.

Continuemos con tus apuntes. Añadiremos la sección sobre cómo dar vida al repositorio en tu máquina local.

---

## 7. Dando Vida al Repositorio Local y Conectándolo a GitHub

Aquí es donde tu directorio local se convierte en un repositorio de Git "inteligente" y aprende a hablar con su gemelo en GitHub. Asumiré que ya tienes Git instalado en tu ordenador. Si no es así, puedes descargarlo desde [git-scm.com].

Todo lo que sigue lo haremos desde una **terminal** o **línea de comandos**. No te asustes, verás que son solo unas pocas instrucciones muy concretas.

### 7.1. Paso 1: Preparar el Directorio Local

1.  **Crea una carpeta para tu proyecto.** Puedes llamarla igual que tu repositorio en GitHub para mantener la coherencia. Por ejemplo, `mis-apuntes-git`.
2.  **Mete tus archivos dentro.** Coge ese archivo Markdown donde estás tomando notas y ponlo dentro de esta nueva carpeta.
3.  **Abre una terminal DENTRO de esa carpeta.** Este paso es crucial.
    *   En Windows: Navega hasta la carpeta, haz clic derecho en un espacio en blanco y selecciona "Abrir en Terminal" o "Git Bash Here" (si lo instalaste con Git).
    *   En Mac/Linux: Abre la aplicación de Terminal, escribe `cd ` (con un espacio al final), y arrastra la carpeta de tu proyecto desde el Finder/explorador de archivos a la ventana de la terminal. Esto pegará la ruta correcta. Luego presiona Enter.

### 7.2. Paso 2: El Bautizo (`git init`)

Ahora le diremos a Git que empiece a "observar" esta carpeta.

Escribe el siguiente comando en tu terminal y presiona Enter:

```bash
git init
```

*   **¿Qué hace esto?** Este comando crea una subcarpeta oculta llamada `.git`. Ahí es donde nuestro "asistente meticuloso" (Git) guardará todo el historial, todas las versiones y toda la información del proyecto. No necesitas tocar nada dentro de esa carpeta, pero es el cerebro de tu repositorio.

### 7.3. Paso 3: La Lista de Ignorados (`.gitignore`)

Como te comenté, hay ciertos archivos que no queremos guardar en nuestro historial (archivos temporales, secretos, archivos de configuración del sistema operativo, etc.). Le diremos a Git que los ignore creando un archivo especial.

1.  **Crea un archivo de texto** dentro de tu carpeta de proyecto y nómbralo exactamente así: `.gitignore` (sí, empieza con un punto).
2.  **Ábrelo con un editor de texto** y añade contenido. Para un proyecto de documentación, un buen punto de partida es ignorar los archivos de sistema comunes:

    ```
    # Archivos de sistema operativo
    .DS_Store
    Thumbs.db

    # Archivos temporales de editores
    *.tmp
    *.swp
    ```

*   **¿Qué hace esto?** Cualquier archivo o patrón que escribas en `.gitignore` será completamente invisible para Git. Es como darle a tu asistente una lista de cosas en las que no debe fijarse.

### 7.4. Paso 4: Tu Primer "Guardado" (`add` y `commit`)

Este es el flujo de trabajo que repetirás cada vez que quieras guardar un punto de control. Consta de dos pasos:

1.  **Preparar los archivos para la "foto" (`git add`)**: Le dices a Git qué cambios específicos quieres incluir en el próximo punto de guardado. 
  ` git add . `

2.  **Tomar la "foto" y describirla (`git commit`)**: Guardas permanentemente esos cambios en el historial con un mensaje que explica qué hiciste.

En tu terminal, ejecuta estos dos comandos, uno después del otro:

```bash
# 1. Añade TODOS los archivos nuevos o modificados de la carpeta (excepto los ignorados)
git add .

# 2. Guarda los cambios en el historial con un mensaje descriptivo
git commit -m "Commit inicial: Creación del proyecto y notas iniciales"
```

*   **¿Qué hemos hecho?** Acabas de crear la **primera versión oficial** de tu proyecto en tu historial local. El mensaje `"Commit inicial..."` es tu nuevo `versiones.txt`, pero ligado de forma precisa e imborrable a este momento exacto.

### 7.5. Paso 5: Conectar con la Nube y Subir tu Trabajo (`remote` y `push`)

Ya tienes el historial en tu ordenador. Ahora vamos a conectarlo con esa "caja fuerte" vacía que creamos en GitHub y a subirle una copia.

1.  **Enseña a tu repositorio local la dirección del remoto:**
    *   Coge la URL de tu repositorio que copiaste de GitHub (la que termina en `.git`).
    *   Ejecuta este comando, **reemplazando `URL_DE_TU_REPOSITORIO`** con tu URL:

    ```bash
    git remote add origin URL_DE_TU_REPOSITORIO
    ```
    *   *Explicación*: `remote add` añade un control remoto. `origin` es el nombre corto que, por convención, le damos a nuestra URL principal.

2.  **Renombra tu línea de tiempo principal a `main`:** Es una buena práctica moderna.
    ```bash
    git branch -M main
    ```

3.  **Sube tu historial a GitHub (`git push`):**
    ```bash
    git push -u origin main
    ```
    *   *Explicación*: `push` significa "empujar" o "subir". Le estás diciendo a Git: "sube el contenido de mi línea de tiempo local `main` al destino `origin`". La bandera `-u` es especial para la primera vez, y crea un enlace para que en el futuro solo necesites escribir `git push`.

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

    ```bash
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

## 8. El Panel de Control: Verificando Cambios (`git status` y `git diff`)

Una vez que el repositorio está conectado, necesitas una forma de saber qué ha cambiado desde tu último punto de guardado (tu último `commit`). Git te ofrece dos comandos principales para esto: uno te da una vista general y el otro, una vista detallada.

### 8.1. La Vista General: `git status`

Piensa en `git status` como preguntarle a tu asistente: **"¿Cuál es la situación actual del proyecto?"**. Te dirá si hay cambios, si hay archivos nuevos, si todo está guardado y limpio, etc. Es el primer comando que debes ejecutar cuando vuelves a un proyecto después de un tiempo.

**Vamos a probarlo ahora mismo.** Ve a tu terminal, asegúrate de estar en la carpeta de tu proyecto, y ejecuta:

```bash
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

```bash
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
*   
F: Línea modificada 

### 8.2. La Vista Detallada: `git diff`

`git status` te dice **QUÉ** archivos han cambiado. Pero `git diff` (de "diferencia") te muestra **EXACTAMENTE QUÉ LÍNEAS** han cambiado dentro de esos archivos. Es tu herramienta para resolver la duda que tenías con tu sistema antiguo: "¿Qué cambié exactamente entre la v2 y la v2.1?".

Con los cambios que acabas de hacer, ejecuta este comando:

```bash
git diff
```

La salida será algo así (puede que te la muestre con `less`, ¡ya sabes cómo salir con `q`!):

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

### Resumen Práctico

*   **¿Quiero saber si he cambiado algo?** -> `git status`
*   **¿Quiero saber qué he cambiado exactamente?** -> `git diff`

Ahora que has visto los cambios, el siguiente paso lógico sería guardarlos. ¿Recuerdas el ciclo?

1.  `git add .` (para preparar los cambios que te mostró `git status`)
2.  `git commit -m "Añadida la sección sobre git status y diff"` (para guardar la "foto")
3.  `git push` (para subir la nueva versión a tu copia de seguridad en GitHub)

Este ciclo (`modificar -> status/diff -> add -> commit -> push`) es el 90% del uso diario de Git para un usuario individual. ¡Lo estás haciendo genial



## 9. La Tríada Mágica: `add`, `commit` y `push`

Imagina que tu proyecto no es una carpeta en tu ordenador, sino que estás organizando un envío de paquetes desde tu casa a un almacén central seguro (que sería GitHub).

En este escenario, tienes tres áreas de trabajo:

1.  **Tu Mesa de Trabajo (El Directorio de Trabajo):** Aquí es donde tienes todos los documentos y herramientas. Modificas los archivos, escribes, borras, creas... es tu zona de "caos" creativo.
2.  **La Caja de Envío (El "Staging Area"):** Es una caja de cartón vacía que tienes al lado de la mesa. Antes de sellarla, decides qué documentos de tu mesa vas a meter dentro para este envío en particular.
3.  **Tu Almacén Local (El Repositorio Local, la carpeta `.git`):** Es una estantería en tu garaje. Aquí guardas todas las cajas que ya has sellado y etiquetado, listas para que el camión de reparto se las lleve. Están a salvo dentro de tu casa.
4.  **El Almacén Central (El Repositorio Remoto en GitHub):** Es el almacén de alta seguridad al que envías tus paquetes para tener una copia perfecta y accesible desde cualquier lugar.

Ahora, veamos qué hace cada comando en esta analogía.

### 1. `git add` - "Meter cosas en la caja"

*   **Qué haces:** Coges un documento modificado de tu mesa de trabajo y lo metes **dentro de la caja de envío**.
*   **Comando:** `git add mi-archivo.md` (mete ese archivo específico) o `git add .` (mete todos los archivos que hayas modificado en la mesa).
*   **Propósito:** Este es un paso intermedio y es **extremadamente útil**. Te permite ser selectivo. Imagina que has modificado 5 archivos en tu mesa, pero solo 3 de ellos pertenecen a la misma "idea" o "tarea". Con `git add`, puedes meter solo esos 3 archivos en la caja, dejando los otros 2 en la mesa para un envío posterior. Permite crear "puntos de guardado" limpios y lógicos.

**En resumen: `git add` no guarda nada de forma permanente. Solo prepara los cambios para el siguiente guardado.**

### 2. `git commit` - "Precintar y etiquetar la caja"

*   **Qué haces:** Coges la caja de envío (que ya tiene dentro los archivos que seleccionaste con `git add`), la cierras con cinta adhesiva y le escribes una etiqueta clara en el exterior que describe su contenido. Por ejemplo: "Contiene el borrador del capítulo 5 y la corrección de la introducción".
*   **Comando:** `git commit -m "Este es el mensaje de mi etiqueta"`
*   **Propósito:** Este es el **verdadero acto de guardar**. Creas un punto de control permanente y seguro en tu historial. La caja (el "commit") se mueve desde la zona de preparación a tu **almacén local** (tu garaje). El cambio ya está registrado para siempre en tu ordenador. **Importante: en este punto, GitHub todavía no sabe nada de esta nueva caja.**

**En resumen: `git commit` crea un punto de guardado permanente en el historial de TU ordenador.**

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


***

# Guía Rápida de Git y GitHub

Este documento es una referencia ágil para el uso diario de Git y la sincronización con un repositorio en GitHub.

---

## 1. Conceptos Fundamentales: ¿Por Qué Usar Git?

Git reemplaza el método manual de guardar versiones (`doc_v1`, `doc_v2`) por un sistema profesional que resuelve sus principales problemas:

| Característica | Sistema Manual | Flujo con Git y GitHub |
| :--- | :--- | :--- |
| **Estructura** | Múltiples copias del mismo archivo/carpeta. | **Un único archivo/carpeta**. El historial es invisible y se gestiona en la subcarpeta `.git`. |
| **Guardado** | Renombrar archivo + anotar cambios en un `.txt` aparte. | `git commit -m "Descripción del cambio"`. El mensaje está ligado inseparablemente al cambio exacto. |
| **Ver Cambios** | Comparar dos archivos visualmente, a ojo. | `git diff` muestra con precisión quirúrgica las líneas añadidas y eliminadas. |
| **Seguridad** | Depende de tu disco duro y copias manuales. | Tu disco duro **Y** una copia completa de todo el historial en GitHub. |
| **Experimentar** | Arriesgado. Genera desorden con archivos de prueba. | Se usan "ramas" (`branch`), líneas de tiempo paralelas que se pueden fusionar o descartar limpiamente. |

---

## 2. Configuración Inicial (Solo se hace una vez)

Pasos para configurar un proyecto desde cero.

### En GitHub:

1.  **Crear Repositorio:** Haz clic en `+` > **New Repository**.
2.  **Configurar:**
    *   **Nombre:** Corto y descriptivo (ej: `mis-apuntes-git`).
    *   **Privacidad:** Selecciona **Privado**.
    *   **IMPORTANTE:** NO marcar las casillas de `README`, `.gitignore` o `license`. Debe ser un repositorio vacío.
3.  **Copiar URL:** Guarda la URL del repositorio (la que termina en `.git`).

### En tu Ordenador:

1.  **Configurar tu identidad de Git** (una vez por ordenador):
    ```bash
    git config --global user.name "Tu Nombre"
    git config --global user.email "tu_email@ejemplo.com"
    ```
2.  **Iniciar el repositorio** en la carpeta de tu proyecto:
    ```bash
    git init
    ```
3.  **Crear un archivo `.gitignore`** para excluir ficheros innecesarios. Contenido de ejemplo:
    ```
    # Archivos de sistema operativo
    .DS_Store
    Thumbs.db
    # Archivos temporales
    *.tmp
    *.swp
    ```4.  **Conectar tu repositorio local con GitHub:**
    ```bash
    # Reemplaza la URL con la tuya
    git remote add origin https://github.com/tu-usuario/tu-repo.git
    ```
5.  **Establecer `main` como la rama principal:**
    ```bash
    git branch -M main
    ```

---

## 3. El Flujo de Trabajo Diario

Este es el ciclo que repetirás constantemente para guardar y sincronizar tus cambios.

### Paso 0: Revisar el Estado del Proyecto

Antes de hacer nada, comprueba la situación actual.

*   **`git status`**: Te da una vista general. ¿Hay archivos modificados, nuevos o preparados para guardar?
*   **`git diff`**: Te muestra el detalle exacto de los cambios, línea por línea.

### Paso 1: Preparar los Cambios (`git add`)

Seleccionas qué cambios quieres incluir en tu próximo punto de guardado. Esto se conoce como "añadir al Staging Area".

*   Para preparar **todos** los archivos modificados:
    ```bash
    git add .
    ```
*   Para preparar un archivo **específico**:
    ```bash
    git add nombre-del-archivo.md
    ```

### Paso 2: Guardar los Cambios Localmente (`git commit`)

Creas un punto de guardado permanente en el historial de tu ordenador.

*   Guarda los cambios preparados con un mensaje descriptivo y obligatorio:
    ```bash
    git commit -m "Se añade la sección de conceptos fundamentales a las notas"
    ```
    *(Consejo: Escribe mensajes claros y en presente, como si dieras una orden: "Añade", "Corrige", "Mejora")*.

### Paso 3: Sincronizar con GitHub (`git push`)

Envías tus "commits" (puntos de guardado) locales al repositorio remoto en la nube.

*   La **primera vez** que subes los cambios:
    ```bash
    git push -u origin main
    ```
*   Para **todas las veces siguientes**:
    ```bash
    git push
    ```

---

## 4. La Tríada Mágica: `add`, `commit`, `push`

La diferencia clave para entender Git, resumida en una tabla.

| Comando | Analogía | Propósito Técnico | ¿Dónde Ocurre? |
| :--- | :--- | :--- | :--- |
| **`git add`** | Meter archivos en una caja de envío. | Añade cambios al **Staging Area**. | En tu ordenador. |
| **`git commit`** | Precintar y etiquetar la caja. | Guarda una "instantánea" en el **historial local**. | En tu ordenador. |
| **`git push`** | Enviar la caja al almacén central. | Sube los commits al **repositorio remoto (GitHub)**. | Entre tu PC y GitHub. |

**El Flujo Visual:**
`Directorio de Trabajo` --> **`git add`** --> `Staging Area` --> **`git commit`** --> `Repositorio Local` --> **`git push`** --> `GitHub`