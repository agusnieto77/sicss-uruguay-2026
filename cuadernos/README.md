# Cuadernos del taller: layout y OCR

Diez cuadernos para los dos primeros días del taller. Los seis primeros trabajan sobre la **misma página común** (*Centro Gallego*, Montevideo, 1917: cuatro columnas, titulares, escudos y un aviso con grabado), para poder comparar qué hace cada herramienta con la misma fuente. Los cuadernos 05 y 06 reconstruyen dos métodos recientes para prensa histórica, cuyos modelos entrenados no están publicados: usan modelos genéricos en su lugar.

**Pregunta que organiza la actividad:** ¿en qué medida las decisiones automatizadas de segmentación y transcripción modifican la fuente histórica sobre la cual construimos nuestras interpretaciones?

| Cuaderno | Qué hace | Abrir |
| --- | --- | --- |
| `01_DocLayout_YOLO_segmentacion.ipynb` | Detecta regiones (títulos, texto, figuras) y exporta un recorte por región | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/01_DocLayout_YOLO_segmentacion.ipynb) |
| `02_PP_StructureV3_layout_OCR.ipynb` | Layout, orden de lectura y OCR con PP-StructureV3 (reconocedor latino, `lang="es"`) | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/02_PP_StructureV3_layout_OCR.ipynb) |
| `03_PaddleOCR_VL_layout_OCR.ipynb` | Layout y reconocimiento con un modelo de visión y lenguaje (PaddleOCR-VL 1.6) | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/03_PaddleOCR_VL_layout_OCR.ipynb) |
| `04_GLM_OCR_pipeline.ipynb` | Pipeline completo de GLM-OCR: layout PP-DocLayoutV3 y reconocimiento GLM-OCR servido con Ollama | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/04_GLM_OCR_pipeline.ipynb) |
| `05_Pipeline_modular_articulos.ipynb` | Pipeline modular para reconstruir **artículos**: bloques (DocLayout-YOLO), filetes (LSD), orden de lectura (LayoutReader) y agrupación por títulos. Reconstrucción de [Mocaër et al. (2026)](https://arxiv.org/html/2607.15082v1) | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/05_Pipeline_modular_articulos.ipynb) |
| `06_Orden_lectura_LLM.ipynb` | Orden de lectura guiado por el sentido del texto: bloques, OCR (Tesseract o PP-OCRv5) y un modelo de lenguaje (Ministral-3 8B en Ollama o Gemini 3.5 Flash-Lite) que decide qué bloque sigue a cuál. Reconstrucción de [Vidal-Gorène et al. (2026)](https://arxiv.org/html/2607.00596v1) | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/06_Orden_lectura_LLM.ipynb) |
| `07_OCR_imprenta.ipynb` | Transcribe cinco páginas impresas a una columna (siglo XIX) con dos OCR clásicos (docTR y Tesseract) y tres modelos de visión y lenguaje (Churro-3B, Qwen3-VL-8B en 4 bits y LightOnOCR-3-4B), y mide CER y WER contra la transcripción humana | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/07_OCR_imprenta.ipynb) |
| `08_OCR_mecanografiado.ipynb` | Lo mismo con cinco párrafos mecanografiados del archivo Berrutti: docTR y Tesseract contra LightOnOCR-3-4B, Qwen3-VL-8B en 4 bits y Chandra OCR 2 | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/08_OCR_mecanografiado.ipynb) |
| `09_OCR_manuscritos.ipynb` | Lo mismo con cinco manuscritos españoles (Edad Media a siglo XVIII): docTR y Tesseract contra Churro-3B, LightOnOCR-3-4B y Chandra OCR 2; agrega un CER normalizado | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/09_OCR_manuscritos.ipynb) |
| `10_OCR_comparacion.ipynb` | Reúne 07, 08 y 09 en un solo cuaderno: los quince documentos pasan por docTR, Tesseract, Churro-3B, LightOnOCR-3-4B, Qwen3-VL-8B en 4 bits y Chandra OCR 2, y cada modelo se descarga una sola vez. Se puede elegir qué tipos de documento procesar y retomar una ejecución cortada | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/10_OCR_comparacion.ipynb) |

Los cuadernos 07 a 10 no usan la página común: comparan dos OCR clásicos (docTR y Tesseract) con los tres mejores modelos abiertos de visión y lenguaje que entran en una T4 para cada tipo de documento, según la evaluación de `informe-ocr-berrutti.md`, sobre páginas que tienen transcripción humana. Las fuentes y sus licencias están en [`datos_ocr/README.md`](datos_ocr/README.md).

