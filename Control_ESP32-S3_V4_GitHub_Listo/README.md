# Control ESP32-S3 V4

Proyecto preparado para controlar una placa ESP32-S3 desde una app Android.

## Arquitectura

- BLE: solo para comandos y estado.
- Wi-Fi: cámara, captura de foto, servidor web, FTP y OTA.
- La cámara no se envía por BLE. La app usa el stream HTTP del ESP32.

## Carpetas

- `android/`: proyecto Android nativo Java listo para compilar con Gradle.
- `firmware/Control_ESP32_S3_V4/Control_ESP32_S3_V4.ino`: sketch para la placa ESP32-S3.
- `.github/workflows/main.yml`: acción de GitHub para crear la APK automáticamente.
- `main.yml.copiar_manual.txt`: copia del workflow para pegarlo manualmente si hace falta.

## Cambios V4 principales

- Auto reconexión BLE en la app.
- Botón WiFi ahora activa/desactiva WiFi + servidor Web/OTA + FTP mediante BLE.
- Cámara por Wi-Fi con stream `http://IP:81/stream`.
- Guardado de foto en Descargas usando `http://IP:81/capture`.
- Navegador interno para seleccionar archivos `.bin` sin usar el selector externo de Android.
- OTA por Wi-Fi con subida HTTP multipart a `/update?key=esp32ota`.
- Control de música: anterior, play/pausa, siguiente, volumen, stop, barra de progreso y barra de volumen.
- Pantalla de la placa: hora arriba a la izquierda y batería arriba a la derecha.
- LED RGB apagado por defecto al arrancar. Solo se enciende al usar LED RGB o con actividad Wi-Fi/microSD.

## GitHub

Sube el contenido de esta carpeta a un repositorio. GitHub ejecutará `.github/workflows/main.yml` y dejará la APK en **Actions > Artifacts**.

## Configuración ESP32-S3 recomendada

- Board: ESP32S3 Dev Module.
- PSRAM: OPI PSRAM.
- Flash: 8 MB.
- Partition Scheme: 8M with SPIFFS / OTA compatible. No usar particiones `No OTA`.
- CPU: 240 MHz.
- USB CDC según tu configuración habitual.
