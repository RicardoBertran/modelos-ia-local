# Modelos y descargas

## DeepSeek R1 Distill Qwen 14B

Para explorar problemas de lógica y razonamiento paso a paso. Es la versión destilada sobre Qwen de 14B; no es el modelo completo DeepSeek R1.

- [Ficha del modelo original](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Qwen-14B).
- [Distribución de Ollama: deepseek-r1:14b](https://ollama.com/library/deepseek-r1:14b).
- La copia identificada es **Q4_K_M**.

```sh
ollama run deepseek-r1:14b
```

## Gemma 4 12B

En el vídeo se utiliza para un problema de lógica. Puede servir como asistente de conversación y generación de texto; sus capacidades generales se describen en la ficha de Google.

- [Ficha de Google](https://huggingface.co/google/gemma-4-12B).
- [Distribución de Ollama: gemma4:12b](https://ollama.com/library/gemma4:12b).
- El lanzador de la demostración utiliza el GGUF **Q4_K_M** de Ollama. La edición QAT de LM Studio es una distribución diferente.

```sh
ollama run gemma4:12b
```

## Qwen3.8 27B Uncensored

La demostración utiliza la variante modificada de **OrcaRouter**, con cuantización **IQ2_XXS**, para conversación técnica y análisis de seguridad. El nombre «Uncensored» identifica esa variante; no implica mayor exactitud.

- [Ficha de OrcaRouter](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored).
- [Archivos GGUF de OrcaRouter](https://huggingface.co/orcarouter/Qwen3.8-27B-Uncensored-GGUF/tree/main).
- Archivo: `Qwen3.8-27B-Uncensored-IQ2_XXS.gguf`.
- [Distribución de Ollama](https://ollama.com/orcarouter/Qwen3.8-27B-Uncensored).

```sh
ollama run orcarouter/Qwen3.8-27B-Uncensored:iq2_xxs
```

El repositorio GGUF de Hugging Face solicita acceso a sus archivos. Puedes usar la distribución de Ollama indicada arriba. Para entradas de imagen con llama.cpp, el distribuidor también publica `mmproj-Qwen3.8-27B-Uncensored-f16.gguf`; la guía de ejecución se centra en texto.

## Qwen3.5 9B

Utilizado para chat y edición de código en Continue.

- [Modelo original de Qwen](https://huggingface.co/Qwen/Qwen3.5-9B).
- [GGUF de Unsloth](https://huggingface.co/unsloth/Qwen3.5-9B-GGUF/tree/main).
- Archivo identificado: `Qwen3.5-9B-Q4_K_M.gguf`.

Descarga desde el listado de archivos y sigue los [comandos de llama.cpp](llama-cpp.md).

## Qwen2.5-Coder 1.5B Base

Es el modelo configurado para completar código mientras escribes. **Base** es parte de la elección: no sustituyas automáticamente esta etiqueta por Instruct.

- [Modelo original](https://huggingface.co/Qwen/Qwen2.5-Coder-1.5B).
- [Etiqueta exacta en Ollama](https://ollama.com/library/qwen2.5-coder:1.5b-base).

```sh
ollama pull qwen2.5-coder:1.5b-base
```

La configuración observada permite confirmar la etiqueta, pero no la cuantización del archivo descargado. Por eso no se atribuye una cuantización concreta a esta entrada.

## Qwen3.5 35B-A3B

Utilizado para generación de proyectos y refactorización. Es un modelo MoE: el nombre distingue el tamaño total de los parámetros activos. Esto no convierte su archivo ni su memoria necesaria en los de un modelo de 3B.

- [Modelo original de Qwen](https://huggingface.co/Qwen/Qwen3.5-35B-A3B).
- [GGUF de Unsloth](https://huggingface.co/unsloth/Qwen3.5-35B-A3B-GGUF/tree/main).
- Archivo identificado: `Qwen3.5-35B-A3B-Q4_K_M.gguf`.

## Cómo interpretar las variantes

GGUF es el formato del archivo que carga llama.cpp. Q4_K_M e IQ2_XXS son tipos de cuantización, no nombres de modelos. Los metadatos GGUF identificados usan `general.file_type` 15 y 19, respectivamente; la correspondencia está definida en [llama.h](https://github.com/ggml-org/llama.cpp/blob/master/include/llama.h).

Las etiquetas de los distribuidores pueden cambiar con el tiempo. Para conservar una ejecución, guarda también la versión del motor, el nombre y la revisión del archivo descargado. Las fichas enlazadas contienen las licencias y condiciones de cada distribución.
