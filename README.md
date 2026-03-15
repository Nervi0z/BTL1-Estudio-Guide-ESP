# Guía Práctica BTL1 — Blue Team Level 1

> Apuntes, cheatsheets y workflows en español para preparar la certificación BTL1 de Security Blue Team. Enfoque 100% práctico: qué hacer, cómo hacerlo y con qué herramienta.

<p align="center">
  <img src="https://img.shields.io/badge/Certificación-BTL1-0078D4?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Idioma-Español-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Estado-En_desarrollo-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Licencia-MIT-yellow?style=for-the-badge" />
</p>

---

## Qué es esto

Esta guía nació de la necesidad de tener en un solo sitio lo que realmente importa para el BTL1: comandos concretos, filtros reales, workflows paso a paso y referencias directas a las herramientas del examen.

No es un resumen del temario oficial. Es una referencia de uso práctico pensada para consultar mientras trabajas en un laboratorio, no para leer de corrido.

El examen BTL1 dura 24 horas, es completamente práctico y termina con un informe. Esta guía está estructurada para ayudarte en ambas partes: la investigación técnica y la documentación de hallazgos.

---

## Para quién

- Estás preparando activamente la certificación BTL1
- Trabajas en un SOC y quieres tener referencias rápidas a mano
- Estás empezando en blue team y buscas una base práctica en español

Se asume conocimiento básico de redes, Windows/Linux y conceptos fundamentales de seguridad. Si partes de cero, empieza por el módulo `00_Introduccion_BTL1`.

---

## Estructura

| Módulo | Contenido |
|--------|-----------|
| [`00_Introduccion_BTL1`](./00_Introduccion_BTL1/) | Formato del examen, mentalidad, estrategia y gestión del tiempo |
| [`01_Phishing_Analysis`](./01_Phishing_Analysis/) | Cabeceras de correo, análisis de URLs, adjuntos maliciosos |
| [`02_Threat_Intelligence`](./02_Threat_Intelligence/) | IOCs, TTPs, MITRE ATT&CK, plataformas de inteligencia |
| [`03_Digital_Forensics`](./03_Digital_Forensics/) | Adquisición de evidencia, artefactos Windows/Linux, memoria, disco |
| [`04_SIEM_Analysis`](./04_SIEM_Analysis/) | Splunk SPL, búsquedas comunes, correlación de eventos |
| [`05_Network_Analysis`](./05_Network_Analysis/) | Wireshark, Tshark, filtros, análisis de PCAPs, patrones maliciosos |
| [`06_Incident_Response`](./06_Incident_Response/) | Live response, contención, triaje en sistemas vivos |

---

## Herramientas cubiertas

**SIEM:** Splunk (SPL), Elastic Stack / KQL básico

**Red:** Wireshark, Tshark

**Memoria:** Volatility 2 y 3

**Disco:** Autopsy, The Sleuth Kit, FTK Imager, KAPE

**Malware / archivos:** VirusTotal, Hybrid Analysis, Any.Run, ExifTool

**File carving:** Scalpel, Foremost

**Threat Intel:** MITRE ATT&CK, URLhaus, AbuseIPDB

---

## Cómo usarla

Usa la tabla de módulos para ir directamente a lo que necesitas. Cada módulo tiene su propio índice con cheatsheets, workflows y recursos de práctica.

Los comandos están pensados para copiar y adaptar, no para memorizar. La práctica real va en BTLO, CyberDefenders o TryHackMe — esta guía es tu referencia mientras trabajas en los laboratorios.

---

## Contribuciones

Si encuentras un error, un comando desactualizado o tienes algo que añadir, abre un Issue. Las pull requests con contenido nuevo son bienvenidas siempre que mantengan el enfoque práctico.

---

## Aviso legal

El contenido se basa en experiencia personal y recursos de acceso público. La ciberseguridad cambia rápido — contrasta siempre con el syllabus oficial y la documentación de cada herramienta.

Este repositorio respeta estrictamente el NDA de Security Blue Team. No contiene preguntas filtradas, soluciones directas a escenarios del examen ni información propietaria de la certificación.

---

## Licencia

MIT — ver [`LICENSE`](./LICENSE)
