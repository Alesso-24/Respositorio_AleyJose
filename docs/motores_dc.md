# 💡 Documentación de la Práctica – Control de Motor DC con ESP32 (PWM y Puente H)

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

<p align="center">
  <img src="../recursos/imgs/practicas/esp32_l298n/esquematico_motor.png" alt="Esquema de conexión ESP32 con L298N y un motor DC" width="600">
  <br><em>Figura 1. Esquema de conexión base de la ESP32 con el módulo L298N y un motor DC.</em>
</p>

---

## 💻 5.1) Código de Programación

### 🔹 Etapa 1 – Control de Dirección Simple (Adelante y Atrás) 🔄
```cpp
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
