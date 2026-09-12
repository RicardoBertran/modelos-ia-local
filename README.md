# Modelos de IA en local

Guía en español de los modelos utilizados en el vídeo `¿Sin tokens? Estas 6 IA funcionan en tu PC`: qué usar para cada tarea, dónde descargarlo y cómo conectarlo a un chat o al editor.

| Modelo | Uso mostrado | Variante identificada |
|---|---|---|
| DeepSeek R1 Distill Qwen 14B | Razonamiento y problemas de lógica | Q4_K_M |
| Gemma 4 12B | Razonamiento y conversación | Q4_K_M, distribución de Ollama |
| Qwen3.8 27B Uncensored | Conversación técnica y análisis de seguridad | OrcaRouter, IQ2_XXS |
| Qwen3.5 9B | Chat y edición de código en el editor | Unsloth, Q4_K_M |
| Qwen2.5-Coder 1.5B **Base** | Autocompletado de código | Etiqueta Ollama `qwen2.5-coder:1.5b-base` |
| Qwen3.5 35B-A3B | Generación de proyectos y refactorización | Unsloth, Q4_K_M |

Los casos de uso describen las demostraciones; no son una clasificación de rendimiento. Las variantes se contrastaron con los archivos de modelos y la configuración del entorno de la grabación. En el vídeo, el rótulo «Qwen3.8 27B» corresponde al modelo **Uncensored** que aparece seleccionado en el chat.

## Empieza aquí

1. Consulta [modelos y descargas](docs/modelos.md).
2. Sigue la [guía de GGUF y llama.cpp](docs/llama-cpp.md) para ejecutar un modelo.
3. Conecta [Continue o una aplicación compatible con la API](docs/integraciones.md).

Para reproducir el flujo del editor, utiliza Qwen3.5 9B para chat y edición, y Qwen2.5-Coder 1.5B Base mediante Ollama para autocompletado. Puedes sustituir el modelo de chat por Qwen3.5 35B-A3B cuando tu equipo permita ejecutarlo.

Los ejemplos ofrecen una base general de ejecución. El consumo de memoria depende del archivo, el contexto y el motor. El tamaño de descarga no equivale a un requisito de RAM o VRAM. Revisa y prueba el código generado antes de utilizarlo.

Este repositorio contiene documentación y ejemplos de conexión. Los pesos se descargan desde sus distribuidores y conservan sus propias licencias.

Fuentes y enlaces revisados el **12 de septiembre de 2026**. Los comandos se contrastaron con la documentación y la ayuda de llama.cpp; no se ha realizado una prueba de inferencia de todos ellos como parte de esta guía.
