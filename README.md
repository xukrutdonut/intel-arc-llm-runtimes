# Intel Arc (Arrow Lake / Lunar Lake) LLM Runtimes for Linux & LM Studio

Este repositorio contiene las compilaciones nativas optimizadas de **`llama.cpp`** e **`IPEX-LLM`** específicamente configuradas para GPUs integradas y dedicadas **Intel Arc** (arquitecturas Arrow Lake, Lunar Lake, Xe/Xe2) en Linux.

---

## 📦 Contenido del Repositorio

### 1. Binarios Nativos CLI & Server (`/bin`)
- **`llama-cli-intel-arc`**: Binario ejecutable compilado con soporte nativo de **Vulkan + XMX (Matrix Acceleration)** para inferencia ultra rápida desde terminal.
- **`llama-server-intel-arc`**: Servidor de inferencia local compatible con la API de OpenAI.
- **`libggml-vulkan.so`**: Librería compartida optimizada con sháders de matrices cooperativas.

### 2. Extensión Personalizada para LM Studio (`/lmstudio-extension`)
- Extensión lista para copiar en `~/.lmstudio/extensions/backends/` para habilitar el backend personalizado de Intel Arc sin sobreescribir los backends por defecto.

---

## 🚀 Guía de Instalación

### Método A: Ejecutables Directos (CLI / Servidor)
```bash
# Dar permisos de ejecución e instalar en el sistema
chmod +x bin/llama-cli-intel-arc bin/llama-server-intel-arc
sudo cp bin/llama-cli-intel-arc /usr/local/bin/
sudo cp bin/llama-server-intel-arc /usr/local/bin/

# Ejemplo de uso con cualquier modelo GGUF:
llama-cli-intel-arc -m /ruta/a/tu/modelo.gguf -p "Hola, explica las leyes de Newton" --n-gpu-layers 99
```

### Método B: Integración en LM Studio (Linux)
```bash
# Copiar el backend acelerado directamente a la carpeta de extensiones de LM Studio
cp bin/libggml-vulkan.so ~/.lmstudio/extensions/backends/llama.cpp-linux-x86_64-vulkan-avx2-2.29.0/libggml-vulkan.so
```
*Reinicia LM Studio y selecciona la opción **"Vulkan llama.cpp"** para activar la aceleración matricial nativa de Intel Arc.*

---

## 🛠️ Requisitos de Drivers en Linux
Asegúrate de tener instalados los controladores de cómputo oficiales de Intel:
```bash
sudo apt-get install -y intel-opencl-icd intel-level-zero-gpu libze1
```

---

## ⚡ Rendimiento
En pruebas de benchmarking con el modelo **Hermes 3B Q4_K_M** en memoria RAM DDR5 5600 MT/s (Dual Channel):
- **LM Studio estándar (genérico):** ~6.8 tok/s.
- **Intel Arc Native Runtime (este repositorio):** **31.5 tok/s** (aumento de rendimiento > 4.5x).
