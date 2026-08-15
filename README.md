# Copyright Law Expert - MX

Plugin de Claude especializado en derecho de autor mexicano. Empaqueta
cuatro corpus de datos —la Ley Federal del Derecho de Autor (LFDA)
completa, el Título Vigésimo Sexto del Código Penal Federal (delitos en
materia de derechos de autor) y 79 tesis y jurisprudencias de la Suprema
Corte de Justicia de la Nación— junto con once skills funcionales para
consulta normativa, búsqueda jurisprudencial, análisis aplicado,
redacción de escritos, generación de material docente y un formato de
citación unificado para todo el plugin.

Las skills se activan automáticamente cuando la solicitud del usuario
coincide con su propósito; no requieren invocación explícita.

## Corpus incluidos

| Archivo | Contenido | Registros |
|---|---|---|
| `corpus_lfda_derecho_autor.json` | LFDA completa, Títulos I-XII (arts. 1-238) | 258 artículos |
| `corpus_infracciones_lfda.json` | LFDA, Título XII: infracciones administrativas (arts. 229-238) | 15 artículos |
| `corpus_cpf_delitos_autor.json` | Código Penal Federal, Título Vigésimo Sexto: delitos (arts. 424-429) | 12 artículos |
| `corpus_tesis_derechos_autor.json` | Tesis y jurisprudencia de la SCJN, 17 categorías temáticas (A-Q) | 79 criterios |

Fechas de corte: LFDA y su Título XII, DOF 14-05-2026; Código Penal
Federal, DOF 13-03-2026; investigación jurisprudencial, 13 de agosto de
2026. Antes de invocar cualquier disposición o criterio en un escrito,
verificar vigencia en las fuentes oficiales (https://www.dof.gob.mx,
https://www.diputados.gob.mx/LeyesBiblio/, https://sjf2.scjn.gob.mx).

## Skills incluidas

1. **consulta-lfda-derecho-autor** — texto literal de la LFDA, Títulos I
   a XI (arts. 1-228): derecho moral y patrimonial, transmisión de
   derechos, derechos conexos, límites y excepciones, símbolos patrios,
   registros, gestión colectiva, INDAUTOR y procedimientos.
2. **consulta-infracciones-lfda** — texto literal del Título XII de la
   LFDA (arts. 229-238): infracciones administrativas de autor y de
   comercio, e impugnación administrativa.
3. **consulta-delitos-autor** — texto literal del Título Vigésimo Sexto
   del Código Penal Federal (arts. 424-429): delitos en materia de
   derechos de autor.
4. **busqueda-criterios-autor** — localiza y cita los 79 criterios de la
   SCJN por categoría, artículo o palabra clave.
5. **analisis-titularidad-originalidad** — dictamina protegibilidad,
   originalidad y titularidad (obra por encargo, coautoría, relación
   laboral).
6. **analisis-infraccion-autoral** — dictamina infracción administrativa,
   delito y/o indemnización civil (las tres vías autónomas), y estima
   exposición económica.
7. **analisis-derecho-imagen** — dictamina la licitud del uso del
   retrato o imagen de una persona (arts. 87-88 LFDA), distinguiéndolo
   del derecho de autor sobre la fotografía.
8. **redaccion-escritos-autorales** — redacta demandas, quejas
   administrativas, querellas, notificaciones de retiro de contenido,
   recursos de impugnación y cláusulas contractuales de cesión de
   derechos.
9. **material-docente-autor** — genera resúmenes temáticos, casos
   prácticos, reactivos de examen, flashcards y cuadros comparativos para
   la enseñanza del derecho de autor mexicano.
10. **actualizar-corpus-autoral** *(opcional, mantenimiento)* — busca
    tesis y reformas posteriores a las fechas de corte. Requiere un
    conector de búsqueda jurisprudencial/normativa disponible en el
    entorno; degrada de forma controlada si no está disponible.
11. **citas-legales-autor** — define el formato único y obligatorio de
    citación de tesis, jurisprudencia y artículos de la LFDA/CPF que usan
    las demás skills de este plugin, evitando que cada una describa su
    propio formato de forma inconsistente.

## Instalación

Instala este plugin en Claude Code, Claude Cowork o cualquier entorno
compatible con el estándar de plugins de Claude, apuntando al directorio
de este repositorio o al archivo `.plugin` empaquetado.

## Limitaciones

- Los corpus son documentos de trabajo generados a partir de una
  investigación puntual; no sustituyen la consulta directa a las fuentes
  oficiales, particularmente ante reformas o criterios posteriores a las
  fechas de corte indicadas arriba.
- Ninguna skill de este plugin constituye asesoría legal definitiva. Todo
  borrador, dictamen o análisis producido requiere revisión de un
  abogado antes de usarse con consecuencias legales.
- Los delitos en materia de derechos de autor no están en la LFDA sino en
  el Código Penal Federal; este plugin distingue expresamente ambas
  fuentes en cada skill relevante.

## Autoría

**Joel Alejandro Gómez Treviño**

## Licencia

CC BY-NC-SA 4.0 (con condiciones adicionales de uso no comercial) — ver `LICENSE.md`.
