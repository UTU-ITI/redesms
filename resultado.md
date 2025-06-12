
fecha-nombrepc-resultado.toml

Ejemplo: `20250612-PCLAB01-Exito.toml`

Luego, deber� ser subido al servidor remoto mediante `scp`.

---

## ?? Instrucciones

1. Crear un script en PowerShell que:
   - Obtenga la fecha actual en formato `yyyymmdd`.
   - Obtenga el nombre del equipo (`hostname`).
   - Detecte si hay conexi�n con el Gateway predeterminado mediante `ping`.
   - Recoja la siguiente informaci�n del sistema:
     - Nombre del Sistema Operativo
     - Direcci�n IP y m�scara
     - CPU (modelo)
     - Cantidad de RAM instalada
     - Capacidad del disco principal (C:)

2. Guardar esa informaci�n en un archivo `.toml` con el formato especificado.

3. Usar `scp` para enviar el archivo al servidor remoto:
