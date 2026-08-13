---
name: actualizar-corpus-autoral
description: >
  Esta skill debe usarse cuando el usuario pida "buscar tesis nuevas de
  derechos de autor", "actualiza el corpus con criterios recientes",
  "hay jurisprudencia nueva sobre INDAUTOR / derecho a la imagen /
  gestión colectiva / delitos de derechos de autor", o quiera verificar
  si la SCJN ha emitido criterios aún no incluidos en el corpus
  empaquetado con este plugin, o si la LFDA o el Título Vigésimo Sexto
  del Código Penal Federal han sido reformados después de las fechas de
  corte reflejadas en los corpus (LFDA: DOF 14-05-2026; CPF: DOF
  13-03-2026; tesis: 13 de agosto de 2026).
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Actualización del corpus de derechos de autor (mantenimiento opcional)

Verifica si existen tesis, jurisprudencias o reformas legislativas en
materia de derechos de autor posteriores a las fechas de corte de los
corpus empaquetados con este plugin, y propone al usuario cómo
incorporarlas.

## Requisito: conector de búsqueda jurisprudencial y normativa

Esta skill requiere un conector capaz de buscar en el Semanario Judicial
de la Federación (tesis y jurisprudencia de la SCJN) y, de forma
deseable, en el Diario Oficial de la Federación (reformas legislativas) —
por ejemplo, un conector tipo "Kriterius". Antes de ejecutar una
búsqueda, verifica si dicho conector está disponible en el entorno
actual.

## Si el conector está disponible

1. Pregunta al usuario (o infiere del contexto) el tema o los artículos
   sobre los que quiere verificar novedades — puedes usar como referencia
   las 17 categorías del corpus de tesis (A-Q) o cualquier Título de la
   LFDA.
2. Busca tesis y jurisprudencias posteriores a la fecha de corte
   (13-08-2026) que no aparezcan ya en
   `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-autor/references/corpus_tesis_derechos_autor.json`
   (compara por `registro_digital` para evitar duplicados).
3. Si el conector también permite consultar el DOF, verifica si existen
   reformas a la LFDA o al Título Vigésimo Sexto del Código Penal Federal
   posteriores a las fechas de corte de
   `corpus_lfda_derecho_autor.json`,
   `corpus_infracciones_lfda.json` y
   `corpus_cpf_delitos_autor.json`.
4. Presenta los hallazgos al usuario con su cita completa y liga oficial
   (sigue el formato de citas-legales-mx si está instalada), agrupados
   por relevancia, y pregunta si desea que los incorpores al corpus
   empaquetado (edición del archivo JSON correspondiente) o si solo
   quiere la referencia para uso inmediato.
5. Nunca modifiques un corpus sin la confirmación explícita del usuario.

## Si el conector NO está disponible (degradación controlada)

Informa al usuario, de forma breve y sin bloquear el resto del plugin,
que esta skill de mantenimiento requiere un conector de búsqueda
jurisprudencial/normativa que no está disponible en este entorno, y
ofrece alternativas:

- Sugerir que el usuario realice la búsqueda manualmente en
  https://sjf2.scjn.gob.mx (SCJN) y https://www.dof.gob.mx (DOF).
- Continuar usando el resto de las skills del plugin con el corpus
  empaquetado actual, aclarando sus fechas de corte.

No intentes buscar en la web abierta como sustituto de un conector
jurisprudencial oficial: los resultados de una búsqueda web genérica no
sustituyen la fuente primaria y pueden inducir a error en materia legal.

## Límites

- Esta skill es de mantenimiento opcional y no forma parte del flujo
  principal de consulta, análisis, redacción o docencia del plugin.
- Cualquier criterio o reforma que se proponga incorporar debe citarse
  con su fuente oficial completa antes de agregarse al corpus.
