# CualitativIA

**Investigación cualitativa privada: transcribir, anonimizar y codificar entrevistas y grupos focales sin que el audio completo ni los nombres reales salgan de tu ordenador.**

Aplicación web de un solo fichero (`index.html`), sin servidor ni instalación. Pensada para investigación en ciencias de la salud y sociales.

> Fernando Borrás Rocher y María del Carmen Lillo Navarro · Universidad Miguel Hernández de Elche

---

## Qué hace

Siete pasos, de la grabación al informe:

| Paso | Qué ocurre |
|---|---|
| 1. Estudio | Objetivos, participantes y lista de nombres a proteger. |
| 2. Transcribir | Transcripción privada en el navegador (ver más abajo) o importación de una transcripción ya hecha (texto, Word, VTT, SRT, marcas de MAXQDA). |
| 3. Quién habla y revisión | Asignas cada voz a su participante, escuchas los fragmentos y corriges. Los turnos dudosos salen en ámbar. |
| 4. Anonimizar | Sustituye nombres, lugares, centros, fechas, contactos y documentos por códigos. La clave de reidentificación se queda contigo. |
| 5. Análisis | Árbol de códigos a varios niveles, con asignación de **todos** los fragmentos y citas literales comprobadas. |
| 6. Métodos mixtos | Cruce de códigos con atributos de los participantes. |
| 7. Exportar | MAXQDA (`.txt`), Word (transcripciones e informe con citas) y proyecto `.qdpx` / codebook `.qdc`. |

Las exportaciones se generan en el propio navegador, sin librerías externas.

---

## Transcripción privada: cómo funciona

Todo el trabajo se hace en tu navegador. Al pulsar **«Transcribir en privado»**:

1. El audio se decodifica localmente.
2. **Whisper local** (tiny, base o small) da el texto con tiempos por palabra. Usa la tarjeta gráfica (WebGPU) si está disponible.
3. Se **separan las voces** (método rápido sin descargas, o modelo WavLM «preciso») y se construyen los turnos.
4. Se **localizan los datos personales** y se **cortan del audio**: tu lista de nombres (con coincidencia aproximada, p. ej. «Giménez» ≈ «Jiménez»), teléfonos, correos, DNI/NIE, IBAN, fechas, números dictados y, opcionalmente, un modelo de lenguaje que detecta nombres y lugares.
5. La app muestra **cuántos trozos se envían, cuántos minutos y el coste estimado**, y espera tu confirmación.
6. Se envía **un trozo por turno** a OpenAI, con nombre de fichero aleatorio, en orden aleatorio y sin contexto.
7. Se recompone el texto en orden y se marcan los turnos dudosos. Las zonas cortadas quedan como `[REDACTADO]`.

Si algo falla (un trozo, la red, el modelo de voces), la app lo indica y recurre al texto local o al método rápido.

### Dos modelos de OpenAI, a elegir

| Uso | Modelo por defecto | Alternativas |
|---|---|---|
| Transcripción (audio sin nombres) | `gpt-4o-mini-transcribe` — 0,003 $/min, el más barato | `gpt-4o-transcribe`, `whisper-1` (0,006 $/min) |
| Análisis (texto anonimizado) | El que elijas en el botón «IA» | Selector propio |

Referencia de coste: una hora de audio cuesta como máximo unos 0,18 $ con el modelo más barato (menos, porque se cortan las zonas con datos personales). Comprueba las tarifas vigentes en OpenAI.

### Turnos dudosos

La app marca en ámbar los turnos con confianza baja del modelo, los que difieren mucho de la transcripción local, los que parecen repetirse o inventarse, los de ritmo de habla anómalo, los que contienen `[inaudible]`, los de voz poco clara y los que tienen una zona cortada. Al editar un turno deja de estar marcado. Hay un filtro «solo dudosos» y un botón «Siguiente dudoso».

---

## Qué sale de tu ordenador

| Sale | No sale |
|---|---|
| Trozos de audio de un turno cada uno, sin las zonas con datos personales detectados, hacia OpenAI | El audio completo |
| Texto **ya anonimizado**, hacia OpenAI, solo si usas el análisis con IA y tras tu confirmación | Los nombres reales y la clave de reidentificación |
| Peticiones de **descarga** de modelos a jsDelivr y Hugging Face (la primera vez) | La transcripción local |
| | La lista de términos protegidos |

