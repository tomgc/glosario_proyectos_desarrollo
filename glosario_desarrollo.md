# Glosario de desarrollo de software e IA

## Auditoría (en desarrollo de software)

### Auditoría

**General:** Revisión sistemática que verifica si algo (un proceso, un dato, un resultado) cumple con lo que se espera de él, detectando errores o desviaciones antes de que causen problemas.

**Técnica:** Verificación sistemática de que el estado de un sistema o de sus outputs cumple reglas, contratos o cifras esperadas, típicamente comparando dos caminos de cálculo independientes (caché contra recálculo desde el dato crudo) con tolerancias definidas como constantes nombradas. Puede aplicarse a código (cumplimiento de convenciones, estructura de carpetas), a datos (integridad, rangos esperados) o a cifras publicadas (validación cruzada antes de publicar).

*Contexto:* En tu cartera, la auditoría de cifras sigue un patrón de tres scripts (helpers + orquestador de familias + spot-check de extremo a extremo): cada cifra se calcula por dos caminos independientes y se compara con tolerancias definidas como constantes nombradas, nunca números mágicos; una familia que falla no aborta la validación de las demás.

---

## Datos

### Microdato

**General:** Un dato que describe a una sola persona, institución o caso individual, a diferencia de un promedio o total que junta a muchos.

**Técnica:** Registro de datos referido a una unidad de observación individual (una persona, un establecimiento, un hogar), antes de cualquier agregación. Los microdatos se combinan y resumen para producir macrodatos o estadísticas agregadas (promedios, totales, indicadores por grupo). La distinción es relevante para gobernanza de datos: un microdato con identificadores (RUT, nombre) suele ser dato personal o sensible, mientras que el agregado que resulta de él generalmente no lo es.

*Contexto:* En tus proyectos con datos educativos, las bases oficiales suelen ser microdato por persona, lo que obliga a publicar solo agregados territoriales (comuna, SLEP, región, país) y a suprimir las celdas con pocos casos, porque una celda territorial chica podría individualizar a una persona.

### Parquet

**General:** Formato de archivo para guardar datos, pensado para que ocupe poco espacio y se pueda leer muy rápido, especialmente cuando el archivo es grande.

**Técnica:** Formato de almacenamiento columnar (orienta el disco por columna, no por fila), de código abierto, que agrupa cada columna con su propio esquema y compresión, permitiendo leer solo las columnas necesarias en una consulta en vez de todo el archivo. Ofrece compresión más eficiente que formatos orientados a fila como CSV (valores del mismo tipo agrupados comprimen mejor), y guarda metadatos y esquema junto al dato, lo que evita ambigüedades de tipo al leerlo desde distintos sistemas.

*Contexto:* En tu política de proyecto, `.parquet` es el formato canónico para datos masivos (frente a `.xlsx`, reservado solo para entregables finales, y `.csv`, solo cuando el destino externo lo exige); la escritura atómica (patrón write → rename) se exige para todo artefacto `.parquet` que alimente procesos posteriores.

---

## Desarrollo de software (general)

### Backlog

**General:** Lista de tareas, pendientes o mejoras que un equipo o proyecto aún no ha resuelto, ordenada para saber qué hacer a continuación.

**Técnica:** Registro histórico y acumulativo de cambios, solicitudes y decisiones de un proyecto, usado como fuente de verdad del avance a lo largo de sesiones o iteraciones. Puede incluir clasificación temática, métricas de qué proporción de cambios cae en cada categoría, y un detalle cronológico con numeración correlativa permanente (nunca se reescribe ni renumera; las correcciones se agregan como entradas nuevas).

*Contexto:* En tu flujo, el backlog vive como `backlog_acumulativo.md` en `50_documentacion/activa/` y es la única fuente de verdad del conteo histórico. Es append-only: en cada cierre se copia íntegro el backlog anterior y los cambios nuevos se agregan al final, con numeración correlativa global y permanente; las entradas previas nunca se reescriben, resumen ni renumeran, y un error se corrige con una entrada nueva.

### CSS

**General:** El lenguaje que define cómo se ve una página web (colores, tipografía, espaciado, diseño), separado del contenido (HTML) y del comportamiento (JavaScript).

**Técnica:** Cascading Style Sheets. Lenguaje de hojas de estilo que define la presentación visual de documentos HTML: layout, tipografía, color, animaciones y comportamiento responsivo. Sigue un modelo de cascada donde reglas más específicas o más cercanas al elemento (inline > interna > externa) sobrescriben a las más generales. Se usa junto con patrones de diseño reutilizables (grillas, layouts tipo Holy Grail, sistemas de columnas) para mantener consistencia y evitar duplicación.

