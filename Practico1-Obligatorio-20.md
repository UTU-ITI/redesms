# 🔍 Evaluación Práctica - Diagnóstico y Solución de Problemas de Conectividad

**Duración:** 45 minutos  
**Puntaje Total:** 20 puntos  
**Criterios de Evaluación:**  
- Pensamiento crítico (identificación y análisis del problema).  
- Pensamiento computacional (uso eficiente de herramientas como `nmap`, `tcpdump`, `ping`, etc.).  
- Creatividad (soluciones alternativas, análisis de causas posibles).  
- Documentación clara y profesional del diagnóstico.

---

## ✅ Objetivo

Diagnosticar y solucionar fallos de conectividad simulados en una red de laboratorio, identificando correctamente la **capa del modelo OSI** afectada, utilizando herramientas de diagnóstico (`nmap`, `tcpdump`, `ping`, `ethtool`, etc.) y proponiendo **una solución viable**.

---

## 🧪 Escenario 1: Falla en Capa 1 - Problema físico (10 puntos)

**Situación:**
El equipo `pc-01` conectado al switch `sw-lab1` no responde a ningún intento de conexión. El equipo fue recién configurado con dirección IP estática. Otros equipos en la misma VLAN funcionan correctamente.

**Tareas:**
1. Describir los pasos para verificar el estado físico de la interfaz (`buscapares`, `ethtool`, luces del switch, etc.).  
2. Realizar una comprobación desde consola para validar conectividad a nivel físico.  
3. Indicar dos posibles causas físicas del fallo y cómo resolverlas.

> 💡 Sugerencia: considera cables dañados, interfaces apagadas, conectores mal crimpados.

---

## 🧪 Escenario 2: Falla en Capa 3 - Problema de enrutamiento (10 puntos)

**Situación:**
El servidor `dns-utu.lab` con IP `192.168.1.53` no puede ser alcanzado desde el equipo `pc-estudiante`, aunque el enlace físico y el ping a la puerta de enlace (`192.168.1.1`) funcionan.

**Tareas:**
1. Ejecutar un `ping`, `traceroute` y `ip route` para analizar el flujo de red.  
2. Diagnosticar si se trata de un problema de **ruteo** o de **configuración IP local**.  
3. Proponer una solución clara al problema encontrado.  
4. Justificar tu análisis con al menos una salida de consola (`ping`, `ip a`, o `ip r`).

> 💡 Pista: hay una ruta estática mal definida o faltante en el router.

## 🧾 Entregable

El informe debe incluir:

- Capturas de comandos utilizados.  
- Diagnóstico detallado para cada escenario.  
- Soluciones propuestas y justificación técnica.  
- Comentario reflexivo final: ¿qué estrategia te permitió detectar con mayor rapidez el problema en cada capa?

---

## 🧠 Evaluación por Competencias (40 puntos)

| Competencia                           | Descripción                                                                 | Puntaje |
|--------------------------------------|-----------------------------------------------------------------------------|---------|
| Pensamiento crítico                  | Capacidad para detectar y clasificar el tipo de fallo                       | 10      |
| Pensamiento computacional            | Elección adecuada de herramientas para cada capa (ping, nmap, tcpdump)     | 10      |
| Creatividad y propuestas de solución| Capacidad de proponer soluciones variadas y contextualizadas                | 10      |
| Claridad y evidencia técnica         | Presentación clara del informe y comandos capturados                        | 10      |

---

✨ *Se valorará la profundidad del análisis, la corrección técnica, y la documentación profesional.*