La política de seguridad de la página (CSP) limita las conexiones a `api.openai.com`, `cdn.jsdelivr.net`, `huggingface.co`, `*.huggingface.co` y `*.hf.co`. Los modelos se descargan una vez (cientos de MB en total) y quedan en la caché del navegador.

Los estudios se guardan en IndexedDB del propio navegador. La clave de OpenAI se guarda en `localStorage`. Los audios no se guardan: hay que volver a vincularlos en cada sesión para escucharlos.

---

## Requisitos

- **Chrome o Edge de escritorio, actualizados.** WebGPU es muy recomendable; sin él, la transcripción local usa el procesador y es más lenta (usa entonces el modelo `tiny`).
- Una **clave de API de OpenAI** con saldo. Sin clave, la app funciona entera salvo la transcripción privada y la propuesta de códigos con IA.
- Conexión a internet la primera vez (descarga de modelos).

Alternativas sin clave: **«Solo Chrome»** (reconocimiento local de Chrome con `processLocally`; no envía nada, pero va al ritmo del audio y no separa voces) o importar una transcripción existente. Hay también un **modo sin IA** que bloquea cualquier envío.

---

## Uso rápido

1. Abre `index.html` (o la versión publicada) en Chrome o Edge.
2. Pulsa «IA», pega tu clave de OpenAI y elige los modelos.
3. Paso 1: rellena participantes y los nombres a proteger. **Cuantos más nombres reales incluyas, mejor se cortan.**
4. Paso 2: añade el audio y pulsa «Transcribir en privado». Revisa el resumen y confirma el envío.
5. Paso 3: asigna las voces y corrige empezando por los turnos en ámbar.
6. Pasos 4 a 7: anonimiza, analiza y exporta.

El **estudio de ejemplo** de la portada no necesita clave.

---

## Análisis con IA

Se trabaja solo con texto anonimizado y, antes de cada envío, la app muestra qué sale y vuelve a buscar datos personales. El selector de **exhaustividad** asigna todos los fragmentos a cada código en lotes pequeños. El nivel máximo es un **tope**, no una garantía: un código solo se subdivide si hay subtemas con evidencia suficiente. El botón ✦ profundiza a mano en cualquier código hoja, y el árbol muestra la cobertura (% de fragmentos con código).

---

## Limitaciones conocidas

- **La detección de datos personales no es infalible.** Revisa siempre el resultado. Si Whisper local no oye bien un nombre, ese trozo puede llegar a OpenAI; la app lo comprueba después, oculta cualquier nombre de tu lista que OpenAI devuelva y te avisa.
- **La separación de voces puede equivocarse**, sobre todo con voces del mismo sexo y tono parecido o con solapamientos. Por eso las voces se asignan a participantes con tu confirmación y se puede escuchar una muestra.
- **La voz es un dato personal** que puede considerarse biométrico. Consulta con tu comité de ética o delegado de protección de datos: OpenAI trata los datos fuera de la UE salvo acuerdo específico.
- Audios de más de una o dos horas pueden agotar la memoria del navegador: divídelos.
- Los trozos se envían en WAV (más pesado que mp3).
- No hay garantía de que los nombres de modelos alojados en Hugging Face sigan disponibles; si uno falla, la app prueba el siguiente y avisa.

---

## Estado de las pruebas

Probado con Playwright en Chromium: borrado de entrevistas, ids únicos, panel de voces, turnos dudosos, exportaciones (Word, informe, `.qdpx`), flujo de transcripción privada con audio sintético de dos voces y OpenAI simulado (sin fugas de zonas sensibles, orden y nombres de fichero aleatorios, cancelación sin envío, manejo de clave rechazada), carga del motor local bajo la política de seguridad, y árbol de códigos con respuestas simuladas.

**Pendiente de validar con audio real:** el rendimiento y la precisión de los modelos locales (Whisper, detector de nombres, WavLM) y la calidad de la separación de voces.

---

## Cómo citar

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23077431.svg)](https://doi.org/10.5281/zenodo.23077431)

> Borrás Rocher, F. y Lillo Navarro, M. C. (2026). *CualitativIA: investigación cualitativa privada* (v1.1.0) [Software]. Universidad Miguel Hernández de Elche. https://doi.org/10.5281/zenodo.23077431

El DOI de concepto apunta siempre a la última versión.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · María del Carmen Lillo Navarro [0000-0002-5074-8338](https://orcid.org/0000-0002-5074-8338)

## Licencia

MIT. Véase [LICENSE](LICENSE).
