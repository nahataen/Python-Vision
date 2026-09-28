# 🖼️ Clasificador de imágenes con Google Vision

> Sube imágenes en una interfaz Gradio, las etiqueta con Google Cloud Vision API y las archiva en carpetas por categoría.

## Qué hace

El archivo `app` (código Python de 103 líneas, sin extensión `.py`) usa `google.cloud.vision.ImageAnnotatorClient.label_detection` y reglas por palabras clave sobre las etiquetas para clasificar cada imagen en: `Anime`, `Memes`, `Screenshots de YouTube`, `Educativo` o `No se pudo clasificar`. La interfaz `gr.Blocks` (`gradio_interface`) acepta múltiples archivos, muestra clasificación + etiquetas con confianza y mueve cada imagen con `shutil.move` a la carpeta de su categoría (las crea con `create_folders()`).

## Estructura

```text
image-classifier-vision-api/
├── app               # Código principal (Python, 103 líneas: classify_image,
│                     # gradio_interface, interfaz gr.Blocks + interface.launch())
├── requirements.txt  # Dependencias fijadas (gradio 4.36.1, google-cloud-vision 3.7.2,
│                     # fastapi, uvicorn, tensorflow, pillow, etc.)
└── README.md         # Este archivo
```

## Requisitos

- Python 3.7+
- Cuenta de Google Cloud con Vision API habilitada y un JSON de credenciales de cuenta de servicio
- Dependencias mínimas reales del código: `google-cloud-vision`, `gradio` (el `requirements.txt` fija además fastapi, tensorflow, pillow y otras transitivas)

## Cómo correr

```bash
git clone https://github.com/nahataen/Python-Vision.git
cd Python-Vision
pip install -r requirements.txt
```

1. Edita la línea 8 de `app` y pon la ruta real de tu JSON de credenciales en `GOOGLE_APPLICATION_CREDENTIALS` (el valor actual es solo un texto de ejemplo).
2. Ejecuta el archivo (hay que indicar el intérprete porque no lleva extensión `.py`):

```bash
python app
```

3. Abre la URL que imprime Gradio, sube imágenes y pulsa **Clasificar**. Cada imagen se mueve a `Anime/`, `Memes/`, `Screenshots de YouTube/`, `Educativo/` o `No se pudo clasificar/`.

## Notas

- El archivo principal se llama `app` sin extensión; renombrarlo a `app.py` no cambia su funcionamiento y facilita abrirlo en editores.
- Las reglas de clasificación son heurísticas por palabras clave en inglés (p. ej. `anime`, `fanart`, `meme`, `screenshot`, `infographic`); no es un modelo entrenado en este repo.
- Cada ejecución mueve físicamente los archivos subidos; usa copias de prueba.
