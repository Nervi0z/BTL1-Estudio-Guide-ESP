# Estrategia para el examen BTL1

## La mentalidad correcta

BTL1 no pide que memorices comandos. Pide que investigues. La diferencia es importante: puedes tener todos los cheatsheets del mundo abiertos durante el examen, pero si no sabes qué pregunta estás intentando responder, los comandos no sirven de nada.

Antes de ejecutar cualquier cosa, hazte estas preguntas:
- ¿Qué estoy buscando?
- ¿Qué herramienta tiene sentido usar aquí?
- ¿Qué espero encontrar si mi hipótesis es correcta?

Esa secuencia — hipótesis, herramienta, validación — es lo que separa una investigación estructurada de ejecutar comandos al azar esperando que algo aparezca.

---

## Gestión de las 24 horas

24 horas parece mucho tiempo. No lo es si no tienes un plan.

**Primera hora — orientación:**
- Lee el escenario completo antes de tocar nada
- Identifica qué dominios están involucrados (red, memoria, SIEM, etc.)
- Anota las preguntas que tienes que responder
- Decide por dónde empezar según lo que tengas disponible

**Bloque principal — investigación:**
- Trabaja por hipótesis, no por herramienta
- Documenta mientras investigas, no al final. Si esperas al final para escribir, perderás detalle y tiempo
- Cada hallazgo relevante: captura de pantalla, comando usado, interpretación

**Última hora — informe:**
- No empieces el informe en la última hora. Debería estar casi listo para entonces
- Reserva ese tiempo para revisar que has respondido todas las preguntas del escenario
- Comprueba que cada afirmación tiene su evidencia asociada

---

## Cómo investigar

### Empieza por lo que tienes

No siempre hay un punto de entrada obvio. Revisa qué artefactos tienes disponibles: logs, PCAPs, imagen de disco, volcado de memoria. Eso te dice por dónde empezar.

### Conecta fuentes

Un incidente real cruza múltiples fuentes de datos. Si encuentras una IP sospechosa en los logs del SIEM, búscala también en el tráfico de red. Si ves un proceso anómalo en memoria, comprueba si hay artefactos relacionados en disco. Las correlaciones son lo que construye el timeline del incidente.

### Cuando te atascas

Si llevas tiempo en un punto sin avanzar, para. Revisa lo que ya tienes, relee el escenario y plantéate si hay otra vía de investigación. A veces la respuesta está en una fuente diferente a la que estás mirando.

### Falsos positivos

No todo lo que parece sospechoso lo es. Antes de concluir que algo es malicioso, comprueba si tiene una explicación legítima. Un proceso con un nombre raro puede ser software corporativo. Una conexión a un puerto inusual puede ser una aplicación legítima mal configurada. El contexto importa.

---

## El informe

El informe es parte de la puntuación, no un trámite. Estos son los errores más comunes:

**No poner evidencia.** Cada hallazgo necesita respaldo: una captura de pantalla, un extracto de log, un hash. "Encontré actividad sospechosa" sin evidencia no puntúa.

**No responder la pregunta directamente.** Lee cada pregunta del escenario y asegúrate de que tu respuesta la responde de forma explícita, no implícita.

**Escribir solo al final.** Documenta mientras investigas. Es más fácil y el resultado es más detallado.

**Ser impreciso con los IOCs.** Si identificas una IP maliciosa, un hash o un dominio, escríbelo exactamente. Los detalles técnicos tienen que ser precisos.

---

## Herramientas durante el examen

El entorno del examen tiene las herramientas preinstaladas. No necesitas instalar nada. Lo que sí necesitas es saber usarlas con eficiencia:

- **Splunk:** escribe las queries correctas desde el principio, no vayas por ensayo y error
- **Wireshark:** usa filtros de display para reducir el ruido antes de analizar
- **Volatility:** identifica el perfil correcto antes de lanzar plugins
- **Autopsy / TSK:** sabe dónde buscar artefactos Windows relevantes sin recorrer todo el disco

Cada módulo de esta guía incluye los comandos y filtros más habituales para cada herramienta. Úsalos como referencia rápida, no como sustituto de entender qué estás ejecutando.

---

## Práctica antes del examen

No entres al examen sin haber practicado en laboratorios reales. Los recursos más útiles para BTL1:

- [Blue Team Labs Online (BTLO)](https://blueteamlabs.online/) — laboratorios del mismo equipo que hace BTL1
- [CyberDefenders](https://cyberdefenders.org/) — casos prácticos de forense y análisis de red
- [TryHackMe](https://tryhackme.com/) — rutas de blue team con laboratorios guiados

El objetivo no es completar el máximo número de laboratorios, sino trabajar con cada herramienta hasta que no tengas que pensar en la sintaxis — solo en lo que estás buscando.
