---
name: material-docente-autor
description: >
  Esta skill debe usarse cuando el usuario pida "crear material de clase
  sobre derechos de autor", "hazme un resumen temático para estudiantes",
  "genera reactivos de examen sobre derecho de autor mexicano", "arma un
  caso práctico para la clase de propiedad intelectual", "prepara
  flashcards sobre derechos morales y patrimoniales", "diseña una
  actividad sobre INDAUTOR o gestión colectiva", o de cualquier otra
  forma necesite material didáctico para un curso de derecho, taller o
  diplomado, con base en la LFDA, el Código Penal Federal y la doctrina
  jurisprudencial de derechos de autor empaquetada con este plugin.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Material docente sobre derechos de autor mexicano

Genera material didáctico (resúmenes temáticos, casos prácticos,
reactivos de examen, flashcards, cuadros comparativos) para la enseñanza
del derecho de autor mexicano, con base exclusivamente en el contenido
empaquetado con este plugin: la LFDA completa, el Título Vigésimo Sexto
del Código Penal Federal y los 79 criterios jurisprudenciales.

## Fuentes de datos

Usa según el tema solicitado:

- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lfda-derecho-autor/references/corpus_lfda_derecho_autor.json`
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-infracciones-lfda/references/corpus_infracciones_lfda.json`
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-delitos-autor/references/corpus_cpf_delitos_autor.json`
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-autor/references/corpus_tesis_derechos_autor.json`

## Ejes temáticos sugeridos (mapeados a las 17 categorías de tesis y a
## los 12 Títulos de la LFDA)

Organiza el material siguiendo, según convenga al nivel del curso, la
misma estructura temática del corpus de tesis (categorías A-Q) o el
índice de Títulos de la LFDA (I-XII). Temas de mayor densidad
jurisprudencial que suelen justificar una sesión propia: Registro
Público del Derecho de Autor e INDAUTOR (categoría E, 12 criterios),
derecho a la imagen y al retrato (categoría H, 8 criterios), regalías y
explotación patrimonial (categoría D, 8 criterios), delitos en materia de
derechos de autor (categoría M, 7 criterios) y excepciones/límites
(categoría J, 7 criterios).

## Tipos de material que puedes producir

- **Resumen temático**: síntesis en lenguaje claro de un Título de la
  LFDA o de una categoría de tesis, con citas textuales de los artículos
  y criterios más relevantes.
- **Caso práctico**: hechos hipotéticos (siempre ficticios, aclarándolo
  expresamente) que planteen un problema de titularidad, infracción o
  derecho a la imagen, con preguntas guía y, si se solicita, la solución
  razonada citando el fundamento aplicable.
- **Reactivos de examen**: opción múltiple, verdadero/falso o pregunta
  abierta, basados en el texto literal de los artículos o en el criterio
  jurídico de las tesis (nunca en interpretaciones no sustentadas en el
  corpus). Indica siempre la respuesta correcta y su fundamento.
- **Flashcards**: pares pregunta/respuesta breves para memorización de
  definiciones, plazos, artículos clave y jerarquía de fuentes.
- **Cuadros comparativos**: p. ej. derecho moral vs. derecho patrimonial;
  vía administrativa vs. penal vs. civil; INDAUTOR vs. IMPI como
  autoridades competentes.

Si el usuario pide construir un examen completo, un temario/syllabus, o
la revisión/calificación de evaluaciones ya elaboradas, considera usar en
conjunto las skills especializadas de docencia jurídica disponibles en el
entorno (creación de exámenes, material de estudio, syllabus o revisión
de evaluaciones), aportando tú el contenido sustantivo de derechos de
autor que esas skills necesiten.

## Reglas de contenido

- Toda afirmación normativa debe fundamentarse en el `texto_completo` del
  artículo correspondiente; toda afirmación jurisprudencial, en el
  contenido de la tesis correspondiente, siguiendo el formato de
  `citas-legales-autor`.
- No inventes artículos, números de registro digital ni rubros de tesis
  que no existan en el corpus.
- Distingue siempre, en el material que generes, entre lo que es texto
  legal vigente y lo que es interpretación judicial de ese texto.

## Límites

- El corpus jurisprudencial está vigente al 13 de agosto de 2026 y la
  LFDA a la reforma DOF 14-05-2026; adviértelo si el material se usará en
  cursos futuros, sugiriendo verificar reformas posteriores.
- Este material es de apoyo docente, no una opinión legal ni un
  sustituto de la lectura directa de las fuentes oficiales por parte del
  estudiante.
