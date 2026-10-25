# Evaluación previa al taller

Pruebas realizadas el 24 de octubre de 2026 sobre las once imágenes de [`imagenes/`](imagenes/), antes de la revisión humana final. Las transcripciones citadas son salidas reales de los modelos; las lecturas correctas entre corchetes son las del documento.

## 1. Funcionamiento

| Cuaderno | Google Colab (T4, Python 3.13) | Otras pruebas |
| --- | --- | --- |
| 01 DocLayout-YOLO | ✅ completo | ✅ CPU (11 imágenes, 74 s) y RTX 5090 (11 imágenes, 37 s) |
| 02 PP-StructureV3 | ✅ completo (instalación ~9 min, página ~2 min) | ✅ CPU (11 imágenes, 140 s) |
| 03 PaddleOCR-VL | ✅ completo, página común y manuscritos (instalación 5 a 16 min según la sesión, página ~1 min) | ❌ RTX 5090 compartida: sin memoria libre; CPU: más de 10 min por página |
| 04 GLM-OCR | ✅ completo (2 min 40 s en total) | ✅ CPU + Ollama (11 imágenes, 44 min) |

### Problemas encontrados y corregidos

- **Versión de PaddlePaddle.** `paddlepaddle` 3.3.1 falla en CPU con PP-StructureV3 (`ConvertPirAttribute2RuntimeAttribute not support`). Se fijó la 3.2.1.
- **Choque de bibliotecas en Colab (02 y 03).** `paddlepaddle-gpu` instala la biblioteca NCCL de CUDA 12 por encima de la de CUDA 13 que usa el PyTorch de Colab; PaddleOCR importa PyTorch y la celda que prepara el pipeline fallaba. La celda de instalación restituye ahora la versión de NCCL que pide PyTorch.
- **Idioma del reconocedor (02).** Sin `lang="es"`, PP-StructureV3 usa un reconocedor entrenado sobre todo con chino e inglés. Con `lang="es"` se usa el reconocedor latino de PP-OCRv5, que conserva tildes y eñes.
- **Configuración de GLM-OCR (04).** El borrador escribía una configuración con solo los datos del servidor; el SDK no completa los valores faltantes y fallaba al iniciar. El cuaderno parte ahora de la configuración que trae el SDK. Además, el borrador dibujaba las cajas con coordenadas normalizadas (0 a 1000) como si fueran píxeles; ahora se reescalan al tamaño de la página.
- **Servidor del modelo (04).** Se reemplazó vLLM por Ollama, que se instala en segundos en Colab y funciona en T4. El cuaderno precarga el modelo, porque la primera carga superaba el tiempo de espera del SDK.
- **Páginas sin resultado (04).** Cuando el SDK no puede procesar una página (por ejemplo, por falta de memoria de GPU), la saltea sin error. El cuaderno avisa ahora qué página no produjo regiones, y las tablas vacías ya no rompen las celdas siguientes.

### Advertencias para la clase

- Conviene ejecutar la celda de instalación de 02 y 03 **antes** de la explicación: tarda alrededor de nueve minutos.
- Colab limita la cantidad de sesiones simultáneas por cuenta. Al pasar de un cuaderno a otro, cerrar la sesión anterior (*Entorno de ejecución → Desconectarse y eliminar entorno de ejecución*).
- PaddleOCR-VL necesita GPU en la práctica. En CPU tarda más de diez minutos por página de prensa.

## 2. Página común (*Centro Gallego*, Montevideo, 1917)

### Segmentación (01)

DocLayout-YOLO detecta 70 regiones: 58 de texto, 6 figuras, 2 títulos y 4 descartables (`abandon`). Lo descartado es el número de página («6»), la cabecera «CENTRO GALLEGO» y un sello en la esquina inferior, detectado dos veces. El modelo trata como prescindible justamente la información que identifica la publicación. Las regiones se numeran de arriba hacia abajo sin respetar columnas: el modelo no sabe en qué orden se lee la página.

### Orden de lectura y transcripción (02 y 04)

PP-StructureV3 reconstruye bien el recorrido de las cuatro columnas (columna 1 completa, luego 2, 3 y 4) y conserva la cabecera y el número de página. GLM-OCR los descarta por defecto (`header`, `number`) y presenta inversiones locales: bloques consecutivos de la misma columna aparecen en orden cambiado.

| Pasaje | PP-StructureV3 (02) | GLM-OCR (04) |
| --- | --- | --- |
| [El vapor "Barceló"] | El vapor "Barcelo'trajo | El vapor "Barceló" trajo |
| [el alcalde] | el alealde | el alcalde |
| [el nuevo alcalde don Carlos Puga Pequeño] | el muevo alcalde don Carios Puga Pequeño | el nuevo alcalde don Carios Puga Pequeño |
| [Galicia] | Galitia | Galicia |
| [embarcaciones] | embarcaciones | embarcações (portugués) |
| [la colonia escolar] | la colonia cscoiar | la colonia escocar |
| Sello de la esquina inferior | (sin texto) | RSAL ACADEMIA GATIEBA INTERNATIONAL EXPURGAR INDONESIA |

