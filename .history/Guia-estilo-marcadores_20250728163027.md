# Sugerencias para un Sistema de Estilo Tipográfico Coherente (en Markdown y Prompts)

La comunicación clara es la base de cualquier proyecto colaborativo, y establecer un "sistema de estilo" para la comunicación escrita es tan importante como tener un buen sistema de control de versiones para el código o los documentos. En el contexto de comunicación `humano -> IA` no se trata de una cortesía sino de un requisito funcional para obtener resultados de calidad.

Pensemos en asignar un rol semántico (un "significado") a cada elemento para que su uso sea intuitivo y consistente.

## Nivel 1: Énfasis y Tono

1. Negrita (**texto**)
* Rol Principal: Énfasis y Jerarquía. Úsala para denotar importancia capital, para que algo salte a la vista inmediatamente.
* Casos de Uso:
    * Palabras clave o conceptos centrales: "**El control de versiones** es fundamental".
    * Advertencias o puntos críticos: "**Cuidado**: este comando sobrescribirá tus cambios locales", "**Importante**
: siempre haz backup antes de hacer un `rebase    * Títulos de sección o encabezados para crear estructura visual.
La negrita es tu herramienta para hacer que información crítica sea imposible de pasar por alto, estableciendo una jerarquía visual clara en el documento. Es más fuerte que la itálica, que tiene un rol más sutil de matiz y designación.
— 
2. Itálica o Cursiva (*texto* o _texto_)
* **Rol Principal: Matiz y Designación**. Es un énfasis más sutil que la negrita. Sirve para señalar que una palabra o frase se está usando de una manera especial.
* **Casos de Uso**:
    * Títulos de obras: "Acabo de leer el libro *Clean Code*".
    * Palabras en otros idiomas: "El concepto de *Zeitgeist* es complejo".
    * *Metalingüística* (hablar sobre la palabra en sí): "La palabra *commit* tiene varios significados".
    * Énfasis sutil: conversacional o para añadir un tono específico: "Creía que lo había guardado, *pero al parecer no*".
— 
## Nivel 2: Contenido Literal y Técnico

3. **Comilla Invertida o Backtick** (`código`)
* **Rol Principal: Delimitador Técnico**. Su función es sagrada en la `documentación técnica`. Separa el "lenguaje humano" del "lenguaje de la máquina". Es para fragmentos cortos y específicos, no para párrafos enteros.
* **Casos de Uso:**
    * **Comandos** de **terminal**: git status, ls -la.
    * Nombres de **archivos** o **carpetas**: `README.md`, .`git/.`
    * Fragmentos de código: `const x = 10;`.
    * Conceptos técnicos específicos de una herramienta: La `Staging Area`, la rama `main`, un `commit`. Por ejemplo, nombres de 'branches'

4. **Bloque de Código (Triple Comilla Invertida ```)**
    * **Rol Principal**: Aislamiento de Contenido Literal. Encapsula múltiples líneas de texto que deben ser tratadas como un bloque intacto, preservando espacios y saltos de línea, y sin ser interpretado como instrucción.
    * **Casos de Uso**:
        * Fragmentos de código fuente.
        * Datos estructurados (JSON, YAML).
        * Mostrar la salida de un terminal.
5. **Guión Simple (-) y Guión Bajo (_)**
   * **Rol Principal**: Separador de Palabras y *Naming Conventions*. Aunque no es un elemento de estilo tipográfico en sí, es importante para la legibilidad y la claridad. Su función principal es crear nombres de archivos, variables o ramas legibles cuando no se pueden usar espacios. Las elección entre uno y otros suele depender de la tecnología o de la convención del equipo.
   El guión es un separador seguro. No tiene significados especiales en los nombres de archivo para la mayoría de los sistemas operativos o servidores web. Es simplemente un carácter. Es un estándar en el mundo del desarrollo web (motores de búsqueda SEO y URLs)
   * **Casos de Uso**:    
     * **Nombres de archivos**: Es muy común usar guiones simples (estilo kebab-case). Por ejemplo: guia-estilo-marcadores.md, calculo-impuestos.js.
     * **Nombres de ramas en Git**: kebab-case es el estándar de facto. Por ejemplo: feat/nuevo-login-usuario, fix/corregir-bug-pago.
     * **Nombres de variables**: Aquí la comunidad está más dividida. Lenguajes como Python o SQL prefieren snake_case (con guion bajo): user_id, total_price. Otros, como JavaScript, prefieren camelCase (userId), evitando el separador por completo.
    **Recomendación de Estilo**: Elige una convención y sé **consistente**. Si tu proyecto usa "kebab-case" (todo en minúsculas y separando cada palabra con un guión simple -las palabras son trozos de carnas y el guió los pincha- mas parecería una brocheta) para los archivos, úsalo para todos. Si usa snake_case para las variables, no lo mezcles con camelCase. La consistencia es más importante que la elección en sí.
## Nivel 3: Citas y Puntuación Expresiva
6. **Comillas Dobles** ("texto")
* **Rol Principal**: Cita Directa. Se usan para reproducir las palabras exactas de alguien o de un texto.
* **Caso de Uso**:
    * "Como dijo Linus Torvalds: 'Talk is cheap. Show me the code'". (Fíjate cómo anido la comilla simple dentro de la doble, una convención común).
