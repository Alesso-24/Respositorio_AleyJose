# 📚 Documentación de la Práctica – Temporizador 555 en modo Astable

> Proyecto académico de electrónica básica: implementación de un oscilador astable con el CI 555 para hacer parpadear un LED.  
> Los cálculos y simulaciones se realizaron en base a la configuración estándar del 555.

---

## 1) Resumen

- **Nombre del proyecto:** Oscilador Astable con 555  
- **Equipo / Autor(es):** Alessandro Reyes, Jose Góngora, Sebastián Cortez  
- **Curso / Asignatura:** Electrónica / Circuitos Digitales  
- **Fecha:** 05/09/2025 (viernes pasado)  
- **Descripción breve:** Se diseñó un circuito con el temporizador 555 en modo astable para encender y apagar un LED cada 3–5 segundos, armado de forma física y documentado con evidencia en fotos y video.

!!! tip "Consejo"
    Este proyecto sirve como introducción al uso del 555 como generador de señales periódicas.

---

## 2) Objetivos

- **General:** Implementar un circuito oscilador astable con el CI 555 para controlar el parpadeo de un LED.  

- **Específicos:**
  - Diseñar el circuito con valores adecuados de resistencias y capacitores.  
  - Calcular teóricamente los tiempos alto y bajo de la señal.  
  - Verificar en la práctica el correcto parpadeo del LED.  
  - Comparar resultados teóricos y experimentales.  

---

## 3) Alcance y Exclusiones

- **Incluye:**  
  - Implementación en protoboard del 555 en modo astable.  
  - LED parpadeando con periodo de 3–5 segundos.  
  - Documentación de cálculos y resultados.  
  - Evidencia en fotos y video.  

- **No incluye:**  
  - Diseño de PCB.  
  - Simulación en software especializado.  
  - Implementación con microcontroladores.  

---

## 4) Requisitos

**Hardware**
- 1 × CI 555  
- 1 × Resistencia R1 = 1 kΩ  
- 1 × Resistencia R2 = 20 kΩ  
- 1 × Capacitor electrolítico C1 = 330 µF  
- 1 × LED + resistencia limitadora (330 Ω – 1 kΩ)  
- Fuente de alimentación (5–9 VDC)  
- Protoboard y cables  

**Conocimientos previos**
- Ley de Ohm y cálculo de resistencias  
- Funcionamiento del temporizador 555  
- Uso de protoboard y multímetro  

---

## 5) Procedimiento e Instalación

1. **Armar el circuito** según el diagrama:  
   ![Diagrama 555](./6b6515ed-f736-4f62-9028-4dc57124b880.png)  

2. **Cálculos teóricos:**  

   - Tiempo alto:  
     \[
     T_h = 0.693 \times (R1 + R2) \times C1
     \]  
     ≈ 4802 ms  

   - Tiempo bajo:  
     \[
     T_l = 0.693 \times R2 \times C1
     \]  
     ≈ 4574 ms  

   - Frecuencia:  
     \[
     f = \frac{1.44}{(R1 + 2R2) \times C1}
     \]  
     ≈ 0.106 Hz  

3. **Observación práctica:** El LED permanece encendido ~4.8 s y apagado ~4.6 s, cumpliendo con el requisito (3–5 s).  

---

## 6) Resultados

- ✅ LED parpadea dentro del rango esperado (aprox. 9.3 s de periodo total).  
- ✅ El comportamiento práctico coincide con las fórmulas.  
- ✅ El 555 demostró ser un generador confiable de pulsos de baja frecuencia.  

📸 **Fotos del montaje físico:**  
_(inserta aquí las imágenes con)_  
```markdown
![Foto montaje 1](./ruta/foto1.jpg)
![Foto montaje 2](./ruta/foto2.jpg)
