# 🕹️ Project Loggy 

**Loggy** es un proyecto de investigación en ciberseguridad diseñado para demostrar vectores de ataque basados en **Ingeniería Social (Social Engineering)** y **Exfiltración de Datos Silenciosa**. 

El sistema utiliza el videojuego clásico DOOM (1993) como un "decoy" (señuelo) para distraer al usuario mientras un bot de comando y control (C2), integrado con Discord, realiza tareas de monitoreo y robo de información en segundo plano.

---

## 🏗️ Arquitectura del Sistema

El flujo de ataque se divide en tres fases críticas:

1.  **Infiltración y Señuelo**: Ejecución de un hilo paralelo que lanza un mensaje de confianza y abre un juego real en el navegador para camuflar el consumo de recursos.
2.  **Establecimiento de C2**: El bot se conecta a Discord mediante WebSockets (Puerto 443), lo que hace que el tráfico sea indistinguible de la navegación normal.
3.  **Exfiltración Dinámica**: El bot identifica la "Zona Cero" del navegador y extrae bases de datos SQLite de múltiples perfiles.



---

## 🚀 Características Técnicas

* **Stealer de Navegadores**: Barrido recursivo en `AppData` para detectar carpetas `Default` y `Profile X`. Utiliza `shutil.copy2` para evadir bloqueos de archivos en uso.
* **Keylogger con Contexto**: Captura pulsaciones de teclas y utiliza la API de Windows para adjuntar el nombre de la ventana activa (ej. "Login Banco").
* **Monitoreo Multimedia**: 
    * **Cámara**: Captura de frames con ajuste automático de brillo.
    * **Audio**: Grabación ambiental en formato `.wav`.
    * **Pantalla**: Capturas de pantalla procesadas **100% en RAM** (`io.BytesIO`) para evitar detecciones de antivirus basadas en archivos.
* **Evasión Anti-Forense**: Uso de `ctypes` para interactuar con el Kernel de Windows y ocultar archivos temporales.

---

## 🛠️ Instalación y Configuración

### 1. Requisitos de Sistema
* Python 3.10 o superior.
* Sistema Operativo: Windows (para funciones de `ctypes` y rutas de AppData).

### 2. Instalación de Dependencias
Instala las librerías necesarias ejecutando el siguiente comando:

```bash
pip install discord.py opencv-python sounddevice scipy pyautogui requests pygetwindow pynput mss python-docx webbrowser 

### 3. Configuración de Credenciales

Debes editar las siguientes variables en el código fuente con tus propios datos obtenidos desde el [Discord Developer Portal](https://discord.com/developers/applications):

```python
# --- CONFIGURACIÓN ---
BOT_TOKEN = "TU_TOKEN_AQUÍ"
CHANNEL_ID = 0000000000000000  # Tu ID de canal de Discord
