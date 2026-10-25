# Cuadernos del taller: layout y OCR

Cuatro cuadernos para los dos primeros días del taller. Todos trabajan sobre la **misma página común** (*Centro Gallego*, Montevideo, 1917: cuatro columnas, titulares, escudos y un aviso con grabado), para poder comparar qué hace cada herramienta con la misma fuente.

**Pregunta que organiza la actividad:** ¿en qué medida las decisiones automatizadas de segmentación y transcripción modifican la fuente histórica sobre la cual construimos nuestras interpretaciones?

| Cuaderno | Qué hace | Abrir |
| --- | --- | --- |
| `01_DocLayout_YOLO_segmentacion.ipynb` | Detecta regiones (títulos, texto, figuras) y exporta un recorte por región | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/01_DocLayout_YOLO_segmentacion.ipynb) |
| `02_PP_StructureV3_layout_OCR.ipynb` | Layout, orden de lectura y OCR con PP-StructureV3 (reconocedor latino, `lang="es"`) | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/02_PP_StructureV3_layout_OCR.ipynb) |
| `03_PaddleOCR_VL_layout_OCR.ipynb` | Layout y reconocimiento con un modelo de visión y lenguaje (PaddleOCR-VL 1.6) | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/03_PaddleOCR_VL_layout_OCR.ipynb) |
| `04_GLM_OCR_pipeline.ipynb` | Pipeline completo de GLM-OCR: layout PP-DocLayoutV3 y reconocimiento GLM-OCR servido con Ollama | [Colab](https://colab.research.google.com/github/agusnieto77/sicss-uruguay-2026/blob/main/cuadernos/04_GLM_OCR_pipeline.ipynb) |

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

Conviene ejecutar la instalación **antes de la clase** o al comienzo de la jornada.

## Elegir las imágenes

La variable `SELECCION`, al comienzo de cada cuaderno, define qué se procesa:

| Valor | Qué procesa |
| --- | --- |
| `"comun"` | la página común (valor por defecto) |
| `"prensa"` | las seis páginas de prensa |
| `"manuscritos"` | las cinco imágenes manuscritas (cartas, actas, diario) |
| `"todas"` | las once imágenes |
| `"propias"` | imágenes subidas por cada participante |

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
| 01 | `doclayout-yolo==0.0.4 huggingface_hub pandas matplotlib` |
| 02 y 03 | `paddlepaddle==3.2.1` (o `paddlepaddle-gpu==3.2.1`) y `paddleocr[doc-parser]==3.7.0 pandas matplotlib` |
| 04 | `glmocr[selfhosted]==0.1.5 pandas matplotlib`, y Ollama con el modelo `glm-ocr` |

`paddlepaddle` 3.3.x falla en CPU con PP-StructureV3; usar 3.2.1. Sin GPU, el cuaderno 03 puede tardar decenas de minutos por página.

Los resultados de la evaluación previa al taller están en [`EVALUACION.md`](EVALUACION.md).
