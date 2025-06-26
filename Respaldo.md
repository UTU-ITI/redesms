# 🧪 Práctica Integrada de Respaldo y Seguridad de Información

## 🎯 Objetivo

Realizar dos procedimientos de respaldo de información en entornos Windows y Linux/Remoto, aplicando buenas prácticas de seguridad informática.

---

## 📦 Parte 1: Respaldo manual en dispositivo USB

### 📝 Instrucciones:

1. Ejecutar un script en PowerShell que:
   - Obtenga las credenciales y datos de conexión desde un archivo `.env`.
   - Solicite al usuario insertar un **pendrive**.
   - Detecte automáticamente el dispositivo.
   - Realice el **respaldo de la base de datos local** (formato `.sql`).
   - Genere un archivo de **registro del respaldo** (formato `.txt`) con:
     - Fecha
     - Usuario
     - Base de datos respaldada
     - Unidad de destino
     - Nombre del archivo
2. Entregar físicamente el pendrive a la oficina del docente o asistente.

---

## 🌐 Parte 2: Respaldo remoto de registros vía SCP con autenticación SSH

### 📝 Instrucciones:

1. Crear un script PowerShell que:
   - Solicite al usuario de forma **interactiva**:
     - Usuario SSH
     - IP del servidor remoto
     - Ruta de destino
   - Busque y seleccione todos los **archivos de registro** del sistema de los **últimos 12 meses**.
     - Ruta sugerida: `C:\Windows\System32\winevt\Logs\` o según software instalado.
     - Filtrar por fecha de modificación (`LastWriteTime`).
   - Use el comando `scp` para transferir los archivos al servidor remoto.
   - La autenticación debe realizarse usando una **clave SSH privada** (preguntar ubicación si es necesario).

2. Verificar con el docente que el respaldo fue recibido correctamente.

---

## 🔐 Recomendaciones de seguridad

- No incluir contraseñas dentro del script.
- Usar claves SSH protegidas por passphrase.
- Verificar la integridad del respaldo antes de cerrar la práctica.
- El pendrive debe estar **rotulado, cerrado** y firmado en el protocolo de entrega.

---

## 📁 Ejemplo de archivo generado

**Nombre del archivo:** `20250612-PC01-Exito.toml`  
**Registro:** `registro_respaldo_20250612.txt`

---

## ✅ Criterios de evaluación

| Competencia                      | Evidencia esperada                           |
|----------------------------------|----------------------------------------------|
| Pensamiento crítico              | Manejo seguro y flexible del entorno         |
| Responsabilidad y procedimiento | Documentación completa y entrega correcta    |
| Dominio técnico                  | Script funcional y sintaxis correcta         |
| Comunicación                    | Registro del proceso en protocolo de respaldo |

---

## 📅 Fecha de entrega: _[completar por el docente]_

