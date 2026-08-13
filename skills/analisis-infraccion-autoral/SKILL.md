---
name: analisis-infraccion-autoral
description: >
  Esta skill debe usarse cuando el usuario pida "analizar si esta
  conducta es una infracción a derechos de autor", "esto es piratería o
  delito", "cuánto podría reclamar de indemnización por el uso no
  autorizado de mi obra", "qué exposición legal tiene una plataforma que
  aloja contenido infractor", "puedo demandar civil, administrativa o
  penalmente", "califica el riesgo de esta conducta frente a la LFDA y el
  Código Penal Federal", o proporcione los hechos de un uso no autorizado
  de una obra, fonograma, videograma o emisión (reproducción, copia,
  distribución, elusión de DRM, uso en Internet) y pregunte por la vía de
  reclamación aplicable, la sanción esperable o el monto de la
  indemnización conforme al derecho de autor mexicano.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Análisis de infracción autoral y exposición legal

Dictamina, con base en los hechos que proporcione el usuario, si una
conducta constituye una infracción administrativa (LFDA), un delito
(Código Penal Federal) y/o da lugar a una indemnización civil por daños y
perjuicios, identificando las tres vías disponibles de forma expresa y
sin confundirlas entre sí.

## Fuentes de datos

- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-infracciones-lfda/references/corpus_infracciones_lfda.json`
  — vía administrativa (arts. 229-238 LFDA).
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-delitos-autor/references/corpus_cpf_delitos_autor.json`
  — vía penal (arts. 424-429 CPF).
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lfda-derecho-autor/references/corpus_lfda_derecho_autor.json`
  — art. 216 Bis (Título XI) para la indemnización civil por daños y
  perjuicios.
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-autor/references/corpus_tesis_derechos_autor.json`
  — categorías **K** (indemnización, art. 216 Bis), **L** (infracciones
  administrativas), **M** (delitos) y **N** (Internet, plataformas
  digitales y medidas cautelares).

## Marco de análisis: las tres vías autónomas

Antes de concluir, evalúa siempre las tres vías por separado — pueden
coexistir para una misma conducta, conforme al lineamiento 8 de
`metadata.conclusiones_y_lineamientos` del corpus de tesis:

1. **Vía administrativa** (INDAUTOR/IMPI, corpus
   `corpus_infracciones_lfda.json`): ¿la conducta encuadra en alguna de
   las fracciones del art. 229 (infracción de autor) o del art. 231
   (infracción de comercio)? Identifica la autoridad competente y el
   rango de sanción (arts. 230 y 232, en UMA).
2. **Vía penal** (Código Penal Federal, corpus
   `corpus_cpf_delitos_autor.json`): ¿existe dolo y fin de lucro o
   especulación comercial (elemento típico central de la mayoría de
   estos delitos)? Identifica el artículo aplicable (424 a 427
   Quinquies), la pena de prisión y si se persigue de oficio o requiere
   querella (art. 429). Sin fin de lucro o especulación comercial, la
   mayoría de estas conductas NO son delito, aunque puedan seguir siendo
   infracción administrativa o generar responsabilidad civil.
3. **Vía civil — indemnización por daños y perjuicios** (art. 216 Bis
   LFDA): calcula conforme al criterio legal (no menor al 40% del precio
   de venta al público de cada producto o de la prestación de servicios
   que impliquen violación, salvo que el titular acredite que el daño
   sufrido es mayor). Cita la jurisprudencia de categoría K sobre los
   criterios de cuantificación y la relación de este artículo con la
   acción de responsabilidad civil general.

## Consideraciones específicas de Internet y plataformas digitales

Cuando los hechos involucren un proveedor de servicios en línea (hosting,
red social, plataforma de contenido generado por usuarios), aplica el
régimen de aviso y retiro del art. 232 Quinquies LFDA (responsabilidad
del proveedor si no remueve el contenido de forma expedita tras notificación
fundada) y consulta la categoría **N** del corpus de tesis (medidas
cautelares e Internet), que es la categoría más reciente y con menor
desarrollo jurisprudencial consolidado — adviértelo expresamente al
usuario si solo hay un criterio disponible.

## Formato de la respuesta

1. Presenta un cuadro o resumen de las tres vías, indicando para cada una
   si aplica ("sí aplica", "no aplica", "aplica con reservas: falta
   acreditar X") y el fundamento correspondiente.
2. Desarrolla el fundamento artículo por artículo, citando siempre
   `texto_completo` del corpus correspondiente.
3. Cita la jurisprudencia aplicable con su rubro y contenido, siguiendo
   el formato de `busqueda-criterios-autor` (contenido completo si son
   1 a 4 criterios; abreviado con `resumen` y opción de ampliar si son 5
   o más), con el `enlace` oficial al final de cada criterio.
4. Si el usuario pide una estimación numérica de indemnización, muestra
   el cálculo del 40% mínimo sobre la base que proporcione, aclarando
   que es un piso legal y no un techo, y que el titular puede acreditar
   un daño mayor.
5. Si se te pide redactar un escrito con este análisis (demanda, querella,
   denuncia, oficio de retiro de contenido), remite a la skill
   `redaccion-escritos-autorales`.

## Límites

- Este es un análisis preliminar de trabajo, no una opinión legal
  definitiva. La calificación penal en particular (dolo, fin de lucro,
  especulación comercial) depende de elementos probatorios que solo un
  juez puede valorar; no la presentes como una certeza.
- Recomienda siempre la revisión de un abogado especializado, y de un
  penalista en particular si hay indicios de conducta delictiva, antes de
  iniciar cualquier acción.
