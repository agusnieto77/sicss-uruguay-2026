# Taller: investigación histórica asistida por IA (en elaboración)

**Segmentación de documentos, reconocimiento de texto y exploración de fuentes con EntropIA Lite**

**Fechas:** viernes 30 de octubre, martes 3, miércoles 4 y jueves 5 de noviembre de 2026.  
**Modalidad:** cuatro encuentros presenciales, cada uno con un bloque conceptual por la mañana y un taller práctico por la tarde.  
**Destinatarios:** estudiantes, docentes e investigadores de historia, humanidades y ciencias sociales.  
**Docente:** Agustín Nieto.  
**Horarios:** 10-13 h | 14-16 h.  
**Sede:** UdelaR.

> Transformar una fuente histórica en datos procesables no es una operación neutral. La identificación de regiones de una página, su transcripción y su posterior consulta mediante modelos de IA implican decisiones sobre la unidad documental, la materialidad de las fuentes, su fidelidad y su interpretación.

## Presentación

El taller propone una introducción crítica y aplicada a herramientas de inteligencia artificial para trabajar con fuentes históricas digitalizadas, especialmente prensa de varias columnas. Combina la reflexión historiográfica sobre archivos, OCR y construcción de herramientas con ejercicios reproducibles en Google Colab y el trabajo integrado en **EntropIA Lite**.

La primera jornada examina el **layout**, es decir, la estructura espacial y editorial de las páginas. La segunda trabaja el **OCR**, sus distintos enfoques y sus errores. La tercera integra el procesamiento documental y la exploración de fuentes en EntropIA Lite. La cuarta introduce la **generación aumentada por recuperación (RAG)** y los **agentes**, entendidos como procedimientos que apoyan consultas y tareas sobre un corpus, sin sustituir la validación humana.

## Objetivos

### Objetivo general

Conocer, aplicar y evaluar críticamente procedimientos de segmentación, transcripción, organización, recuperación y análisis de fuentes históricas mediante herramientas abiertas y servicios de IA.

### Objetivos específicos

- Comprender cómo la estructura de una página influye en la identificación de artículos, titulares, imágenes, anuncios y orden de lectura.
- Utilizar modelos YOLO de análisis documental para detectar regiones, visualizarlas y exportarlas como recortes.
- Comparar OCR convencional, OCR estructurado y OCR multimodal, identificando errores que afectan las interpretaciones historiográficas.
- Construir y explorar un corpus acotado en EntropIA Lite, conservando su vínculo con los originales.
- Experimentar con búsquedas textuales y semánticas, RAG y tareas asistidas por agentes, verificando las respuestas contra las fuentes.
- Reflexionar sobre el desarrollo de aplicaciones para humanidades y ciencias sociales como práctica científica que incorpora decisiones metodológicas.

## Organización de los encuentros

| Fecha | Módulo | Mañana 10-13 h: conceptual | Tarde 14-16 h: práctica |
|---|---|---|---|
| **Vie. 30/10** | **1. Layout: estructura y organización de los documentos** | Materialidad de la prensa, jerarquías editoriales, unidades documentales y sesgos de segmentación. YOLO y análisis de layout. | Colab con DocLayout-YOLO: página con **cajas y etiquetas**; exportación de **segmentos recortados** y coordenadas. |
| **Mar. 03/11** | **2. OCR: reconocimiento de texto y control de errores** | OCR tradicional, reconocimiento estructurado y modelos multimodales. CER/WER, normalización, omisiones y alucinaciones. | Colabs con PP-StructureV3, PaddleOCR-VL y, si los recursos lo permiten, GLM-OCR: **layout nativo visualizado** y **texto extraído**. |
| **Mié. 04/11** | **3. Layout y OCR en EntropIA Lite: procesamiento, exploración y análisis de fuentes históricas** | Digitalización crítica, decisiones incorporadas al software, procedencia y trazabilidad. | Importar una muestra, crear colecciones, ejecutar el procesamiento disponible, inspeccionar o corregir resultados y explorar el corpus. |
| **Jue. 05/11** | **4. RAG y agentes en EntropIA Lite** | Búsqueda literal y semántica, recuperación por pasajes, respuestas fundamentadas, límites de los agentes y validación de evidencia. | Consultas sobre el corpus, comparación con documentos originales, registro de aciertos, omisiones y respuestas no fundamentadas; actividad integradora. |

