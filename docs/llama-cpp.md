# Ejecutar GGUF con llama.cpp

## Instalación

Descarga una compilación para tu sistema desde las [releases oficiales](https://github.com/ggml-org/llama.cpp/releases). Extrae el paquete completo para conservar las bibliotecas que acompañan al ejecutable.

Los ejemplos de Windows se ejecutan en PowerShell, desde la carpeta que contiene `llama-server.exe`. Coloca los GGUF descargados en una subcarpeta `models`. En Linux o macOS, utiliza la ruta del ejecutable `llama-server` de tu instalación.

## CUDA y cuBLAS

CUDA es el soporte de cálculo de NVIDIA utilizado por el backend de llama.cpp. [cuBLAS](https://docs.nvidia.com/cuda/cublas/) es su biblioteca de álgebra lineal. El GGUF contiene el modelo; no tiene una edición «CUDA» distinta. La aceleración corresponde al motor y sus bibliotecas.

En Windows, elige el paquete CUDA de las releases que corresponda a tu sistema y conserva sus DLL junto a los ejecutables. Si la release distribuye bibliotecas CUDA aparte, sigue sus indicaciones. El controlador debe ser compatible con la versión CUDA del paquete. No mezcles bibliotecas de versiones diferentes.

También puedes compilar el backend CUDA desde el código fuente. Necesitas las herramientas de compilación indicadas en la [guía oficial](https://github.com/ggml-org/llama.cpp/blob/master/docs/build.md), incluido el CUDA Toolkit para esta opción:

```sh
git clone https://github.com/ggml-org/llama.cpp
cd llama.cpp
cmake -B build -DGGML_CUDA=ON
cmake --build build --config Release
```

La opción documentada es **`GGML_CUDA`**. Consulta la salida del servidor para comprobar que ha detectado CUDA y cómo distribuye la carga. Esta guía no fija arquitectura de GPU, número de capas descargadas ni tamaños de caché.

## Qwen3.5: ejecución directa

Descarga los archivos exactos enlazados en [modelos](modelos.md). Ejecuta **una** de estas líneas:

```powershell
.\llama-server.exe -m ".\models\Qwen3.5-9B-Q4_K_M.gguf" --alias qwen3.5-9b --host 127.0.0.1 --port 8080 --jinja --fit on
```

```powershell
.\llama-server.exe -m ".\models\Qwen3.5-35B-A3B-Q4_K_M.gguf" --alias qwen3.5-35b-a3b --host 127.0.0.1 --port 8080 --jinja --fit on
```

Para el GGUF de OrcaRouter, una vez descargado:

```powershell
.\llama-server.exe -m ".\models\Qwen3.8-27B-Uncensored-IQ2_XXS.gguf" --alias qwen3.8-27b-uncensored --host 127.0.0.1 --port 8080 --jinja --fit on
```

Abre [el chat local](http://127.0.0.1:8080) cuando termine la carga. Detén el servidor con `Ctrl+C` antes de iniciar otro en el mismo puerto.

`--alias` fija el identificador para los clientes; `--jinja` habilita las plantillas de chat. `--fit on` permite adaptar argumentos no fijados a la memoria disponible y no garantiza que cualquier modelo quepa. Fuente: [servidor llama.cpp](https://github.com/ggml-org/llama.cpp/blob/master/tools/server/README.md).

## Reutilizar los GGUF descargados con Ollama

Para DeepSeek y Gemma, descarga la distribución identificada y consulta la ruta que imprime `FROM`:

```sh
ollama pull deepseek-r1:14b
ollama show --modelfile deepseek-r1:14b
```

```sh
ollama pull gemma4:12b
ollama show --modelfile gemma4:12b
```

La [referencia de Modelfile](https://docs.ollama.com/modelfile) muestra cómo consultar el archivo y su ruta. En un modelo GGUF, el archivo puede llamarse `sha256-...` y seguir siendo un GGUF. Usa la ruta de tu propia instalación; no hace falta renombrar ni mover el archivo.

Sustituye el marcador por la ruta local mostrada, manteniendo las comillas:

```powershell
.\llama-server.exe -m "RUTA_GGUF_DE_DEEPSEEK" --alias deepseek-r1-14b --host 127.0.0.1 --port 8080 --jinja --fit on
```

```powershell
.\llama-server.exe -m "RUTA_GGUF_DE_GEMMA" --alias gemma4-12b --host 127.0.0.1 --port 8080 --jinja --fit on
```

Estos ejemplos usan texto. La ejecución multimodal requiere los componentes compatibles con el modelo y el motor; no intercambies proyectores entre distribuciones. La [documentación multimodal de llama.cpp](https://github.com/ggml-org/llama.cpp/tree/master/tools/mtmd) detalla el uso de `--mmproj`.

## Comprobar la conexión

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8080/v1/models"
```

El identificador devuelto debe coincidir con el alias que utilizarás en el cliente. Si aparece un error de arquitectura o de plantilla, revisa la compatibilidad de tu versión del motor con la distribución descargada.
