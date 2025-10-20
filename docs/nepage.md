# 💻 Documentación de la Práctica – Control de LED con ESP32

> Proyecto académico de introducción a la mecatrónica: uso de una placa **ESP32** como microcontrolador para interactuar con componentes básicos (LED y botón) y establecer comunicación **Bluetooth Serial** con una aplicación móvil.

---

## 1) Resumen

- **Nombre del proyecto:** Control de LED por GPIO, Interrupción y Bluetooth Serial con ESP32
- **Equipo / Autor(es):** [Tus Nombres]
- **Curso / Asignatura:** Introducción a la Mecatrónica / Programación de Microcontroladores
- **Fecha:** [Fecha de la práctica]
- **Descripción breve:** Se implementaron tres funcionalidades básicas en una ESP32: encendido/apagado simple de un LED, control del LED mediante un botón y control remoto del LED enviando datos por Bluetooth Serial desde un smartphone.

!!! tip "Consejo"
    Este proyecto introduce el manejo de entradas/salidas digitales (GPIO) en la ESP32, el uso de entradas digitales y la comunicación inalámbrica básica (Bluetooth).

---

## 2) Objetivos

**General:** Desarrollar habilidades básicas de programación y conexión de hardware en el entorno del microcontrolador ESP32 para controlar un actuador simple (LED) y recibir comandos externos (botón y Bluetooth).

**Específicos:**
  - Configurar un pin GPIO para salida digital y controlar el encendido/apagado de un LED.
  - Leer el estado de un botón para controlar el LED.
  - Establecer comunicación serial vía Bluetooth (SPP) entre la ESP32 y una aplicación Android.
  - Procesar comandos de texto recibidos por Bluetooth (`HIGH`, `LOW`) para alternar el estado del LED.

---

## 3) Alcance y Exclusiones

**Incluye:**
  - Control de LED directo por código (`blink`).
  - Implementación de un botón usando lectura de estado (`polling`).
  - Comunicación y control **Bluetooth Serial** (SPP/Classic Bluetooth).
  - Código y esquemáticos para cada una de las tres etapas.

**No incluye:**
  - Uso de Interrupciones Externas.
  - Uso de Wi-Fi o protocolos TCP/IP.
  - Diseño de PCB o montaje permanente.

---

## 4) Requisitos

**Hardware**
- 1 × Placa de desarrollo **ESP32** (ej. ESP32 DevKitC)
- 1 × LED de cualquier color
- 1 × Resistencia limitadora para el LED (**220 Ω** – 1 kΩ)
- 1 × Botón (pulsador)
- 1 × Resistencia **Pull-down** (ej. **10 kΩ**)
- 1 × Protoboard y cables de conexión
- Fuente de alimentación (USB o externa, 5 VDC)
- Smartphone con **Bluetooth** y aplicación **Bluetooth Serial** instalada.

**Conocimientos previos**
- Programación básica en C/C++ (entorno Arduino IDE).
- Concepto de GPIOs.
- Lectura de entradas digitales.
- Fundamentos de comunicación Serial y Bluetooth.

---

## 5) Procedimiento e Instalación

1. **Montaje del Hardware:** Conectar el **LED** al **GPIO 2** (con su resistencia limitadora) y el **Botón** al **GPIO 4** (con resistencia Pull-down externa a GND).

2. **Carga de Código:** Cargar el *sketch* correspondiente para cada etapa.

3. **Prueba de Funcionalidad:**
    * **Etapa 1:** Verificar que el LED parpadee cada segundo.
    * **Etapa 2:** Verificar que el LED solo se encienda mientras se mantiene presionado el botón.
    * **Etapa 3:** Conectar la aplicación Bluetooth Serial y enviar los comandos `HIGH` o `LOW`.

<img src="../recursos/imgs/practicas/esp32_led/esquematico_base.png" alt="Esquema de conexión base ESP32 LED y Botón" width="600">
<p><em>Figura 1. Esquema de conexión base del LED (GPIO 2) y Botón (GPIO 4) a la ESP32</em></p>

---

## 5.1) Código de Programación

### Etapa 1: LED Parpadeante Simple (Blink) ⏳

Este código enciende y apaga el LED cada segundo.

```cpp
// Definición del pin del LED
const int ledPin = 2; // Usamos el GPIO 2

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // Enciende el LED
  digitalWrite(ledPin, HIGH);
  delay(1000); // Espera 1 segundo (1000 milisegundos)

  // Apaga el LED
  digitalWrite(ledPin, LOW);
  delay(1000); // Espera 1 segundo
}