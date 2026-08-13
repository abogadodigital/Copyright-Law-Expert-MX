---
name: consulta-lfda-derecho-autor
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué dice el artículo
  [número] de la LFDA", "qué dice la ley sobre derechos morales /
  derechos patrimoniales / transmisión de derechos / derechos conexos /
  límites y excepciones / símbolos patrios / registro público del
  derecho de autor / gestión colectiva / INDAUTOR / procedimientos", "en
  qué consiste el derecho de cita", "cuánto dura el derecho patrimonial
  de autor", "qué es la reserva de derechos", "cómo se calcula la
  indemnización del artículo 216 Bis", o cuando necesite el texto
  literal de cualquier disposición de los Títulos I a XI de la Ley
  Federal del Derecho de Autor (LFDA), arts. 1 a 228, a diferencia de la
  jurisprudencia que interpreta esas disposiciones o de las infracciones
  administrativas del Título XII (ver consulta-infracciones-lfda).
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Consulta del texto de la LFDA (Títulos I a XI)

Responde dudas sobre el contenido literal de la Ley Federal del Derecho
de Autor, Títulos I a XI (arts. 1 a 228: disposiciones generales, derecho
de autor, transmisión de derechos patrimoniales, protección al derecho
de autor, derechos conexos, límites y excepciones, símbolos patrios y
culturas populares, registros de derechos, gestión colectiva, INDAUTOR y
procedimientos), citando siempre el texto legal exacto contenido en el
corpus empaquetado. No parafrasees el artículo como si fuera la única
fuente de verdad sin antes mostrar o citar su texto íntegro; no inventes
artículos, fracciones o incisos que no existan en el corpus.

## Regla de citación obligatoria (no negociable)

