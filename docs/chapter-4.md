# **Capítulo IV: Resultados Consolidados**

## **4.1 Matriz de Vulnerabilidades**

A continuación, se presenta una matriz consolidada de las vulnerabilidades identificadas durante el Sprint 2, basada en los resultados de las herramientas Nessus, Gobuster y Nikto. La matriz incluye solo hallazgos confirmados y relevantes, clasificados por severidad (utilizando CVSS v3.0 donde aplica, o categorización cualitativa). Se priorizan los impactos críticos como la fuga de información, y se incluyen recomendaciones de mitigación. Los hallazgos se agrupan por categoría para evitar duplicados (ej: cabeceras de seguridad confirmadas por múltiples herramientas).

| Vulnerabilidad                                                               | Severidad (CVSS v3.0) | Categoría/Familia                       | Descripción                                                                                                                                                                                                                                                                                             | Herramienta que la Detectó                | Posible Impacto                                                                                                                     | Recomendación de Mitigación                                                                                                                                                                                               |
| ---------------------------------------------------------------------------- | --------------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fuga de Información Crítica (Archivos de Backup y Certificados Expuestos)    | CRÍTICO (9.8)         | Exposición de Datos Sensibles (CWE-530) | Exposición masiva de archivos sensibles como certificados (.pem, .jks), backups (.tgz, .tar, .war) y definiciones de datos (.html). Ejemplos: /tavolo.pem, /database.tgz, /tavolo.eastus2.cloudapp.jks, /site.tar.lzma. Permite acceso no autorizado a claves privadas, código fuente y datos internos. | Nikto                                     | Compromiso total del sistema: descifrado de tráfico TLS, suplantación de identidad, exposición de credenciales y lógica de negocio. | Implementar controles de acceso estrictos en el servidor web (ej: .htaccess o reglas de Nginx para denegar acceso a archivos sensibles). Eliminar o mover archivos expuestos. Usar WAF para bloquear patrones de fuzzing. |
| Ausencia de Cabecera Strict-Transport-Security (HSTS)                        | MEDIUM (6.5)          | Web Servers                             | El servidor no fuerza el uso exclusivo de HTTPS, permitiendo ataques de degradación de protocolo (SSL Stripping). Confirmado en respuestas HTTP/HTTPS.                                                                                                                                                  | Nessus, Nikto                             | Secuestro de sesiones, intercepción de datos sensibles mediante downgrade a HTTP.                                                   | Agregar la cabecera `Strict-Transport-Security: max-age=31536000; includeSubDomains` en la configuración de Nginx para forzar HTTPS.                                                                                      |
| Ausencia o Permisiva Cabecera X-Frame-Options                                | INFO (4.3)            | CGI Abuses / Web Servers                | No se define la cabecera, permitiendo que el sitio sea incrustado en iframes maliciosos.                                                                                                                                                                                                                | Nessus, Nikto                             | Ataques de Clickjacking: manipulación de clics del usuario en contextos superpuestos.                                               | Configurar `X-Frame-Options: DENY` o `SAMEORIGIN` en las respuestas HTTP de Nginx.                                                                                                                                        |
| Ausencia o Permisiva Directiva Content-Security-Policy (CSP) frame-ancestors | INFO (4.3)            | CGI Abuses                              | La directiva frame-ancestors no está configurada, similar a X-Frame-Options pero con menor granularidad.                                                                                                                                                                                                | Nessus                                    | Exposición a Clickjacking avanzado y inyecciones de contenido.                                                                      | Incluir `Content-Security-Policy: frame-ancestors 'self'` en las cabeceras, o fortalecer con políticas CSP completas.                                                                                                     |
| Ausencia de Cabecera X-Content-Type-Options                                  | INFO (4.3)            | Web Servers                             | No se define `nosniff`, permitiendo que los navegadores interpreten MIME types erróneamente.                                                                                                                                                                                                            | Nikto                                     | Ataques de MIME Sniffing: ejecución de scripts maliciosos disfrazados como archivos inofensivos.                                    | Agregar `X-Content-Type-Options: nosniff` en la configuración del servidor.                                                                                                                                               |
| Exposición de Tipo y Versión del Servidor HTTP                               | INFO (2.7)            | Web Servers                             | La cabecera Server revela `nginx/1.24.0 (Ubuntu)`, facilitando la búsqueda de CVEs específicos.                                                                                                                                                                                                         | Nessus, WhatWeb (de Sprint 1, confirmado) | Reconocimiento pasivo: atacantes pueden targeting vulnerabilities conocidas en Nginx 1.24.0.                                        | Suprimir la cabecera Server en Nginx con `server_tokens off;` en el archivo de configuración.                                                                                                                             |
| Compresión HTTP Habilitada (Vulnerable a BREACH)                             | MEDIUM (5.9)          | Web Servers                             | Content-Encoding: deflate está activo, potencialmente exponiendo datos sensibles a ataques de compresión.                                                                                                                                                                                               | Nikto                                     | Extracción de secrets (ej: CSRF tokens, cookies) mediante side-channel attacks como BREACH.                                         | Deshabilitar compresión HTTP en páginas con datos sensibles, o implementar padding en respuestas para mitigar BREACH.                                                                                                     |
| Error de Bad Gateway en Rutas de API                                         | LOW (3.7)             | Misconfiguración de Servidor            | Rutas /api y /apis devuelven 502 Bad Gateway, indicando fallo en reverse proxy o backend.                                                                                                                                                                                                               | Gobuster                                  | Denegación de servicio indirecta o exposición de misconfiguraciones; podría indicar rutas sensibles no protegidas adecuadamente.    | Revisar configuración de load balancer/reverse proxy en Azure. Asegurar que rutas de API estén protegidas con autenticación y no expuestas públicamente si no es intencional.                                             |

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

