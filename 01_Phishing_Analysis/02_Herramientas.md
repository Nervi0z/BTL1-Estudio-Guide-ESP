# Herramientas para Análisis de Phishing

Organizado por tipo de tarea. La mayoría son servicios online gratuitos — úsalos desde un entorno controlado cuando manejes artefactos potencialmente maliciosos.

---

## Reputación de IOCs

### VirusTotal
**[virustotal.com](https://www.virustotal.com/)**

Analiza URLs, IPs, dominios y hashes contra decenas de motores. Imprescindible.

Lo que más importa en un análisis de phishing:
- Pestaña **Relations**: dominios que resuelven a una IP, IPs a las que ha resuelto un dominio, URLs asociadas a un hash
- Pestaña **Community**: comentarios de otros analistas, a veces con contexto que los motores no dan
- **Passive DNS**: historial de resoluciones — útil para pivotar entre IOCs

Precaución: subir un archivo a VirusTotal lo hace visible públicamente. Si el archivo contiene información sensible, usa el hash solamente.

### URLhaus
**[urlhaus.abuse.ch](https://urlhaus.abuse.ch/)**

Base de datos de URLs asociadas a distribución de malware. Más específica que VT para URLs. Muestra el malware relacionado, estado (activo/inactivo) y tags de la campaña.

### AbuseIPDB
**[abuseipdb.com](https://www.abuseipdb.com/)**

Reputación de IPs. Muestra número de reportes, categorías de abuso (spam, C2, escaneo) y comentarios. Útil para la IP de origen del correo.

### OTX — AlienVault Open Threat Exchange
**[otx.alienvault.com](https://otx.alienvault.com/)**

Busca cualquier IOC y obtén "pulsos" — informes de la comunidad con IOCs relacionados, TTPs mapeadas a MITRE ATT&CK y contexto de campaña. Útil para saber si el IOC forma parte de una campaña conocida.

---

## Análisis de cabeceras

### MxToolbox Email Header Analyzer
**[mxtoolbox.com/EmailHeaders.aspx](https://mxtoolbox.com/EmailHeaders.aspx)**

Pega el bloque completo de cabeceras y las parsea: ruta de entrega, resultados SPF/DKIM/DMARC, retrasos entre saltos.

### Google Messageheader
**[toolbox.googleapps.com/apps/messageheader](https://toolbox.googleapps.com/apps/messageheader/)**

Similar. Más limpio visualmente para trazar la ruta y ver los resultados de autenticación de un vistazo.

---

## Análisis de URLs

### URLScan.io
**[urlscan.io](https://urlscan.io/)**

Visita la URL en un entorno aislado y te devuelve: captura de pantalla, IP final, dominios contactados durante la carga, tecnologías detectadas, hashes de archivos descargados. Permite ver qué hay detrás de un enlace sin ningún riesgo.

Para phishing, la captura de pantalla suele ser suficiente para confirmar si es una página de login falsa.

**Expansores de URL** — para acortadores (bit.ly, tinyurl): busca "url expander" online. Obtén la URL final antes de analizarla.

---

## Sandboxes — análisis dinámico

Cuando el hash es desconocido en VT o necesitas ver el comportamiento real del adjunto.

### Any.Run
**[any.run](https://any.run/)**

Sandbox interactivo. Puedes ver en tiempo real los procesos creados, conexiones de red y modificaciones al sistema mientras el archivo se ejecuta en una VM Windows. La versión gratuita cubre la mayoría de casos de BTL1.

### Hybrid Analysis
**[hybrid-analysis.com](https://www.hybrid-analysis.com/)**

Análisis estático + dinámico. Genera informes con TTPs mapeadas a MITRE ATT&CK, tráfico de red (PCAP descargable) y comparación con bases de datos de malware conocido.

### Triage
**[tria.ge](https://tria.ge/)**

Sandbox con soporte para Windows y Linux. Extracción de IOCs y mapeo ATT&CK. Versión gratuita generosa.

---

## Plataforma integrada

### PhishTool
**[phishtool.com](https://www.phishtool.com/)**

Integra análisis de cabeceras, URLs y adjuntos en una sola interfaz orientada específicamente a phishing. Tiene plan gratuito. Útil si quieres un flujo de trabajo centralizado en lugar de usar cada herramienta por separado.

---

## Regla de oro

Nunca hagas clic en un enlace ni abras un adjunto directamente en tu máquina. Usa siempre una VM aislada o los servicios online listados. Si trabajas con datos sensibles, evita subir archivos completos a servicios públicos — usa el hash.
