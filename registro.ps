# Script PowerShell: Diagnóstico del PC y exportación en formato TOML

# Obtener fecha y nombre del equipo
$fecha = Get-Date -Format "yyyyMMdd"
$nombrePC = $env:COMPUTERNAME

# Intentar hacer ping al Gateway
$gateway = (Get-NetRoute -DestinationPrefix "0.0.0.0/0").NextHop
$ping = Test-Connection -ComputerName $gateway -Count 1 -Quiet
if ($ping) {
    $estado = "Exito"
} else {
    $estado = "Fallo"
}

# Obtener información del sistema
$so = Get-CimInstance Win32_OperatingSystem
$ipInfo = Get-NetIPAddress -AddressFamily IPv4 | Where-Object {$_.PrefixOrigin -eq "Dhcp" -or $_.PrefixOrigin -eq "Manual"}
$cpu = Get-CimInstance Win32_Processor
$ram = [math]::Round($so.TotalVisibleMemorySize / 1024 / 1024, 2) # en GB
$disco = Get-CimInstance Win32_LogicalDisk -Filter "DeviceID='C:'"
$discoTotal = [math]::Round($disco.Size / 1GB, 2)

# Ruta y nombre de archivo de salida
$archivo = "$fecha-$nombrePC-$estado.toml"

# Crear contenido TOML
$contenido = @"
[info_general]
fecha = "$($fecha)"
nombre_pc = "$($nombrePC)"
estado_conexion = "$($estado)"

[sistema_operativo]
nombre = "$($so.Caption)"
version = "$($so.Version)"

[red]
ip = "$($ipInfo.IPAddress)"
mascara = "$($ipInfo.PrefixLength)"
default_gateway = "$($gateway)"

[hardware]
cpu = "$($cpu.Name)"
ram_gb = $ram
disco_c_gb = $discoTotal
"@

# Guardar archivo
$contenido | Out-File -FilePath $archivo -Encoding utf8

# (Opcional) Subir con SCP - Ajustar con tus datos reales
# scp $archivo usuario@IP:/ruta/de/destino/

Write-Output "Archivo generado: $archivo"
