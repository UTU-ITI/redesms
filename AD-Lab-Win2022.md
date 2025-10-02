# Active Directory — Laboratorio con Windows Server 2022

**Materia:** Redes Microsoft  
**Objetivo:** que los estudiantes instalen, configuren y administren Active Directory Domain Services (AD DS) en un entorno controlado de laboratorio.

---

## 🖥️ 1. Requisitos y arquitectura de laboratorio

- **Hipervisores soportados en clase:**
  - **VirtualBox** (Oracle, libre, multiplataforma).
  - **Hyper-V** (Windows).
  - **VMware Workstation / ESXi**.
  - **Proxmox VE** (Linux, KVM/QEMU).
- **Máquinas necesarias:**
  - 1 VM Windows Server 2022 (DC01).  
  - Opcional: 1 VM adicional Windows Server 2022 (DC02 para replicación).  
  - Opcional: 1–2 VMs Windows 10/11 como clientes de dominio.
- **Configuración mínima para el DC:**
  - 2 CPU, 4 GB RAM, 40 GB disco.  
  - Tarjeta de red en modo **Red Interna** (VirtualBox/Proxmox) o **Virtual Switch interno** (Hyper-V).  
  - IP estática en el rango de laboratorio.  

**Ejemplo de dominio a usar:**  
```
contoso.local
```

---

## ⚙️ 2. Preparación del servidor

1. Asignar **IP estática** y configurar DNS apuntando a sí mismo:
   ```powershell
   New-NetIPAddress -InterfaceAlias "Ethernet0" -IPAddress 192.168.56.10 -PrefixLength 24 -DefaultGateway 192.168.56.1
   Set-DnsClientServerAddress -InterfaceAlias "Ethernet0" -ServerAddresses 192.168.56.10
   Rename-Computer -NewName "DC01" -Restart
   ```
   *(Ejemplo con VirtualBox red interna: 192.168.56.0/24)*

2. Verificar con:
   ```powershell
   ipconfig /all
   nslookup localhost
   ```

---

## 🏗️ 3. Instalación AD DS — GUI (Server Manager)

1. Abrir **Server Manager** → *Manage* → *Add Roles and Features*.  
2. Seleccionar **Active Directory Domain Services**.  
3. Completar wizard e instalar.  
4. En **Server Manager**, clic en *Promote this server to a domain controller*.  
5. Seleccionar **Add a new forest** → `contoso.local`.  
6. Configurar contraseña DSRM y confirmar instalación.  
7. El servidor se reinicia como **Domain Controller**.

---

## 🖥️ 4. Instalación AD DS — PowerShell

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Import-Module ADDSDeployment

$DSRM = Read-Host -AsSecureString "Ingrese DSRM password"

Install-ADDSForest `
  -DomainName "contoso.local" `
  -DomainNetbiosName "CONTOSO" `
  -InstallDNS `
  -SafeModeAdministratorPassword $DSRM `
  -Force
```

---

## 🔍 5. Comprobaciones

- Revisar DNS:  
  ```powershell
  nslookup contoso.local
  ```
- Estado del DC:  
  ```powershell
  dcdiag /v
  repadmin /replsummary
  ```

---

## 🗂️ 6. Diseño de OUs y Grupos (AGDLP)

- **Crear OU:**
  ```powershell
  New-ADOrganizationalUnit -Name "Students" -Path "DC=contoso,DC=local"
  ```
- **Crear grupo Global y Domain Local:**
  ```powershell
  New-ADGroup -Name "GG_Students" -GroupScope Global -GroupCategory Security -Path "OU=Groups,DC=contoso,DC=local"
  New-ADGroup -Name "DL_ClassroomFiles" -GroupScope DomainLocal -GroupCategory Security -Path "OU=Groups,DC=contoso,DC=local"
  ```
- **Agregar usuario a grupo:**
  ```powershell
  Add-ADGroupMember -Identity "GG_Students" -Members "student01"
  ```

---

## 🔑 7. Delegación de Control

- Usar el **Delegation of Control Wizard** en ADUC.  
- Delegar en la OU `Students` al grupo `Helpdesk`:  
  - Resetear contraseñas.  
  - Desbloquear cuentas.  
  - Crear usuarios.  

---

## 🏛️ 8. FSMO Roles

Ver propietarios:
```powershell
Get-ADForest | Select SchemaMaster,DomainNamingMaster
Get-ADDomain | Select RIDMaster,PDCEmulator,InfrastructureMaster
```

Transferir a otro DC:
```powershell
Move-ADDirectoryServerOperationMasterRole -Identity "DC02" -OperationMasterRole 0,1,2,3,4
```

---

## 📦 9. Buenas prácticas en laboratorio

- Mantener **2 DCs** en entornos productivos (1 basta en laboratorio).  
- Activar **AD Recycle Bin** para recuperar objetos.  
- No usar cuentas de administrador para tareas diarias.  
- Hacer **System State Backup** regularmente.  

---

## ✅ 10. Ejercicios prácticos (con checklist)

### Ejercicio 1 — Promoción de DC
- [ ] Configurar IP estática en la VM (VirtualBox/Proxmox/Hyper-V/VMware).  
- [ ] Instalar rol AD DS.  
- [ ] Crear bosque `lab.local`.  
- [ ] Comprobar con `dcdiag`.  

### Ejercicio 2 — AGDLP
- [ ] Crear OU `Students`.  
- [ ] Crear usuarios `student01..03`.  
- [ ] Crear grupos `GG_Students` y `DL_ClassroomFiles`.  
- [ ] Asignar permisos a carpeta compartida.  

### Ejercicio 3 — Delegación Helpdesk
- [ ] Crear grupo `Helpdesk`.  
- [ ] Delegar permisos de **reset de password** en OU `Students`.  
- [ ] Verificar con usuario de prueba.  

### Ejercicio 4 — FSMO
- [ ] Consultar roles FSMO en DC01.  
- [ ] Transferir PDC Emulator a DC02.  
- [ ] Confirmar el cambio.  

---

## 📚 Recursos recomendados
- Microsoft Docs — [AD DS Overview (Windows Server 2022)](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)  
- Microsoft Docs — [Install-ADDSForest cmdlet](https://learn.microsoft.com/en-us/powershell/module/addsdeployment/install-addsforest)  
- Microsoft Docs — [Delegation of Control Wizard](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/delegate-control)  
