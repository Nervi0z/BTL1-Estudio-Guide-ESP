# Qué es BTL1 y cómo funciona el examen

## La certificación

BTL1 (Blue Team Level 1) es una certificación práctica de Security Blue Team orientada a roles de ciberdefensa. Lo que la diferencia de la mayoría de certificaciones de entrada es que no tiene preguntas de opción múltiple: el examen entero consiste en investigar un incidente simulado y documentar los hallazgos.

Está dirigida a perfiles que quieren demostrar que saben hacer el trabajo, no solo que conocen la teoría. Eso la hace especialmente valorada para roles de SOC Analyst y posiciones júnior en respuesta a incidentes.

---

## Formato del examen

- **Duración:** 24 horas continuas
- **Entorno:** Laboratorio virtual con múltiples máquinas (Windows, Linux, SIEM, etc.) y herramientas preinstaladas
- **Tarea:** Se te presenta un escenario de incidente. Tienes que investigarlo, analizarlo y documentar lo que encuentras
- **Entregable:** Un informe escrito con tus hallazgos, evidencias y respuestas a las preguntas del escenario

El informe no es secundario. Vale tanto como el análisis técnico. Un buen hallazgo que no está bien documentado no puntúa igual que uno que sí lo está.

---

## Dominios evaluados

El examen cubre seis áreas. Las secciones de esta guía están organizadas alrededor de ellas:

1. **Análisis de phishing** — identificación y disección de correos maliciosos
2. **Threat Intelligence** — contextualización de IOCs, TTPs y actores
3. **Forense digital** — análisis de disco y memoria
4. **Análisis SIEM** — investigación de eventos y alertas en Splunk
5. **Análisis de red** — análisis de capturas de tráfico con Wireshark/Tshark
6. **Respuesta a incidentes** — triaje y análisis en sistemas vivos

En el examen, estas áreas no aparecen separadas. Un escenario real cruza varias: puede que encuentres un IOC en los logs del SIEM, lo correlaciones con tráfico de red sospechoso y termines analizando un fichero en memoria. La guía está organizada por dominio para facilitar el estudio, pero durante el examen tendrás que conectar los puntos.

---

## Qué valoran los empleadores

BTL1 ha ganado reconocimiento rápido precisamente porque demuestra capacidad práctica. Para un responsable de contratación, un candidato con BTL1 ha demostrado que puede investigar un incidente, usar las herramientas del sector y escribir un informe coherente. Eso reduce el riesgo de contratar a alguien que sabe la teoría pero no ha tocado un PCAP en su vida.

Las áreas que evalúa — forense, SIEM, respuesta a incidentes, análisis de red — son las tareas diarias de un analista SOC Tier 1. No hay desconexión entre lo que se pide en el examen y lo que se hace en el trabajo.

---

## Nivel de entrada recomendado

BTL1 no es una certificación para partir desde cero absoluto. Antes del examen conviene tener claro:

- Fundamentos de redes: TCP/IP, DNS, HTTP, puertos comunes
- Manejo básico de Linux y Windows desde línea de comandos
- Qué es un SIEM y para qué sirve
- Conceptos básicos de análisis de malware y phishing

Si tienes lagunas en alguna de estas áreas, el módulo `00_Introduccion_BTL1` incluye recursos para cubrirlas antes de entrar en materia.
