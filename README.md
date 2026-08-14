# Intel Arc (Arrow Lake / Lunar Lake) LLM Runtimes for Linux & LM Studio

Este repositorio contiene los dos runtimes personalizados y optimizados para GPUs y NPUs **Intel Arc** en Linux y LM Studio.

---

## 📦 Contenido del Repositorio

### 1. Binarios Nativos CLI & Server (`/bin`)
- **`llama-cli-intel-arc`**: Binario ejecutable compilado con soporte nativo de **Vulkan + XMX (Matrix Acceleration)** para inferencia ultra rápida desde terminal.
- **`llama-server-intel-arc`**: Servidor de inferencia local compatible con la API de OpenAI.
- **`libggml-vulkan.so`**: Librería compartida optimizada con sháders de matrices cooperativas.

### 2. Extensiones Personalizadas para LM Studio
- **`/lmstudio-extension-vulkan`**: Extensión acelerada con Vulkan/XMX para copiar en `~/.lmstudio/extensions/backends/llama.cpp-linux-x86_64-vulkan-intelarc-1.0.0/`.
- **`/lmstudio-extension-ipex`**: Extensión basada en Intel IPEX-LLM (SYCL/XPU) para copiar en `~/.lmstudio/extensions/backends/llama.cpp-linux-x86_64-ipex-intelarc-1.0.0/`.

---

## 🚀 Guía de Instalación en LM Studio

Copiar las dos extensiones directamente a tu carpeta de backends de LM Studio:

```bash
mkdir -p ~/.lmstudio/extensions/backends/

# 1. Copiar Runtime Intel Arc Vulkan/XMX
cp -r lmstudio-extension-vulkan ~/.lmstudio/extensions/backends/llama.cpp-linux-x86_64-vulkan-intelarc-1.0.0

# 2. Copiar Runtime Intel Arc IPEX-LLM
cp -r lmstudio-extension-ipex ~/.lmstudio/extensions/backends/llama.cpp-linux-x86_64-ipex-intelarc-1.0.0
```

Reinicia LM Studio y verás los dos nuevos runtimes en el menú desplegable:
- `Intel Arc (Vulkan/XMX Optimized)`
- `Intel Arc IPEX-LLM (SYCL/XPU)`

---

## ⚡ Rendimiento
En pruebas de benchmarking con el modelo **Hermes 3B Q4_K_M** en memoria RAM DDR5 5600 MT/s (Dual Channel):
- **LM Studio estándar (genérico):** ~6.8 tok/s.
- **Intel Arc Native Runtime (este repositorio):** **31.5 tok/s** (aumento de rendimiento > 4.5x).