*Contexto:* En tu cartera, el CSS se sistematiza en una hoja de marca compartida (`suite_estilos.css`) que define tokens en `:root` (colores de marca, radios, sombras, tipografías gobCL y Museo Sans), grillas armadas con CSS Grid que colapsan a una sola columna en pantallas chicas, y una paleta institucional reutilizable entre proyectos hermanos.

### Commit

**General:** Guardar una versión de tu trabajo con una nota que explica qué cambiaste, de forma que siempre puedas volver a ese punto exacto más adelante.

**Técnica:** Unidad atómica de cambio en un sistema de control de versiones (Git), que registra el estado de uno o más archivos junto con metadatos (autor, fecha, mensaje descriptivo) y un identificador único (hash). Los commits forman el historial granular del proyecto; se recomiendan frecuentes y con mensajes descriptivos, y son la base sobre la que se construyen ramas y Pull Requests.

*Contexto:* En tu flujo, los commits van en español, con mensaje en imperativo y primera línea breve; el cuerpo, opcional, explica el "por qué" del cambio, no el "qué". La convención está documentada en el flujo de trabajo Git de tus proyectos, e incluye pasar el pre-commit hook local, sin `--no-verify` salvo justificación documentada.

### End-to-end (en desarrollo de software)

**General:** Probar o ejecutar un proceso completo, de principio a fin, tal como lo experimentaría un usuario real, en lugar de revisar solo una parte aislada.

**Técnica:** Enfoque de prueba o ejecución que cubre todo el flujo de un sistema, desde la entrada inicial hasta la salida final, verificando que todos los componentes trabajen correctamente en conjunto (no solo cada uno por separado). Un pipeline que "corre end-to-end" ejecuta todas sus etapas de forma encadenada y produce el resultado esperado sin intervención manual.

*Contexto:* En tus pipelines, que un proceso "corra end-to-end" significa que `run_all()` ejecuta el pipeline completo de principio a fin, de cero y sin intervención manual; es una pregunta fija en la auditoría de cierre de cada proyecto y un paso de validación obligatorio tras un refactor o una migración, junto a los tests y la verificación visual.

### Git y GitHub

**General:** Git es un programa que guarda el historial de cambios de un proyecto de código, permitiendo volver atrás o ver qué cambió y cuándo. GitHub es un sitio web que almacena esos proyectos en la nube y permite compartirlos o trabajar en equipo sobre ellos.

**Técnica:** Git es un sistema de control de versiones distribuido que registra el historial de cambios de un repositorio mediante commits, permite trabajo en ramas (branches) paralelas y ofrece mecanismos de fusión (merge). GitHub es una plataforma de alojamiento de repositorios Git que añade funciones colaborativas: Pull Requests, revisión de código, control de acceso, Issues, Actions (integración continua) y protección de ramas.

*Contexto:* Trabajas con repos privados en GitHub bajo el plan Free, lo que implica que las ramas privadas no tienen branch protection nativa; lo compensas con disciplina de Pull Request documentada, Secret Scanning y Dependabot habilitados, un workflow de CI que valida en cada push la ausencia de extensiones de datos, patrones de RUT y tokens, y un flujo de squash merge con eliminación automática de la rama (`gh pr merge --squash --delete-branch`).

### Gobernanza (en desarrollo de software)

**General:** El conjunto de reglas que definen quién puede acceder a los datos de un proyecto, cómo se protegen y qué está permitido hacer con ellos, especialmente cuando se trata de información sensible o de personas.

**Técnica:** Marco de principios, reglas y controles que rige cómo se manejan los datos y las decisiones arquitectónicas de un proyecto: separación física entre datos sensibles y código, control de acceso, cumplimiento normativo (protección de datos personales), y trazabilidad de las decisiones que afectan esa gestión. Incluye la documentación formal de qué datos se manejan, su categoría legal, quién tiene acceso y el procedimiento ante un incidente de seguridad.

*Contexto:* En tus proyectos, la gobernanza de datos exige que los datos personales (RUT, nombres, resultados individuales) nunca entren al repositorio Git. La separación entre raíz de código (Git) y raíz de datos (OneDrive institucional) es física y está documentada en un `gobernanza_datos.md` por proyecto: la raíz de datos se resuelve mediante una variable de entorno canónica (`<PROYECTO>_DATA_ROOT`) que aborta la ejecución si no está definida, y un workflow de CI bloquea cualquier intento de subir datos o RUT, más allá del `.gitignore`.

