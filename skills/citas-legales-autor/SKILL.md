---
name: citas-legales-autor
description: >
  Esta skill define el formato obligatorio para citar tesis,
  jurisprudencia y artículos de la LFDA o del Código Penal Federal (CPF)
  en cualquier respuesta de este plugin. Las demás skills de este plugin
  (busqueda-criterios-autor, consulta-lfda-derecho-autor,
  consulta-infracciones-lfda, consulta-delitos-autor,
  analisis-titularidad-originalidad, analisis-infraccion-autoral,
  analisis-derecho-imagen, redaccion-escritos-autorales,
  material-docente-autor) deben consultarla cada vez que citen un
  criterio de la SCJN o un artículo de la LFDA/CPF, en vez de describir
  su propio formato. También úsala cuando el usuario pregunte
  directamente "cómo citas la jurisprudencia", "cuál es el formato de
  citas de este plugin" o equivalente.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Formato de citación

Todas las demás skills de este plugin que citen jurisprudencia, tesis o
artículos de la LFDA o del Código Penal Federal deben seguir exactamente
las reglas de este documento. Ninguna otra skill debe describir su
propio formato de citación en prosa ni inventar variantes: solo debe
remitir aquí
(`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-autor/SKILL.md`).

## 1. Citación de jurisprudencia y tesis

### 1.1 Cuántos resultados dicta qué formato

- **1 a 4 criterios** → formato completo (sección 1.2). Es obligatorio
  siempre que la consulta arroje entre 1 y 4 resultados, sin excepción —
  nunca lo sustituyas por el formato abreviado solo porque el contenido
  del registro es extenso.
- **5 o más criterios** → formato abreviado (sección 1.3).

### 1.2 Formato completo (1 a 4 criterios)

Para cada criterio, en este orden, cada etiqueta en su propia línea, sin
fusionar dos etiquetas en un mismo renglón:

```
[TÍTULO COMPLETO DE LA TESIS O JURISPRUDENCIA, el `rubro` tal cual del corpus]
Autoridad emisora: [autoridad_emisora] (Ejemplo: Pleno de la Suprema Corte de Justicia de la Nación)
Tipo y época: [tipo_y_epoca] (Ejemplo: Jurisprudencia, Duodécima Época)
Fecha: [fecha, formato DD/MM/AAAA]
Registro digital: [registro_digital]
Enlace: [enlace] (Ejemplo: https://sjf2.scjn.gob.mx/detalle/tesis/2032298)
Resumen: [redacta un texto breve que resuma los hechos, el criterio jurídico y la justificación; puedes apoyarte en el campo `resumen` del corpus]

- Contenido de la tesis -
Hechos: [copia los hechos en su totalidad]
Criterio jurídico: [copia el criterio jurídico en su totalidad]
Justificación: [copia la justificación en su totalidad]
```

Si el registro del corpus no tiene la estructura Hechos/Criterio
jurídico/Justificación sino un campo `texto_integro` (tesis de
estructura tradicional en bloque único, típica de épocas anteriores a la
Décima), sustituye el bloque "- Contenido de la tesis -" por el
`texto_integro` completo, sin parafrasear ni resumir la regla legal
operativa. Si un registro no trae alguno de los tres campos, omite esa
línea específica y conserva las demás.

No omitas ninguna etiqueta (Autoridad emisora, Tipo y época, Fecha,
Registro digital, Enlace, Resumen) aunque el dato parezca obvio por el
contexto. Nunca uses etiquetas distintas a las de esta plantilla.

### 1.3 Formato abreviado (5 o más criterios)

Numera cada criterio por orden de aparición y usa las mismas etiquetas
de la sección 1.2, sin el bloque de "Contenido de la tesis":

```
[N]. [TÍTULO COMPLETO DE LA TESIS O JURISPRUDENCIA]
Autoridad emisora: [autoridad_emisora]
Tipo y época: [tipo_y_epoca]
Fecha: [fecha]
Registro digital: [registro_digital]
Enlace: [enlace]
Resumen: [el campo `resumen` del corpus, sin parafrasear]
```

No incluyas `hechos`/`criterio_juridico`/`justificacion`/`texto_integro`
en esta lista abreviada. Al final de la lista, pregunta al usuario si
quiere conocer el contenido completo de alguna tesis, pidiéndole que la
identifique **por orden de aparición** ("¿quieres que te muestre el
contenido de la primera, la segunda, la tercera...?"), no por número de
registro digital. Cuando el usuario responda, entrega ese criterio en el
formato completo de la sección 1.2.

### 1.4 Excepción expresa

Si el usuario pide explícitamente solo el título y el enlace (p. ej.
"solo dame los títulos y el link"), respeta esa instrucción y omite el
resto de las etiquetas, sin perder el título ni el enlace oficial.

## 2. Citación de artículos de ley

Cada vez que cites un artículo, usa este formato, identificando siempre
el ordenamiento entre paréntesis:

```
Artículo [número] (LFDA): [texto completo del artículo, incluyendo
todos sus párrafos, fracciones e incisos]
```

o, cuando se trate de un delito del Código Penal Federal (Título
Vigésimo Sexto):

```
Artículo [número] (CPF): [texto completo del artículo]
```

Ejemplos: `Artículo 21 (LFDA): [texto_completo del art. 21]`;
`Artículo 424 Bis (CPF): [texto_completo del art. 424 Bis]`.

Nunca cites solo el número de artículo sin su texto completo, ni
parafrasees el texto legal — reprodúcelo tal cual aparece en el campo
`texto_completo` del corpus normativo correspondiente
(`corpus_lfda_derecho_autor.json`, `corpus_infracciones_lfda.json` o
`corpus_cpf_delitos_autor.json`, según el artículo). Identifica siempre
expresamente si el artículo citado es de la LFDA o del CPF: son
ordenamientos distintos y no deben confundirse, en particular porque los
delitos en materia de derechos de autor están en el CPF, no en la LFDA.

## 3. Fuente de la cita: el corpus empaquetado

Cada criterio que cites proviene del corpus integrado con este plugin
(`corpus_tesis_derechos_autor.json`), curado a partir de fuentes
oficiales (SJF2). Al citar un criterio, la fuente que reportas al usuario
es siempre ese corpus y el `enlace` oficial de verificación que trae cada
registro — esa es la referencia correcta y suficiente; no hace falta
añadir explicaciones sobre cómo se integró el corpus ni de dónde salió
originalmente cada dato.

Todas las skills de este plugin que citan jurisprudencia trabajan contra
este corpus ya integrado. La única excepción es `actualizar-corpus-autoral`,
que sí puede consultar un conector de investigación jurídica en vivo, pero
solo cuando el usuario se lo pida expresamente y ese conector esté
disponible en el entorno — y únicamente para proponer altas nuevas al
corpus, no para responder una consulta normal.

## 4. Regla general

Ninguna otra skill de este plugin debe reimplementar ni parafrasear
estas reglas: deben remitir a este documento para el formato exacto de
citación, tanto de jurisprudencia como de artículos de la LFDA o del
CPF.
