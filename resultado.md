
fecha-nombrepc-resultado.toml

Ejemplo: `20250612-PCLAB01-Exito.toml`

Luego, deberá ser subido al servidor remoto mediante `scp`.

---

## ?? Instrucciones

1. Crear un script en PowerShell que:
   - Obtenga la fecha actual en formato `yyyymmdd`.
   - Obtenga el nombre del equipo (`hostname`).
   - Detecte si hay conexión con el Gateway predeterminado mediante `ping`.
   - Recoja la siguiente información del sistema:
     - Nombre del Sistema Operativo
     - Dirección IP y máscara
     - CPU (modelo)
     - Cantidad de RAM instalada
     - Capacidad del disco principal (C:)

2. Guardar esa información en un archivo `.toml` con el formato especificado.

3. Usar `scp` para enviar el archivo al servidor remoto:
