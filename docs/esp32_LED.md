# 💻 Documentación de la Práctica – Control de LED con ESP32 (Múltiples Modos)

> Proyecto académico de introducción a la mecatrónica: implementación de la placa **ESP32** para control de un LED en tres modos distintos: temporizado, mediante interacción física (botón), y por comunicación inalámbrica (**Bluetooth Serial**).

---

## 1) Resumen

- **Nombre del proyecto:** LED Multi-Control con ESP32 (Blink, Botón y BT)
- **Equipo / Autor(es):** [Tus Nombres]
- **Curso / Asignatura:** Introducción a la Mecatrónica / Programación de Microcontroladores
- **Fecha:** [Fecha de la práctica]
- **Descripción breve:** Se exploraron las funcionalidades básicas de la ESP32 (GPIOs, temporización, lectura de entradas y comunicación inalámbrica) implementando tres programas que controlan un LED: parpadeo constante, encendido por pulsación de botón, y control remoto por comandos de texto vía Bluetooth.

!!! tip "Consejo"
    Esta práctica es fundamental para comprender la versatilidad de la ESP32 en la interacción con el entorno (inputs físicos) y la comunicación remota (Bluetooth).

---

## 2) Objetivos

**General:** Aplicar los conceptos básicos de programación de microcontroladores para controlar un actuador (LED) y procesar diferentes tipos de entradas (tiempo, señal digital, dato serial).

**Específicos:**
  - Controlar el tiempo de encendido/apagado del LED usando `delay()`.
  - Leer el estado de un botón (entrada digital) y reflejarlo en el LED.
  - Implementar la comunicación **Bluetooth Serial (SPP)**.
  - Procesar los comandos de texto (`HIGH`/`LOW`) recibidos por Bluetooth.

---

## 3) Alcance y Exclusiones

**Incluye:**
  - Implementación de tres programas independientes cargados a la ESP32.
  - Uso de LED en **GPIO 2** y Botón en **GPIO 4**.
  - Configuración y prueba de la comunicación Bluetooth Serial.
  - Código fuente para las tres etapas.

**No incluye:**
  - Uso de interrupciones o temporizadores avanzados.
  - Diseño de PCB.
  - Control basado en Wi-Fi.

---

## 4) Requisitos

**Hardware**
- 1 × Placa de desarrollo **ESP32**
- 1 × LED de cualquier color
- 1 × Resistencia limitadora para el LED (220 Ω)
- 1 × Botón (pulsador)
- 1 × Resistencia **Pull-down** (10 kΩ) para el botón (conectada a GND)
- 1 × Protoboard y cables de conexión
- Fuente de alimentación (5 VDC)
- Smartphone con **Bluetooth** y aplicación **Bluetooth Serial** instalada.

**Conocimientos previos**
- Programación C/C++ (Arduino IDE).
- Manejo de entradas y salidas digitales (GPIO).
- Concepto de comunicación serial.

---

## 5) Procedimiento e Instalación

1. **Montaje del Hardware:** Conectar el **LED** al **GPIO 2** (con su resistencia limitadora) y el **Botón** al **GPIO 4** (con resistencia Pull-down a GND).
2. **Carga secuencial de Código:** Cargar cada uno de los tres códigos de forma individual a la ESP32 para verificar su funcionamiento.
3. **Prueba funcional:**
    * Etapa 1: Verificar el parpadeo de 1 segundo.
    * Etapa 2: Verificar el encendido solo al presionar el botón.
    * Etapa 3: Emparejar por Bluetooth y enviar comandos `HIGH`/`LOW`.

<img src="../recursos/imgs/practicas/esp32_led/esquematico_base.png" alt="Esquema de conexión base ESP32 LED y Botón" width="600">
<p><em>Figura 1. Esquema de conexión base del LED (GPIO 2) y Botón (GPIO 4) a la ESP32</em></p>

---

## 5.1) Código de Programación

### Etapa 1: LED Parpadeante Simple (Blink) ⏳

El LED se enciende y apaga cada segundo.

