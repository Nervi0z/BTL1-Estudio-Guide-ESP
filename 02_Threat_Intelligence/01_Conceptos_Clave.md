# Threat Intelligence — Conceptos Clave

La Inteligencia de Amenazas (CTI) es el contexto que convierte un dato en algo útil. Una IP sin contexto es ruido. Esa misma IP con historial de C2, campaña asociada y TTPs documentadas es inteligencia accionable.

En BTL1 no se pide ser analista de CTI senior, pero entender estos conceptos marca la diferencia entre un informe que dice "se encontró actividad sospechosa" y uno que dice "el actor usó T1566.001 para el acceso inicial y T1059.001 para la ejecución".

---

## IOCs vs TTPs

### Indicadores de Compromiso (IOCs)

Evidencia observable de actividad maliciosa. Son el nivel más básico de la inteligencia táctica.

Tipos comunes:
- IPs de servidores C2, phishing o escaneo
- Dominios y URLs maliciosas
- Hashes de archivos maliciosos (MD5, SHA1, SHA256)
- Direcciones de correo del atacante
- Rutas de archivo, claves de registro o mutex creados por malware
- User-Agents o patrones de tráfico específicos

**Limitación:** los IOCs son fáciles de cambiar para el atacante. Una IP de C2 puede rotarse en horas. Son útiles para detección y bloqueo inmediato, pero no para entender al adversario.

### Tácticas, Técnicas y Procedimientos (TTPs)

Describen el *comportamiento* del atacante, no artefactos concretos.

- **Táctica:** el objetivo de una acción (ej. `Initial Access`, `Persistence`, `Exfiltration`)
- **Técnica:** el método usado para lograr esa táctica (ej. `Phishing`, `Registry Run Keys`)
- **Procedimiento:** la implementación concreta observada (ej. un script PowerShell específico que descarga y ejecuta un payload desde un dominio DGA)

Las TTPs son mucho más difíciles de cambiar que los IOCs. Detectar comportamiento en lugar de artefactos es lo que hace robustas las reglas de detección.

---

## La Pirámide del Dolor

Creada por David J. Bianco. Ilustra qué tipos de indicadores causan más "dolor" al atacante cuando los defensores los detectan o bloquean.

```
        /\
       /  \   TTPs              ← Máximo dolor para el atacante
      /----\
     / Tools \                  ← Herramientas específicas
    /----------\
   / Host Artifacts \           ← Artefactos en el sistema
  /--------------\
 / Network Artifacts \          ← Patrones de tráfico
/---------\
    IPs / Dominios              ← Fácil de cambiar
    Hashes                      ← Trivial de cambiar
```

Bloquear un hash es útil hoy. Detectar el comportamiento (TTP) sigue siendo útil aunque el atacante cambie todas sus herramientas.

---

## Tipos de inteligencia

Para BTL1 los relevantes son dos:

**Táctica** — IOCs concretos para detección y bloqueo inmediato. Lo que usas en el día a día de un SOC.

**Operacional** — TTPs y comportamiento del adversario. Útil para entender el alcance de un incidente, anticipar movimientos y diseñar detecciones más robustas.

(La inteligencia estratégica, sobre el panorama de amenazas a largo plazo, es para dirección y está fuera del alcance de BTL1.)

---

## El ciclo de investigación

En un análisis de BTL1 sigues informalmente este proceso:

1. **¿Qué necesito saber?** — lo define el escenario del examen
2. **Recolección** — logs, cabeceras, resultados de herramientas, artefactos
3. **Procesamiento** — extraer IOCs, normalizar datos
4. **Análisis** — buscar en plataformas CTI, correlacionar, identificar TTPs
5. **Conclusión** — veredicto y resumen para el informe

La diferencia entre un analista junior y uno con experiencia está en el paso 4: saber qué pregunta hacerle a cada herramienta.
