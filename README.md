# CualitativIA

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23077431.svg)](https://doi.org/10.5281/zenodo.23077431)

**Aplicación:** https://fborrasumh.github.io/cualitativia/

Investigación cualitativa con **datos sensibles**: entrevistas y grupos focales que se transcriben **en tu ordenador**, se anonimizan antes de cualquier IA y se analizan con árboles de códigos a varios niveles y desde varias interpretaciones, con citas literales verificadas. Exporta a MAXQDA (REFI-QDA). Aplicación de un solo fichero (`index.html`), sin servidor, con el diseño de la familia Forja.

## Privacidad por diseño

| Siempre en tu ordenador | Solo si lo pides, y anonimizado |
|---|---|
| Audio y vídeo, y su transcripción (reconocimiento de voz local de Chrome con `processLocally = true`) | Propuesta de árboles de códigos con OpenAI, enviando solo el texto anonimizado y los objetivos |
| Nombres reales y clave de reidentificación | Antes de cada análisis: vista previa exacta de lo que sale, nueva búsqueda de datos personales y confirmación expresa |
| Anonimización, métodos mixtos y exportaciones | «Modo sin IA» para bloquear cualquier envío |

- **Política de seguridad (CSP):** la página solo puede conectar con `api.openai.com` (y cargar librerías de cdnjs). Cualquier otra conexión la bloquea el navegador.
- **Reconocimiento solo local:** si el paquete del idioma no está instalado en el equipo, la app no transcribe en la nube; ofrece descargar el paquete cuando Chrome lo tiene disponible.

## Recorrido

1. **Estudio**: objetivos y participantes con código (P1, P2…). Nombres y atributos solo en local.
2. **Transcribir**: audio o vídeo con el reconocimiento local de Chrome, en el idioma y la variante de cada fichero (es-ES, es-AR, en, ca, gl…). También importa transcripciones existentes (texto, Word, VTT o SRT, incluidas las de MAXQDA).
3. **Quién habla**: turnos por pausas; la investigadora asigna cada turno, escuchando el fragmento. Etiquetas rápidas ([llora], [se solapan]…), y turnos que se unen o se dividen.
4. **Anonimizar**: detección local de nombres, lugares, centros, fechas, contactos y documentos de identidad; sustitución por códigos; vista previa lado a lado.
5. **Analizar**: árboles de códigos con **profundidad desigual**. Cada rama se subdivide solo mientras haya subtemas con evidencia propia y se indica por qué se detiene. Hay **varias interpretaciones**: temática (Braun y Clarke), relacional (condiciones, estrategias y consecuencias, con relaciones entre códigos) y desde un marco teórico. Las citas se **verifican literalmente** contra su segmento; las que no aparecen se descartan.
6. **Métodos mixtos**: matrices de códigos × participantes y × atributo, calculadas en local y exportables a SPSS o R.
7. **Exportar**: libro de códigos (`.qdc`) y proyecto (`.qdpx`) REFI-QDA para MAXQDA, ATLAS.ti o NVivo; transcripciones con marcas de tiempo `#hh:mm:ss-0#`; informe en Word con citas; copia completa y clave de reidentificación por separado.

## Límites

- La transcripción va al ritmo de la grabación (una hora de audio tarda una hora) y requiere Chrome de escritorio actualizado.
- El reconocimiento de voz no distingue hablantes: la asignación en grupos focales es manual.
- Los idiomas disponibles dependen de los paquetes locales de Chrome en cada equipo.
- La detección de datos personales no es infalible: revisa siempre la vista previa.
- OpenAI trata los datos fuera de la UE salvo acuerdo específico. Consulta con el comité de ética antes de usar el análisis automático, aunque el texto vaya anonimizado.
- El análisis lo hace la investigadora: la IA propone árboles alternativos como apoyo.

Desarrollada a partir de las necesidades de investigación cualitativa con familias de personas con discapacidad planteadas por M.ª Carmen Lillo Navarro (UMH).

## Cómo citar

Borrás Rocher, F. (2026). *CualitativIA* (versión 1.0.0) [Software]. Universidad Miguel Hernández de Elche. https://doi.org/10.5281/zenodo.23077431

El DOI es el de concepto: apunta siempre a la última versión. GitHub ofrece la cita en APA y BibTeX con el botón *Cite this repository*, a partir de `CITATION.cff`.

Forma parte del catálogo [Herramientas IA para la academia](https://fborrasumh.github.io/ia/).

## Licencia

MIT © 2026 Fernando Borrás Rocher · Universidad Miguel Hernández de Elche.