**Nota:** Las demostraciones de la tercera y cuarta jornadas se ajustarán a las funcionalidades disponibles en la versión instalada de EntropIA Lite. Para utilizar las herramientas que requieran servicios remotos, será necesario contar con conexión a Internet y las correspondientes claves de API (*API keys*). **Quienes no dispongan de estas claves podrán utilizar las que serán facilitadas por el docente durante el taller**, de modo que todos los participantes puedan realizar las actividades prácticas previstas, sujetas a las cuotas y límites de uso de los proveedores.

## Desarrollo de las actividades

### Módulo 1. Layout: estructura y organización de los documentos

**Preguntas orientadoras:** ¿qué constituye una noticia o una unidad documental en una página? ¿Qué información se pierde al separar un artículo de su ubicación y relaciones visuales? ¿Cómo afectan los errores de detección a la construcción de un corpus?

**Conceptual:** prensa histórica como objeto material; columnas, avisos, ilustraciones, títulos y orden de lectura; segmentación automática y decisiones de clasificación; lectura crítica de resultados.

**Práctico en Google Colab:** cargar una imagen de prensa multicolumna; aplicar **DocLayout-YOLO**; revisar etiquetas, cajas y umbrales de confianza; guardar la página anotada (`regiones.png`), la carpeta `recortes/`, `regiones.csv` y `regiones.json`. Comparar los recortes con la página original e identificar cortes incorrectos o asociaciones perdidas.

**Producto:** una página anotada, una carpeta de recortes y una ficha breve de errores y decisiones de segmentación.

### Módulo 2. OCR: reconocimiento de texto y control de errores

**Preguntas orientadoras:** ¿cuándo una transcripción es suficientemente fiel? ¿Por qué una salida fluida puede ser incorrecta? ¿Qué sucede cuando el OCR confunde columnas, nombres, cifras o anuncios?

**Conceptual:** OCR basado en reconocimiento de caracteres y modelos especializados; pipelines de layout + OCR; OCR multimodal; fidelidad paleográfica y ortográfica; métricas CER/WER y control cualitativo; trazabilidad y preservación de versiones.

**Práctico en Google Colab:** ejecutar sobre la misma página **PP-StructureV3** y **PaddleOCR-VL**, con **GLM-OCR** como alternativa avanzada cuando el entorno permita ejecutar su pipeline completo. Inspeccionar **visualizaciones nativas del layout**, transcripciones y archivos estructurados. Comparar el orden de lectura y corregir manualmente un fragmento de referencia de 100 a 200 palabras.

**Producto:** visualizaciones del layout, transcripciones, una tabla de errores observados y una breve conclusión sobre la utilidad de cada enfoque para la investigación.

> La ruta de GLM-OCR que produce layout no debe confundirse con la ejecución aislada del reconocedor textual: requiere un pipeline de análisis de regiones, como el que integra PP-DocLayout.

### Módulo 3. Layout y OCR en EntropIA Lite

**Preguntas orientadoras:** ¿qué decisiones historiográficas se incorporan a una aplicación? ¿Cómo se documenta el pasaje del archivo al corpus? ¿Qué controles debe conservar el investigador?

**Conceptual:** aplicaciones como instrumentos científicos; *toolmaking* y crítica de herramientas; diseño centrado en prácticas de investigación; procedencia, revisión y sostenibilidad del software.

