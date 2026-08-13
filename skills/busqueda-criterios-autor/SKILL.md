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

## Regla de citación obligatoria (no negociable)

Cada vez que cites una tesis o jurisprudencia del corpus, incluye su liga
oficial (el campo `enlace`, SJF2), incluso en respuestas breves. Cada vez
que cites un artículo de la LFDA o del Código Penal Federal, incluye el
número de artículo y, si aplica, la fracción. Nunca formules una
conclusión legal sin ambos elementos.

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

## Formato de citación (regla obligatoria, no negociable)

El objetivo de esta skill es aprovechar el contenido rico del corpus, no
actuar como un directorio de ligas. Por eso el contenido sustantivo de
cada criterio citado (no solo el rubro y el enlace) es parte obligatoria
de la respuesta. El **enlace oficial del SJF2 va siempre al final** de
cada criterio, presentado explícitamente como referencia de verificación
("para consultar el criterio íntegro y hacer tu propio 'double check' en
la fuente oficial"), nunca como sustituto del contenido.

La forma de presentar el contenido depende de cuántos criterios responden
la consulta:

### 1 a 4 criterios → contenido completo

Para cada criterio, en este orden:

1. Cita corta: **[RUBRO completo en mayúsculas].** [Autoridad emisora].
   [Tipo], [Época]. Registro digital: [registro_digital].
2. Contenido completo, según el tipo de tesis: si tiene
   `hechos`/`criterio_juridico`/`justificacion`, preséntalos con esos tres
   encabezados (no fusiones ni omitas ninguno); si en cambio tiene
   `texto_integro`, reprodúcelo tal cual. No parafrasees la regla legal
   operativa, solo la explicación circundante si se pide un resumen.
3. Al final del criterio: "Consulta oficial (SJF2): [enlace]."

Sigue la convención de citas-legales-mx en el paso 1 cuando esté
instalada, conservando de todos modos los pasos 2 y 3.

### 5 o más criterios → formato abreviado con opción de ampliar

Copiar el contenido completo de cinco o más tesis en una sola respuesta
satura al usuario y no es la mejor forma de aprovechar el corpus. En su
lugar:

1. Numera cada criterio (1, 2, 3, …) y preséntalo de forma abreviada:
   **[N]. [RUBRO completo en mayúsculas].** [Autoridad emisora]. [Tipo],
   [Época]. Registro digital: [registro_digital]. **Resumen:** el
   contenido literal del campo `resumen` del corpus (no lo parafrasees).
2. No incluyas `hechos`/`criterio_juridico`/`justificacion`/
   `texto_integro` en esta lista abreviada — eso es lo que el usuario
   puede pedir a continuación.
3. Cierra la lista invitando explícitamente a pedir el contenido completo
   de cualquiera de los criterios listados, por número o por registro
   digital (p. ej. "dame completo el 3", "amplía el registro 2018640").
   Nota de entorno: como esta skill opera dentro de una conversación de
   chat, no existen botones interactivos reales — el mecanismo
   equivalente es que el usuario responda señalando el número o registro
   que le interesa, y entonces le entregas ese criterio en el formato
   completo de la sección anterior (incluyendo el enlace SJF2 al final).
4. Agrupa la lista por `categoria_codigo` y presenta primero la fuente de
   mayor jerarquía (Pleno > Salas > Plenos de Circuito > Tribunales
   Colegiados), conforme a las notas de jerarquía en
   `metadata.conclusiones_y_lineamientos`.

### Excepción expresa

Si el usuario pide explícitamente solo el rubro y el enlace (p. ej. "solo
dame los títulos y el link"), respeta esa instrucción y omite el
contenido completo o el resumen, sin perder la referencia al enlace
oficial.

## Cuando no hay coincidencias

Si ningún registro del corpus responde la consulta, dilo claramente y
sugiere al usuario realizar una búsqueda en vivo en el Semanario Judicial
de la Federación oficial (https://sjf2.scjn.gob.mx), o, si el conector
Kriterius está disponible en este entorno, ofrece usarlo directamente.
Nunca fabriques un registro digital ni un rubro.

## Advertencia de vigencia

Señala siempre, al entregar una cita para uso en un escrito, que el
corpus está vigente al 13 de agosto de 2026 y que la vigencia debe
confirmarse en la fuente oficial antes de usarse.
