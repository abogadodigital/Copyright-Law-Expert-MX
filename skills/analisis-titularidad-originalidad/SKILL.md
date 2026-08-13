---
name: analisis-titularidad-originalidad
description: >
  Esta skill debe usarse cuando el usuario pida "analizar si una obra es
  protegible por derechos de autor", "quién es el titular de los
  derechos de esta obra", "hay coautoría en este proyecto", "es una obra
  por encargo o una obra hecha en relación laboral", "quién tiene los
  derechos patrimoniales si contraté a un freelancer / empleado /
  agencia para crear esto", "se necesita registro ante el INDAUTOR para
  que exista protección", "esta obra es originaria o derivada", o
  proporcione los hechos de una creación (obra literaria, artística,
  software, diseño, fotografía, obra por encargo) y pregunte sobre su
  protegibilidad, originalidad o titularidad conforme al derecho de autor
  mexicano (LFDA).
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Análisis de originalidad y titularidad de derechos de autor

Dictamina, con base en los hechos que proporcione el usuario, si una obra
es susceptible de protección por derechos de autor conforme a la LFDA, y
quién es (o quiénes son) su titular originario y, en su caso, derivado.
Fundamenta cada conclusión citando el o los artículos aplicables de la
LFDA y, cuando exista, la jurisprudencia empaquetada que la sustente.

## Fuentes de datos

- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lfda-derecho-autor/references/corpus_lfda_derecho_autor.json`
  — Título I (arts. 1-10, obras protegidas y clasificación del art. 4),
  Título II (arts. 11-29, derecho de autor, obras que no son objeto de
  protección conforme al art. 14), Título III (arts. 30-76, transmisión
  de derechos patrimoniales, contratos de edición, obra por encargo).
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-autor/references/corpus_tesis_derechos_autor.json`
  — categorías **B** (concepto de obra, objeto y requisitos de
  protección) y **G** (obra por encargo, coautoría y titularidad
  derivada); complementa con **E** (Registro Público del Derecho de
  Autor e INDAUTOR) cuando el usuario pregunte sobre el efecto probatorio
  del registro.

## Marco de análisis (en este orden)

1. **Protegibilidad**: ¿la creación es una obra en el sentido del art. 3
   LFDA (creación original susceptible de divulgarse o reproducirse) y
   está fijada en un soporte material (art. 5)? Recuerda que la
   protección NO requiere registro ni formalidad alguna (art. 5, segundo
   párrafo) — cita la jurisprudencia de categoría B que confirma que
   basta la originalidad y la fijación material. Verifica también que no
   se trate de una de las exclusiones del art. 14 (ideas, procedimientos,
   sistemas, esquemas, nombres, títulos aislados, aprovechamiento
   industrial o comercial de las ideas, textos legislativos/judiciales/
   administrativos, contenido informativo de noticias, información de
   uso común, etc.).
2. **Clasificación de la obra** conforme al art. 4 (según su autor:
   conocida/anónima/seudónima; según su comunicación: divulgada/inédita/
   publicada; según su origen: primigenia/derivada; según los creadores
   que intervienen: individual/de colaboración/colectiva) — esta
   clasificación determina las reglas de titularidad aplicables.
3. **Titularidad originaria**: por regla general, el autor es la persona
   física que crea la obra (art. 12). Si es obra de colaboración,
   distingue si es divisible o indivisible (arts. 15-16); si es obra
   colectiva, identifica al organizador conforme al art. 4, fracción
   D-III.
4. **Titularidad derivada / obra por encargo / relación laboral**:
   analiza si existe cesión, licencia o presunción legal de transmisión
   de derechos patrimoniales. Bajo la LFDA, la transmisión de derechos
   patrimoniales debe pactarse **expresamente y por escrito** (art. 30 y
   siguientes) — no existe cesión automática de derechos patrimoniales
   por el solo hecho de la relación laboral o del pago de honorarios,
   salvo pacto expreso. Cita la jurisprudencia de categoría G sobre este
   punto, que es una de las áreas de mayor litigiosidad práctica.
5. **Derechos morales**: recuerda siempre que, exista o no cesión de
   derechos patrimoniales, el derecho moral (paternidad, integridad,
   divulgación) es perpetuo, inalienable, irrenunciable e imprescriptible
   (arts. 18-21) y permanece siempre en la persona física autora, salvo
   las excepciones expresas de la propia Ley.
6. **Efecto del registro ante el INDAUTOR**: el registro (Título VIII,
   arts. 162-191) NO es constitutivo de derechos, sino declarativo y
   genera una presunción de autoría o titularidad que admite prueba en
   contrario — cita la jurisprudencia de categoría E sobre este punto.

## Formato de la respuesta

1. Presenta primero la conclusión (¿es protegible?, ¿quién es el
   titular originario?, ¿hubo transmisión válida de derechos
   patrimoniales?) en un párrafo breve.
2. Desarrolla el fundamento artículo por artículo, citando siempre
   `texto_completo` o el fragmento relevante de la LFDA.
3. Cita la jurisprudencia aplicable con su rubro y `enlace`, siguiendo el
   formato de `busqueda-criterios-autor`.
4. Señala expresamente los riesgos o vacíos probatorios (p. ej. "no hay
   constancia escrita de cesión de derechos patrimoniales, por lo que el
   creador conserva la titularidad patrimonial salvo prueba en
   contrario").
5. Si la consulta involucra el derecho a la imagen de una persona
   retratada (no la autoría de la fotografía), remite a la skill
   `analisis-derecho-imagen`, que trata esa figura de forma autónoma.

## Límites

- Este es un análisis preliminar de trabajo, no una opinión legal
  definitiva ni un dictamen pericial. Recomienda siempre la revisión de
  un abogado especializado antes de tomar decisiones con consecuencias
  patrimoniales o de litigio.
- Si los hechos son insuficientes para concluir (p. ej. no se sabe si
  hubo contrato escrito), dilo expresamente y enumera qué información
  falta para dictaminar con certeza.