GLM-OCR produce un texto más limpio, y por eso sus errores son más difíciles de ver: cambia una palabra española por su forma portuguesa, inventa el texto de un sello ilegible y **duplica** la frase «Madrid cotizose en la capitai de España a los siguientes precios», que aparece en dos bloques seguidos. PP-StructureV3 comete más errores de caracteres, pero son visibles.

## 3. Manuscritos

DocLayout-YOLO no detecta texto en ningún manuscrito: cada página completa se clasifica como una única `figure`. Los modelos de OCR, en cambio, sí producen texto, con resultados muy dispares:

| Documento | PP-StructureV3 (02) | GLM-OCR (04) |
| --- | --- | --- |
| Acta de Baradero, 1857 [En veinte y dos de Octubre de mil ochocientos cincuenta y siete] | En veinle y das de Detubre de mul oshocienlos ceomonta y vile | En veinte y das de Octubre de mul oshociendas comentanta y pide; inserta letras cirílicas («loно'») |
| Carta de Díez Colunje, 1905 | «Sr. Dn guje iagni Mey estizado aiga.» Texto poco legible | «Sr. Du gerje Iragerri Muy estimado arrigo.» Estructura de carta reconocible |
| Carta de Cullen, 1823 | 565 caracteres sin sentido («CANGS 2osn AA *4A (23)Junise l Hhanyge…») | Solo «Senior Juan Co Solano Antuña / bueno Sep 1823»: **omite el resto de la carta sin aviso** |
| Diario de Olivares, 1745 | 101 caracteres sin sentido | Solo «1745» |
| Acta de Medellín, 1814 | Fragmentos sueltos («mpue l E. or ensi Jeme…») | Texto fluido con errores de sentido («Mpuesto el Emir. Sor. Presidene…») |

Ningún modelo es utilizable para transcribir manuscritos coloniales sin revisión completa. El riesgo más serio no es el texto ilegible, que se detecta enseguida, sino el texto **plausible e incompleto**: GLM-OCR devuelve encabezados correctos y descarta el cuerpo de la carta, y una lectura rápida puede tomarlo por una transcripción.

## 4. PaddleOCR-VL (03)

Se probó en Colab con la página común y con los cinco manuscritos. Es, con diferencia, el que mejor lee la escritura manuscrita, aunque sigue lejos de una transcripción utilizable sin revisión:

| Documento | PaddleOCR-VL (03) |
| --- | --- |
| Diario de Olivares, 1745 [Diario del viage que yo D. Joachin de Olivares y Centeno, Comandante de la Fragata de S. M. nombrada S. Antonio…] | «Dianio del viage, que To D. Toachin de Olivano, y Centeno Comandante de la Fragata de SM nombraba T. Antonio, he hecho desde el Rio de la La…». Recupera el sentido del encabezamiento, donde 02 devolvió caracteres sin sentido y 04 solo «1745» |
| Acta de Baradero, 1857 | «En weinte y das de Octubre de mul oshocienos cermenta y gite»: la fecha sigue sin poder leerse, y los nombres de los concejales quedan desfigurados («D. Fallip Syrrh») |
| Carta de Cullen, 1823 | Transcribe la carta completa (987 caracteres), pero con frases sin sentido («Guaide Haug. Anlenoch Llygu. or etc. conduct») |
| Carta de Díez Colunje, 1905 | Estructura y vocabulario reconocibles («Muy estimado amigo»), con nombres propios alterados («Beabiz O'Donnell de Pombo») y caracteres de reemplazo (`�`) |
| Acta de Medellín, 1814 | Sustituye palabras por otras existentes que cambian el sentido: «Representante» se lee «Represión» |

El riesgo característico de este modelo es la **sustitución por palabras verosímiles**: produce palabras españolas reales («Represión») donde el documento dice otra cosa. Es más difícil de detectar que el texto ilegible de 02.

La prueba en la RTX 5090 no pudo hacerse: otro usuario ocupaba 26 de sus 32 GB con un servicio propio, y PaddleOCR-VL no entró en la memoria restante.

## 5. Preguntas que estos resultados permiten discutir

1. ¿Qué información descarta cada herramienta por considerarla «encabezado» o «pie»? ¿Quién decidió que no era contenido?
2. ¿Es más peligroso un OCR con muchos errores visibles o uno fluido que modifica, inventa u omite sin aviso?
3. Una misma palabra mal leída de dos maneras distintas (*Carios*, *escocar*, *cscoiar*): ¿cómo afecta la búsqueda de nombres propios en un corpus?
4. ¿Qué controles mínimos habría que aplicar antes de incorporar una transcripción automática a un corpus de investigación?
