# Chat, editor y API

## Chat en el navegador

`llama-server` incluye un chat en [localhost:8080](http://127.0.0.1:8080). Es la primera forma de comprobar que el modelo responde antes de conectar el editor.

## Continue

La configuración de ejemplo utiliza Qwen3.5 9B para chat, edición y aplicación de cambios, y Ollama para el autocompletado.

1. Inicia Qwen3.5 9B con el alias de la [guía de ejecución](llama-cpp.md).
2. Instala y abre [Ollama](https://ollama.com/download), y ejecuta `ollama pull qwen2.5-coder:1.5b-base`.
3. Abre la configuración local de [Continue](https://docs.continue.dev/reference) e incorpora las entradas de [continue.yaml](../examples/continue.yaml). Si ya tienes una configuración, combina las entradas de `models`.
4. Selecciona Qwen3.5 9B en Chat/Edit y Qwen2.5-Coder 1.5B Base en Autocomplete.

Para usar 35B-A3B, cambia el modelo del servidor y el campo `model` a `qwen3.5-35b-a3b`. El nombre seleccionado en el editor debe corresponder al servidor que está en ejecución.

`provider: openai` selecciona el protocolo de conexión compatible; `apiBase` apunta al servidor local. Consulta [proveedor compatible](https://docs.continue.dev/customize/model-providers/top-level/openai) y [proveedor Ollama](https://docs.continue.dev/customize/model-providers/top-level/ollama).

La disponibilidad de herramientas en Agent depende de la compatibilidad entre modelo, plantilla, servidor y cliente. Una conexión de chat por sí sola no verifica llamadas a herramientas. Los ejemplos configuran los roles que se observaron en el editor sin forzar capacidades adicionales.

## Aplicaciones con API de chat compatible

Configura estos datos en el cliente:

| Campo | Valor |
|---|---|
| URL base | `http://127.0.0.1:8080/v1` |
| Modelo | Alias devuelto por `/v1/models` |
| Autenticación | La que hayas configurado en tu servidor; los ejemplos locales no establecen una clave |

Ejemplo en PowerShell con Qwen3.5 9B:

```powershell
$body = @{
    model = "qwen3.5-9b"
    messages = @(@{
        role = "user"
        content = "Explica este concepto: una cola de tareas asíncronas."
    })
} | ConvertTo-Json -Depth 5

Invoke-RestMethod -Method Post `
    -Uri "http://127.0.0.1:8080/v1/chat/completions" `
    -ContentType "application/json; charset=utf-8" `
    -Body ([System.Text.Encoding]::UTF8.GetBytes($body))
```

Si el cliente está dentro de un contenedor o en otro ordenador, `127.0.0.1` apunta a ese entorno, no al equipo del modelo. La configuración anterior es para aplicaciones ejecutadas en el mismo equipo.

Fuente: [API del servidor de llama.cpp](https://github.com/ggml-org/llama.cpp/blob/master/tools/server/README.md).
