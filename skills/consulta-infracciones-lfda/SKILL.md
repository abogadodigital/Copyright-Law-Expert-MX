---
name: consulta-infracciones-lfda
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué sanción tiene
  [conducta] en materia de derechos de autor", "qué es una infracción
  administrativa en materia de derecho de autor", "qué es una infracción
  en materia de comercio conforme a la LFDA", "qué multa impone el
  INDAUTOR o el IMPI", "cómo se sanciona la piratería o la elusión de
  medidas tecnológicas de protección", "qué dice el artículo [número,
  entre 229 y 238] de la LFDA", "cómo se impugna una resolución del
  INDAUTOR", o cuando necesite el texto literal del Título XII (De los
  Procedimientos Administrativos) de la Ley Federal del Derecho de Autor,
  a diferencia de los delitos (Código Penal Federal, ver
  consulta-delitos-autor) o del derecho de autor sustantivo (ver
  consulta-lfda-derecho-autor).
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Consulta del texto de la LFDA sobre infracciones administrativas

Responde dudas sobre el contenido literal del Título XII de la LFDA ("De
los Procedimientos Administrativos", arts. 229 a 238), citando siempre el
texto legal exacto contenido en el corpus empaquetado. No parafrasees el
artículo como si fuera la única fuente de verdad sin antes mostrar o
citar su texto íntegro; no inventes artículos, fracciones o incisos que
no existan en el corpus.

## Regla de citación obligatoria (no negociable)

Cita siempre el artículo (y la fracción, si aplica) de la LFDA que
fundamenta la respuesta. Si la respuesta también hace referencia a una
tesis del corpus de jurisprudencia de este plugin (categorías L
"Infracciones administrativas y sanciones" o M "Delitos en materia de
derechos de autor" — para delitos, ver `consulta-delitos-autor`, no esta
skill), incluye igualmente su liga oficial (campo `enlace`).

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-infracciones-lfda/references/corpus_infracciones_lfda.json`

Estructura:

- `metadata`: título del Título XII, capítulos (I Infracciones en
  Materia de Derechos de Autor, II Infracciones en Materia de Comercio,
  III De la Impugnación Administrativa), `leyenda_materia`,
  `nota_delitos` (aclara que los delitos NO están en este corpus ni en la
  LFDA) y `relacion_con_otros_corpus`.
- `articulos[]`: 15 registros (arts. 229 a 238, incluyendo 232 Bis, 232
  Ter, 232 Quáter, 232 Quinquies y 232 Sexies), cada uno con `numero`,
  `capitulo_codigo`/`capitulo_nombre`, `materia`
  (`infraccion_autor` | `infraccion_comercio` | `impugnacion_administrativa`),
  `texto_intro`, `fracciones[]`, `parrafos_finales[]` y `texto_completo`
  (usar siempre este último para citar textualmente).

## Mapa de capítulos

- **Cap. I — Infracciones en Materia de Derechos de Autor** (art. 229):
  14 fracciones (celebrar contratos en contravención a la ley, infringir
  licencia obligatoria, ostentarse falsamente como sociedad de gestión
  colectiva, omitir menciones obligatorias en obras/fonogramas, publicar
  sin mencionar al autor o con menoscabo de su reputación, títulos que
  induzcan a confusión, etc.). Sancionadas por el INDAUTOR (art. 230:
  multas en Unidades de Medida y Actualización, UMA).
- **Cap. II — Infracciones en Materia de Comercio** (arts. 231-236):
  comunicación/puesta a disposición no autorizada, elusión de medidas
  tecnológicas de protección (art. 232 Bis), alteración de información
  sobre gestión de derechos (art. 232 Quáter), régimen de aviso y
  retiro/"notice and takedown" para proveedores de servicios en línea
  (art. 232 Quinquies), piratería física y comercial. Sancionadas por el
  IMPI (art. 234).
- **Cap. III — De la Impugnación Administrativa** (arts. 237-238):
  recursos de los afectados por resoluciones del INDAUTOR o el IMPI en
  estos procedimientos.

## Estrategia de búsqueda

1. Número de artículo exacto, incluyendo variantes "Bis"/"Ter"/"Quáter"/
   "Quinquies"/"Sexies".
2. `materia` (infracción de autor vs. infracción de comercio vs.
   impugnación) cuando el usuario describe la naturaleza de la conducta
   sin dar número de artículo.
3. Búsqueda de texto libre en `texto_intro`, `fracciones[].texto` y
   `parrafos_finales` (p. ej. "vender copias piratas en la calle",
   "plataforma que no retira contenido infractor", "descifrar señal de
   satélite").

Si la consulta involucra responsabilidad penal (prisión), remite siempre
a la skill `consulta-delitos-autor` (Código Penal Federal, arts.
424-429) — este corpus solo cubre la vía administrativa. Si involucra
jurisprudencia, usa `busqueda-criterios-autor` (categorías L y M). Si
involucra el cálculo de una indemnización civil por daños y perjuicios,
remite a `consulta-lfda-derecho-autor` (art. 216 Bis, Título XI).

## Formato de respuesta

1. Cita el o los artículos aplicables con su número y fracción exacta,
   reproduciendo `texto_completo`.
2. Identifica expresamente la autoridad competente (INDAUTOR para
   infracciones de autor, IMPI para infracciones de comercio) y el rango
   de la sanción aplicable (art. 230 o art. 232, según corresponda).
3. Explica en lenguaje llano la conducta sancionada, después de la cita
   textual.
4. Distingue siempre, cuando sea relevante, entre la vía administrativa
   (este corpus), la vía penal (`consulta-delitos-autor`) y la vía civil
   de indemnización (art. 216 Bis, `consulta-lfda-derecho-autor`): son
   tres cauces autónomos que pueden coexistir para una misma conducta.

## Límites

- Este corpus es un documento de trabajo del usuario, no una fuente
  oficial en tiempo real. Verificar reformas posteriores a DOF
  14-05-2026 en https://www.dof.gob.mx o
  https://www.diputados.gob.mx/LeyesBiblio/.
- No es una opinión legal definitiva; los borradores que produzcas
  requieren revisión de un abogado antes de usarse.