Cita siempre el artículo (y la fracción, si aplica) de la LFDA que
fundamenta la respuesta. Si la respuesta también hace referencia a una
tesis o jurisprudencia del corpus de jurisprudencia de este plugin
(`skills/busqueda-criterios-autor/references/corpus_tesis_derechos_autor.json`),
incluye igualmente su liga oficial (campo `enlace`, SJF2) — nunca la
omitas, incluso en respuestas breves.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-lfda-derecho-autor/references/corpus_lfda_derecho_autor.json`

Estructura:

- `metadata`: título de la ley, fuente (DOF), fecha de publicación
  original (24-12-1996), última reforma reflejada en el corpus
  (DOF 14-05-2026), lista `titulos` (I a XII, cada uno con `capitulos`,
  `rango_articulos` y `total_articulos`), `total_articulos` general,
  `nota_delitos` (aclara que los delitos NO están en la LFDA sino en el
  Código Penal Federal — ver skill `consulta-delitos-autor`) y
  `relacion_con_otros_corpus`.
- `articulos[]`: 258 registros, cada uno con:
  - `numero`: número de artículo (p. ej. `"11"`, `"9 Bis"`, `"216 Bis"`).
  - `titulo_numero` / `titulo_nombre`: Título (I a XII) al que pertenece.
  - `capitulo_codigo` / `capitulo_nombre`: capítulo dentro del Título.
  - `texto_intro`: primera oración del artículo.
  - `fracciones[]`: cada una con `marcador` (romano o, excepcionalmente,
    letra de agrupación como en el art. 4), `texto` e `incisos[]`
    (`letra` + `texto`).
  - `parrafos_finales[]`: párrafos de cierre o continuación del artículo.
  - `reformas[]`: anotaciones de reforma tal como aparecen en el texto
    vigente.
  - `texto_completo`: el artículo íntegro, verbatim, en el orden
    original del documento fuente. **Usa siempre este campo cuando cites
    o reproduzcas el texto legal** — los campos estructurados
    (`fracciones`, `incisos`, `parrafos_finales`) son un índice de apoyo
    para localizar y filtrar contenido, no un sustituto de la cita
    literal. Nota: dado que la ley original numera algunas fracciones
    con letras mayúsculas de agrupación (p. ej. art. 4: A/B/C/D con
    números romanos anidados dentro de cada letra), el índice de
    `fracciones[]` puede no reflejar perfectamente esa jerarquía anidada;
    en esos casos apóyate en `texto_completo`.

## Mapa de Títulos (para orientar la búsqueda temática)

- **I** — Disposiciones Generales (arts. 1-10).
- **II** — Del Derecho de Autor: Cap. I Reglas Generales, Cap. II Del
  Derecho Moral, Cap. III Del Derecho Patrimonial (arts. 11-29).
- **III** — De la Transmisión de los Derechos Patrimoniales: contratos de
  edición, obra por encargo, obra plástica/fotográfica, obra
  cinematográfica/audiovisual, publicidad, radio y televisión (arts.
  30-76).
- **IV** — De la Protección al Derecho de Autor: obras fotográficas,
  programas de cómputo, bases de datos, obras arquitectónicas (arts.
  77-114, incluye 114 Octies).
- **V** — De los Derechos Conexos: artistas intérpretes o ejecutantes,
  editores de libros, productores de fonogramas, productores de
  videogramas, organismos de radiodifusión (arts. 115-146).
- **VI** — De las Limitaciones del Derecho de Autor y de los Derechos
  Conexos: límite por copia privada, derecho de cita, uso didáctico,
  bibliotecas, reproducción sin autorización en casos específicos (arts.
  147-153).
- **VII** — De los Derechos de Autor sobre los Símbolos Patrios y de las
  Expresiones de las Culturas Populares (arts. 154-161).
- **VIII** — De los Registros de Derechos: Registro Público del Derecho
  de Autor, reserva de derechos al uso exclusivo (arts. 162-191).
- **IX** — De la Gestión Colectiva de Derechos: sociedades de gestión
  colectiva (arts. 192-207).
- **X** — Del Instituto Nacional del Derecho de Autor, INDAUTOR (arts.
  208-212).
- **XI** — De los Procedimientos: avenencia, arbitraje, medidas
  precautorias, e indemnización por daños y perjuicios del art. 216 Bis
  (arts. 213-228).
- **XII** — De los Procedimientos Administrativos (infracciones,
  arts. 229-238): consulta también incluida aquí, pero para un análisis
  especializado usa la skill `consulta-infracciones-lfda`.

## Estrategia de búsqueda

Empareja la pregunta del usuario, en este orden de precedencia:

1. Número de artículo exacto (`numero`), incluyendo variantes "Bis",
   "Ter", "Octies", etc.
2. Título/Capítulo temático cuando el usuario pregunta por un tema
   general (usa el mapa de Títulos anterior).
3. Búsqueda de texto libre sobre `texto_intro`, `fracciones[].texto`,
   `fracciones[].incisos[].texto` y `parrafos_finales` cuando el usuario
   describe un supuesto sin dar número de artículo (p. ej. "¿puedo usar
   un fragmento de un libro para un trabajo escolar sin permiso del
   autor?", "¿qué pasa si el registro ante el INDAUTOR se impugna?").

Si la pregunta también involucra jurisprudencia o tesis, complementa la
respuesta remitiendo al usuario a la skill `busqueda-criterios-autor` de
este mismo plugin. Si involucra infracciones administrativas (Título
XII) usa `consulta-infracciones-lfda`; si involucra delitos, usa
`consulta-delitos-autor` (Código Penal Federal, fuera de la LFDA).

## Formato de respuesta

1. Cita el o los artículos aplicables con su número y, si es relevante,
   la fracción/inciso exacto, reproduciendo el texto de `texto_completo`
   entre comillas o en bloque de cita.
2. Si el artículo tiene entradas en `reformas[]`, adviértelo brevemente.
3. Da una explicación breve en lenguaje llano de lo que dice el artículo,
   después de la cita textual, no en lugar de ella.
4. Si el usuario pide fundamento para un escrito o dictamen, usa el
   formato de citas-legales-mx cuando esté instalado; si no, cita como:
   > Artículo [número], [fracción/inciso si aplica], de la Ley Federal
   > del Derecho de Autor (Título [numeral romano] — [nombre del
   > Título], Capítulo [código] — [nombre del capítulo]).

## Límites

- Este corpus es un documento de trabajo del usuario, no una fuente
  oficial en tiempo real. Si el usuario necesita certeza absoluta sobre
  reformas recientes (después de DOF 14-05-2026), sugiere verificar el
  texto vigente en el portal del DOF (https://www.dof.gob.mx) o en la
  Cámara de Diputados (https://www.diputados.gob.mx/LeyesBiblio/).
- No mezcles el texto legal con jurisprudencia sin distinguir claramente
  cuál es cuál.
- No es una opinión legal definitiva; los borradores que produzcas
  requieren revisión de un abogado antes de usarse.
