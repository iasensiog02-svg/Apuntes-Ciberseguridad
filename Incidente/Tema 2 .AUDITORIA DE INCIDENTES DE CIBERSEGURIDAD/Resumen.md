1. El SOC: Estructura, Roles y Ciclo de Vida del Incidente

El **Centro de Operaciones de Seguridad (SOC)** es el núcleo de la protección de la información, cuyo objetivo principal es la **gestión de incidentes** para prevenir ataques y restaurar la operación rápidamente.

- **Jerarquía Organizativa:** Liderada por el **CISO** (estrategia y riesgos), seguido por el **Head of Security Operations** (coordinación del SOC), el **Head of Architecture & Engineering** (diseño de infraestructura técnica) y el área de **GRC** (cumplimiento de normativas como ISO 27001 o GDPR).
- **Analistas del Blue Team:**
    - **Nivel 1 (Tier 1):** Monitoriza alertas en tiempo real, abre tickets y realiza mitigaciones básicas como bloquear IPs o aislar equipos.
    - **Nivel 2 (Tier 2):** Realiza investigaciones profundas y propone remediaciones técnicas complejas.
    - **Nivel 3 (Tier 3/SME):** Expertos en **Threat Hunting** (búsqueda proactiva de amenazas no detectadas), ingeniería inversa de malware y respuesta ante incidentes críticos como brechas de datos.
- **Fases de Gestión:** Preparación, Identificación, Contención, Mitigación, Recuperación y Post-incidente.

2. Herramientas Técnicas de Monitorización y Respuesta

**Wazuh (SIEM y HIDS)**

Es una solución de código abierto para la detección de amenazas e integridad de archivos.

- **Requisitos e Instalación:** Requiere sistemas Linux de 64 bits con un mínimo de **8 GB de RAM y 4 núcleos** de CPU.
- **Arquitectura:** Los agentes en los terminales envían datos al servidor mediante **certificados SSL**. Se integra con la **Pila Elastic (ELK)**: Elasticsearch (motor de búsqueda), Logstash (filtrado de datos), Kibana (visualización) y Beats (agentes recolectores).
- **Respuesta Activa:** Permite automatizar acciones mediante scripts definidos en `ossec.conf`. Comandos típicos incluyen `firewall-drop` (bloqueo en iptables), `disable-account` y `host-deny`. Las respuestas se configuran con parámetros como `<location>` (local, server o all), `<level>` (gravedad mínima) y `<timeout>` (duración en segundos).

**Suricata (IDS/IPS de Red)**

Es un motor de alto rendimiento que inspecciona el tráfico mediante reglas.

- **Implementación Técnica:** Se instala en un sensor dedicado conectado a un puerto **SPAN (Switch Port Analyzer)**, lo que le permite ver una copia espejo de todo el tráfico de la red sin interferir en su velocidad.
- **Reglas de Suricata:** Se escriben en `/etc/suricata/rules/local.rules`. Constan de una **cabecera** (acción, protocolo, IPs/puertos origen y destino, dirección `->` o `<>`) y **opciones** como el mensaje (`msg`), el identificador único (`sid`) y la revisión (`rev`).
- **Funciones Avanzadas:** Soporta **inspección profunda de paquetes (DPI)** y protocolos como HTTP, TLS, DNS y SMB. Permite el uso de expresiones regulares (`pcre`) y **thresholding** para limitar la frecuencia de alertas y evitar la saturación del SIEM.

3. Inteligencia de Fuentes Abiertas (OSINT)

La metodología **OSINT** transforma datos públicos en conocimiento útil mediante un ciclo de: Requisitos, Identificación de fuentes, Adquisición, Procesamiento, Análisis y Presentación.

- **Buscadores Generales y Dorks:** Uso de operadores avanzados en Google como `intitle:"index of" inurl:ftp` para hallar servidores abiertos o `filetype:pdf` para extraer metadatos con herramientas como **Metagoofil**.
- **Buscadores Tecnológicos:** **Shodan** rastrea dispositivos por puertos como el 21 (FTP), 22 (SSH) o 3389 (RDP). **Censys** y **Zoomeye** complementan esta búsqueda de infraestructura expuesta.
- **Investigación de Identidad:** Herramientas como **Sherlock** o **OSRFramework** (módulos `usufy`, `mailfy`) localizan perfiles en cientos de redes sociales. Sitios como **Have I Been Pwned?** o **Dehashed** verifican si credenciales han sido filtradas en brechas de datos.
- **Análisis Forense y Legal:** **Wayback Machine** permite ver el histórico de una web. Para presentar pruebas ante un juez, **eGarante** emite certificados con firma electrónica que demuestran el contenido de una web en una fecha exacta.

4. Clasificación y Valoración de Incidentes

Los incidentes se clasifican según su impacto y peligrosidad para determinar los tiempos de respuesta del SOC.

- **Niveles de Impacto (Escala 0-5):**
    - **Crítico (5):** Ransomware activo, caída total de servicios o exfiltración masiva de datos.
    - **Bajo (1):** Actividad anómala leve o alertas aisladas.
- **Prioridad y Tiempos Máximos (SLA):** Un incidente de prioridad "Superior" debe atenderse en menos de **5 minutos**, mientras que uno de prioridad "Baja" tiene un margen de 1 hora.
- **Notificación:** Debe seguir un flujo escalonado, informando internamente al CISO y externamente a los **CSIRT** de referencia si la ley o la gravedad lo exigen.

5. Seguridad Física y Normativa ISO

La seguridad integral depende de proteger también el hardware y el entorno.

- **Riesgos Físicos:** Incluyen desastres naturales, fallos de suministro eléctrico (solucionados con **SAI/UPS** y tomas de tierra) y acceso físico no autorizado (mitigado con biometría y CCTV).
- **Controles Ambientales:** La temperatura ideal en un CPD es de **10ºC a 30ºC**. Ante temperaturas extremas, se recomienda usar aire acondicionado o sustituir discos **HDD por SSD** para mayor resistencia.
- **Estándares ISO:**
    - **ISO/IEC 27001 (Anexo A.11):** Define objetivos para áreas seguras y protección del equipamiento.
    - **ISO/IEC 27002 (Apartado 7):** Establece **14 controles genéricos**, incluyendo perímetros de seguridad, seguridad en el cableado y mantenimiento preventivo del hardware.
