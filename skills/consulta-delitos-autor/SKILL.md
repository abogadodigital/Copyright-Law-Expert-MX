---
name: consulta-delitos-autor
description: >
  Esta skill debe usarse cuando el usuario pregunte "cuáles son los
  delitos en materia de derechos de autor", "qué pena tiene vender
  copias piratas / discos piratas / películas piratas", "qué dice el
  artículo [número, entre 424 y 429] del Código Penal Federal", "en qué
  casos se persigue de oficio el delito de piratería", "qué sanción penal
  tiene eludir una medida tecnológica de protección con fines de lucro",
  "cuánto tiempo de prisión corresponde por vender un dispositivo para
  descifrar señal de cable o satélite", o cuando necesite el texto
  literal del Título Vigésimo Sexto (De los Delitos en Materia de
  Derechos de Autor) del Código Penal Federal, a diferencia de las
  infracciones administrativas de la LFDA (ver consulta-infracciones-lfda).
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Consulta del texto del Código Penal Federal sobre delitos de derechos de autor

Responde dudas sobre el contenido literal del Título Vigésimo Sexto del
Código Penal Federal (CPF), "De los Delitos en Materia de Derechos de
Autor" (arts. 424 a 429), citando siempre el texto legal exacto contenido
en el corpus empaquetado. No parafrasees el artículo como si fuera la
única fuente de verdad sin antes mostrar o citar su texto íntegro; no
inventes artículos, fracciones o penas que no existan en el corpus.

## Advertencia de arquitectura legal (importante)

A diferencia del derecho marcario mexicano —donde infracciones y delitos
conviven en un mismo título de la LFPPI—, en derechos de autor **los
delitos NO están en la Ley Federal del Derecho de Autor**. Están
tipificados en un ordenamiento distinto: el Código Penal Federal. Si el
usuario pregunta por "infracciones" en general sin especificar, aclara
esta distinción y ofrece cubrir ambas vías (remite a
`consulta-infracciones-lfda` para la vía administrativa).

## Formato de citación

Sigue el formato de citación (artículos, identificados siempre como CPF,
y jurisprudencia) definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-autor/SKILL.md`.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-delitos-autor/references/corpus_cpf_delitos_autor.json`

Estructura:

- `metadata`: título del Título Vigésimo Sexto, fuente (DOF), fecha de
  publicación original del CPF (14-08-1931), última reforma reflejada en
  el corpus (DOF 13-03-2026), `nota_alcance` (explica la distinción
  frente a la LFDA), `nota_persecucion` (querella vs. oficio) y
  `relacion_con_otros_corpus`.
- `articulos[]`: 12 registros (arts. 424, 424 Bis, 424 Ter, 425, 426,
  427, 427 Bis, 427 Ter, 427 Quáter, 427 Quinquies, 428 y 429), cada uno
  con `numero`, `texto_intro`, `fracciones[]`, `parrafos_finales[]` y
  `texto_completo` (usar siempre este último para citar textualmente).

## Mapa de conductas típicas

- **Art. 424** — especulación con libros de texto gratuitos; producir
  más ejemplares de una obra que los autorizados; uso doloso con fin de
  lucro sin autorización (prisión de 6 meses a 6 años).
- **Art. 424 Bis** — piratería comercial: producir, introducir al país,
  almacenar, transportar, distribuir, vender o arrendar copias de obras,
  fonogramas, videogramas o libros con fin de especulación comercial;
  fabricar dispositivos para desactivar protecciones de software; grabar
  una película en sala de cine ("camming") (prisión de 3 a 10 años, la
  pena más alta del título).
- **Art. 424 Ter** — venta directa al consumidor final en vía pública de
  copias piratas (prisión de 6 meses a 6 años); si es en establecimiento
  comercial o de forma organizada/permanente, aplica el 424 Bis.
- **Art. 425** — explotación con fines de lucro de una interpretación o
  ejecución sin derecho (afecta a artistas intérpretes/ejecutantes).
- **Art. 426** — piratería de señales: descifrar señal de satélite o
  cable cifrada sin autorización del distribuidor legítimo.
- **Art. 427** — publicar a sabiendas una obra sustituyendo el nombre del
  autor por otro (usurpación de autoría/plagio con publicación).
- **Arts. 427 Bis a 427 Quinquies** — elusión de medidas tecnológicas de
  protección (DRM) y alteración de información sobre gestión de
  derechos, con fines de lucro.
- **Art. 428** — la sanción pecuniaria no exime de la reparación del
  daño (mínimo 40% del precio de venta al público).
- **Art. 429** — regla de persecución: de oficio, EXCEPTO los delitos de
  los arts. 424 fracción II, 424 Bis fracción III y 427, que requieren
  querella de parte ofendida.

## Estrategia de búsqueda

1. Número de artículo exacto, incluyendo variantes "Bis"/"Ter"/"Quáter"/
   "Quinquies".
2. Conducta descrita por el usuario, usando el mapa de conductas típicas
   anterior.
3. Búsqueda de texto libre en `texto_intro`, `fracciones[].texto` y
   `parrafos_finales`.

Si la consulta es sobre la vía administrativa (multas del INDAUTOR/IMPI,
no prisión), remite a `consulta-infracciones-lfda`. Si involucra
jurisprudencia penal en la materia, usa `busqueda-criterios-autor`
(categoría M).

## Formato de respuesta

1. Cita el o los artículos aplicables del Código Penal Federal con su
   número y fracción exacta, reproduciendo `texto_completo`.
2. Indica siempre la pena de prisión y la multa aplicables (en días
   multa, no en UMA, a diferencia de las infracciones administrativas).
3. Señala si el delito se persigue de oficio o requiere querella,
   conforme al art. 429.
4. Explica en lenguaje llano la conducta tipificada, después de la cita
   textual.
5. Aclara siempre, cuando sea relevante, que esta es la vía penal,
   distinta y autónoma de la vía administrativa (LFDA) y de la vía civil
   de indemnización (art. 216 Bis LFDA).

## Límites

- Este corpus es un documento de trabajo del usuario, no una fuente
  oficial en tiempo real. Verificar reformas posteriores a DOF
  13-03-2026 en https://www.dof.gob.mx o
  https://www.diputados.gob.mx/LeyesBiblio/.
- No es una opinión legal definitiva ni un consejo sobre estrategia de
  defensa o querella; los borradores que produzcas requieren revisión de
  un abogado penalista antes de usarse.
