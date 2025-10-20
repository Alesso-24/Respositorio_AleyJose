# 📚 Documentación de la Práctica – Control de Motor DC con ESP32 (PWM y Puente H)

## 🧠 Proyecto académico de introducción a la mecatrónica
**Implementación de la placa ESP32 para el control de la dirección y velocidad de un motor DC utilizando el controlador L298N.**

---

## 🧭 1) Resumen

| **Elemento** | **Descripción** |
|---------------|----------------|
| **Nombre del proyecto:** | Control de Motor DC con L298N y ESP32 (Velocidad y Dirección) |
| **Equipo / Autor(es):** | Alessandro Reyes, José Compeán |
| **Curso / Asignatura:** | Introducción a la Mecatrónica / Programación de Microcontroladores |
| **Fecha:** | 19 sep 2025 |
| **Descripción breve:** | Se exploraron las funcionalidades de la ESP32 para controlar actuadores de mayor potencia. Se implementó el módulo L298N para manejar un motor DC, aplicando señales digitales (dirección) y PWM (velocidad) para realizar cambios de sentido y transiciones de aceleración/desaceleración. |

💡 **Consejo:**  
Esta práctica es crucial para entender el uso de puentes H (como el L298N) para el control de motores y la importancia del PWM para modular la potencia en la mecatrónica.

---

## 🎯 2) Objetivos

### **General**
Aplicar los conceptos de modulación por ancho de pulso (PWM) y el manejo de puentes H para lograr un control preciso sobre la velocidad y dirección de un motor DC.

### **Específicos**
- Configurar y utilizar los pines PWM de la ESP32 (LED Control).  
- Implementar el control de dirección del motor usando pines digitales.  
- Conectar y alimentar correctamente el módulo controlador L298N.  
- Desarrollar un programa que realice una secuencia de aceleración máxima seguida de desaceleración gradual usando un ciclo `for`.

---

## 📋 3) Alcance y Exclusiones

**Incluye:**
- Control de un solo motor DC (Motor A).  
- Implementación de tres programas independientes cargados a la ESP32.  
- Uso de PWM para control de velocidad.  
- Uso de una fuente de alimentación externa para el L298N.  
- Control de la dirección del motor.  

**No incluye:**
- Uso de encoders para feedback de velocidad.  
- Control de motores stepper o servomotores.  
- Control remoto (Wi-Fi o Bluetooth).  

---

## ⚙️ 4) Requisitos

### 🧰 **Hardware**
- 1 × Placa de desarrollo **ESP32**  
- 1 × Módulo controlador de motores **L298N (Puente H)**  
- 1 × Motor DC de baja potencia (ej. 5V–12V)  
- 1 × Fuente de alimentación externa (ej. batería 9V o adaptador 12V)  
- 1 × Protoboard y cables  
- Cables Jumper (al menos 6 M–F)  

### 📘 **Conocimientos previos**
- Programación en **C/C++ (Arduino IDE)**  
- Manejo de entradas y salidas digitales (**GPIO**)  
- Conceptos de **PWM** y *duty cycle*  
- Principios de funcionamiento de un **Puente H**  

---

## 🔧 5) Procedimiento e Instalación

### **Montaje del Hardware**
1. Conectar la ESP32 al lado del motor A del L298N.  
2. Utilizar la fuente externa para la alimentación del L298N (pin **+12V** y **GND**).  

### **Cableado**
- Conectar los pines de dirección (**IN1**, **IN2**) a pines digitales de la ESP32 (ej. GPIO 25 y 26).  
- Conectar el pin de velocidad (**ENA**) a un pin con capacidad PWM de la ESP32 (ej. GPIO 27).  
- Conectar el motor a las salidas **OUT1/OUT2**.  

### **Carga secuencial de Código**
Cargar cada uno de los tres códigos de forma individual para verificar la funcionalidad (dirección, velocidad fija y aceleración/desaceleración).

---

## 💻 5.1) Código de Programación

### 🔹**Etapa 1 – Control de Dirección Simple (Adelante y Atrás) 🔄**

// Pines de control para el Motor
const int IN1 = 25; // Dirección 1
const int IN2 = 26; // Dirección 2

void setup() {
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
}

void loop() {
  // 1. Gira hacia Adelante (HIGH, LOW)
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  delay(3000);

  // 2. Detiene el motor (LOW, LOW)
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  delay(1000);

  // 3. Gira hacia Atrás (LOW, HIGH)
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  delay(3000);

  // 4. Detiene el motor (LOW, LOW)
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  delay(1000);
}




### 🔹**Etapa 2 – Control de Velocidad Fija con PWM (50%) ⚡**

