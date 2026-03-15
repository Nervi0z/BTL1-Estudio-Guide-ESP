# Análisis de Phishing — Conceptos Clave

El phishing es el vector de acceso inicial más frecuente en incidentes reales. Tu trabajo como analista es determinar si un correo es malicioso y, si lo es, extraer los IOCs que permitan la detección, el bloqueo y el enriquecimiento de la investigación.

El análisis se divide en cuatro artefactos principales: cabeceras, cuerpo, URLs y adjuntos.

---

## Cabeceras del correo

Las cabeceras contienen la trazabilidad completa del mensaje. Se leen de abajo hacia arriba para seguir la ruta real.

### Campos críticos

**`Received:`** — Cada salto entre servidores añade una entrada. La más baja es el origen. Busca la IP del servidor de envío real, que puede no coincidir con el dominio del remitente.

**`From:`** — Puede estar falsificado. No confíes en él solo.

**`Reply-To:` y `Return-Path:`** — Si difieren del `From:`, es una señal. Los correos legítimos suelen tener consistencia entre estos tres campos.

**`Authentication-Results:`** — Aquí están los resultados de SPF, DKIM y DMARC. Son lo más importante de las cabeceras para detectar spoofing.

### SPF, DKIM y DMARC

| Mecanismo | Qué verifica | Resultado sospechoso |
|-----------|-------------|----------------------|
| SPF | Si la IP de envío está autorizada por el dominio | `fail` o `softfail` |
| DKIM | Firma digital del mensaje — que no fue alterado | `fail` |
| DMARC | Política sobre qué hacer si SPF o DKIM fallan | `fail` + política `reject` ignorada |

Un `DMARC fail` con política `reject` que llega igualmente a la bandeja de entrada indica que el servidor receptor no está aplicando la política — o que el correo pasó por una ruta alternativa.

---

## Cuerpo del mensaje

Lo que el usuario ve. Busca:

- Urgencia artificial: "tu cuenta será suspendida en 24h", "factura vencida"
- Saludos genéricos en lugar del nombre real del destinatario
- Errores ortográficos o de formato inconsistente con comunicaciones previas de la entidad suplantada
- Peticiones fuera de lo normal: credenciales, transferencias, datos personales
- Texto de enlace que no coincide con la URL real al pasar el cursor

---

## URLs y dominios

Nunca hagas clic directamente. Examina la URL real:

**Técnicas de engaño comunes:**
- Typosquatting: `paypaI.com` (i mayúscula), `arnazon.com`
- Subdominios falsos: `paypal.security-update-required.com` — el dominio real es `security-update-required.com`
- Acortadores de URL que ocultan el destino real
- IPs directas en lugar de nombres de dominio

**Defanging** — cuando documentes una URL sospechosa, desactívala para evitar clics accidentales:

```
http://evil.com/login.php  →  hxxp://evil[.]com/login.php
```

---

## Adjuntos

**Nunca abrir directamente.** Calcula el hash primero y busca reputación antes de cualquier otra acción.

Tipos de archivo que requieren atención inmediata:

- Ejecutables y scripts: `.exe`, `.scr`, `.bat`, `.ps1`, `.vbs`, `.js`
- Archivos comprimidos que pueden contenerlos: `.zip`, `.rar`, `.iso`, `.img`
- Documentos Office con macros habilitadas: `.docm`, `.xlsm`
- Doble extensión: `factura.pdf.exe` — Windows oculta la extensión real por defecto
- Archivos protegidos por contraseña (la contraseña viene en el cuerpo para evadir el escaneo automático)

---

## IOCs que extraer

Del análisis completo debes consolidar:

- IPs del servidor de envío real (cabeceras `Received:`)
- Dominios y URLs del cuerpo y cabeceras
- Hashes MD5 y SHA256 de los adjuntos
- Direcciones de correo del atacante (`From:`, `Reply-To:`, `Return-Path:`)
- Asunto del correo (útil para crear reglas de detección por patrón)