### Orquestador

**General:** El programa o script que coordina y ejecuta, en el orden correcto, todos los pasos de un proceso más grande, para que no haya que correrlos uno por uno a mano.

**Técnica:** Punto de entrada único de un pipeline que secuencia la ejecución de sus etapas, valida precondiciones antes de correr, mide duración por paso, y falla con mensaje claro ante error en lugar de continuar silenciosamente. No contiene lógica de negocio propia: su responsabilidad es coordinar, no transformar datos.

*Contexto:* En tu arquitectura, el orquestador (`00_run_all.R`) ancla la raíz del proyecto, carga primero las utilidades de bootstrapping, y expone argumentos estándar (`from`, `to`, `only`, `skip`) para ejecutar el pipeline completo o subconjuntos de él.

### Render

**General:** El proceso por el cual un programa (como un navegador o una app) toma datos o código y los convierte en lo que finalmente se ve en la pantalla.

**Técnica:** Proceso de transformar una representación abstracta (datos, código, un modelo) en su salida visual final. En desarrollo web, el navegador construye el DOM y el CSSOM a partir del HTML y CSS, calcula estilos, determina el layout (tamaño y posición de cada elemento) y pinta los píxeles en pantalla. En aplicaciones de datos o dashboards, "renderizar" un componente significa generar su representación visible (una tabla, un gráfico, una tarjeta) a partir del dato subyacente.

*Contexto:* En tu cartera, "renderizar" aparece sobre todo como paso de pipeline: `quarto render` (vía `quarto::quarto_render()`) transforma un `.qmd` en el entregable final (`.docx` o `.html`), con chequeo del código de salida y el resultado movido de forma atómica a OneDrive; también nombra el motor HTML que genera fichas y tarjetas de establecimiento a partir del dato subyacente.

---

## Inteligencia artificial

### Inteligencia artificial generativa

**General:** Tipo de inteligencia artificial que no solo analiza información existente, sino que crea contenido nuevo (texto, imágenes, audio, código) a partir de patrones aprendidos de grandes cantidades de datos.

**Técnica:** Subcampo de la inteligencia artificial enfocado en modelos (generalmente basados en aprendizaje profundo, como transformers o modelos de difusión) entrenados para generar contenido nuevo y original que sigue la distribución estadística de los datos de entrenamiento, en lugar de solo clasificar o predecir sobre datos existentes. Los modelos de lenguaje grandes (LLM) son el caso más extendido de esta categoría.

### LLM (large language model)

**General:** Un programa de inteligencia artificial entrenado con enormes cantidades de texto, capaz de entender lo que se le escribe y responder con lenguaje natural, como Claude o ChatGPT.

**Técnica:** Modelo de aprendizaje profundo, típicamente basado en arquitectura Transformer, entrenado sobre grandes volúmenes de texto para predecir la siguiente unidad de texto (token) en una secuencia. Esa capacidad de predicción, escalada a miles de millones de parámetros, produce comprensión y generación de lenguaje natural de propósito general (clasificación, traducción, generación de código, razonamiento), sin que cada tarea requiera reglas programadas explícitamente.

*Contexto:* En tu flujo distingues explícitamente el rol de dos LLM, el "reparto dual-Claude" documentado con una tabla de "hace / no hace": Claude conversacional como colaborador estratégico (análisis, metodología, decisiones de diseño, redacción y traspaso) y Claude Code como entorno de ejecución (terminal, git, edición de archivos, verificación), que no decide metodología ni qué es correcto.

### Machine learning

**General:** Rama de la inteligencia artificial en la que un programa aprende a partir de ejemplos y datos, en lugar de seguir reglas escritas a mano por una persona.

**Técnica:** Conjunto de técnicas y algoritmos que permiten a un sistema mejorar su desempeño en una tarea a partir de la exposición a datos, ajustando parámetros internos (pesos de un modelo) sin que cada regla de decisión sea programada explícitamente. Incluye enfoques supervisados, no supervisados y de refuerzo, y es la base técnica sobre la que se construyen el deep learning y los modelos generativos modernos.

*Contexto:* En tu cartera hay al menos un caso real de machine learning: un modelo predictivo de riesgo (elastic net logístico con `glmnet`, validación cruzada de k=10 para elegir lambda y holdout temporal estricto), que además controla el AUC por subgrupo como chequeo de equidad. Es aprendizaje supervisado real, no un modelo de reglas.