## Cómo usarlos en Colab

1. Abrir el cuaderno con el enlace de la tabla.
2. Verificar que el entorno tenga GPU: *Entorno de ejecución → Cambiar tipo de entorno de ejecución → T4 GPU*.
3. *Entorno de ejecución → Ejecutar todas*.

No hace falta descargar nada: cada cuaderno instala lo que necesita y trae las imágenes desde este repositorio.

**Tiempos medidos en Colab con GPU T4** (página común, primera ejecución):

| Cuaderno | Instalación | Procesamiento |
| --- | --- | --- |
| 01 | menos de 1 min | menos de 1 min |
| 02 | ~9 min | ~3 min |
| 03 | 5 a 16 min | ~1 min |
| 04 | ~1 min | ~1 min |
| 05 y 06 | sin medir todavía | sin medir todavía |
| 07 a 09 | 10 a 15 min por cuaderno, con la descarga de los tres modelos (unos 25 GB) y los datos | sin medir en T4; en una RTX 5090, 1 a 3 min |
| 10 | 15 a 25 min, con la descarga de los cuatro modelos (unos 45 GB) y los datos | sin medir en T4 |

Conviene ejecutar la instalación **antes de la clase** o al comienzo de la jornada.

## Elegir las imágenes

La variable `SELECCION`, al comienzo de cada cuaderno, define qué se procesa:

| Valor | Qué procesa |
| --- | --- |
| `"comun"` | la página común (valor por defecto) |
| `"prensa"` | las seis páginas de prensa |
| `"manuscritos"` | las cinco imágenes manuscritas (cartas, actas, diario) |
| `"todas"` | las once imágenes |
| `"propias"` | imágenes o PDF de cada participante: en Colab se suben varios archivos o una carpeta completa; fuera de Colab se leen de `mis_imagenes/` |

Cada página de un PDF se convierte en una imagen PNG (`DPI_PDF = 200`) antes de procesarla.

No subir a Colab material sensible o con restricciones de uso.

## Imágenes

Las imágenes están en [`imagenes/`](imagenes/) y sus fichas en [`imagenes/fuentes.csv`](imagenes/fuentes.csv): título, fecha, lugar, institución, URL de origen, licencia y evidencia de la licencia. Diez son de dominio público; el acta de Baradero (1857) es CC BY-SA 4.0 y exige atribución.

## Qué produce cada cuaderno

Cada cuaderno guarda sus resultados en `resultados/<cuaderno>/` y permite descargarlos como `.zip`:

- visualizaciones de las regiones detectadas y, en 02 y 03, del orden de lectura;
- la transcripción en Markdown y el JSON completo del pipeline;
- una tabla (`regiones.csv` o `bloques.csv`) con una columna `evaluacion_humana` para registrar errores;
- `procesamiento.json`, con herramienta, versiones, modelo, parámetros, fecha y dispositivo.

## Ejecutar fuera de Colab

Los cuadernos funcionan también en una computadora propia; en ese caso no instalan nada y leen las imágenes de `imagenes/`. Se probaron con Python 3.12 en entornos separados:

| Cuaderno | Paquetes |
| --- | --- |
| 01 | `doclayout-yolo==0.0.4 huggingface_hub pandas matplotlib pypdfium2` |
| 02 y 03 | `paddlepaddle==3.2.1` (o `paddlepaddle-gpu==3.2.1`) y `paddleocr[doc-parser]==3.7.0 pandas matplotlib pypdfium2` |
| 04 | `glmocr[selfhosted]==0.1.5 pandas matplotlib pypdfium2`, y Ollama con el modelo `glm-ocr` |
| 05 | `doclayout-yolo==0.0.4 transformers opencv-python pandas matplotlib pypdfium2` |
| 06 | `doclayout-yolo==0.0.4 pytesseract pandas matplotlib pypdfium2` y Tesseract con el idioma `spa`; además, según la configuración, Ollama con `ministral-3:8b`, `google-genai` o `paddlepaddle==3.2.1 paddleocr==3.7.0` |
| 07 a 10 | `transformers>=5.5.4 accelerate bitsandbytes torch torchvision python-doctr pytesseract jiwer pandas pyarrow huggingface_hub`, y Tesseract instalado en el sistema (el cuaderno baja el modelo `spa` de `tessdata_best`) |

`paddlepaddle` 3.3.x falla en CPU con PP-StructureV3; usar 3.2.1. Sin GPU, el cuaderno 03 puede tardar decenas de minutos por página.

Los resultados de la evaluación previa al taller están en [`EVALUACION.md`](EVALUACION.md).
