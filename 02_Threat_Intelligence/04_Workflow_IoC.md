# Workflow — Investigación de IOCs con CTI

Una vez extraídos los IOCs de un análisis (correo, logs, forense), el siguiente paso es enriquecerlos: contexto, riesgo, relaciones con otros indicadores y TTPs asociadas.

La clave es **pivotar**: cada IOC puede llevar a otro. Una IP lleva a un dominio, ese dominio a otros archivos descargados, esos archivos a más IPs. Documenta cada paso — el grafo de relaciones entre IOCs es parte de lo que explica el alcance del incidente.

---

## IP sospechosa

**1. Reputación**
- VirusTotal: ratio de detección, pestaña Community, Passive DNS (dominios que han resuelto a esta IP)
- AbuseIPDB: categorías de abuso, número de reportes, comentarios
- OTX: pulsos relacionados, TTPs asociadas

**2. Contexto de red**
- WHOIS de la IP: ASN, propietario, país, rango de red
- ¿Es un hosting conocido? ¿Un proveedor de VPN? ¿Un nodo Tor? El contexto cambia la interpretación

**3. Passive DNS — pivoting**
- VirusTotal → Relations: ¿qué dominios han resuelto a esta IP?
- Investiga cada dominio que parezca sospechoso

**4. Servicios expuestos (opcional)**
- Shodan/Censys: puertos abiertos, banners, servicios
- ¿Tiene el puerto 4444 abierto? ¿C2 típico de Metasploit. ¿Puerto 8080 con un panel de administración expuesto?

---

## Dominio sospechoso

**1. Reputación**
- VirusTotal: detección, URLs asociadas, Passive DNS
- URLhaus: si distribuye malware
- OTX: pulsos relacionados

**2. Registro**
- WHOIS: fecha de creación (¿registrado esta semana?), registrador, nameservers
- Un dominio registrado hace 3 días que simula ser el banco X es un indicador fuerte

**3. DNS actual e histórico**
- ¿A qué IP resuelve ahora? → investiga esa IP
- Passive DNS en VT: ¿ha resuelto a otras IPs en el pasado? ¿Cuáles?
- Subdominios asociados: pueden revelar más infraestructura

**4. Análisis de la URL**
- URLScan.io: captura de pantalla, IPs contactadas durante la carga, tecnologías detectadas
- ¿Es una página de login falsa? ¿Un panel de administración? ¿Un redirect a malware?

---

## Hash de archivo

**1. VirusTotal — análisis completo**

Es la fuente más importante para hashes. Revisa en orden:

- **Detection ratio**: ¿cuántos motores lo detectan? ¿Con qué nombre de familia?
- **First/Last seen**: ¿coincide la primera aparición con tu incidente?
- **Names**: ¿con qué nombres de archivo se ha visto? Un `invoice.exe` que se detecta como `Qakbot` es más contexto que solo el hash
- **Behavior tab**: procesos creados, conexiones de red establecidas, archivos modificados, TTPs de MITRE ATT&CK
- **Relations tab**: ¿dónde se descargó? ¿Desde qué URLs? ¿Está relacionado con otros archivos (dropper + payload)?

**2. Otras plataformas**
- OTX: pulsos relacionados con el hash
- MalwareBazaar: tags de familia, muestras relacionadas
- Hybrid Analysis: informe de sandbox alternativo con PCAP

**3. Si el hash es desconocido (0 detecciones en VT)**

No significa que sea limpio. Si tiene contexto sospechoso (vino en un correo de phishing confirmado, está en una ruta inusual), sube a sandbox para análisis dinámico. Documenta el razonamiento.

---

## URL completa

**1. Descomponer la URL**
- Extrae el dominio e investígalo con el workflow de dominios
- Extrae la IP a la que resuelve e investígala con el workflow de IPs

**2. Buscar la URL completa**
- VirusTotal, URLhaus y OTX: busca la URL exacta
- Si es un acortador, expande primero

**3. URLScan.io**
- Envía la URL completa
- Examina: ¿la URL final es diferente a la inicial (redirecciones)? ¿Qué dominios e IPs contacta la página? ¿Descarga algún archivo?

---

## Documentar el pivoting

Mantén una tabla o diagrama mientras investigas:

```
IP 185.220.101.45
  → AbuseIPDB: 97/100, categoría C2+Scanner
  → VT Passive DNS: resuelve a evil-domain.com, update-service.net
      → evil-domain.com: VT 12/94, registrado hace 4 días
          → URLScan: página de login falsa de Office365
      → update-service.net: URLhaus: distribución de QakBot
```

Esa cadena de relaciones es lo que construye el contexto del incidente y lo que hace valioso el informe final.