**Práctico:** instalar o abrir EntropIA Lite; crear una colección; importar documentos de muestra; realizar el procesamiento documental disponible; contrastar imágenes y texto; examinar la organización de documentos y metadatos; ensayar búsquedas y anotaciones. Registrar una decisión de diseño que facilite una tarea y otra que la dificulte.

**Producto:** colección funcional con documentos procesados y una ficha de crítica de la herramienta que distinga usabilidad de decisiones epistemológicas.

### Módulo 4. RAG y agentes en EntropIA Lite

**Preguntas orientadoras:** ¿qué diferencia hay entre hallar un documento y generar una respuesta sobre él? ¿Qué significa que una respuesta esté fundamentada? ¿Qué decisiones debe validar el investigador?

**Conceptual:** recuperación por palabras y por similitud; fragmentación del corpus; RAG; agentes y cadenas de tareas; citas, verificabilidad y límites del procesamiento automatizado.

**Práctico:** formular preguntas documentales concretas; comparar búsquedas literales y semánticas; utilizar las funciones de consulta o asistencia presentes en EntropIA Lite; comprobar la correspondencia entre afirmaciones generadas y pasajes originales; registrar casos de omisión, descontextualización e invención.

**Producto final integrador:** breve informe que documente una fuente original, su segmentación y transcripción, su incorporación a EntropIA y una consulta fundamentada sobre el corpus, junto con sus limitaciones.

## Requisitos técnicos y preparación previa

