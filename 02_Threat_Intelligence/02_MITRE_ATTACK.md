# MITRE ATT&CK

MITRE ATT&CK es una base de conocimiento pública que cataloga el comportamiento de atacantes reales. No es teoría — cada técnica está documentada con ejemplos de uso real por grupos de amenaza específicos.

Para blue team, ATT&CK sirve para tres cosas concretas: contextualizar hallazgos durante una investigación, diseñar detecciones basadas en comportamiento y comunicar con precisión qué hizo el atacante en el informe.

---

## Estructura

### Tácticas

Son las columnas de la matriz. Representan el *objetivo* de una acción del atacante, no el método. Las 14 tácticas de la matriz Enterprise, en orden cronológico en un ataque típico:

| ID | Táctica | Qué representa |
|----|---------|----------------|
| TA0043 | Reconnaissance | Recopilar información sobre el objetivo |
| TA0042 | Resource Development | Preparar infraestructura y herramientas |
| TA0001 | Initial Access | Entrar en la red |
| TA0002 | Execution | Ejecutar código malicioso |
| TA0003 | Persistence | Mantener acceso tras reinicios o cambios |
| TA0004 | Privilege Escalation | Obtener más permisos |
| TA0005 | Defense Evasion | Evitar ser detectado |
| TA0006 | Credential Access | Robar credenciales |
| TA0007 | Discovery | Entender el entorno interno |
| TA0008 | Lateral Movement | Moverse entre sistemas |
| TA0009 | Collection | Reunir datos de interés |
| TA0011 | Command and Control | Comunicar con la infraestructura del atacante |
| TA0010 | Exfiltration | Sacar datos fuera de la red |
| TA0040 | Impact | Destruir, interrumpir o manipular |

### Técnicas y sub-técnicas

Cada celda de la matriz es una técnica con un ID único: `T1566 — Phishing`.

Las sub-técnicas refinan la técnica con un decimal: `T1566.001 — Spearphishing Attachment`, `T1566.002 — Spearphishing Link`.

Cuando documentes un hallazgo, usa la sub-técnica si puedes identificarla — es más preciso y demuestra mayor profundidad de análisis.

### Procedimientos

Implementaciones concretas observadas en el mundo real. La página de cada técnica en ATT&CK lista ejemplos de grupos de amenaza que la han usado y cómo. Esto es útil cuando quieres entender qué artefactos buscar para detectar esa técnica.

---

## Cómo usarlo durante una investigación

El flujo habitual es:

1. Encuentras un artefacto o comportamiento sospechoso
2. Buscas en [attack.mitre.org](https://attack.mitre.org/) palabras clave relacionadas
3. Identificas la técnica o sub-técnica
4. Lees la página: descripción, procedimientos de grupos conocidos, detecciones sugeridas, mitigaciones
5. Documentas la TTP en tus notas con el ID y el artefacto que la evidencia

**Ejemplo:**
Encuentras un nuevo servicio de Windows creado por un proceso sospechoso. Buscas "windows service creation" en ATT&CK. Llegas a `T1543.003 — Create or Modify System Process: Windows Service`. La página te dice que se usa para `Persistence` y `Privilege Escalation`, y qué eventos de Windows registran esta actividad (Event ID 7045).

---

## ATT&CK Navigator

**[mitre-attack.github.io/attack-navigator](https://mitre-attack.github.io/attack-navigator/)**

Herramienta visual para trabajar con la matriz. Permite:
- Colorear las técnicas observadas en un incidente
- Marcar las que tienes cubiertas con detecciones
- Comparar capas (ej. cobertura actual vs TTPs de un grupo específico)
- Exportar la matriz anotada

En BTL1 no es obligatorio usarlo, pero para el informe final una capa del Navigator con las TTPs identificadas añade valor visual.

---

## Técnicas más frecuentes en BTL1

Estas técnicas aparecen en muchos de los escenarios del examen. Vale la pena leer su página en ATT&CK antes del examen:

| Técnica | ID | Por qué importa en BTL1 |
|---------|----|-------------------------|
| Phishing: Spearphishing Attachment | T1566.001 | Vector de acceso inicial más común |
| Phishing: Spearphishing Link | T1566.002 | Variante con enlace en lugar de adjunto |
| PowerShell | T1059.001 | Ejecución de scripts maliciosos |
| Windows Command Shell | T1059.003 | Comandos cmd.exe sospechosos |
| Registry Run Keys / Startup Folder | T1547.001 | Persistencia |
| Scheduled Task/Job | T1053.005 | Persistencia alternativa |
| OS Credential Dumping | T1003 | Robo de credenciales |
| Remote Services: SMB/Windows Admin Shares | T1021.002 | Lateral movement |
| Exfiltration Over C2 Channel | T1041 | Exfiltración |
| Application Layer Protocol: Web Protocols | T1071.001 | C2 por HTTP/HTTPS |
