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