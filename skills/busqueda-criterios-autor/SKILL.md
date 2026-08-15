---
name: busqueda-criterios-autor
description: >
  Esta skill debe usarse cuando el usuario pida "buscar tesis sobre
  derechos de autor", "encuentra jurisprudencia sobre X" (derecho moral,
  derecho patrimonial, regalías, INDAUTOR, gestión colectiva, obra por
  encargo, derecho a la imagen, excepciones y límites, indemnización del
  216 Bis, infracciones, delitos, Internet, radiodifusión, fonogramas,
  competencia jurisdiccional, etc.), "cita el criterio del registro
  [número]", "qué dice la tesis sobre el artículo [número] de la LFDA",
  o necesite localizar y citar correctamente uno o más de los 79
  criterios de la SCJN sobre derechos de autor empaquetados con este
  plugin.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Búsqueda y cita de criterios sobre derechos de autor

Localiza el criterio o los criterios relevantes dentro del corpus
empaquetado y devuélvelos en formato de citación legal mexicana correcto.
No busques en internet ni inventes criterios: esta skill trabaja
exclusivamente contra el archivo empaquetado.

## Formato de citación (obligatorio — ver skill dedicada)

El formato exacto de citación (jurisprudencia completa/abreviada y
artículos de la LFDA/CPF), así como la prohibición de atribuir el
contenido a cualquier conector o búsqueda en vivo, están definidos en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-autor/SKILL.md`. Esta skill
no repite esas reglas: consúltalas ahí y aplícalas al pie de la letra
cada vez que entregues un criterio de este corpus.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-autor/references/corpus_tesis_derechos_autor.json`

Estructura: `metadata.categorias` (A-Q con títulos y conteo),
`metadata.marco_normativo`, `metadata.conclusiones_y_lineamientos` (10
lineamientos prácticos transversales), y `criterios[]`: 79 registros con
`id`, `rubro`, `categoria_codigo`/`categoria_titulo`, `autoridad_emisora`,
`tipo_y_epoca`, `fecha`, `registro_digital`, `enlace`, `resumen`, y
`hechos`/`criterio_juridico`/`justificacion` (para tesis con estructura
en tres partes, típica de Décima Época en adelante) o `texto_integro`
(para tesis más antiguas o de estructura tradicional).

## Mapa de categorías (A-Q, 79 criterios)

- **A** — Fundamentos constitucionales y de derecho humano de la
  propiedad autoral (2).
- **B** — Concepto de obra, objeto y requisitos de protección (4).
- **C** — Naturaleza y contenido de los derechos morales y patrimoniales
  (6).
- **D** — Regalías y explotación patrimonial de la obra (8).
- **E** — Registro Público del Derecho de Autor, INDAUTOR y reserva de
  derechos (12, la categoría más numerosa).
- **F** — Sociedades de gestión colectiva (2).
- **G** — Obra por encargo, coautoría y titularidad derivada (3).
- **H** — Derecho a la imagen y al retrato en la legislación autoral (8).
- **I** — Responsabilidad editorial y daño moral en medios de
  comunicación (3).
- **J** — Excepciones y limitaciones: derecho de cita, bibliotecas y
  depósito legal (7).
- **K** — Indemnización por daños y perjuicios, artículo 216 Bis (5).
- **L** — Infracciones administrativas y sanciones (4).
- **M** — Delitos en materia de derechos de autor (7).
- **N** — Internet, plataformas digitales y medidas cautelares (1).
- **O** — Radiodifusión, televisión restringida y organismos vinculados
  (2).
- **P** — Fonogramas y productores (3).
- **Q** — Competencia jurisdiccional (2).

## Estrategia de búsqueda

Empareja la solicitud del usuario, en este orden de precedencia:

1. `registro_digital` exacto, si se proporciona.
2. `categoria_codigo`/`categoria_titulo` si el usuario nombra un tema que
   corresponde a una de las 17 categorías anteriores.
3. Referencias a artículos de la LFDA o del CPF mencionadas en el
   `resumen`, `hechos`, `criterio_juridico`, `justificacion` o
   `texto_integro` (p. ej. "artículo 216 Bis", "artículo 87", "artículo
   424 Bis").
4. Coincidencias de texto libre en `rubro` y `resumen`.

Lee `metadata.conclusiones_y_lineamientos` cuando el usuario haga una
pregunta sintética ("¿cuál es el criterio de mayor jerarquía sobre X?",
"¿cómo se relacionan estos criterios?", "dame un panorama general"): esa
sección ya sistematiza 10 lineamientos prácticos transversales (jerarquía
de fuentes, distinción entre derecho moral y patrimonial, divulgación vs.
explotación, derecho a la imagen como figura autónoma, INDAUTOR y
presunción de titularidad, obra por encargo, límites de interpretación
estricta, vías civil/administrativa/penal autónomas, retos de Internet, y
vigencia temporal).

Al presentar el formato abreviado de 5 o más criterios, agrupa la lista
por `categoria_codigo` y presenta primero la fuente de mayor jerarquía
(Pleno > Salas > Plenos de Circuito > Tribunales Colegiados), conforme a
las notas de jerarquía en `metadata.conclusiones_y_lineamientos`.

## Cuando no hay coincidencias

Si ningún registro del corpus responde la consulta, dilo claramente y
sugiere al usuario realizar una búsqueda en vivo en el Semanario Judicial
de la Federación oficial (https://sjf2.scjn.gob.mx), o, si hay algún
conector de búsqueda jurisprudencial disponible en este entorno, ofrece
usarlo directamente sin dar por hecho de cuál se trata.
Nunca fabriques un registro digital ni un rubro.

## Advertencia de vigencia

Señala siempre, al entregar una cita para uso en un escrito, que el
corpus está vigente al 13 de agosto de 2026 y que la vigencia debe
confirmarse en la fuente oficial antes de usarse.
