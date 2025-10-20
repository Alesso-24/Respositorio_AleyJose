# 💡 **Documentación de la Práctica – Control de LED con ESP32 (Múltiples Modos)**

> 🧠 *Proyecto académico de introducción a la mecatrónica:*  
> Implementación de la placa **ESP32** para el control de un LED en tres modos distintos: temporizado, mediante interacción física (botón) y por comunicación inalámbrica (**Bluetooth Serial**).

---

## 🧭 **1) Resumen**

| **Elemento** | **Descripción** |
|---------------|----------------|
| **Nombre del proyecto:** | LED Multi-Control con ESP32 (Blink, Botón y Bluetooth) |
| **Equipo / Autor(es):** | [Tus Nombres] |
| **Curso / Asignatura:** | Introducción a la Mecatrónica / Programación de Microcontroladores |
| **Fecha:** | [Fecha de la práctica] |
| **Descripción breve:** | Se exploraron las funcionalidades básicas de la **ESP32** (GPIOs, temporización, lectura de entradas y comunicación inalámbrica) implementando tres programas que controlan un LED: parpadeo constante, encendido por pulsación de botón y control remoto por comandos de texto vía Bluetooth. |

> 💡 **Consejo:**  
> Esta práctica es fundamental para comprender la versatilidad de la ESP32 en la interacción con el entorno (inputs físicos) y la comunicación remota (Bluetooth).

---

## 🎯 **2) Objetivos**

**General:**  
Aplicar los conceptos básicos de programación de microcontroladores para controlar un actuador (LED) y procesar diferentes tipos de entradas (tiempo, señal digital y datos seriales).

**Específicos:**
- Controlar el tiempo de encendido/apagado del LED usando `delay()`.
- Leer el estado de un botón (entrada digital) y reflejarlo en el LED.
- Implementar la comunicación **Bluetooth Serial (SPP)**.
- Procesar los comandos de texto (`HIGH` / `LOW`) recibidos por Bluetooth.

---

## 📋 **3) Alcance y Exclusiones**

**Incluye:**
- Implementación de tres programas independientes cargados a la ESP32.  
- Uso del LED en **GPIO 2** y botón en **GPIO 4**.  
- Configuración y prueba de la comunicación Bluetooth Serial.  
- Código fuente para las tres etapas.

**No incluye:**
- Uso de interrupciones o temporizadores avanzados.  
- Diseño de PCB.  
- Control basado en Wi-Fi.

---

## ⚙️ **4) Requisitos**

### 🧰 **Hardware**
- 1 × Placa de desarrollo **ESP32**  
- 1 × LED de cualquier color  
- 1 × Resistencia limitadora (220 Ω)  
- 1 × Botón (pulsador)  
- 1 × Resistencia **Pull-down** (10 kΩ)  
- 1 × Protoboard y cables  
- Fuente de alimentación (5 VDC)  
- Smartphone con **Bluetooth** y aplicación *Bluetooth Serial*

### 📘 **Conocimientos previos**
- Programación en **C/C++ (Arduino IDE)**  
- Manejo de entradas y salidas digitales (GPIO)  
- Conceptos básicos de comunicación serial

---

## 🔧 **5) Procedimiento e Instalación**

1. **Montaje del Hardware:**  
   Conectar el **LED** al **GPIO 2** (con su resistencia limitadora) y el **Botón** al **GPIO 4** (con resistencia Pull-down a GND).

2. **Carga secuencial de Código:**  
   Cargar cada uno de los tres códigos de forma individual a la ESP32 para verificar su funcionamiento.

3. **Prueba funcional:**  
   - Etapa 1: Verificar el parpadeo de 1 s.  
   - Etapa 2: Verificar el encendido solo al presionar el botón.  
   - Etapa 3: Emparejar por Bluetooth y enviar comandos `HIGH` / `LOW`.

<p align="center">
  <img src="../recursos/imgs/practicas/esp32_led/esquematico_base.png" alt="Esquema de conexión base ESP32 LED y Botón" width="600">
  <br><em>Figura 1. Esquema de conexión base del LED (GPIO 2) y Botón (GPIO 4) a la ESP32</em>
</p>

---

## 💻 **5.1) Código de Programación**

### 🔹 **Etapa 1 – LED Parpadeante Simple (Blink) ⏳**

!!! tip "Consejo"
    Este proyecto sirve como introducción al uso del 555 como generador de señales periódicas.

---



🔹 Etapa 2 – Control del LED con Botón 🔘
El LED se enciende mientras el botón está siendo presionado.

!!! tip "Consejo"
    Este proyecto sirve como introducción al uso del 555 como generador de señales periódicas.

---



🔹 Etapa 3 – Control del LED por Bluetooth Serial 📲
El LED se controla enviando el texto HIGH o LOW desde una app Bluetooth.

/***********************************************************************
 *  LED + Bluetooth Serial – ESP32
 *  Descripción: Control remoto del LED mediante comandos Bluetooth.
 ***********************************************************************/
!!! tip "Consejo"
    Este proyecto sirve como introducción al uso del 555 como generador de señales periódicas.

---

📊 6) Resultados
Etapa	Descripción	Resultado
1️⃣ Blink	Control temporizado del LED	✅ Precisión de 2 s por ciclo
2️⃣ Botón	Control físico con entrada digital	✅ Funcionamiento estable
3️⃣ Bluetooth	Control remoto vía comandos	✅ Comunicación correcta

🔍 Se demostró la capacidad de la ESP32 para manejar tareas de temporización, entradas digitales y comunicación inalámbrica mediante Bluetooth.

<p align="center"> <img src="../recursos/imgs/practicas/esp32_led/armado_1.png" alt="Montaje físico ESP32 con LED y Botón" width="300"> <br><em>Figura 2. Montaje físico – Vista general con ESP32, LED y botón</em> </p> <p align="center"> <img src="../recursos/imgs/practicas/esp32_led/app_bluetooth.png" alt="App Bluetooth Serial" width="300"> <br><em>Figura 3. Captura de la app Bluetooth Serial</em> </p>
🎥 7) Videos de Funcionamiento
▶️ Video 1 – Control Simple de LED (Blink)
<div align="center"> <iframe src="[ENLACE_DE_TU_VIDEO_1]" width="800" height="450" frameborder="0" allowfullscreen></iframe> <p><em>Video 1. LED parpadeando con tiempos fijos.</em></p> <p>🔗 <a href="[ENLACE_DE_TU_VIDEO_1]">Ver video</a></p> </div>
▶️ Video 2 – Control de LED con Botón
<div align="center"> <iframe src="[ENLACE_DE_TU_VIDEO_2]" width="800" height="450" frameborder="0" allowfullscreen></iframe> <p><em>Video 2. El LED se enciende solo mientras se mantiene presionado el botón.</em></p> <p>🔗 <a href="[ENLACE_DE_TU_VIDEO_2]">Ver video</a></p> </div>
▶️ Video 3 – Control de LED por Bluetooth
<div align="center"> <iframe src="[ENLACE_DE_TU_VIDEO_3]" width="800" height="450" frameborder="0" allowfullscreen></iframe> <p><em>Video 3. Control remoto del LED enviando HIGH/LOW vía Bluetooth.</em></p> <p>🔗 <a href="[ENLACE_DE_TU_VIDEO_3]">Ver video</a></p> </div>