- **Computadora portátil** con permisos para instalar aplicaciones y espacio disponible para una muestra documental.
- **EntropIA Lite instalada antes de comenzar.** En **Windows**, se recomienda Microsoft Store. Para **macOS o Linux**, comprobar primero la disponibilidad de instaladores compatibles en los lanzamientos oficiales de GitHub. Consultar la [página de EntropIA en HLab](https://hlab.com.ar/herramientas/entropia-lite) y sus enlaces de descarga. **No se presupone compatibilidad universal de Lite con todos los sistemas.**
- **Conexión estable a Internet**, necesaria para Google Colab y las funciones remotas de EntropIA Lite.
- **Cuenta de Google (Gmail)** para acceder a [Google Colab](https://colab.research.google.com/). Se recomienda iniciar sesión y comprobar que puede crearse un notebook.
- **Navegador actualizado**, preferentemente Chrome o Firefox.
- **Revisión previa (informativa, no requiere contratación):** [AssemblyAI](https://www.assemblyai.com/docs/) (transcripción de audio), [OpenRouter](https://openrouter.ai/docs) (acceso a modelos), [Z.ai](https://docs.z.ai/) y [GLM-OCR](https://github.com/zai-org/GLM-OCR) (reconocimiento documental). La necesidad de cuenta, clave API o saldo se informará de acuerdo con los ejercicios efectivos.
- **GPU:** no es obligatorio contar con GPU propia para los notebooks. Colab puede ofrecer aceleradores sujetos a disponibilidad y restricciones. Los ejercicios avanzados podrán reemplazarse por resultados de muestra si no hay GPU compatible.

### Material documental

El docente facilitará una **muestra común de páginas de prensa histórica multicolumna** para asegurar comparabilidad entre ejercicios. Cada participante puede aportar **hasta 100 imágenes** de fuentes que utilice habitualmente en sus investigaciones. Para las prácticas guiadas bastará con un subconjunto pequeño (por ejemplo, 3 a 10 páginas).

**Formatos sugeridos:** JPG, PNG o PDF; imágenes legibles, preferentemente sin recortes que eliminen columnas o márgenes. Se recomienda conservar la imagen original, el nombre del archivo y, cuando sea posible, fecha, publicación, número, página, repositorio y procedencia. Evitar subir documentos sensibles o restringidos a servicios externos sin autorización.

**Descarga anticipada:** se compartirán la muestra docente y los notebooks de Colab para facilitar la preparación previa. Los archivos de los participantes deben mantenerse organizados por colección o procedencia.

## Notebooks y recursos prácticos

El paquete de ejercicios está en la carpeta [`cuadernos/`](cuadernos/README.md). Los cuatro notebooks se abren directamente en Google Colab, instalan lo que necesitan y trabajan sobre una misma página común de prensa multicolumna (*Centro Gallego*, Montevideo, 1917), con la opción de procesar también otras páginas de prensa, cartas, actas y un diario manuscrito de dominio público:

1. `01_DocLayout_YOLO_segmentacion.ipynb`: detección de layout, imagen anotada, recortes y tabla de regiones.
2. `02_PP_StructureV3_layout_OCR.ipynb`: layout, orden de lectura y OCR estructurado con visualizaciones y texto.
3. `03_PaddleOCR_VL_layout_OCR.ipynb`: reconocimiento multimodal con salida visual y textual.
4. `04_GLM_OCR_pipeline.ipynb`: pipeline completo de GLM-OCR (layout PP-DocLayoutV3 y reconocimiento GLM-OCR servido con Ollama).

Los cuatro se probaron en Google Colab con GPU T4. Aun así son materiales experimentales: los resultados varían según la página, y la instalación de los cuadernos 02 y 03 tarda alrededor de nueve minutos, por lo que conviene ejecutarla antes de cada jornada.

## Modalidad de trabajo y evaluación formativa

Cada jornada alterna exposición breve, discusión bibliográfica, demostración y experimentación en grupos o de manera individual. No se presupone experiencia previa en programación. El trabajo se centrará en **comparar resultados y justificar decisiones**, no solamente en conseguir que los modelos se ejecuten.

La evaluación formativa se basará en los cuatro productos de taller y en el informe integrador. Se valorará la identificación de errores, la conservación del vínculo con el documento original, la claridad de los criterios y la capacidad de explicar los límites de los resultados.

## Bibliografía por módulos

La lista combina textos de reflexión historiográfica, estudios aplicados y literatura sobre herramientas. Cada bloque corresponde a un módulo del taller y distingue **lecturas sugeridas**, que orientan la discusión de cada jornada, de **lecturas ampliatorias**, para profundizar. Las sugeridas no son obligatorias. 

Las copias de lectura de estos textos se encuentran en la carpeta [`bibliografia/`](bibliografia/README.md), organizada con la misma estructura.

### A. Layout, materialidad y segmentación (Módulo 1)

**Lecturas sugeridas**

- Prescott, A., y Hughes, L. (2018). [*Why Do We Digitize? The Case for Slow Digitization*](bibliografia/A/sugerida/Prescott-Hughes_2018_Why-Do-We-Digitize.pdf). *Archive Journal*.
- Lee, B. C. G., Mears, J., Jakeway, E., Ferriter, M., Adams, C., Yarasavage, N., Thomas, D., Zwaard, K., y Weld, D. S. (2020). [*The Newspaper Navigator Dataset: Extracting and Analyzing Visual Content from 16 Million Historic Newspaper Pages in Chronicling America*](bibliografia/A/sugerida/Lee-et-al_2020_Newspaper-Navigator.pdf). En *Proceedings of the 29th ACM International Conference on Information & Knowledge Management (CIKM '20)* (pp. 3055–3062). ACM.
- Dell, M., Carlson, J., Bryan, T., Silcock, E., Arora, A., Shen, Z., D'Amico-Wong, L., Le, Q., Querubin, P., y Heldring, L. (2023). [*American Stories: A Large-Scale Structured Text Dataset of Historical U.S. Newspapers*](bibliografia/A/sugerida/Dell-et-al_2023_American-Stories.pdf). En *Advances in Neural Information Processing Systems 36* (pp. 80744–80772).
- Macicior-Mitxelena, J., y Garcia-Serrano, A. (2026). [*Data Matters: Looking for High-Quality Corpora to Build Robust and Reliable Models for Humanists*](bibliografia/A/sugerida/Macicior-Garcia_2026_Data-Matters.pdf). En *Proceedings of the First Workshop on Creating Interoperable Corpora of Historical Newspapers (PressMint 2026)* (pp. 82–91). ACL.

**Lecturas ampliatorias**

- Silva dos Santos Júnior, E., Paixão, T., y Alvarez, A. B. (2025). [*Comparative Performance of YOLOv8, YOLOv9, YOLOv10, and YOLOv11 for Layout Analysis of Historical Documents Images*](bibliografia/A/ampliatoria/SilvaDosSantos-et-al_2025_YOLO-Layout-Historical.pdf). *Applied Sciences, 15*(6), 3164.
- Beyene, F. S., y Dancy, C. L. (2025). [*Layout-Aware OCR in Black Digital Archives: An Unsupervised Evaluation Approach*](bibliografia/A/ampliatoria/Beyene-Dancy_2025_Layout-Aware-OCR-Black-Archives.pdf). Preprint, arXiv.
- Prescott, A. (2018). [*Searching for Dr. Johnson: The Digitisation of the Burney Newspaper Collection*](bibliografia/A/ampliatoria/Prescott_2018_Searching-for-Dr-Johnson.pdf). En S. G. Brandtzæg, P. Goring y C. Watson (Eds.), *Travelling Chronicles: News and Newspapers from the Early Modern Period to the Eighteenth Century* (pp. 51–71). Brill.
- Prescott, A. (2019). [*Slow Digitisation and the Battle of the Books*](bibliografia/A/ampliatoria/Prescott_2019_Slow-Digitisation-Battle-of-Books.pdf). En C. E. Karkov (Ed.), *Slow Scholarship: Medieval Research and the Neoliberal University* (pp. 143–162). D. S. Brewer.
- Hitchcock, T. (2013). [*Confronting the Digital: Or How Academic History Writing Lost the Plot*](bibliografia/A/ampliatoria/Hitchcock_2013_Confronting-the-Digital.pdf). *Cultural and Social History, 10*(1), 9–23.

### B. OCR, errores y crítica de fuentes digitalizadas (Módulo 2)

**Lecturas sugeridas**

- Milligan, I. (2013). [*Illusionary Order: Online Databases, Optical Character Recognition, and Canadian History, 1997–2010*](bibliografia/B/sugerida/Milligan_2013_Illusionary-Order.pdf). *Canadian Historical Review, 94*(4), 540–569.
- Putnam, L. (2016). [*The Transnational and the Text-Searchable: Digitized Sources and the Shadows They Cast*](bibliografia/B/sugerida/Putnam_2016_Transnational-and-Text-Searchable.pdf). *The American Historical Review, 121*(2), 377–402.
- Cordell, R. (2017). [*“Q i-jtb the Raven”: Taking Dirty OCR Seriously*](bibliografia/B/sugerida/Cordell_2017_Taking-Dirty-OCR-Seriously.pdf). *Book History, 20*, 188–225.
- Strange, C., McNamara, D., Wodak, J., y Wood, I. (2014). [*Mining for the Meanings of a Murder: The Impact of OCR Quality on the Use of Digitized Historical Newspapers*](bibliografia/B/sugerida/Strange-et-al_2014_Mining-Meanings-of-a-Murder.pdf). *Digital Humanities Quarterly, 8*(1).
- Beelen, K., Lawrence, J., Wilson, D. C. S., y Beavan, D. (2023). [*Bias and Representativeness in Digitized Newspaper Collections: Introducing the Environmental Scan*](bibliografia/B/sugerida/Beelen-et-al_2023_Bias-Representativeness-Newspapers.pdf). *Digital Scholarship in the Humanities, 38*(1), 1–22.

**Lecturas ampliatorias**

- Levchenko, M. (2025). [*Evaluating LLMs for Historical Document OCR: A Methodological Framework for Digital Humanities*](bibliografia/B/ampliatoria/Levchenko_2025_Evaluating-LLMs-Historical-OCR.pdf). Preprint, arXiv.
- Vesalainen, A., Mäkelä, E., Ruotsalainen, L., y Tolonen, M. (2026). [*Error Patterns in Historical OCR: A Comparative Analysis of TrOCR and a Vision–Language Model*](bibliografia/B/ampliatoria/Vesalainen-et-al_2026_Error-Patterns-Historical-OCR.pdf). Preprint, arXiv.
- Cordell, R. (2019). [*Why You (A Humanist) Should Care About Optical Character Recognition*](bibliografia/B/ampliatoria/Cordell_2019_Why-Humanist-Should-Care-OCR.pdf). Blog académico.
- Burchardt, J. (2023). [*Are Searches in OCR-generated Archives Trustworthy?*](bibliografia/B/ampliatoria/Burchardt_2023_OCR-Archives-Trustworthy.pdf). *Jahrbuch für Wirtschaftsgeschichte, 64*(1), 31–54.
- Milligan, I. (2022). [*The Transformation of Historical Research in the Digital Age*](bibliografia/B/ampliatoria/Milligan_2022_Transformation-Historical-Research.pdf). Cambridge University Press (Elements in Historical Theory and Practice).
- Miller, C., y Banerjee, B. (2025). [*Optical Character Recognition for Pre-Digital Historical Documents using Large Language Models*](bibliografia/B/ampliatoria/Miller-Banerjee_2025_OCR-Pre-Digital-LLMs.pdf). Manuscrito aceptado, depositado en VTechWorks (Virginia Tech).
- Boros, E., y colaboradores (2026). [*Can LLMs Correct Historical OCR Without Rewriting History?*](bibliografia/B/ampliatoria/Boros_2026_LLMs-Correct-Historical-OCR.pdf). Blog académico.
- Sanz Cabrerizo, A. (2018). [*Prensa digitalizada: herramientas y métodos digitales para una investigación a escala*](bibliografia/B/ampliatoria/SanzCabrerizo_2018_Prensa-Digitalizada.pdf). *Revista de Humanidades Digitales, 2*, 1–14.
- Comesaña, D., y Vilches-Blázquez, L. M. (2019). [*Un estudio de la prensa latinoamericana entre los siglos XIX y XX con un enfoque en eventos meteorológicos*](bibliografia/B/ampliatoria/Comesana-VilchesBlazquez_2019_Prensa-Latinoamericana-Eventos-Meteorologicos.pdf). *Revista de Historia de América, 156*, 29–59.
- Oberbichler, S., y Pfanzelter, E. (2022). [*Tracing Discourses in Digital Newspaper Collections: A Contribution to Digital Hermeneutics while Investigating ‘Return Migration’ in Historical Press Coverage*](bibliografia/B/ampliatoria/Oberbichler-Pfanzelter_2022_Tracing-Discourses-Digital-Newspapers.pdf). En E. Bunout, M. Ehrmann y F. Clavert (Eds.), *Digitised Newspapers – A New Eldorado for Historians?* (pp. 125–152). De Gruyter.

### C. EntropIA Lite, desarrollo y crítica de herramientas (Módulo 3)

**Lecturas sugeridas**

- Jacomy, M., Rieder, B., Borra, E., Plique, G., Enevoldsen, K. C., y van Eck, N. J. (2026). *Toolmaking is science by other means*. En A. K. Madsen y A. K. Munk (Eds.), *Handbook of Digital and Computational Research Methods* (pp. 294–306). Edward Elgar. Se trabaja con la Parte III completa (introducción y capítulos 20–25): [traducción docente no oficial](bibliografia/C/sugerida/Jacomy-et-al_2026_Handbook-Parte-III_ES.pdf) y [original en inglés](bibliografia/C/sugerida/Jacomy-et-al_2026_Handbook-Parte-III_EN.pdf).
- Rieder, B., Peeters, S., y Borra, E. (2024). [*From Tool to Tool-Making: Reflections on Authorship in Social Media Research Software*](bibliografia/C/sugerida/Rieder-Peeters-Borra_2024_From-Tool-to-Tool-Making.pdf). *Convergence, 30*(1), 216–235.
- Ramsay, S., y Rockwell, G. (2012). [*Developing Things: Notes toward an Epistemology of Building in the Digital Humanities*](bibliografia/C/sugerida/Ramsay-Rockwell_2012_Developing-Things.pdf). En M. K. Gold (Ed.), *Debates in the Digital Humanities*. University of Minnesota Press.
- Van Es, K. (2023). [*Unpacking Tool Criticism as Practice, in Practice*](bibliografia/C/sugerida/VanEs_2023_Unpacking-Tool-Criticism.pdf). *Digital Humanities Quarterly, 17*(2).
- Rockwell, G., y Sinclair, S. (2016). *Hermeneutica: Computer-Assisted Interpretation in the Humanities*. MIT Press. Capítulos 2 ([«The Measured Words: How Computers Analyze Texts»](bibliografia/C/sugerida/Rockwell-Sinclair_2016_Hermeneutica-cap2-Measured-Words.pdf), pp. 25–43) y 7 ([«False Positives: Opportunities and Dangers in Big-Data Text Analysis»](bibliografia/C/sugerida/Rockwell-Sinclair_2016_Hermeneutica-cap7-False-Positives.pdf), pp. 113–136).

**Lecturas ampliatorias**

- Chao, J., van Geenen, D., Gerlitz, C., y van der Vlist, F. N. (2024). [*Digital Methods for Sensory Media Research: Toolmaking as a Critical Technical Practice*](bibliografia/C/ampliatoria/Chao-et-al_2024_Digital-Methods-Sensory-Media.pdf). *Convergence, 30*(1), 236–263.
- Koolen, M., van Gorp, J., y van Ossenbruggen, J. (2019). [*Toward a Model for Digital Tool Criticism: Reflection as Integrative Practice*](bibliografia/C/ampliatoria/Koolen-et-al_2019_Digital-Tool-Criticism.pdf). *Digital Scholarship in the Humanities, 34*(2), 368–385.
- Given, L. M., y Willson, R. (2018). [*Information Technology and the Humanities Scholar: Documenting Digital Research Practices*](bibliografia/C/ampliatoria/Given-Willson_2018_IT-and-Humanities-Scholar.pdf). *Journal of the Association for Information Science and Technology, 69*(6), 807–819.
- Galina Russell, I. (Coord.). (2022). [*Pautas para el desarrollo y la evaluación de proyectos digitales en las humanidades*](bibliografia/C/ampliatoria/Galina-et-al_2022_Pautas-Proyectos-Digitales.pdf). UNAM, Instituto de Investigaciones Bibliográficas (Instrumenta Bibliographica, 3).
- Del Rio Riande, G., y Ferreyra, D. (2016). [*Definir, clasificar, apoderarse de las herramientas para empoderar a las Humanidades Digitales: TaDIRAH y DIRT en español*](bibliografia/C/ampliatoria/DelRioRiande-Ferreyra_2016_TaDIRAH-DIRT.pdf) [presentación]. Repositorio SEDICI, UNLP.
- Toscano, M., Cobo, M. J., y Herrera-Viedma, E. (2022). [*Software Solutions for Web Information Systems in Digital Humanities: Review, Analysis and Comparative Study*](bibliografia/C/ampliatoria/Toscano-Cobo-HerreraViedma_2022_Software-Web-DH.pdf). *Profesional de la Información, 31*(2), e310211.
- Prescott, A. (2025). [*‘The Past Went That-a-Way’: Editing in the Rearview Mirror?*](bibliografia/C/ampliatoria/Prescott_2025_Past-Went-That-a-Way.pdf). En *Digital Editing and Publishing in the Twenty-First Century*.
- Abate, A., y Bocchi, L. (2024). [*Herramientas digitales para la edición del teatro aurisecular: el informe de una tentativa a partir de EVT (Edition Visualization Technology)*](bibliografia/C/ampliatoria/Abate-Bocchi_2024_Edicion-Teatro-Aurisecular-EVT.pdf). *Revista de Humanidades Digitales, 9*, 114–131.

### D. RAG, agentes y consulta asistida (Módulo 4)

**Lecturas sugeridas**

- Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W., Rocktäschel, T., Riedel, S., y Kiela, D. (2020). [*Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*](bibliografia/D/sugerida/Lewis-et-al_2020_Retrieval-Augmented-Generation.pdf). En *Advances in Neural Information Processing Systems 33* (pp. 9459–9474).
- Shah, C., y Bender, E. M. (2022). [*Situating Search*](bibliografia/D/sugerida/Shah-Bender_2022_Situating-Search.pdf). En *Proceedings of the 2022 Conference on Human Information Interaction and Retrieval (CHIIR '22)* (pp. 221–232). ACM.
- Murugaraj, K., Lamsiyah, S., During, M., y Theobald, M. (2025). [*Topic-RAG for Historical Newspapers: Enhancing Information Retrieval in Humanities Research through Topic-Based Retrieval-Augmented Generation*](bibliografia/D/sugerida/Murugaraj-et-al_2025_Topic-RAG-Historical-Newspapers.pdf). *Computational Humanities Research, 1*, e15.
- Liu, N. F., Zhang, T., y Liang, P. (2023). [*Evaluating Verifiability in Generative Search Engines*](bibliografia/D/sugerida/Liu-Zhang-Liang_2023_Verifiability-Generative-Search.pdf). En *Findings of the Association for Computational Linguistics: EMNLP 2023* (pp. 7001–7025). ACL.

**Lecturas ampliatorias**

- Tran, T. T., González-Gallardo, C.-E., y Doucet, A. (2024). [*Retrieval Augmented Generation for Historical Newspapers*](bibliografia/D/ampliatoria/Tran-et-al_2024_RAG-Historical-Newspapers.pdf). En *Proceedings of the 24th ACM/IEEE Joint Conference on Digital Libraries (JCDL '24)*. ACM.
- Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., y Cao, Y. (2023). [*ReAct: Synergizing Reasoning and Acting in Language Models*](bibliografia/D/ampliatoria/Yao-et-al_2023_ReAct.pdf). En *International Conference on Learning Representations (ICLR 2023)*.

## Orientaciones para el trabajo con fuentes y modelos

1. **Conservar el original:** ningún recorte, transcripción o respuesta automatizada reemplaza la imagen histórica de referencia.
2. **Hacer visibles las mediaciones:** registrar herramienta, versión, configuración, modelo y fecha de procesamiento.
3. **Revisar el orden de lectura:** una transcripción correcta de cada bloque puede resultar históricamente equívoca si se ensamblan mal las columnas.
4. **Diferenciar legibilidad y fidelidad:** la corrección lingüística de un texto generado no garantiza su correspondencia con la fuente.
5. **Fundamentar las respuestas:** contrastar afirmaciones, nombres, fechas y citas con los pasajes originales.
6. **Reconocer los alcances y límites del diseño:** las herramientas facilitan ciertas operaciones analíticas y dificultan otras, por lo que también deben convertirse en objeto de crítica.

## Resultado esperado

Al finalizar, cada participante habrá experimentado el pasaje **imagen original → regiones de layout → transcripción OCR → colección documental → consulta y análisis asistidos**, con registros de los errores, decisiones y límites de cada etapa. La meta no es automatizar la interpretación histórica, sino ampliar las posibilidades de investigación sin renunciar a la crítica de fuentes.

---

**Enlaces generales:** [EntropIA Lite / HLab](https://hlab.com.ar/herramientas/entropia-lite) · [Google Colab](https://colab.research.google.com/) · [DocLayout-YOLO](https://github.com/opendatalab/DocLayout-YOLO) · [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) · [GLM-OCR](https://github.com/zai-org/GLM-OCR).
