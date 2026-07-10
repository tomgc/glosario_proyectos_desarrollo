# Glosario de proyectos de desarrollo

Glosario personal de terminos de desarrollo de software, inteligencia
artificial y datos. Cada entrada tiene una definicion general y una
definicion tecnica, mas contexto de uso real cuando aplica (donde y como
aparece el termino en los proyectos de la cartera).

Es documentacion publica: solo contenido tecnico, sin datos personales,
sin datos de ninos, ninas y adolescentes, sin informacion institucional
sensible.

## Version publicada

El glosario se sirve en HTML por GitHub Pages:
https://tomgc.github.io/glosario_proyectos_desarrollo/

(Puede tardar unos minutos en estar activo tras el primer deploy.)

## Contenido

- `index.html`: version navegable del glosario (la que sirve GitHub
  Pages). Es autocontenida: todo el contenido y los estilos van
  embebidos, no depende de archivos externos.
- `glosario_desarrollo.md`: la fuente en Markdown. Mantiene este nombre
  por ser el documento original del glosario.
- `cola_pendientes.md`: terminos propuestos que todavia no se
  incorporan; se acumulan hasta lanzar un lote de investigacion.

## Como se actualiza

El flujo de trabajo vive en el repositorio de instrumental
`herramientas_dev`, no aqui:

1. Los terminos propuestos en conversacion se acumulan en
   `cola_pendientes.md`.
2. Al llegar a cinco, se lanza un encargo autonomo de Claude Code
   (`herramientas_dev/prompts/encargo_glosario_lote_v1.md`) que investiga
   el uso real de cada termino en la cartera de proyectos antes de buscar
   definiciones en la web.
3. El resultado se integra a `glosario_desarrollo.md` y se regenera
   `index.html`.

Los encargos reutilizables permanecen en `herramientas_dev/prompts/`
porque son instrumental compartido de la cartera, no contenido de este
proyecto.

## Estructura del proyecto

Este es un proyecto de documentacion pura, sin pipeline de datos. Por eso
no sigue la estructura numerada canonica de la politica de proyectos (que
esta pensada para proyectos con procesamiento de datos): usa una
estructura minima plana en la raiz. Es una excepcion justificada por el
tipo de proyecto, no deuda heredada.

## Convenciones de este proyecto

Este proyecto se trata como sesión tipo BIBLIOTECA (protocolo
`SETTINGS_Y_PROMPTS_OPERACIONALES.md` §1.5 del repositorio
`herramientas_dev`): cierre liviano por sesión, no el protocolo completo
de traspasos (`traspaso_cierre_vNN.md` + `backlog_acumulativo.md` +
escaner). Ese protocolo completo esta pensado para proyectos con
pipeline y estados intermedios que coordinar entre sesiones; este
proyecto no tiene pipeline ni estados intermedios, solo contenido que se
actualiza por lotes.

Cada sesion de trabajo sustantivo cierra con un archivo en
`50_documentacion/cierres/AAAAMMDD_cierre.md`, con esta forma:

```markdown
# Cierre — AAAA-MM-DD

## Artefactos producidos o modificados
[lista de archivos con que cambio]

## Decisiones clave
[2-4 decisiones de diseno que conviene recordar]

## Terminos agregados o modificados en esta sesion
[lista, si aplica]

## Proximos artefactos posibles
[ideas no materializadas, si las hay]
```

## Licencia

MIT. Ver `LICENSE`.