### Modelo de IA

**General:** El "cerebro" entrenado que usa un sistema de inteligencia artificial para tomar decisiones o generar respuestas; es el resultado de haber entrenado un algoritmo con muchos datos.

**Técnica:** Artefacto computacional resultante de un proceso de entrenamiento, compuesto por una arquitectura (por ejemplo, una red neuronal) y un conjunto de parámetros (pesos) ajustados sobre datos, que produce predicciones, clasificaciones o generación de contenido ante una nueva entrada. Los modelos fundacionales son modelos de gran escala entrenados con datos generales, capaces de adaptarse a múltiples tareas sin reentrenamiento específico para cada una.

*Contexto:* En tu cartera, la expresión "modelo de IA" no designa el modelo estadístico propio de un pipeline (un elastic net de riesgo es machine learning, no "modelo de IA"), sino un LLM externo distinto de Claude al que se le encarga una auditoría metodológica independiente del proyecto (revisar rigor estadístico, ausencia de leakage y similares). Ningún proyecto construye un modelo de IA propiamente tal.

### Panel adversarial

**General:** Revisión que, en vez de solo confirmar que el código corrió sin error, intenta activamente encontrarle fallas al resultado: recalcula todo por un camino distinto e independiente para ver si las cifras coinciden.

**Técnica:** Verificación independiente que re-deriva el resultado desde el dato crudo (no desde los objetos intermedios ya calculados), usando código propio y comprobando invariantes lógicos explícitos (por ejemplo: que ninguna unidad se doble-cuente entre series, o que un subconjunto sea siempre ≤ que su superconjunto por construcción). Si un invariante falla, indica un bug de lógica y detiene el proceso en vez de continuar.

*Contexto:* El panel adversarial es un paso obligatorio post-cómputo en tus auditorías: agentes de solo lectura re-derivan las cifras clave desde el parquet fuente con código independiente y verifican la fidelidad censal (que ninguna cifra publicada haya sido alterada), con un mismatch esperado de 0 sobre cientos de miles de filas; el resultado se reporta como panel "N/N" y cualquier discrepancia detiene el proceso.

### Prompt

**General:** El texto o instrucción que le escribes a un sistema de inteligencia artificial para pedirle que haga algo.

**Técnica:** Entrada textual (o multimodal) que se entrega a un modelo de IA para condicionar su salida. Su diseño (prompt engineering) afecta directamente la calidad, precisión y formato de la respuesta: incluye técnicas como dar ejemplos positivos y negativos, pedir razonamiento paso a paso, especificar formato de salida o restricciones de longitud.

*Contexto:* En tu flujo de trabajo, los prompts que van dirigidos a Claude Code se distinguen explícitamente de la prosa conversacional: siempre en bloques de código, marcados con "→ Claude Code:", sin excepción incluso para instrucciones de una sola línea.

---

## Reuso de código

### Patrón de familia

**General:** Cuando varios proyectos parecidos comparten una misma pieza de código o de diseño, y en vez de copiarla en cada uno, se centraliza en un solo lugar del que todos la usan.

**Técnica:** Estrategia de reuso transversal entre proyectos hermanos que comparten una base de código o convenciones (por ejemplo, un mismo dominio o cartera de proyectos), consistente en identificar utilidades, módulos o convenciones repetidas (idealmente byte-idénticas) y extraerlas a un paquete o carpeta central de la cual cada proyecto consume, en lugar de mantener copias locales que pueden desincronizarse.

*Contexto:* En tu cartera, "reuso y patrón de familia" es una categoría viva del backlog y fue objeto de una auditoría de duplicación entre proyectos hermanos que clasifica cada candidato de reuso: byte-idéntico y seguro de extraer (por ejemplo `d3`/`pako` o rutas auxiliares duplicadas en varios `10_utils/`), con firmas incompatibles entre proyectos (requiere resolución explícita antes de centralizar), o con la hipótesis de reuso refutada (una supuesta utilidad compartida que resultó existir en un solo proyecto).

---

## Pendientes

- Encargo autónomo a Claude Code: escanear `backlog_acumulativo.md` y la documentación de cada proyecto de la cartera para buscar buenos ejemplos reales de los términos ya definidos, como insumo para enriquecer la sección "Contexto" de cada entrada.
- Revisión de estilo: verificar en cada actualización que no queden bloques en mayúscula sostenida (ALLCAPS), salvo siglas o palabras que lo justifiquen.
