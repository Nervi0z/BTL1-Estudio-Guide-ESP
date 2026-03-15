# Workflow — Análisis de un Correo Sospechoso

Proceso paso a paso para analizar un correo de phishing de forma estructurada. Adapta el nivel de profundidad según el contexto: un correo de spam genérico no requiere el mismo análisis que un spearphishing dirigido a un ejecutivo.

Trabaja siempre desde un entorno aislado. Si tienes el correo como archivo `.eml` o `.msg`, mejor — preserva las cabeceras completas y puedes analizarlo offline.

---

## Paso 1 — Evaluación inicial (sin hacer clic en nada)

Lee el correo sin interactuar con ningún elemento.

**Remitente:**
- ¿El nombre mostrado coincide con la dirección real? (`Display Name <real@domain.com>`)
- ¿El dominio del remitente es el esperado o un lookalike?

**Asunto:**
- ¿Es genérico, alarmista o inesperado?
- ¿Contiene errores o caracteres inusuales?

**Cuerpo:**
- ¿Hay urgencia artificial, amenazas o peticiones fuera de lo normal?
- ¿Saludos genéricos en lugar de tu nombre?
- ¿El estilo visual y de redacción coincide con comunicaciones anteriores de esa entidad?

**Enlaces (hover, sin clic):**
- Pasa el cursor sobre cada enlace y compara el texto mostrado con la URL real que aparece en la barra de estado.

Con esta evaluación inicial ya puedes tener una hipótesis clara: legítimo, sospechoso o malicioso con alta probabilidad. El resto del análisis confirma o refuta.

---

## Paso 2 — Análisis de cabeceras

Extrae el bloque completo de cabeceras y pégalo en MxToolbox o Google Messageheader.

1. **Traza la ruta**: sigue las entradas `Received:` de abajo hacia arriba. Identifica la IP del servidor de origen real.

2. **Analiza la IP de origen**: búscala en AbuseIPDB, VirusTotal y OTX. ¿Está reportada? ¿En qué categorías?

3. **Revisa autenticación**: SPF, DKIM y DMARC. Cualquier `fail` es relevante. Un `pass` en todos no garantiza legitimidad (el atacante puede tener su propio dominio bien configurado), pero un `fail` es una señal clara.

4. **Compara `From:`, `Reply-To:` y `Return-Path:`**: si difieren, documéntalo. Es una táctica común para que las respuestas vayan a una cuenta controlada por el atacante.

---

## Paso 3 — Extracción y análisis de URLs

Lista todas las URLs únicas del cuerpo. Defángalas para documentarlas.

Para cada URL:
1. Busca el dominio en VirusTotal y URLhaus
2. Consulta el historial WHOIS: ¿fue registrado recientemente?
3. Envía la URL a URLScan.io para ver captura de pantalla y análisis sin riesgo
4. Si es un acortador, expande primero la URL antes de analizarla

Si una URL es desconocida pero sospechosa y necesitas ver el comportamiento completo, usa Any.Run o Triage.

---

## Paso 4 — Análisis de adjuntos

**No abrir directamente bajo ningún concepto.**

1. Calcula SHA256 (y MD5 si la plataforma lo requiere)
2. Busca el hash en VirusTotal — revisa detección, nombre de la familia de malware y pestaña Behavior si hay análisis de sandbox
3. Verifica el tipo real del archivo con `file` (Linux) o comprobando los magic bytes
4. Si el hash es desconocido y tienes sospecha fundada: súbelo a un sandbox (Any.Run, Hybrid Analysis, Triage)

Si el archivo tiene contraseña y la contraseña viene en el cuerpo del correo, es casi siempre un intento de evadir el escaneo automático. Documéntalo como indicador en sí mismo.

---

## Paso 5 — Consolidación de IOCs y veredicto

Reúne todos los indicadores encontrados:

| Tipo | Valor | Fuente | Reputación |
|------|-------|--------|------------|
| IP | `185.220.101.45` | Header `Received:` | AbuseIPDB 97/100 |
| Dominio | `paypal-security[.]update.com` | Enlace en cuerpo | VT 12/94 |
| Hash SHA256 | `d41d8cd9...` | Adjunto `factura.exe` | VT 45/72 |
| Email | `noreply@paypal-security.update.com` | `From:` | — |

**Veredicto:** Malicioso / Sospechoso / Legítimo

Escribe un resumen de 2-3 frases explicando el razonamiento: qué artefactos confirman el veredicto y por qué.

---

## Paso 6 — Documentación

Documenta mientras analizas, no al final. Para cada hallazgo:
- Captura de pantalla o extracto relevante
- Herramienta usada y resultado obtenido
- Interpretación en una línea

Si estás en el examen BTL1, el informe final es parte de la puntuación. Un análisis brillante sin evidencia documentada no puntúa igual que uno bien respaldado.
