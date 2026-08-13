---
name: analisis-derecho-imagen
description: >
  Esta skill debe usarse cuando el usuario pida "analizar si se puede
  usar la foto o el video de una persona sin su consentimiento", "hay
  violación al derecho a la imagen o al retrato", "qué dice el artículo
  87 u 88 de la LFDA", "puedo usar la imagen de una persona famosa en
  publicidad", "qué pasa si publico una fotografía de alguien sin
  autorización", "es lo mismo el derecho de autor de la foto que el
  derecho a la imagen de la persona fotografiada", o proporcione hechos
  sobre el uso, publicación o explotación de la imagen, retrato o
  semejanza de una persona (fotografía, video, IA generativa) y pregunte
  por su licitud conforme a la legislación autoral mexicana (arts. 87 y
  88 LFDA) y su jurisprudencia.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Análisis del derecho a la imagen y al retrato

Dictamina, con base en los hechos que proporcione el usuario, si el uso,
captura o publicación de la imagen o el retrato de una persona requiere
su consentimiento conforme a los artículos 87 y 88 de la LFDA, y si se
actualiza alguna excepción legal.

## Advertencia conceptual (no confundir)

El derecho a la imagen que regula la LFDA en su Título IV es una figura
**distinta y autónoma** del derecho de autor sobre la fotografía o el
video en sí. Quien toma la fotografía tiene derechos de autor sobre la
imagen como obra (Título II/IV de la LFDA, ver skill
`analisis-titularidad-originalidad`); la persona retratada tiene, por
separado, un derecho a que no se publique, reproduzca o explote su
imagen sin su consentimiento (art. 87 LFDA). Ambos derechos pueden
coexistir en cabezas distintas y deben analizarse por separado. Cita
siempre la jurisprudencia de categoría H, que confirma esta autonomía.

## Fuentes de datos

- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lfda-derecho-autor/references/corpus_lfda_derecho_autor.json`
  — arts. 87 y 88 (Título IV, De la Protección al Derecho de Autor).
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-autor/references/corpus_tesis_derechos_autor.json`
  — categoría **H** (derecho a la imagen y al retrato en la legislación
  autoral, 8 criterios — la segunda categoría más numerosa del corpus
  después de la de registro/INDAUTOR); complementa con categoría **I**
  (responsabilidad editorial y daño moral en medios de comunicación)
  cuando el uso indebido de la imagen ocurrió en un medio de
  comunicación.

## Marco de análisis

1. **Regla general (art. 87)**: el retrato de una persona no puede ser
   usado, publicado, expuesto, comercializado o divulgado sin su
   consentimiento expreso, o el de sus representantes o causahabientes.
2. **Excepciones legales (art. 88 y jurisprudencia de categoría H)**:
   analiza si aplica alguna excepción, típicamente: la persona retratada
   forma parte menor de un conjunto o de un lugar público; el retrato se
   obtiene con motivo de fines informativos, periodísticos o
   educativos; se trata de personas que ejercen cargos públicos, en el
   ejercicio de sus funciones; hay consentimiento tácito derivable de
   las circunstancias. No des por sentada ninguna excepción sin
   verificarla contra el texto exacto del art. 88 y la jurisprudencia
   aplicable.
3. **Consentimiento y su alcance**: si hubo consentimiento, analiza su
   alcance (¿fue para un uso específico, con límite de tiempo, medio o
   territorio?) — el consentimiento no se presume extensivo a usos no
   contemplados originalmente.
4. **Personas fallecidas y menores de edad**: identifica si los hechos
   involucran a herederos/causahabientes (art. 87, segundo párrafo) o a
   menores de edad, casos en los que la jurisprudencia empaquetada puede
   ofrecer un estándar reforzado; señálalo expresamente si el corpus
   contiene un criterio aplicable.
5. **Concurrencia con otros derechos**: si los hechos también involucran
   difamación, daño moral fuera del ámbito autoral, protección de datos
   personales biométricos, o uso de inteligencia artificial para generar
   una semejanza sintética de la persona, adviértelo y aclara que esta
   skill cubre exclusivamente el ángulo de la LFDA (arts. 87-88), no esas
   otras materias, que requieren análisis bajo otras leyes.

## Formato de la respuesta

1. Presenta la conclusión (¿se requería consentimiento?, ¿se actualiza
   una excepción?) en un párrafo breve.
2. Cita el texto íntegro de los arts. 87 y 88 aplicables.
3. Cita la jurisprudencia de categoría H (y, en su caso, I) con rubro y
   contenido, siguiendo el formato de `busqueda-criterios-autor`
   (contenido completo si son 1 a 4 criterios; abreviado con `resumen` y
   opción de ampliar si son 5 o más), con el `enlace` oficial al final de
   cada criterio.
4. Si el uso indebido de la imagen también genera exposición bajo el
   régimen de infracciones o indemnización (arts. 229 y 216 Bis LFDA),
   remite a la skill `analisis-infraccion-autoral` para cuantificar esa
   exposición.

## Límites

- Este es un análisis preliminar de trabajo, no una opinión legal
  definitiva. La ponderación entre el derecho a la imagen y la libertad
  de expresión o el interés público suele requerir un análisis
  constitucional más amplio que excede el corpus empaquetado; adviértelo
  cuando los hechos lo sugieran.
- Recomienda siempre la revisión de un abogado especializado antes de
  tomar decisiones con consecuencias legales.
