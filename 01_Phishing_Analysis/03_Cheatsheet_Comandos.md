# Cheatsheet — Comandos para Análisis de Phishing

Referencia rápida para las tareas más comunes en la línea de comandos. Todos estos comandos se ejecutan en tu entorno de análisis aislado, nunca en producción.

---

## Hashing de archivos

El hash es lo primero que calculas antes de hacer cualquier otra cosa con un adjunto sospechoso.

| Tarea | Linux | Windows (PowerShell) |
|-------|-------|----------------------|
| Hash MD5 | `md5sum archivo.exe` | `Get-FileHash -Algorithm MD5 archivo.exe` |
| Hash SHA256 | `sha256sum archivo.exe` | `Get-FileHash -Algorithm SHA256 archivo.exe` |
| Hash SHA1 | `sha1sum archivo.exe` | `Get-FileHash -Algorithm SHA1 archivo.exe` |

SHA256 es el más usado en plataformas de reputación. Cálcula siempre SHA256 como mínimo.

---

## Identificación del tipo real de archivo

Las extensiones mienten. Verifica el tipo real antes de asumir qué es el archivo.

```bash
# Linux — usa magic bytes, no la extensión
file archivo_sospechoso.pdf
# Ejemplo de salida reveladora:
# archivo_sospechoso.pdf: PE32 executable (GUI) Intel 80-386
```

En Windows, habilita "Mostrar extensiones de nombre de archivo conocidas" en el Explorador de archivos. Sin esto, `factura.pdf.exe` se muestra como `factura.pdf`.

---

## Extracción de strings

Busca texto legible incrustado en archivos binarios: URLs, IPs, rutas, mensajes de error, nombres de funciones.

```bash
# Linux
strings archivo_sospechoso.exe

# Filtrar solo URLs
strings archivo_sospechoso.exe | grep -E "https?://"

# Filtrar IPs
strings archivo_sospechoso.exe | grep -E "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b"

# Guardar salida para revisar con calma
strings archivo_sospechoso.exe > strings_output.txt
```

En Windows, `strings.exe` de Sysinternals hace lo mismo:
```cmd
strings.exe archivo_sospechoso.exe
```

---

## Descarga controlada de artefactos

Solo en entorno aislado. Nunca ejecutes lo descargado.

```bash
# Descargar sin seguir redirecciones
curl -O --max-redirs 0 "hxxps://evil[.]com/payload.exe"

# Descargar guardando también las cabeceras HTTP de respuesta
curl -D headers.txt -O "https://evil.com/payload.exe"

# wget
wget "https://evil.com/payload.exe"
```

---

## Análisis de cabeceras desde archivo .eml

Si tienes el correo como archivo `.eml`:

```bash
# Ver cabeceras completas
cat correo.eml | head -100

# Extraer solo el bloque de cabeceras (hasta la primera línea en blanco)
sed '/^$/q' correo.eml

# Buscar campos específicos
grep -i "received:" correo.eml
grep -i "x-originating-ip:" correo.eml
grep -i "authentication-results:" correo.eml
grep -i "dkim-signature:" correo.eml
```

---

## Defanging rápido en terminal

Para documentar URLs e IPs de forma segura:

```bash
# Defang una URL
echo "https://evil.com/login.php" | sed 's/http/hxxp/g; s/\./[.]/g'
# → hxxp://evil[.]com/login[.]php

# Defang una IP
echo "185.220.101.45" | sed 's/\./[.]/g'
# → 185[.]220[.]101[.]45
```

---

## Consultas DNS rápidas

Para investigar dominios del correo sin visitarlos:

```bash
# Registro A (IP actual)
nslookup evil.com
dig A evil.com +short

# Registros MX (servidores de correo del dominio)
dig MX evil.com +short

# Registro TXT (SPF y otros)
dig TXT evil.com +short

# Nameservers
dig NS evil.com +short

# Resolución inversa de una IP
dig -x 185.220.101.45 +short
```

En Windows:
```cmd
nslookup -type=MX evil.com
nslookup -type=TXT evil.com
```
