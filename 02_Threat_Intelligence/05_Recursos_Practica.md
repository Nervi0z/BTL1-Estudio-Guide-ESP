# Recursos de Práctica — Threat Intelligence

---

## Plataformas con laboratorios

**[CyberDefenders](https://cyberdefenders.org/)** — los retos de CTI aquí son los mejores para practicar pivoting entre IOCs. Muchos incluyen análisis de campañas completas donde tienes que correlacionar IPs, dominios, hashes y TTPs.

**[Blue Team Labs Online (BTLO)](https://blueteamlabs.online/)** — retos que combinan CTI con forense y análisis de red, parecido al formato del examen BTL1.

**[TryHackMe](https://tryhackme.com/)** — salas de Threat Intelligence y la ruta "SOC Level 1" que cubre MITRE ATT&CK, plataformas CTI y análisis de IOCs. Buen punto de partida si partes desde cero.

---

## Recursos clave para MITRE ATT&CK

**[attack.mitre.org](https://attack.mitre.org/)** — la fuente. Dedica tiempo a leer las páginas de las técnicas más frecuentes en BTL1 (listadas en `02_MITRE_ATTACK.md`). No para memorizar IDs, sino para entender qué artefactos producen y cómo detectarlas.

**[ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)** — practica creando capas con las TTPs de un incidente simulado. Es una habilidad que se usa en informes reales.

**[Sigma Rules en GitHub](https://github.com/SigmaHQ/sigma)** — repositorio de reglas de detección mapeadas a ATT&CK. Útil para ver cómo se traduce una TTP a una regla de SIEM concreta.

---

## Fuentes de inteligencia para mantenerse al día

Leer análisis de campañas reales es la forma más rápida de interiorizar cómo se usa CTI en la práctica:

- [Mandiant / Google Threat Intelligence Blog](https://cloud.google.com/blog/topics/threat-intelligence)
- [CrowdStrike Blog](https://www.crowdstrike.com/blog/)
- [Cisco Talos](https://blog.talosintelligence.com/)
- [Unit 42 — Palo Alto Networks](https://unit42.paloaltonetworks.com/)
- [SANS ISC Diary](https://isc.sans.edu/) — más corto y frecuente, bueno para el día a día

Todos publican análisis con IOCs, TTPs mapeadas a ATT&CK y contexto de campaña. Leer uno a la semana es suficiente para mantener el ritmo.

---

## Fuentes de IOCs y feeds

**[abuse.ch](https://abuse.ch/)** — agrupa URLhaus, MalwareBazaar, Feodo Tracker y ThreatFox. Para practicar investigación de IOCs con datos reales.

**[OTX](https://otx.alienvault.com/)** — explora pulsos recientes para ver cómo se estructura la inteligencia y qué IOCs están activos.

**Twitter/X** — `#ThreatIntel`, `#CTI`, `#DFIR`, `#Malware`. Los hilos de análisis de campaña publicados por investigadores son muy didácticos y están a tiempo real.