—
7. **Comillas Simples** ('texto')
* **Rol Principal**: Distanciamiento o "Scare Quotes". Son perfectas para indicar que estás usando un término de forma irónica, dudosa o no literal. También para resaltar una palabra sobre la que quieres llamar la atención sin el énfasis de la itálica. 
No estás citando a otra persona, sino que estás distanciando una frase que representa tu propio penamiento interno, poníendola "entre comillas" para señarar que es ua representación de tu estado mental. Es un uso matizado y muy efectivo.
* **Casos de Uso**:
    * "Me entregó su versión 'final' del documento... por tercera vez".
    * "Este nuevo 'feature' en realidad ha roto tres funcionalidades antiguas".
— 
8. **Guiones Largos o Rayas** (—)
* **Rol Principal**: Inciso o Aclaración Enfática. La raya (que en muchos editores se crea escribiendo dos guiones cortos --) es una herramienta de puntuación muy potente para insertar una idea o aclaración en medio de una frase, de una forma más marcada que con comas.
* **Caso de Uso**:
    * "El rebase —una de las herramientas más potentes y peligrosas de Git— debe usarse con conocimiento".
    * "Al final, la solución era simple —como casi siempre ocurre— y solo requería un cambio de una línea".

## Nivel 4: Estructura y Semántica (Clave para Prompts)

9. **Listas (Numeradas 1. y con Viñetas - o *)**
    * Rol Principal: Secuenciación y Enumeración. Para desglosar instrucciones, requisitos o puntos clave de forma ordenada y fácil de seguir. Organizan la información en pasos o grupos claros, mejorando la legibilidad frente a un párrafo denso. Los modelos de IA son excelentes procesando listas.
    * 
    * **Caso de Uso**: Definir pasos a seguir o un conjunto de restricciones que la respuesta debe cumplir.
      * Para secuencias ordenadas donde el número es importante, usar listas nueradas (1., 2., etc.)
      * Para listas de elementos donde el orden no es crítico, usar viñetas (- o '*' ). Se pueden usar ambos pero extensiones como Prettier utilizan '*' para la definición de listas
10. **Enlaces o Hipervínculos** ([texto](URL))
    * **Rol Principal**: Referencia Externa. Permite al lector acceder a información adicional o recursos relacionados. Facilitan elaborar una red de conocimiento en lugar de un documento aislado, referenciando fuentes, definiciones o recursos externos de forma limpia y semántica.
    * **Casos de Uso**: 
    * Incluir documentación, tutoriales o artículos relevantes que complementen el contenido principal.
      * **Citar una fuente**: "Según la [documentación oficial de Mozilla](enlace), el elemento <section> representa una sección temática de un documento".
      * **Navegación interna**: (En plataformas que lo soportan)
      * **Clarificar un término**: "Usaremos el patrón *Factory*, puedes leer más sobre él en este [articulo de Refactoring Guru](https://refactoring.guru/es/design-patterns/factory-method)".
11. **Líneas en Blanco**
    * **Rol Principal**: Separador de Bloques Conceptuales. Es la señal visual y estructural más fuerte para separar ideas. Indica al lector (humano o IA) que un bloque de pensamiento ha terminado y empieza otro.
    * **Caso de Uso**: En prompts, es esencial para separar Rol, Instrucciones, Datos de Entrada y Formato de Salida.
12. **Comillas Angulares (< >) y Etiquetas XML (<tag></tag>)**
    * **Rol Principal**: Etiquetado Semántico y Variables. El método más explícito y robusto para estructurar una petición a una IA.
    * **Casos de Uso**:
        * Como variable o placeholder: Crea un resumen sobre <tema>.
        * Como etiquetas para delimitar secciones, eliminando toda ambigüedad:

**A Sistema Propuesto en Acción**
Aquí tienes un párrafo que usa este sistema:
Para entender bien el cherry-pick, primero debemos dominar el concepto de rama. Una rama, en esencia, es un "laboratorio de experimentos seguro" —una idea que exploraremos a fondo—. No es simplemente una copia, como tu antigua versión 'final_v2'. El propio manual de Git lo describe como un lightweight movable pointer. Al usar el comando git branch mi-experimento, no estás duplicando archivos, solo estás creando una nueva línea de tiempo. Cuidado: confundir esto es la causa principal de muchos errores de principiante.

**B Sistema Propuesto en Acción (Ejemplo de Prompt Avanzado)** 

Aquí tienes un prompt para una IA que utiliza casi todos los elementos de nuestra guía para lograr la máxima precisión:
<role>
Actúa como un experto en **control de versiones** con Git y un excelente comunicador técnico. Tu audiencia son desarrolladores junior.
</role>

<task>
Quiero que expliques el concepto de "rama" en Git. Tu explicación debe cumplir los siguientes requisitos:
1.  Comienza con una analogía simple —no uses la típica del 'árbol'—.
2.  Define qué es una rama en términos técnicos, mencionando que es un *lightweight movable pointer*.
3.  Incluye un ejemplo práctico de cuándo crear una rama, usando el placeholder `<nombre-de-la-feature>`.
4.  **Advertencia:** Termina explicando por qué el comando `git checkout -b <nombre-de-la-feature>` es un atajo útil.
</task>

<input_data>
Para tu referencia, aquí tienes un ejemplo de la salida del comando `git log --oneline --graph` que podrías usar en tu explicación:

* e7a4d2f (HEAD -> main) Final commit on main| * c3b1a8a (feature/login) Add password validation| * 8a2d65c Add username field|/
* 1d8f3b6 Initial commit
</input_data>

<output_format>
La respuesta debe ser un texto coherente y fluido. No respondas con una lista, sino integrando los puntos de la tarea en un párrafo bien redactado. No uses la palabra 'feature' de forma irónica o entre comillas simples.
</output_format>

**Prueba de paso de RTF a Markdown**

 Prueba de paso de **RTF** a _Markdown_
prueba de código
```bash