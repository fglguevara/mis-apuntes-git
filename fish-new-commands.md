# Nuevos comandos instalados en `Fish`

En el chat de Copilot se puede chatear con  
@github, @Copilot, @vscode, @workspace
You can also help me understand your question by using the following variables:

- #file

## Preguntándole a `@terminal` sobre un uso sencillo del comando `grep`

```fish
grep "{pattern}" {file}
```

{pattern}: The text pattern you want to search for
{file}: The file you want to search in

Here are some examples of how to use `grep`:
Search for a pattern in a file:

```fish
grep "hello" file.txt
```

Case-insensitive search:

```fish
grep -i "hello" file.txt
```

Search recursively in all files :

```fish
grep -r "hello" .
```

Show line numbers in the output:

```fish
grep -n "hello" file.txt
```

Search for whole words only:

```fish
grep -w "hello" file.txt
```

Invert match (show lines that do not match):

```fish
grep -v "hello" file.txt
```

Search for a pattern in multiple files:

```fish
grep "hello" file1.txt file2.txt
```

Search for a pattern in files with a specific extension:

```fish
grep "hello" *.txt
```

Count matching lines:

```fish
grep -c "hello" file.txt
```

## Ventajas de utilizar `grep` sobre utilizar la búsqueda en VSC

1. **Rendimiento**: `grep` es una herramienta de línea de comandos que puede ser más rápida que la búsqueda en un IDE, especialmente en proyectos grandes.
2. **Flexibilidad**: `grep` ofrece una amplia gama de opciones y patrones de búsqueda que pueden no estar disponibles en la búsqueda de VSC.
   - `grep -E "(error|warning|fatal)" *.log`
3. **Integración en scripts**: `grep` se puede utilizar fácilmente en scripts de shell y automatización, lo que permite flujos de trabajo más eficientes.
   ```fish
   if grep -q "TODO" *.js; then
     echo "Hay tareas pendientes"
   fi
   ```
4. **Uso de tuberías**: `grep` se puede combinar con otras herramientas de línea de comandos a través de tuberías, lo que permite un procesamiento de texto más poderoso y flexible.
   - `grep -v "debug" logfile.txt | grep "user"`

## Comandos alternativos a grep

`ripgrep`(rg)

