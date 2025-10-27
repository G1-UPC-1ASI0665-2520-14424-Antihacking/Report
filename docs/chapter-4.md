# **Capítulo IV: Resultados Consolidados**

## **4.1 Matriz de Vulnerabilidades**

| ID | Vulnerabilidad Identificada | Descripción Técnica | CVSS v3.1 | Impacto | Prioridad |
|----|-----------------------------|----------------------|------------|----------|------------|
| **VULN‑001** | Falta de cabecera **Strict‑Transport‑Security (HSTS)** | El servidor HTTPS no implementa la cabecera HSTS, permitiendo ataques de downgrade y SSL Stripping. | 6.5 (Medium) | Compromete la confidencialidad y permite ataques Man‑in‑the‑Middle (MitM). | Alta |
| **VULN‑002** | Ausencia de cabecera **X‑Frame‑Options** | No se restringe la carga del sitio en <iframe>, permitiendo **Clickjacking**. | 5.0 (Medium) | Puede llevar a acciones fraudulentas sobre usuarios legítimos. | Media |
| **VULN‑003** | Falta de cabecera **X‑Content‑Type‑Options** | Permite *MIME sniffing*, posible ejecución de contenido no intencionado como JavaScript. | 4.3 (Low) | Riesgo moderado de inyección de código. | Media |
| **VULN‑004** | Fuga de archivos de **backup y certificados (.pem, .jks, .tgz)** | Nikto detectó exposición de archivos sensibles en el servidor, incluyendo claves privadas y bases de datos. | 9.8 (Critical) | Compromiso total de la confidencialidad y autenticidad del sistema. | Crítica |
| **VULN‑005** | **Información de servidor expuesta** en cabecera HTTP (Server: nginx/1.24.0 Ubuntu) | Divulga versión y SO, facilitando fingerprinting para ataques dirigidos. | 3.7 (Low) | Aumenta la probabilidad de explotación selectiva de CVE. | Baja |
| **VULN‑006** | **Error 502 en /API y /APIS** (Reverse Proxy) | El backend de la API no responde correctamente, indicando mala configuración de proxy o restricción de acceso. | 6.0 (Medium) | Interrupción del servicio y posible filtrado inadecuado de solicitudes. | Media |


## **4.2 Evidencias Técnicas**

### **1. Nmap – Reconocimiento de Puertos**
- **Comando:** `nmap -p- -sV -sC -O -A 40.84.58.167`  
- **Resultado:** Identificación de 3 puertos abiertos (80, 443, 8020) y 32 041 filtrados.  
- **Tecnología detectada:** *nginx 1.24.0 (Ubuntu)*.  
![Evidencia Nmap](../evidencias/nmap_evidencia_1.png)



### **2. Curl – Redirección HTTPS**
- **Comando:** `curl -I tavolo.eastus2.cloudapp.azure.com`  
- **Resultado:** Código 301 (Moved Permanently), confirmando redirección forzada a HTTPS.  
- **Servidor:** nginx/1.24.0 (Ubuntu).  
![Evidencia Curl](../evidencias/curl_evidencia_1.png)



### **3. Sslscan – Validación TLS/SSL**
- **Comando:** `sslscan 40.84.58.167:443`  
- **Protocolos habilitados:** TLS 1.2 y 1.3.  
- **Criptografía:** ECC 256 bits, certificado válido (2025–2026).  
- **Conclusión:** Configuración TLS robusta sin vulnerabilidad Heartbleed.  
![Evidencia Sslscan](../evidencias/sslscan_evidencia_1.png)



### **4. WhatWeb – Fingerprinting**
- **Comando:** `whatweb -v https://40.84.58.167`  
- **Resultado:** Detección de *Vite App* sin CMS, infraestructura custom sobre Ubuntu.  
![Evidencia WhatWeb](../evidencias/whatweb_evidencia_1.png)



### **5. Nessus – Web Application Tests**
- **Host:** tavolo.eastus2.cloudapp.azure.com (40.84.58.167)  
- **Duración:** 28 minutos.  
- **Hallazgos:**  
  - Falta de HSTS, X‑Frame‑Options, y Content‑Security‑Policy.  
  - Exposición de versión del servidor nginx.  
![Evidencia Nessus 1](../evidencias/nessus_evidencia_1.png)  
![Evidencia Nessus 2](../evidencias/nessus_evidencia_2.png)  
![Evidencia Nessus 3](../evidencias/nessus_evidencia_3.png)



### **6. Gobuster – Enumeración de Directorios**
- **Comando:** `gobuster dir -u https://tavolo.eastus2.cloudapp.azure.com -w /usr/share/wordlists/dirb/common.txt --exclude-length 441`  
- **Hallazgos:**  
  - `/assets` → 301 (redirección válida).  
  - `/api` y `/apis` → 502 (Bad Gateway).  
- **Conclusión:** Evidencia de fallo en reverse proxy o backend de API.  
![Evidencia Gobuster](../evidencias/gobuster_evidencia_1.png)



### **7. Nikto – Escaneo Profundo**
- **Comando:** `nikto -h https://tavolo.eastus2.cloudapp.azure.com:443`  
- **Hallazgos:**  
  - Fuga crítica de archivos de backup y certificados (.pem, .jks, .tgz).  
  - Falta de cabeceras de seguridad (HSTS, X‑Frame‑Options, X‑Content‑Type‑Options).  
  - Posible riesgo BREACH por Content‑Encoding “deflate”.  
![Evidencia Nikto](../evidencias/nikto_evidencia_1.png)



## **4.3 Impacto en el Negocio**

### **1. Fuga de Información Crítica (VULN‑004)**
- **Impacto:** Compromiso de claves privadas, certificados y bases de datos.  
- **Consecuencia:** Pérdida de confianza de clientes y riesgo de suplantación de identidad digital.  
- **Efecto en el Negocio:** Daño reputacional y riesgo de sanción por incumplir normas de protección de datos.



### **2. Falta de Cabeceras de Seguridad (VULN‑001 – VULN‑003)**
- **Impacto:** Riesgo de Clickjacking, SSL Stripping y MIME Sniffing.  
- **Consecuencia:** Pérdida de integridad en las sesiones y exposición a ataques dirigidos.  
- **Efecto en el Negocio:** Afecta la percepción de seguridad y la confianza del usuario final.



### **3. Exposición de Información del Servidor (VULN‑005)**
- **Impacto:** Facilita ataques específicos por CVE.  
- **Consecuencia:** Incremento de riesgo en campañas de explotación selectiva.  
- **Efecto en el Negocio:** Potencial interrupción de servicio por ataques automatizados.



### **4. Error de Configuración de API (VULN‑006)**
- **Impacto:** Interrupción de servicio y limitación de funcionalidad.  
- **Consecuencia:** Pérdida temporal de operatividad y degradación de la experiencia de usuario.  
- **Efecto en el Negocio:** Pérdida de productividad y riesgo de inactividad del servicio.



## **Conclusión del Capítulo IV**

El análisis consolidado de los Sprints 1 y 2 evidencia que la infraestructura de **Tavolo Tech Solutions S.A.C.** mantiene una superficie de ataque reducida y adecuadamente filtrada a nivel perimetral; sin embargo, se detectaron configuraciones inseguras en las cabeceras HTTP y una fuga crítica de archivos sensibles.  

La vulnerabilidad de fuga de información constituye el riesgo principal para la continuidad del negocio y debe priorizarse su mitigación inmediata.  
Se recomienda implementar medidas de *hardening* en nginx, revisar las políticas de acceso a la API y establecer un ciclo de parches y monitoreo basado en OWASP Top 10 y ISO/IEC 27002.