// Parámetros PWM de la ESP32
const int freq = 5000;      // Frecuencia PWM (5 kHz)
const int ledChannel = 0;   // Canal PWM a usar (0-15)
const int resolution = 8;   // Resolución de 8 bits (0-255)
const int dutyCycle = 127;  // 50% de velocidad (127 de 255)

// Pines de control
const int IN1 = 25; // Dirección 1
const int IN2 = 26; // Dirección 2
const int ENA = 27; // Habilitación/Velocidad (PWM)

void setup() {
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);

  ledcSetup(ledChannel, freq, resolution);
  ledcAttachPin(ENA, ledChannel);
}

void loop() {
  // 1. Gira Adelante a 50% de velocidad
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  ledcWrite(ledChannel, dutyCycle);
  delay(4000);

  // Detener el motor
  ledcWrite(ledChannel, 0);
  delay(1000);
}



### 🔹**Etapa 3 – Secuencia de Aceleración y Desaceleración Gradual ⬆️⬇️**

// Pines y parámetros PWM
const int IN1 = 25;
const int IN2 = 26;
const int ENA = 27;
const int ledChannel = 0;
const int freq = 5000;
const int resolution = 8; // Max dutyCycle = 255

void setup() {
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  ledcSetup(ledChannel, freq, resolution);
  ledcAttachPin(ENA, ledChannel);

  // Establecer una dirección fija (Adelante)
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
}

void loop() {
  // 1. Acelera rápidamente a velocidad máxima (100%)
  ledcWrite(ledChannel, 255);
  delay(3000);

  // 2. Desaceleración gradual (100% a 0)
  for (int dutyCycle = 255; dutyCycle >= 0; dutyCycle -= 5) {
    ledcWrite(ledChannel, dutyCycle);
    delay(50);
  }

  delay(4000); // Motor detenido por 4s antes de repetir
}


## **📊 6) Resultados**

| Etapa | Descripción | Resultado |
| :--- | :--- | :--- |
| **1️⃣ Dirección** | Control del sentido de giro (adelante/atrás) | ✅ Reversibilidad lograda |
| **2️⃣ Velocidad Fija** | Control de velocidad con PWM | ✅ Velocidad estable al 50% |
| **3️⃣ Acel./Desac.** | Secuencia de máxima velocidad seguida de desaceleración gradual | ✅ Transición de velocidad controlada |

🔍 Se demostró el **control total** sobre la potencia (**velocidad**) y el sentido de giro (**dirección**) de un motor DC, validando el uso del módulo **L298N** como interfaz de potencia.

---

## 🎥 7) Videos de Funcionamiento

### ▶️ Video 1 – Aprendiendo a usar un motor

<div align="center">
  <iframe src="https://iberopuebla-my.sharepoint.com/personal/203032_iberopuebla_mx/_layouts/15/embed.aspx?UniqueId=1f14984d-9644-4f31-82d3-270bf94e850e&embed=%7B%22ust%22%3Atrue%2C%22hv%22%3A%22CopyEmbedCode%22%7D&referrer=StreamWebApp&referrerScenario=EmbedDialog.Create" width="640" height="360" frameborder="0" scrolling="no" allowfullscreen title="motor_1.mp4"></iframe>
  <p><em>Video 1. Aprendiendo a usar un motor DC.</em></p>
  <p>🔗 <a href="https://iberopuebla-my.sharepoint.com/:v:/g/personal/203032_iberopuebla_mx/EU2YFB9EljFPgtMnC_lOhQ4BJORseFZcSpRQcb3aITU0og?e=jDeAxC&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D">Ver video</a></p>
</div>

### ▶️ Video 2 – Secuencia de Aceleración y Desaceleración

<div align="center">
  <iframe src="https://iberopuebla-my.sharepoint.com/personal/203032_iberopuebla_mx/_layouts/15/embed.aspx?UniqueId=a40bd434-ffd9-49bb-b802-1c7b38d05265&embed=%7B%22ust%22%3Atrue%2C%22hv%22%3A%22CopyEmbedCode%22%7D&referrer=StreamWebApp&referrerScenario=EmbedDialog.Create" width="640" height="360" frameborder="0" scrolling="no" allowfullscreen title="motor_aumento_disminucion.mp4"></iframe>
  <p><em>Video 2. Observación de la aceleración a velocidad máxima y el frenado progresivo con el ciclo 'for'.</em></p>
  <p>🔗 <a href="https://iberopuebla-my.sharepoint.com/:v:/g/personal/203032_iberopuebla_mx/ETTUC6TZ_7tJuAIcezjQUmUB7DQc6xwFXwyhb8DLkVwr-Q?e=gUG3TL&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D">Ver video</a></p>
</div>