```fish
    rg "pattern" file.txt
    rg -i "error" *.log          # Case insensitive
    rg -r "function" .           # Recursive search
    # Buscar en archivos .md específicamente
    rg --type md "sistema de estilo"
    # Buscar patrones de Markdown (encabezados)
    rg "^#{1,6}\s" *.md
    # Buscar código en bloques (backticks)
    rg "`[^`]+`" guia-estilo-marcadores.md
    # Buscar enlaces de Markdown
    rg "\[.*\]\(.*\)" *.md
```

- Más rápido que grep tradicional sobre todo en archivos grandes
- Sintaxis más intuitiva, simple y moderna
- Mejor soporte para "Unicode"
- Salida más clara: Colores por defecto y mejor formato
- Buena gestión de expresiones regulares complejas para Markdown

#### Uso básico de `ripgrep`. Primeros pasos.

1. Instalación mediante `brew` y `rg --version`para verificar instalación
1. Búsqueda simple
   - # Buscar una palabra en archivos del directorio actual
     rg "énfasis"
   - # Buscar en un archivo específico
     rg "sistema de estilo" Guia-estilo-marcadores.md
1. Búsquedas específicas para Markdown

### Fuzzy Finder `fzf` el comando de búsqueda más potente

    - Interfaz interactiva para navegar resultados
    - Preview en tiempo real del contenido
    - Filtrado progresivo mientras escribes

### Bat para visualización

### `fd`Para búsqueda de archivos (alternativa a `find`)

En resumen: `fd` es la versión moderna y eficiente del comando `find` - perfecto para localizar archivos rápidamente antes de usar ripgrep para buscar contenido dentro de ellos.

Para trabajar con documentación técnica como tu guía, la combinación `fd + fzf + ripgrep + bat` es superior a cualquier herramienta individual. Te permite:

    - Encontrar archivos rápidamente (fd)
    - Buscar contenido eficientemente (ripgrep)
    - Navegar resultados interactivamente (fzf)
    - Visualizar con sintaxis highlighting (bat)

# Nuevos comandos que deberías conocer

#### 1. `ripgrep` (rg)

- **Corrección en la expresión regular:** Tu ejemplo para buscar enlaces de Markdown `[.*]\(.*\)` es conceptualmente correcto, pero en la mayoría de los shells, los corchetes `[]` y los paréntesis `()` son caracteres especiales que necesitan ser escapados con una barra invertida `\` para que la expresión regular funcione como esperas.
  - **Correcto:** `rg '\[.*\]\(.*\)' *.md`
- **Mejora:** Has capturado perfectamente sus ventajas. `ripgrep` es increíblemente rápido porque está construido sobre el motor de regex de Rust, que utiliza automatización de estados finitos, y realiza búsquedas en paralelo de forma predeterminada. [[1]](https://simonwillison.net/2019/Apr/16/ripgrep/)[[2]](https://blog.burntsushi.net/ripgrep/) Además, ignora de forma inteligente los archivos binarios y los directorios ocultos o definidos en `.gitignore`, lo que lo hace ideal para trabajar en repositorios de código. [[3]](https://docs.rs/fd-find/6.2.0)

#### 2. `fzf` (Fuzzy Finder)

- **Ampliación del concepto:** Lo describes como un "comando de búsqueda potente", lo cual es cierto, pero su verdadero poder reside en que es un **filtro interactivo de propósito general**. `fzf` lee una lista de elementos de la entrada estándar (stdin), te permite filtrarla de forma difusa (fuzzy) y luego imprime el elemento seleccionado en la salida estándar (stdout). Esto lo hace increíblemente componible.
- **Ejemplos más potentes:**
  - **Navegar el historial de comandos:** Presiona `CTRL+R` (si lo tienes configurado) y busca interactivamente en tu historial. [[4]](https://logico.ar/blog/2019/07/13/fzf-el-buscador-nix)
  - **Cambiar de rama en Git:** `git branch | fzf | xargs git checkout`
  - **Matar procesos:** `ps -ef | fzf | awk '{print $2}' | xargs kill -9`

#### 3. La Combinación Dorada: `fd` + `fzf` + `rg` + `bat`

Tu resumen es perfecto. Esta combinación es el "santo grial" del flujo de trabajo moderno en la terminal. Aquí tienes un ejemplo práctico que une todo y muestra su poder:

**Objetivo:** _Buscar interactivamente un archivo de Markdown (`.md`) en el directorio actual, previsualizar su contenido con resaltado de sintaxis y, una vez seleccionado, buscar dentro de ese archivo una palabra específica._

```fish
# 1. fd encuentra todos los archivos .md
# 2. fzf los muestra en una lista interactiva con previsualización de bat
# 3. rg busca "patrón" dentro del archivo seleccionado por fzf
rg "patrón" (fd --type f --extension md | fzf --preview "bat --color=always --style=numbers {}")
```

- **`fd --type f --extension md`**: Encuentra todos los archivos (`-t f`) con la extensión `md`. [[5]](https://www.linode.com/docs/guides/finding-files-with-fd-command/)[[6]](https://www.baeldung.com/linux/fd-find-alternative)
- **`| fzf --preview "..."`**: La salida de `fd` (la lista de archivos) se envía a `fzf`. [[4]](https://logico.ar/blog/2019/07/13/fzf-el-buscador-nix) `fzf` la muestra interactivamente. Para cada línea (archivo) que resaltas, ejecuta el comando de previsualización. [[7]](https://www.youtube.com/watch?v=aLMepxvUj4s)[[8]](https://www.youtube.com/watch?v=Dt6gAzmqyoc)
- **`bat --color=always --style=numbers {}`**: `bat` muestra el contenido del archivo (`{}` es el marcador de posición para el elemento seleccionado) con colores y números de línea. [[7]](https://www.youtube.com/watch?v=aLMepxvUj4s)
- **`rg "patrón" (...)`**: `rg` toma el archivo que finalmente seleccionas en `fzf` y busca el "patrón" dentro de él.

---

### **Nuevos Comandos que Deberías Conocer**

¡Absolutamente! Dado tu interés, aquí tienes una lista de herramientas que siguen la misma filosofía de `rg`, `fd`, `fzf` y `bat`. Casi todas están escritas en Rust, lo que garantiza un rendimiento excepcional.

#### 1. **`eza` (Alternativa a `ls`)**

`eza` es un reemplazo moderno y mantenido para el comando `ls`. [[9]](https://eza.rocks/)[[10]](https://terminaltrove.com/eza/) Es un _fork_ del proyecto `exa` (que ya no tiene mantenimiento activo) y lo mejora. [[11]](https://denisrasulev.medium.com/eza-the-best-ls-command-replacement-f6f6af6a5839)

- **¿Por qué es mejor?**

  - **Colores y iconos:** Utiliza colores para distinguir tipos de archivos y metadatos, y puede mostrar iconos si tienes una "Nerd Font" instalada. [[12]](https://www.datadice.io/en/blog/upgrade-your-ls-command-to-eza)
  - **Información útil:** Muestra permisos, tamaño, fechas, e incluso el estado de Git de los archivos de un vistazo. [[13]](https://github.com/eza-community/eza)
  - **Vistas avanzadas:** Incluye una vista de árbol (`--tree`) y una vista de cuadrícula (`--grid`). [[12]](https://www.datadice.io/en/blog/upgrade-your-ls-command-to-eza)

- **Ejemplo de uso:**
  ```fish
  # Reemplaza 'ls -l' con algo mucho más informativo
  eza --long --header --git --icons
  ```

#### 2. **`zoxide` (Alternativa a `cd`)**

`zoxide` es una reinvención del comando `cd`. [[14]](https://mskelton.dev/bytes/zoxide-a-smarter-cd-command)[[15]](https://medium.com/quick-programming/using-zoxide-to-superpower-your-cd-command-in-linux-e74d9327ced9) Aprende de los directorios que más visitas y te permite saltar a ellos con pocas pulsaciones. [[16]](https://github.com/ajeetdsouza/zoxide)[[17]](https://www.reddit.com/r/commandline/comments/1clcfr9/i_love_zoxide/)

- **¿Por qué es mejor?**

  - **Navegación por "frecuencia":** En lugar de escribir rutas largas, saltas a un directorio basándote en una parte de su nombre. `zoxide` te llevará al que mejor coincida con tus hábitos. [[15]](https://medium.com/quick-programming/using-zoxide-to-superpower-your-cd-command-in-linux-e74d9327ced9)
  - **Interactivo:** Se integra perfectamente con `fzf` para mostrarte una lista interactiva si hay varias coincidencias. [[18]](https://dev.to/chamal1120/zoxide-a-faster-alternative-to-boring-cd-command-1ae3)
  - **Rápido y compatible:** Es extremadamente rápido y funciona en todos los shells principales (Bash, Zsh, Fish). [[16]](https://github.com/ajeetdsouza/zoxide)

- **Ejemplo de uso:**

  ```fish
  # Si visitas frecuentemente /home/user/projects/work/documentation
  # Simplemente escribe:
  z doc

  # Si hay varias carpetas con "doc", puedes buscar interactivamente:
  zi doc
  ```

#### 3. **`sd` (Alternativa a `sed` para reemplazar)**

`sd` es una alternativa intuitiva para buscar y reemplazar, inspirada en la simplicidad. [[19]](https://terminaltrove.com/sd/)[[20]](https://www.youtube.com/watch?v=Kps2uLk-1KU) Mientras que `sed` es increíblemente potente, su sintaxis puede ser críptica para tareas simples. [[21]](https://github.com/chmln/sd)

- **¿Por qué es mejor?**

  - **Sintaxis simple y legible:** `sd 'texto_a_buscar' 'texto_de_reemplazo'`. No más barras inclinadas confusas ni la necesidad de recordar la bandera `-i` para editar en el sitio. [[21]](https://github.com/chmln/sd)[[22]](https://www.reddit.com/r/rust/comments/a9sncx/sd_an_intuitive_find_replace_cli_sed_alternative/)
  - **Expresiones regulares modernas:** Usa la sintaxis de regex a la que probablemente ya estás acostumbrado (similar a la de Python o JavaScript). [[21]](https://github.com/chmln/sd)

- **Ejemplo de uso:**
  ```fish
  # Reemplazar todas las instancias de "color" por "colour" en un archivo
  sd "color" "colour" guia-estilo.md
  ```

#### 4. **`jq` (Procesador de JSON)**

Si trabajas con APIs, logs o cualquier dato en formato JSON, `jq` es indispensable. Es como `sed` o `awk`, pero diseñado específicamente para JSON. [[23]](https://vergaracarmona.es/guia-del-comando-jq/)[[24]](https://www.linode.com/docs/guides/using-jq-to-process-json-on-the-command-line/?lang=es)

- **¿Por qué es indispensable?**

  - **Filtrado y extracción:** Permite extraer valores de estructuras JSON complejas con una sintaxis de filtros muy potente. [[25]](https://geekland.eu/extraer-datos-de-ficheros-json-con-jq/)[[26]](https://helloit.es/2020/06/introduccion-a-jq-con-ejemplos/)
  - **Transformación:** Puedes reestructurar, combinar y transformar datos JSON directamente desde la terminal. [[25]](https://geekland.eu/extraer-datos-de-ficheros-json-con-jq/)
  - **Composición:** Se integra perfectamente en pipelines con `curl` para procesar respuestas de API.

- **Ejemplo de uso:**
  ```fish
  # Obtener los nombres de todos los repositorios de un usuario de GitHub
  curl -s "https://api.github.com/users/google/repos" | jq '.[].name'
  ```

#### 5. **`tldr` (Alternativa a `man`)**

Las páginas `man` son completas, pero a menudo demasiado largas cuando solo necesitas un ejemplo rápido. [[27]](https://www.redhat.com/en/blog/tldr-linux) `tldr` (Too Long; Didn't Read) te da exactamente eso: ejemplos prácticos y concisos. [[28]](https://www.tecmint.com/tldr-easy-to-understand-linux-man-pages/)[[29]](https://tldr.sh/)

- **¿Por qué es mejor?**

  - **Basado en ejemplos:** Muestra los 5-8 casos de uso más comunes de un comando en lugar de una documentación exhaustiva. [[27]](https://www.redhat.com/en/blog/tldr-linux)
  - **Gestionado por la comunidad:** Las páginas son mantenidas y actualizadas por la comunidad, asegurando que los ejemplos sean relevantes. [[30]](https://github.com/tldr-pages/tldr)
  - **Rápido y al grano:** Es la herramienta perfecta para refrescar la memoria. [[31]](https://www.geeksforgeeks.org/linux-unix/tldr-read-man-pages-in-simple-format/)

- **Ejemplo de uso:**
  ```fish
  # ¿Cómo descomprimir un archivo .tar.gz?
  tldr tar
  ```

#### 6. **`dust` (Alternativa a `du`)**

`dust` es una versión más intuitiva de `du` (disk usage) que te ayuda a visualizar qué directorios están ocupando más espacio. [[32]](https://opensource.com/article/21/6/dust-linux)[[33]](https://www.linode.com/docs/guides/dust-command-on-linux-installation/)

- **¿Por qué es mejor?**

  - **Salida visual:** Muestra un árbol de directorios ordenado por tamaño, con barras de colores que facilitan la identificación de los más pesados. [[34]](https://medium.com/@okoanton/dust-instead-of-du-fa0e4a3ad597)[[35]](https://www.x-cmd.com/pkg/dust/)
  - **Inteligente por defecto:** Automáticamente profundiza en los directorios más grandes para mostrarte dónde se concentra el uso del disco. [[33]](https://www.linode.com/docs/guides/dust-command-on-linux-installation/)

- **Ejemplo de uso:**
  ```fish
  # Analiza el directorio actual y muestra un resumen visual
  dust
  ```

#### 7. **`procs` (Alternativa a `ps`)**

`procs` es un reemplazo moderno para `ps` que muestra información sobre los procesos del sistema de una manera más legible y colorida. [[36]](https://www.linode.com/docs/guides/view-active-linux-processes-with-procs/)[[37]](https://www.linuxuprising.com/2021/05/procs-is-modern-replacement-for-ps-with.html)

- **¿Por qué es mejor?**

  - **Salida legible:** Columnas bien organizadas, con colores y formato amigable. [[38]](https://users.rust-lang.org/t/procs-a-modern-replacement-for-ps-written-in-rust/24794)
  - **Información adicional:** Puede mostrar puertos TCP/UDP, rendimiento de E/S y nombres de contenedores Docker. [[39]](https://github.com/dalance/procs)
  - **Funcionalidades modernas:** Incluye un modo de vigilancia (como `top`) y una vista de árbol. [[39]](https://github.com/dalance/procs)

- **Ejemplo de uso:**
  ```fish
  # Busca todos los procesos que contengan la palabra "fish"
  procs fish
  ```

### **Resumen Final**

Aquí tienes una tabla resumen para que tengas una referencia rápida:

| Tarea Clásica            | Comando Clásico | Alternativa Moderna |
| :----------------------- | :-------------- | :------------------ |
| Listar archivos          | `ls`            | **`eza`**           |
| Buscar contenido         | `grep`          | **`rg` (ripgrep)**  |
| Buscar archivos          | `find`          | **`fd`**            |
| Cambiar directorio       | `cd`            | **`zoxide`**        |
| Ver archivos             | `cat`           | **`bat`**           |
| Reemplazar texto         | `sed`           | **`sd`**            |
| Ver uso de disco         | `du`            | **`dust`**          |
| Ver procesos             | `ps`            | **`procs`**         |
| Leer manuales            | `man`           | **`tldr`**          |
| Filtrar interactivamente | (N/A)           | **`fzf`**           |
| Procesar JSON            | (Varios)        | **`jq`**            |

Integrar estas herramientas en tu flujo de trabajo diario con `fish` a través de alias y funciones personalizadas te dará una productividad y una experiencia de usuario muy superiores. ¡Has empezado por un camino excelente

---

Learn more:

1. [ripgrep is faster than {grep, ag, git grep, ucg, pt, sift} - Simon Willison's Weblog](https://simonwillison.net/2019/Apr/16/ripgrep/)
2. [ripgrep is faster than {grep, ag, git grep, ucg, pt, sift} - Andrew Gallant's Blog](https://blog.burntsushi.net/ripgrep/)
3. [fd-find 6.2.0 - Docs.rs](https://docs.rs/fd-find/6.2.0)
4. [FZF - EL buscador \*nix. - Lógico Blog](https://logico.ar/blog/2019/07/13/fzf-el-buscador-nix)
5. [How to Find Files With the fd Command | Linode Docs](https://www.linode.com/docs/guides/finding-files-with-fd-command/)
6. [fd: An Alternative to the Linux find Command - Baeldung](https://www.baeldung.com/linux/fd-find-alternative)
7. [Using FZF to Preview Text Files on the Command Line and within Vim - YouTube](https://www.youtube.com/watch?v=aLMepxvUj4s)
8. [Navega como un ninja en tu Terminal con fzf (Linux y Mac) Previsualiza y Abre al Instante.](https://www.youtube.com/watch?v=Dt6gAzmqyoc)
9. [eza | A modern, maintained replacement for ls, written in rust](https://eza.rocks/)
10. [eza - A modern replacement for ls - Terminal Trove](https://terminaltrove.com/eza/)
11. [EZA: The Best LS Command Replacement | by Denis Rasulev - Medium](https://denisrasulev.medium.com/eza-the-best-ls-command-replacement-f6f6af6a5839)
12. [Upgrade Your ls Command to eza - Blog - Datadice](https://www.datadice.io/en/blog/upgrade-your-ls-command-to-eza)
13. [eza-community/eza: A modern alternative to ls - GitHub](https://github.com/eza-community/eza)
14. [Zoxide, A Smarter cd Command - Mark Skelton](https://mskelton.dev/bytes/zoxide-a-smarter-cd-command)
15. [Using Zoxide to superpower your \`cd\` command in Linux | by mbvissers.eth | Quick Programming | Medium](https://medium.com/quick-programming/using-zoxide-to-superpower-your-cd-command-in-linux-e74d9327ced9)
16. [ajeetdsouza/zoxide: A smarter cd command. Supports all major shells. - GitHub](https://github.com/ajeetdsouza/zoxide)
17. [I love Zoxide : r/commandline - Reddit](https://www.reddit.com/r/commandline/comments/1clcfr9/i_love_zoxide/)
18. [zoxide - A faster alternative to boring cd command - DEV Community](https://dev.to/chamal1120/zoxide-a-faster-alternative-to-boring-cd-command-1ae3)
19. [sd - Intuitive find & replace CLI (sed alternative) - Terminal Trove](https://terminaltrove.com/sd/)
20. [SD IS BETTER THAN SED! - YouTube](https://www.youtube.com/watch?v=Kps2uLk-1KU)
21. [chmln/sd: Intuitive find & replace CLI (sed alternative) - GitHub](https://github.com/chmln/sd)
22. [sd - an intuitive find & replace CLI (sed alternative) : r/rust - Reddit](https://www.reddit.com/r/rust/comments/a9sncx/sd_an_intuitive_find_replace_cli_sed_alternative/)
23. [Guía del comando jq - Manuel Vergara Carmona](https://vergaracarmona.es/guia-del-comando-jq/)
24. [Cómo usar JQ para procesar JSON en la línea de comandos | Linode Docs](https://www.linode.com/docs/guides/using-jq-to-process-json-on-the-command-line/?lang=es)
25. [Extraer datos de ficheros json con jq - geekland](https://geekland.eu/extraer-datos-de-ficheros-json-con-jq/)
26. [introducción a JQ con ejemplos - Hello, IT](https://helloit.es/2020/06/introduccion-a-jq-con-ejemplos/)
27. [Display more user-friendly Linux man pages with the tldr command - Red Hat](https://www.redhat.com/en/blog/tldr-linux)
28. [TLDR - Easy to Understand Man Pages for Linux Commands - Tecmint](https://www.tecmint.com/tldr-easy-to-understand-linux-man-pages/)
29. [tldr pages](https://tldr.sh/)
30. [tldr-pages/tldr: Collaborative cheatsheets for console commands - GitHub](https://github.com/tldr-pages/tldr)
31. [TLDR - Read man pages in simple format - GeeksforGeeks](https://www.geeksforgeeks.org/linux-unix/tldr-read-man-pages-in-simple-format/)
32. [Replace du with dust on Linux - Opensource.com](https://opensource.com/article/21/6/dust-linux)
33. [Check Disk Usage on Linux with the dust Command - Linode](https://www.linode.com/docs/guides/dust-command-on-linux-installation/)
34. [Dust instead of du - by Anton Okolelov - Medium](https://medium.com/@okoanton/dust-instead-of-du-fa0e4a3ad597)
35. [dust | x-cmd pkg | A modern alternative to the \`du\` command, used to view disk space usage](https://www.x-cmd.com/pkg/dust/)
36. [View Active Processes in Linux with the procs Command | Linode Docs](https://www.linode.com/docs/guides/view-active-linux-processes-with-procs/)
37. [procs Is A Modern Replacement For ps With Colored Output, Additional Information (Written In Rust) - Linux Uprising Blog](https://www.linuxuprising.com/2021/05/procs-is-modern-replacement-for-ps-with.html)
38. [Procs: A modern replacement for ps written in Rust](https://users.rust-lang.org/t/procs-a-modern-replacement-for-ps-written-in-rust/24794)
39. [dalance/procs: A modern replacement for ps written in Rust - GitHub](https://github.com/dalance/procs)