```cpp
// Definición del pin del LED
const int ledPin = 2; // Usamos el GPIO 2

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // Enciende el LED
  digitalWrite(ledPin, HIGH);
  delay(1000); // Espera 1 segundo

  // Apaga el LED
  digitalWrite(ledPin, LOW);
  delay(1000); // Espera 1 segundo
}
Etapa 2: Control del LED con Botón 🔘
El LED se enciende mientras el botón está siendo presionado.

C++

// Definición de pines
const int ledPin = 2;   // LED en GPIO 2
const int buttonPin = 4; // Botón en GPIO 4

void setup() {
  pinMode(ledPin, OUTPUT);
  // El botón está conectado con una resistencia pull-down externa
  pinMode(buttonPin, INPUT); 
}

void loop() {
  // Leer el estado del botón (HIGH al presionar, LOW al soltar)
  int buttonState = digitalRead(buttonPin);

  // Escribir el estado del botón directamente al LED
  digitalWrite(ledPin, buttonState);

  // Pequeña espera para estabilización
  delay(10);
}
Etapa 3: Control del LED por Bluetooth Serial 📲
El LED se controla enviando el mensaje de texto HIGH o LOW (en mayúsculas) desde la aplicación móvil.

C++

#include "BluetoothSerial.h"

#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled!
#endif

BluetoothSerial SerialBT;

const int ledPin = 2;
String message = ""; // Buffer para el comando

void setup() {
  Serial.begin(115200);
  pinMode(ledPin, OUTPUT);
  
  SerialBT.begin("ESP32_Control_LED"); // Nombre del dispositivo BT
  Serial.println("Bluetooth iniciado.");
}

void loop() {
  if (SerialBT.available()) {
    char incomingChar = SerialBT.read();
    
    if (incomingChar != '\n') {
      message += incomingChar; 
    } else {
      message.trim();
      message.toUpperCase(); 

      Serial.print("Comando recibido: ");
      Serial.println(message);

      if (message == "HIGH") {
        digitalWrite(ledPin, HIGH);
        SerialBT.println("LED Encendido");
      } else if (message == "LOW") {
        digitalWrite(ledPin, LOW);
        SerialBT.println("LED Apagado");
      } else {
        SerialBT.println("Comando Invalido. Use HIGH o LOW.");
      }
      
      message = "";
    }
  }
  delay(20);
}
6) Resultados
✅ Etapa 1: El temporizado fue preciso, con un período total de 2 segundos.

✅ Etapa 2: La lectura de la entrada digital (botón) fue exitosa, controlando el LED de forma directa.

✅ Etapa 3: La comunicación Bluetooth se estableció y los comandos remotos controlaron el actuador.

✅ Se demostró la capacidad de la ESP32 para manejar tareas de temporización, I/O y comunicaciones.

Fotos del montaje físico:

<img src="../recursos/imgs/practicas/esp32_led/armado_1.png" alt="Foto montaje ESP32 con LED y Botón" width="300"> <p><em>Figura 2. Montaje físico – Vista general con ESP32, LED y botón</em></p>

<img src="../recursos/imgs/practicas/esp32_led/app_bluetooth.png" alt="Captura app Bluetooth Serial" width="300"> <p><em>Figura 3. Captura de pantalla de la app de control Bluetooth Serial</em></p>

7) Video de funcionamiento
Video 1: Control Simple de LED (Blink)
<div align="center"> <iframe src="[ENLACE DE TU VIDEO 1 - CONTROL SIMPLE]" width="800" height="450" frameborder="0" scrolling="no" allowfullscreen title="ESP32_LED_Simple.mp4"></iframe> <p><em>Video 1. LED parpadeando con tiempos fijos.</em></p> <p>🔗 <a href="[ENLACE DE TU VIDEO 1 - CONTROL SIMPLE]">Ver video en tu plataforma</a></p> </div>

Video 2: Control de LED con Botón
<div align="center"> <iframe src="[ENLACE DE TU VIDEO 2 - BOTÓN]" width="800" height="450" frameborder="0" scrolling="no" allowfullscreen title="ESP32_LED_Boton.mp4"></iframe> <p><em>Video 2. El LED se enciende solo mientras se mantiene presionado el botón.</em></p> <p>🔗 <a href="[ENLACE DE TU VIDEO 2 - BOTÓN]">Ver video en tu plataforma</a></p> </div>

Video 3: Control de LED por Bluetooth Serial
<div align="center"> <iframe src="[ENLACE DE TU VIDEO 3 - BLUETOOTH]" width="800" height="450" frameborder="0" scrolling="no" allowfullscreen title="ESP32_LED_BT_Serial.mp4"></iframe> <p><em>Video 3. Demostración del control remoto del LED enviando HIGH/LOW vía Bluetooth.</em></p> <p>🔗 <a href="[ENLACE DE TU VIDEO 3 - BLUETOOTH]">Ver video en tu plataforma</a></p> </div>