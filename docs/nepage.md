# 📚 Documentación de Prácticas – ESP32 y Control de LED

> Proyecto académico de electrónica y programación con ESP32: encendido de LED mediante control directo, botón y Bluetooth.  
> Las prácticas fueron realizadas por Alessandro Reyes y Jose Góngora.

---

## 1) Resumen

- **Nombre del proyecto:** Control de LED con ESP32  
- **Equipo / Autor(es):** Alessandro Reyes, Jose Góngora  
- **Curso / Asignatura:** Electrónica / Microcontroladores  
- **Fecha:** 18/09/2025  
- **Descripción breve:** Se realizaron tres prácticas con ESP32: encendido de LED con parpadeo automático, control mediante botón y control remoto vía Bluetooth usando la app “Serial Bluetooth Terminal”. Se documenta el código, montaje físico y evidencia multimedia.

!!! tip "Consejo"
    Estas prácticas permiten introducirse al control de periféricos digitales con microcontroladores y comunicación inalámbrica básica.

---

## 2) Objetivos

**General:** Desarrollar habilidades en la programación de microcontroladores ESP32 y el control de dispositivos digitales (LED) con diferentes métodos.  

**Específicos:**
- Encender y apagar un LED con parpadeo automático.  
- Implementar control de LED mediante un botón.  
- Controlar un LED vía comunicación Bluetooth usando un smartphone.  
- Documentar el montaje, diagrama y evidencia práctica.

---

## 3) Alcance y Exclusiones

**Incluye:**  
- Montaje de circuitos en protoboard con ESP32 y LED.  
- Programación básica con Arduino IDE.  
- Documentación de código, fotos y video.  
- Diagramas de Tinkercad como guía visual.  

**No incluye:**  
- Diseño de PCB profesional.  
- Programación avanzada o manejo de interrupciones complejas.  
- Conexión de múltiples LEDs u otros periféricos.

---

## 4) Requisitos

**Hardware**
- 1 × ESP32  
- 1 × LED  
- 1 × Resistencia limitadora (220–330 Ω)  
- 1 × Pulsador (solo práctica botón)  
- Cables y protoboard  
- Fuente de alimentación USB 5V  

**Software**
- Arduino IDE  
- App Serial Bluetooth Terminal (solo práctica Bluetooth)  

**Conocimientos previos**
- Manejo básico de Arduino IDE  
- Conceptos de entradas y salidas digitales  
- Ley de Ohm para resistencias

---

## 5) Prácticas y Procedimiento

### **Práctica 1 – ESP32 + LED (Parpadeo automático)**

```cpp
const int led = 2;

void setup() {
  Serial.begin(115200);
  pinMode(led, OUTPUT);
}

void loop() {
  digitalWrite(led, 1);
  delay(1000);
  digitalWrite(led, 0);
  delay(1000);
}
