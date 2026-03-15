# Herramientas para Threat Intelligence

Organizado por tipo de consulta. La mayoría son gratuitas con registro o tienen plan free suficiente para BTL1.

---

## Reputación e investigación de IOCs

### VirusTotal
**[virustotal.com](https://www.virustotal.com/)**

El punto de partida para cualquier IOC. Más allá del ratio de detección, lo que importa para CTI:

- **Pestaña Relations**: dominios que han resuelto a una IP, IPs a las que ha resuelto un dominio, URLs asociadas a un hash, archivos descargados desde una URL. Es el punto de pivoting más potente que tiene VT.
- **Pestaña Behavior**: si hay análisis de sandbox del archivo, muestra procesos, conexiones de red y TTPs mapeadas a MITRE ATT&CK.
- **Passive DNS**: historial completo de resoluciones. Clave para encontrar infraestructura relacionada que ya no está activa.
- **Pestaña Community**: comentarios de analistas. A veces dan contexto que los motores automatizados no ofrecen.

### AbuseIPDB
**[abuseipdb.com](https://www.abuseipdb.com/)**

Específico para IPs. Muestra número de reportes, categorías (spam, C2, escaneo, brute force) y comentarios con contexto. Útil para evaluar rápidamente el riesgo de una IP.

### URLhaus
**[urlhaus.abuse.ch](https://urlhaus.abuse.ch/)**

URLs asociadas a distribución de malware. Busca por URL, dominio o IP. Muestra el malware relacionado (si se conoce), estado (activo/offline) y tags de campaña.

### OTX — AlienVault Open Threat Exchange
**[otx.alienvault.com](https://otx.alienvault.com/)**

Plataforma colaborativa de CTI. Busca cualquier IOC y obtén "pulsos" — informes de la comunidad con IOCs agrupados, TTPs de MITRE ATT&CK asociadas y contexto de campaña. Útil para saber si un IOC forma parte de algo más grande.

### URLScan.io
**[urlscan.io](https://urlscan.io/)**

Analiza URLs de forma segura. Para CTI es especialmente útil por:
- IPs y dominios contactados durante la carga de la página (infraestructura adicional)
- Tecnologías detectadas (puede identificar kits de phishing conocidos)
- Hashes de archivos descargados por la página
- Captura de pantalla para ver el contenido sin riesgo

---

## Análisis de dominios e IPs

### WHOIS

Para cualquier dominio sospechoso, lo primero es verificar cuándo fue registrado y por quién.

```bash
# Linux
whois evil.com
whois 185.220.101.45

# Herramientas online
# whois.domaintools.com
# who.is
```

Señales de alerta:
- Dominio registrado en los últimos días o semanas
- Registrador de bajo coste o asociado a hosting de abuso conocido
- Servidores de nombres sospechosos o genéricos

### DNS y Passive DNS

Consultas DNS directas:
```bash
# Registro A actual
dig A evil.com +short

# Registros MX (servidores de correo)
dig MX evil.com +short

# Registros TXT (SPF y otros)
dig TXT evil.com +short

# Nameservers
dig NS evil.com +short

# Resolución inversa
dig -x 185.220.101.45 +short
```

Para historial de resoluciones (Passive DNS), usa la pestaña Relations de VirusTotal. Es la fuente más completa accesible sin coste.

### Shodan / Censys
**[shodan.io](https://www.shodan.io/)** / **[censys.io](https://search.censys.io/)**

Para una IP sospechosa: qué puertos tiene abiertos, qué servicios corre, qué banners expone. Útil para identificar si es un servidor de C2, un nodo Tor, un servidor VPN o infraestructura legítima mal atribuida.

La versión gratuita de Shodan es limitada pero suficiente para consultas básicas.

---

## Análisis de malware

### MalwareBazaar
**[bazaar.abuse.ch](https://bazaar.abuse.ch/)**

Base de datos de muestras de malware. Busca por hash, nombre de archivo, etiqueta o familia. Proporciona hashes adicionales (si el mismo malware se ha visto con otros nombres), tags y contexto de campaña.

### Hybrid Analysis
**[hybrid-analysis.com](https://www.hybrid-analysis.com/)**

Informes de análisis estático y dinámico con TTPs mapeadas a MITRE ATT&CK, tráfico de red (PCAP descargable) y comparación con familias conocidas.

---

## Intercambio de inteligencia

### MISP
**[misp-project.org](https://www.misp-project.org/)**

Estándar open-source para almacenar, compartir y correlacionar CTI. Usado en CERTs, ISACs y equipos de seguridad empresariales. En BTL1 probablemente no lo uses directamente, pero el concepto aparece en el examen — entiende para qué sirve y qué estructura tiene un evento MISP.

### Feodo Tracker
**[feodotracker.abuse.ch](https://feodotracker.abuse.ch/)**

Rastrea infraestructura C2 activa de familias específicas (Emotet, Dridex, QakBot). Útil para verificar si una IP está en el feed de C2 conocido.
