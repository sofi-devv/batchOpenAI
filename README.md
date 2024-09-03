# OpenAI Batch Processing Script

Este repositorio contiene un script de Python diseñado para automatizar el proceso de carga y procesamiento de archivos de comentarios mediante la API de OpenAI. El script recorre una lista de prompts y DataFrames, sube archivos de entrada a OpenAI, y maneja el procesamiento de estos lotes, guardando las respuestas procesadas en un directorio designado.

## Tabla de Contenidos

- [Requisitos](#requisitos)
- [Instalación](#instalación)
- [Uso](#uso)
- [Descripción del Script](#descripción-del-script)
- [Mejoras Sugeridas](#mejoras-sugeridas)
- [Contribuciones](#contribuciones)
- [Licencia](#licencia)

## Requisitos

- Python 3.x
- [OpenAI Python client](https://pypi.org/project/openai/)
- [pandas](https://pandas.pydata.org/)
- Módulos estándar de Python: `os`, `time`

## Instalación

1. Clona el repositorio:

    ```bash
    git clone https://github.com/tuusuario/openai-batch-processing.git
    cd openai-batch-processing
    ```

2. Instala los paquetes necesarios:

    ```bash
    pip install openai pandas
    ```

## Uso

1. Prepara tus archivos de entrada en formato JSONL y colócalos en el directorio `data/batches/`, asegurándote de que sigan el siguiente patrón de nombres:
   data/batches/prompt{prompt_index}/input_comments_batch_{batch_index}.jsonl

2. Configura tu clave de API de OpenAI como una variable de entorno:

 ```bash
 export OPENAI_API_KEY='tu-api-key'
 ```

3. Ejecuta el script:

 ```bash
 python batch_processing_script.py
 ```

## Descripción del Script

El script realiza las siguientes tareas:

1. **Iteración sobre Prompts y DataFrames**: Recorre los prompts a partir del séptimo y los DataFrames asociados, procesando cada combinación.
2. **Carga de Archivos a OpenAI**: Sube los archivos de entrada a OpenAI para su procesamiento.
3. **Creación y Monitoreo de Lotes**: Crea un lote de procesamiento para cada archivo y verifica su estado hasta que esté en proceso o completado.
4. **Procesamiento de Resultados**: Recupera y procesa los archivos de salida cuando el lote se completa, guardando los resultados en un archivo CSV.

### Directorios y Archivos

- **`data/batches/`**: Contiene los archivos de entrada en formato JSONL.
- **`results2/`**: Directorio de salida donde se guardan los archivos CSV con las respuestas procesadas.

### Funciones Clave

- `client.files.create()`: Carga archivos a OpenAI.
- `client.batches.create()`: Crea un proceso por lotes en OpenAI.
- `client.batches.retrieve()`: Recupera el estado del proceso por lotes.
- `procesar_respuestas(file_response)`: Función personalizada para procesar las respuestas y convertirlas en un DataFrame.

## Mejoras Sugeridas

- **Manejo de Errores**: Implementar un manejo de excepciones más robusto para manejar posibles fallos en la API.
- **Configuraciones Flexibles**: Usar archivos de configuración o variables de entorno para gestionar las rutas de archivo y tiempos de espera.
- **Logging**: Incluir un sistema de registro para mejorar la trazabilidad y facilitar la depuración.

## Contribuciones

¡Las contribuciones son bienvenidas! Siéntete libre de hacer un fork de este repositorio y enviar un pull request con tus mejoras.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.
