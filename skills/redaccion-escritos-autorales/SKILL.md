---
name: redaccion-escritos-autorales
description: >
  Esta skill debe usarse cuando el usuario pida "redactar una demanda
  por infracción a derechos de autor", "redacta una queja o denuncia ante
  el INDAUTOR", "prepara una notificación de retiro de contenido para
  una plataforma", "arma el capítulo de fundamento jurídico sobre
  titularidad / infracción / derecho a la imagen", "redacta un contrato o
  cláusula de cesión de derechos patrimoniales", "prepara los argumentos
  para impugnar una resolución del INDAUTOR o del IMPI", o necesite un
  borrador de argumentación legal o de un documento (demanda, denuncia,
  queja administrativa, notificación de retiro, recurso de impugnación,
  cláusula contractual) con base en la doctrina de derechos de autor
  empaquetada con este plugin.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Redacción de escritos en materia de derechos de autor

Genera un borrador de trabajo (nunca un documento final listo para
presentar sin revisión) para escritos legales en materia de derechos de
autor, fundamentado siempre en el texto literal de la LFDA, el Código
Penal Federal y/o la jurisprudencia empaquetada con este plugin.

## Flujo de trabajo

1. Identifica el tipo de escrito solicitado y el objetivo del cliente.
2. Si el usuario no ha proporcionado los hechos relevantes (partes,
   obra, conducta, fechas, pruebas disponibles), pregúntalos antes de
   redactar — no inventes hechos ni fechas.
3. Ejecuta primero el análisis correspondiente usando la skill de
   análisis aplicable de este mismo plugin:
   - Cuestión de titularidad/originalidad → `analisis-titularidad-originalidad`.
   - Cuestión de infracción, delito o indemnización → `analisis-infraccion-autoral`.
   - Cuestión de derecho a la imagen → `analisis-derecho-imagen`.
4. Redacta el escrito integrando el fundamento obtenido en el paso
   anterior, citando artículos y tesis siguiendo el formato de
   `citas-legales-autor`.

## Tipos de escritos cubiertos

- **Demanda o reclamación civil** por infracción a derechos de autor,
  incluyendo el capítulo de fundamento de la indemnización (art. 216
  Bis).
- **Queja o denuncia administrativa** ante el INDAUTOR (infracciones de
  autor, art. 229) o ante el IMPI (infracciones de comercio, art. 231).
- **Notificación de aviso y retiro** ("notice and takedown") a un
  proveedor de servicios en línea conforme al art. 232 Quinquies LFDA.
- **Querella o denuncia penal** por los delitos de los arts. 424 a 427
  Quinquies del Código Penal Federal (advirtiendo siempre cuáles
  requieren querella conforme al art. 429).
- **Recurso de impugnación administrativa** contra resoluciones del
  INDAUTOR o del IMPI (arts. 237-238 LFDA).
- **Cláusulas contractuales** de cesión o licencia de derechos
  patrimoniales, contratos de edición, o de obra por encargo, que
  cumplan con el requisito de constar expresamente y por escrito (arts.
  30 y siguientes LFDA).
- **Contestaciones** a cualquiera de los escritos anteriores.

## Estructura sugerida (adaptar según el tipo de escrito)

1. Proemio y personalidad de las partes.
2. Hechos, numerados y ordenados cronológicamente.
3. Fundamento de derecho: cita literal de cada artículo aplicable de la
   LFDA/CPF, seguida de su explicación aplicada al caso concreto.
4. Jurisprudencia de apoyo: cita cada tesis siguiendo el formato de
   `citas-legales-autor`, explicando por qué es aplicable a los hechos.
5. Petitorios o pretensiones concretas (incluyendo, si aplica, el monto
   de indemnización estimado conforme al art. 216 Bis).
6. Pruebas que se ofrecen o que se sugiere recabar.

## Reglas de citación

Sigue el formato definido en `citas-legales-autor` para todo el plugin:
nunca formules un argumento legal sin citar el artículo (identificando
siempre LFDA o CPF) y, cuando exista, la tesis que lo sustenta.

## Límites (advertencia obligatoria en cada entrega)

- Todo lo que produzcas es un **borrador de trabajo para revisión de un
  abogado**, no un documento final ni una opinión legal definitiva. Dilo
  expresamente al entregar el escrito.
- No asumas hechos, fechas, montos ni pruebas que el usuario no haya
  proporcionado.
- Advierte siempre sobre la necesidad de verificar la vigencia de las
  disposiciones citadas (LFDA: DOF 14-05-2026; CPF: DOF 13-03-2026) antes
  de presentar el escrito ante cualquier autoridad.
