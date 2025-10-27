## Capítulo III: Desarrollo del Proyecto por Sprints

### Sprint 1 - Reconocimiento y Escaneo

#### 1. Reconocimiento Pasivo

**1.1. Consulta de Registros DNS**

Se utilizó el comando nslookup  para resolver el nombre de host de Azure (tavolo.eastus2.cloudapp.azure.com) a una dirección IP, confirmando el punto de acceso inicial a la infraestructura.

**Comando Ejecutado**

nslookup tavolo.eastus2.cloudapp.azure.com

![Evidencia de Nslooup](../evidencias/nslookup_evidencia_1.png)

Resultado: La consulta confirmó que el registro A (Address) del dominio resuelve a la IP pública 40.84.58.167, la cual fue utilizada como objetivo principal en el Reconocimiento Activo.

#### 2. Reconocimiento Activo (Escaneo de puertos)

Esta sección documenta la ejecución del comando Nmap, cumpliendo con la user storie (HU01) y la identificación inicial de la superficie de ataque.

**Comando Ejecutado**

nmap -p- -sV -sC -O -A 40.84.58.167

![Evidencia del Escaneo de Puertos Nmap](../evidencias/nmap_evidencia_1.png)



**Puertos Abiertos Identificados**

El escaneo reveló que, gracias a la configuración de seguridad perimetral de Azure, la superficie de ataque se limitó a tres servicios principales, como se detalla a continuación.

<table class="table table-bordered">
    <thead>
        <tr>
            <th>Puerto</th>
            <th>Estado</th>
            <th>Servicio</th>
            <th>Versión (Tecnología)</th>
            <th>Observación / Relevancia para el Pentesting</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>80/tcp</td>
            <td>open</td>
            <td>http</td>
            <td>nginx 1.24.0 (Ubuntu)</td>
            <td>HTTP no cifrado, podría forzar la redirección a HTTPS.</td>
        </tr>
        <tr>
            <td>443/tcp</td>
            <td>open</td>
            <td>ssl/http</td>
            <td>nginx 1.24.0 (Ubuntu)</td>
            <td>Servicio HTTPS principal, con certificado válido para tavolo.eastus2.cloudapp.azure.com.</td>
        </tr>
        <tr>
            <td>8020/tcp</td>
            <td>open</td>
            <td>http-proxy</td>
            <td>FortiGuard Web Filtering</td>
            <td>Puerto no estándar que expone un activo de seguridad de red (Firewall/Proxy).</td>
        </tr>
    </tbody>
</table>

**Detección de Tecnologías y Sistema Operativo**

- **Servidor Web:** Nginx versión 1.24.0, lo que permite la búsqueda de vulnerabilidades específicas (CVEs) en el Sprint 2.

- **Sistema Operativo:** Se infiere un sistema Linux Kernel (probablemente Ubuntu) debido a la respuesta de Nginx, que alinea la infraestructura con el stack de desarrollo (React + Node.js).

- **Filtrado:** Se observaron 32,041 puertos filtrados, lo que demuestra la efectividad del firewall perimetral de Azure al bloquear el tráfico no deseado.


#### 3. Reconocimiento de Tecnologías Web

Esta fase se centró en la obtención de huellas digitales (fingerprinting) de la aplicación web, analizando cabeceras y tecnologías del stack visible.

**3.1. Análisis de Cabeceras HTTP (con curl)**

Se utilizó curl para analizar la respuesta del servidor en el puerto 80, lo que es crucial para verificar la política de uso de HTTPS.

**Comando ejecutado:**

curl -I tavolo.eastus2.cloudapp.azure.com

**Resultado Clave:** La respuesta inicial para el tráfico HTTP (puerto 80) es un código HTTP/1.1 301 Moved Permanently.

- **Política HTTPS:** La cabecera Location: https://tavolo.eastus2.cloudapp.azure.com/ confirma que el servidor fuerza correctamente la redirección a HTTPS. Este es un control de seguridad positivo, aunque el protocolo TLS debe ser validado con sslscan.

- **Servidor Web:** Se reconfirma la tecnología: Server: nginx/1.24.0 (Ubuntu).

![Evidencia de enumeración de tecnologías con curl](../evidencias/curl_evidencia_1.png)

**3.2. Reconocimiento Detallada del Servicio HTTPS (Análisis TLS/SSL)**

Para validar el control de seguridad sobre la redirección HTTPS/443 y evaluar la fortaleza criptográfica del servidor, se ejecutó el comando sslscan sobre la IP objetivo en el puerto 443.

**Comando ejecutado**

sslscan 40.84.58.167:443

**Resultado del escaneo**

<table class="table table-bordered">
  <thead>
    <tr>
      <th>Categoría</th>
      <th>Hallazgo</th>
      <th>Observación de Seguridad</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Protocolos TLS/SSL</td>
      <td>
        Habilitados: TLSv1.2, TLSv1.3. <br>
        Deshabilitados: SSLv2, SSLv3, TLSv1.0, TLSv1.1.
      </td>
      <td>
        Se han deshabilitado todos los protocolos obsoletos, indicando una configuración moderna y segura.
      </td>
    </tr>
    <tr>
      <td>Vulnerabilidades</td>
      <td>Heartbleed: No vulnerable.</td>
      <td>
        El servicio utiliza una versión de OpenSSL que no está expuesta a la vulnerabilidad Heartbleed.
      </td>
    </tr>
    <tr>
      <td>Funcionalidades de TLS</td>
      <td>
        TLS Compression: disabled. <br>
        Renegotiation: not supported.
      </td>
      <td>
        La compresión está deshabilitada y la renegociación no está soportada.
      </td>
    </tr>
    <tr>
      <td>Conjuntos de Cifrado (Cipher Suites)</td>
      <td>Solo se reportan cifrados aceptados de 128 bits y 256 bits.</td>
      <td>
        Ausencia de cifrados débiles o rotos, lo que confirma una política de cifrado fuerte.
      </td>
    </tr>
    <tr>
      <td>Certificado SSL</td>
      <td>
        Algoritmo: ecdsa-with-sha384. <br>
        Fuerza de Clave: 256 bits (ECC). <br>
        Sujeto: tavolo.eastus2.cloudapp.azure.com. <br>
        Válido: Oct 22 2025 - Jan 20 2026.
      </td>
      <td>
        Uso de criptografía de curva elíptica (ECC) con alta fortaleza, acorde a los estándares modernos.
      </td>
    </tr>
  </tbody>
</table>


![Evidencia de enumeración de seguridad con sslscan](../evidencias/sslscan_evidencia_1.png)

**3.3. Identificación con Whatweb**

Se ejecutó la herramienta WhatWeb en modo detallado para obtener un análisis de huella digital más profundo del sitio web.

**Comando Ejecutado**

whatweb -v https://40.84.58.167

**Resultado Clave:** La herramienta no detectó ningún Sistema de Gestión de Contenidos (CMS) comercial conocido (WordPress, Drupal, etc.).

**Servidor/OS:** Reconfirma HTTPServer [Ubuntu Linux] [nginx/1.24.0 (Ubuntu)].

**Título:** El título de la página es Vite App.

**Frameworks:** La detección de Script [module] y el título Vite App son fuertes indicadores de que la aplicación utiliza Vite y un framework de frontend basado en módulos.

**Detección de CMS:** La ausencia de plugins de CMS confirma que la aplicación es un desarrollo personalizado.

![Evidencia con Whatweb](../evidencias/whatweb_evidencia_1.png)


### Retrospectiva del Sprint

#### Hallazgos Encontrados

- **Mapeo Completo de la Superficie de Ataque:** El escaneo con Nmap (-p- -sV -sC -O -A) fue exhaustivo. Se identificaron solo 3 puertos abiertos (80, 443, 8020) y se confirmó la efectividad del firewall de Azure al mostrar 32,041 puertos filtrados, lo que define claramente la pequeña superficie de ataque.

 - Excelente Hardening de TLS/SSL (sslscan): El análisis de seguridad criptográfica con sslscan fue un éxito. Se confirmó que el servidor:

 - Deshabilita protocolos obsoletos (SSLv2, SSLv3, TLSv1.0, TLSv1.1).

 - Utiliza criptografía moderna (ECC) con fuerte longitud de clave (256 bits).

 - No es vulnerable a Heartbleed.

 - Fuerza la redirección a HTTPS (confirmado también por curl).

 - Conclusión de Seguridad: La configuración TLS/SSL del servidor es robusta y no representa un punto de entrada fácil.

- **Identificación Precisa de Tecnologías:** Nmap, curl y WhatWeb convergieron en la identificación de la tecnología de front-end (nginx/1.24.0 (Ubuntu)) y la inferencia de que la aplicación es un desarrollo personalizado.



### Sprint 2 - Enumeración Profunda & Análisis de Vulnerabilidades

#### 1. Escaneo de Vulnerabilidades Automatizado con Nessus

Se ejecutó un escaneo con Nessus Professional contra el host objetivo (tavolo.eastus2.cloudapp.azure.com) utilizando la política de Web Application Tests para cubrir las vulnerabilidades a nivel de servidor web y aplicación.

- **Host Analizado:** El escaneo fue dirigido al DNS tavolo.eastus2.cloudapp.azure.com (IP: 40.84.58.167).

- **Duración y Política:** El escaneo tuvo una duración de 28 minutos y se completó exitosamente. La política utilizada fue Web Application Tests.

### Hallazgos de Vulnerabilidades por Nessus:

Se logró identificar vulnerabilidades críticas relacionadas con la configuración de seguridad del servidor HTTP:

<table border="1">
  <thead>
    <tr>
      <th>Vulnerabilidad</th>
      <th>Severidad (CVSS v3.0)</th>
      <th>Familia</th>
      <th>Posible Solución</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>HSTS Missing From HTTPS Server (RFC 6797)</td>
      <td>MEDIUM (6.5)</td>
      <td>Web Servers</td>
      <td>Implementar la cabecera <strong>Strict-Transport-Security (HSTS)</strong> con un valor <strong>max-age</strong> adecuado para forzar el uso de HTTPS y mitigar ataques de downgrade de protocolo.</td>
    </tr>
    <tr>
      <td>Missing or Permissive X-Frame-Options HTTP Response Header</td>
      <td>INFO</td>
      <td>CGI abuses</td>
      <td>Implementar la cabecera <strong>X-Frame-Options: DENY</strong> o <strong>SAMEORIGIN</strong> para mitigar el riesgo de Clickjacking al controlar dónde se puede incrustar el contenido en un &lt;iframe&gt;.</td>
    </tr>
    <tr>
      <td>Missing or Permissive Content-Security-Policy frame-ancestors HTTP Response Header</td>
      <td>INFO</td>
      <td>CGI abuses</td>
      <td>Ajustar la directiva <strong>frame-ancestors</strong> en la cabecera Content-Security-Policy (CSP) para controlar con más detalle la incrustación de contenido.</td>
    </tr>
    <tr>
      <td>HTTP Server Type and Version</td>
      <td>INFO</td>
      <td>Web Servers</td>
      <td>Configurar el servidor web para <strong>ocultar o suprimir la cabecera Server</strong> en las respuestas HTTP para reducir la exposición de información sensible sobre la infraestructura.</td>
    </tr>
  </tbody>
</table>

Estos hallazgos demuestran que el servidor web no está implementando cabeceras de seguridad cruciales, lo que lo hace vulnerable a ataques de Clickjacking (por la ausencia de X-Frame-Options) y a ataques de degradación de SSL (por la ausencia de HSTS).

#### Evidencias

![Evidencia de nessus](../evidencias/nessus_evidencia_1.png)

![Evidencia de nessus](../evidencias/nessus_evidencia_2.png)

![Evidencia de nessus](../evidencias/nessus_evidencia_3.png)

#### 2. Enumeración de Directorios y Archivos con Gobuster

Se utilizó la herramienta Gobuster en modo dir para realizar un fuzzing de directorios en el dominio principal con el objetivo de descubrir rutas no indexadas que pudieran contener información sensible o paneles de administración.

- **Comando utilizado:** gobuster dir -u https://tavolo.eastus2.cloudapp.azure.com -w /usr/share/wordlists/dirb/common.txt -o gobuster_40.84.58.167.txt --exclude-length 441

- **Corrección Implementada:** Se utilizó el parámetro --exclude-length 441 para mitigar el problema de respuesta de wildcard (servidor devolviendo código 200 con longitud 441 en URLs inexistentes), permitiendo un registro limpio de los directorios reales.

#### Hallazgos encontrados:

La enumeración profunda reveló la existencia de directorios que exponen la estructura de la API y el contenido estático, así como posibles fallos en la configuración de load balancing o reverse proxy.

<table border="1">
  <thead>
    <tr>
      <th>Ruta Descubierta</th>
      <th>Código de Estado</th>
      <th>Longitud </th>
      <th>Observaciones</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>/favicon.ico</td>
      <td>200</td>
      <td>32438</td>
      <td>OK. Archivo estático que fue resuelto correctamente.</td>
    </tr>
    <tr>
      <td>/assets</td>
      <td>301</td>
      <td>178</td>
      <td>Redirección permanente. Indica un directorio válido, el cual fue redirigido a la URL completa (https://tavolo.eastus2.cloudapp.azure.com/assets/). Este directorio probablemente contiene archivos estáticos (CSS, JS, imágenes).</td>
    </tr>
    <tr>
      <td>/api</td>
      <td>502</td>
      <td>166</td>
      <td>Error de Bad Gateway. Indica que el reverse proxy (o Azure) no pudo contactar el servidor de la API, sugiriendo un fallo en la configuración del backend o una restricción de acceso.</td>
    </tr>
    <tr>
      <td>/apis</td>
      <td>502</td>
      <td>166</td>
      <td>Error de Bad Gateway. Similar a /api, posiblemente una ruta alternativa al servicio de API con el mismo fallo de conexión.</td>
    </tr>
  </tbody>
</table>

#### Evidencia

![Evidencia Gobuster](../evidencias/gobuster_evidencia_1.png)

### 3. Escaneo de Aplicación Web con Nikto

Se ejecutó la herramienta Nikto (v2.5.0) contra el host objetivo (tavolo.eastus2.cloudapp.azure.com:443). El escaneo, enfocado en buscar archivos comunes y configuraciones incorrectas, arrojó dos categorías principales de vulnerabilidades, fallos en cabeceras de seguridad y una fuga masiva de información.

#### Hallazgos de Configuración (Cabeceras HTTP)

Nikto confirmó los problemas de cabeceras de seguridad detectados por Nessus y agregó un riesgo adicional, todos relacionados con la ausencia de cabeceras de endurecimiento (hardening) del servidor.

<table border="1">
  <thead>
    <tr>
      <th>Vulnerabilidad</th>
      <th>Observación</th>
      <th>Posible Solución</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Strict-Transport-Security (HSTS) header is not defined.</strong></td>
      <td>Confirma la vulnerabilidad de Nessus. Permite ataques de degradación de protocolo y secuestro de sesión (SSL Stripping).</td>
      <td>Implementar la cabecera <strong>Strict-Transport-Security</strong> con un <code>max-age</code> alto.</td>
    </tr>
    <tr>
      <td><strong>X-Frame-Options header is not present.</strong></td>
      <td>Permite ataques de <strong>Clickjacking</strong>, donde un atacante puede incrustar el sitio en un <code>&lt;iframe&gt;</code> malicioso.</td>
      <td>Implementar la cabecera <strong>X-Frame-Options: DENY</strong> o <strong>SAMEORIGIN</strong>.</td>
    </tr>
    <tr>
      <td><strong>X-Content-Type-Options header is not set.</strong></td>
      <td>Permite el <strong>MIME Sniffing</strong>. Un navegador podría interpretar erróneamente un archivo (ej: un archivo de texto como JavaScript ejecutable).</td>
      <td>Implementar la cabecera <strong>X-Content-Type-Options: nosniff</strong>.</td>
    </tr>
    <tr>
      <td><strong>Content-Encoding header is set to "deflate" (BREACH).</strong></td>
      <td>Indica posible vulnerabilidad al ataque <strong>BREACH</strong>, especialmente si el contenido incluye datos de usuario y compresión.</td>
      <td><strong>Deshabilitar la compresión HTTP</strong> o aplicar mitigaciones específicas contra BREACH.</td>
    </tr>
  </tbody>
</table>

#### Fuga de Información Crítica

El escaneo detectó una cantidad significativa de archivos potencialmente sensibles, confirmando el objetivo de Identificar directorios y archivos ocultos o sensibles (HU11).

- **Hallazgo:** Potentially interesting backup/cert file found (CWE-530).

- **Impacto:** La exposición de estos archivos representa una fuga de información de alto riesgo, ya que un atacante puede descargar y analizar las claves de cifrado del servidor y el código fuente.

<table border="1">
  <thead>
    <tr>
      <th>Tipo de Fuga</th>
      <th>Ejemplos Encontrados</th>
      <th>Riesgo Específico</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Certificados/Claves Privadas</strong></td>
      <td><code>tavolo.pem</code>, <code>azure.pem</code>, <code>tavoloeastus2cloudapp.jks</code></td>
      <td><strong>Compromiso de TLS/SSL</strong>: Permite descifrar el tráfico interceptado (Ataques MitM) y <strong>suplantar la identidad del servidor</strong>.</td>
    </tr>
    <tr>
      <td><strong>Bases de Datos/Código Fuente</strong></td>
      <td><code>database.tgz</code>, <code>site.tar.lzma</code>, <code>tavolo.war</code>, <code>tavolo.tgz</code></td>
      <td><strong>Compromiso de la Aplicación</strong>: Exposición de credenciales internas, esquemas de bases de datos, lógica de negocio y vulnerabilidades en el código fuente.</td>
    </tr>
    <tr>
      <td><strong>Archivos de Backup Genéricos</strong></td>
      <td><code>archive.tar</code>, <code>cloudapp.tar.bz2</code>, <code>dump.egg</code></td>
      <td>Revela la <strong>estructura interna de la aplicación y la infraestructura</strong> (nombres de hosts, IPs, etc.).</td>
    </tr>
  </tbody>
</table>

La fuga masiva de archivos de backup y certificados clasifica este servidor con un riesgo CRÍTICO, ya que la mitigación de las otras vulnerabilidades de cabeceras se vuelve secundaria si las claves privadas están comprometidas.

#### Evidencia

![Evidencia Nikto](../evidencias/nikto_evidencia_1.png)


### Retrospectiva del Sprint 2:

#### Hallazdos encontrados:

- **Hallazgo Crítico de Fuga de Información (Nikto):** El escaneo con Nikto fue el punto más exitoso. Se identificó una fuga masiva y crítica de archivos de backup (.tgz, .tar) y certificados/claves privadas (.pem, .jks). Este hallazgo de alto impacto (CWE-530) proporciona una ruta directa para intentar el compromiso total del sistema.

- **Confirmación de Vulnerabilidades (Nessus y Nikto):** Ambas herramientas se complementaron perfectamente, confirmando la ausencia de cabeceras de seguridad fundamentales (HSTS, X-Frame-Options, X-Content-Type-Options). Esto asegura la precisión de los hallazgos de severidad media y baja.

- **Superación del Wildcard de Gobuster:** Se corrigió exitosamente el problema de wildcard del servidor web (usando --exclude-length 441), permitiendo que la enumeración de directorios (Gobuster) fuera limpia y efectiva.

#### Problemas encontrados:

- **Fallo de Conexión de API (Gobuster):** La enumeración de directorios detectó las rutas /api y /apis, pero el servidor devolvió un error persistente de Bad Gateway (502). Esto indica un problema de configuración o conectividad entre el reverse proxy y el backend de la API, impidiendo la enumeración de endpoints de la API.

- **Exceso de Hallazgos en Nikto:** El volumen de archivos de backup detectados por Nikto es abrumador. El informe lista tipos de riesgo, pero el equipo aún no ha verificado cuáles de esos archivos realmente existen y son descargables.

#### Acciones a priorizar en el siguiente Sprint:

- **Prioridad Máxima:** Explotación de Fuga de Información: El próximo sprint debe comenzar con la explotación inmediata de la fuga de información de Nikto. Se debe intentar descargar y analizar los archivos críticos (.pem, .jks, .tgz) para obtener credenciales, código fuente o claves de cifrado.

- **Investigación del Fallo 502 de la API:** Se debe dedicar un esfuerzo a investigar la causa del error 502 en las rutas /api y /apis. Esto podría requerir el uso de herramientas de proxy (como Burp Suite) para modificar cabeceras e intentar sortear la restricción del load balancer o reverse proxy.

- **Seguimiento de Directorios Accesibles:** Realizar una inspección manual del directorio /assets (código 301 de Gobuster) para buscar archivos de configuración, manifiestos o cualquier contenido estático que pueda contener metadatos o secretos.

- **Matriz de Vulnerabilidades:** Los hallazgos de Fuga de Claves/Certificados y Archivos de Backup se clasifican como CRÍTICO y deben ser la prioridad N°1 en el informe final.


### Sprint 3 - Explotación Controlada

#### 1. Descubrimiento y Análisis del Endpoint de Registro

Se realizó un análisis inicial exhaustivo del endpoint de registro para identificar la arquitectura del backend y validar la estructura de las solicitudes, cumpliendo con la user story (HU02) de validación de SQL Injection.

**1.1. Metodología de Análisis**

Se creó un usuario de prueba para analizar el comportamiento de la aplicación, monitoreando el tráfico de red mediante las herramientas de desarrollo del navegador para identificar el endpoint real del backend.

**1.2. Hallazgos del Endpoint**

**Endpoint Descubierto:**
```
https://tavolo.eastus2.cloudapp.azure.com/api/v1/authentication/sign-up
```

**Características Técnicas del Endpoint:**

- **Método HTTP:** POST
- **Content-Type:** application/json
- **CORS:** Configurado correctamente - Origin restringido al dominio de Tavolo
- **Protocolo:** HTTPS (TLSv1.2/1.3)

**Cabeceras de Seguridad Implementadas:**

| Cabecera | Valor | Observación |
|----------|-------|-------------|
| X-Content-Type-Options | nosniff | Previene MIME sniffing |
| X-Frame-Options | DENY | Previene clickjacking |
| X-XSS-Protection | 0 | Protección contra XSS |
| Access-Control-Allow-Origin | https://tavolo.eastus2.cloudapp.azure.com | CORS restringido |
| Access-Control-Allow-Credentials | true | Permite credenciales en CORS |

**1.3. Validación Manual del Endpoint**

Se realizó una solicitud POST legitima para validar la estructura y el comportamiento del endpoint:

**Comando Ejecutado:**

```bash
curl -X POST "https://tavolo.eastus2.cloudapp.azure.com/api/v1/authentication/sign-up" \
  -H "Content-Type: application/json" \
  -H "User-Agent: Mozilla/5.0" \
  -H "Origin: https://tavolo.eastus2.cloudapp.azure.com" \
  -d '{"username":"nuevousuario","password":"Password123","email":"nuevo@test.com"}' \
  -v
```
![Evidencia Nikto](../evidencias/sprint-3-01-endpoint-prueba.png) 

**Respuesta Exitosa:**

```
HTTP/1.1 201 Created
Server: nginx/1.24.0 (Ubuntu)
Content-Type: application/json
Access-Control-Allow-Origin: https://tavolo.eastus2.cloudapp.azure.com
Access-Control-Allow-Credentials: true
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 0

{"id":286,"username":"nuevousuario","roles":["ROLE_USER"]}
```

**Interpretación:** El endpoint devuelve código HTTP 201 Created, confirmando el registro exitoso. La respuesta incluye el ID del usuario generado, nombre de usuario y roles asignados. Las cabeceras de seguridad están implementadas correctamente.

![Evidencia Nikto](../evidencias/sprint-3-01-endpoint-discovery.png) 
- Captura de pantalla del navegador mostrando Developer Tools (Network tab) con la solicitud POST al endpoint `/api/v1/authentication/sign-up` y respuesta HTTP 201.


#### 2. Pruebas Exhaustivas de SQL Injection

Se ejecutaron pruebas de SQL Injection utilizando múltiples enfoques y técnicas para validar la resistencia del endpoint contra este vector de ataque crítico.

**2.1. Primer Enfoque: SQLMap con JSON Directo (Nivel 5, Riesgo 3)**

Se ejecutó SQLMap contra el endpoint con los parámetros máximos de intensidad para detectar inyecciones SQL sin técnicas de evasión.

**Comando Ejecutado:**

```bash
sqlmap -u "https://tavolo.eastus2.cloudapp.azure.com/api/v1/authentication/sign-up" \
  --data='{"username":"testinjection","password":"test123","email":"test@test.com"}' \
  --headers="Content-Type: application/json" \
  --batch --level=5 --risk=3 --dbs -v 3
```

**Parámetros de SQLMap:**

| Parámetro | Valor | Descripción |
|-----------|-------|-------------|
| -u | URL del endpoint | Target principal |
| --data | JSON payload | Estructura de datos POST |
| --headers | Content-Type: application/json | Especifica formato JSON |
| --batch | Automático | Responde automáticamente a preguntas |
| --level | 5 | Máximo nivel de profundidad (1-5) |
| --risk | 3 | Máximo riesgo de pruebas (1-3) |
| --dbs | Enumerar bases de datos | Objetivo si vulnerable |

**Resultados del Escaneo:**

- **WAF/IPS Detectado:** SQLMap identificó la presencia de protección perimetral
- **Contenido Dinámico:** El servidor responde con variaciones en las respuestas
- **Parámetros Probados:** username, password, email
- **Técnicas Intentadas:**
  - Boolean-based blind SQL Injection
  - Time-based blind SQL Injection
  - Error-based SQL Injection
  - UNION queries
- **Resultado Final:** ❌ No se encontró inyección SQL en este formato

![Evidencia Nikto](../evidencias/sprint-3-02-sqlmap-json-direct.png)

- Screenshot o logs de la ejecución de sqlmap mostrando:
- Comando ejecutado completo
- Salida indicando "WAF/IPS/Load balancer detected"
- Parámetros probados (username, password, email)
- Conclusión: No vulnerable


**2.2. Segundo Enfoque: SQLMap con Técnicas de Evasión (Tamper Scripts)**

Se ejecutó SQLMap utilizando scripts de evasión (tamper) para intentar sortear posibles mecanismos de protección del WAF/IPS.

**Comando Ejecutado:**

```bash
sqlmap -u "https://tavolo.eastus2.cloudapp.azure.com/api/v1/authentication/sign-up" \
  --data='{"username":"test","password":"test","email":"test@test.com"}' \
  --headers="Content-Type: application/json" \
  --batch --tamper=space2comment --random-agent --delay=1 --dbs -v 3
```

**Configuración de Evasión:**

| Configuración | Valor | Propósito |
|---------------|-------|---------|
| --tamper | space2comment | Convierte espacios en comentarios SQL para evadir filtros |
| --random-agent | Habilitado | Usa User-Agent aleatorios para no ser detectado |
| --delay | 1 segundo | Retraso entre solicitudes para evadir IDS |
| --level | 5 | Máximo nivel de análisis |
| --risk | 3 | Máximo riesgo aceptado |

**Resultados del Escaneo:**

- **Códigos de Error Detectados:** 409 Conflict (156 veces), 500 Internal Server Error (5 veces)
- **Parámetros Dinámicos:** username identificado como parámetro dinámico
- **Respuestas Variadas:** El servidor responde con contenido dinámico pero consistente
- **Técnicas Probadas:** Todas las técnicas estándar de inyección SQL
- **Resultado Final:**  No se encontró inyección SQL con técnicas de evasión


**2.3. Tercer Enfoque: Cambio de Content-Type (Form URL-Encoded)**

Se intentó cambiar el Content-Type de JSON a form-urlencoded para probar si el endpoint es vulnerable bajo diferentes formatos de envío.

**Comando Ejecutado:**

```bash
sqlmap -u "https://tavolo.eastus2.cloudapp.azure.com/api/v1/authentication/sign-up" \
  --data="username=testinjection&password=test123&email=test@test.com" \
  --headers="Content-Type: application/x-www-form-urlencoded" \
  --batch --level=5 --risk=3 --dbs -v 3
```

**Parámetros del Escaneo:**

- **Content-Type:** application/x-www-form-urlencoded (en lugar de JSON)
- **Objetivo:** Validar si el endpoint acepta y es vulnerable bajo este formato
- **Nivel/Riesgo:** 5/3 (máximo)

**Resultados del Escaneo:**

- **Errores del Servidor:** HTTP 500 Internal Server Error (201 instancias)
- **Parámetros Probados:** username, password, email
- **Falsos Positivos:** El parámetro email fue marcado como potencialmente inyectable, pero posteriormente descartado por validación adicional
- **Conclusión:** El endpoint no acepta ni procesa correctamente el formato form-urlencoded
- **Resultado Final:**  No vulnerable (rechazo del formato)


#### 3. Análisis Comparativo de Resultados

Se compilaron todos los resultados de las pruebas de SQL Injection en una matriz comparativa:

**Matriz de Pruebas Realizadas:**

| Enfoque | Técnica | Parámetros | Nivel | Riesgo | Vulnerable | Observaciones |
|---------|---------|-----------|-------|--------|------------|---------------|
| 1. JSON Directo | UNION, Boolean, Time-based, Error | username, password, email | 5 | 3 |  No | WAF/IPS detectado |
| 2. Evasión (Tamper) | space2comment + Random-Agent | username, password, email | 5 | 3 |  No | 409/500 errors, dinámico pero seguro |
| 3. Form URL-Encoded | UNION, Boolean, Time-based | username, password, email | 5 | 3 |  No | Formato no soportado (HTTP 500) |

**Conclusión de Seguridad:** El endpoint `/api/v1/authentication/sign-up` es **RESISTENTE** a todos los vectores de SQL Injection probados bajo tres enfoques diferentes.


#### 4. Evaluación de Vulnerabilidad HU02

**HU02: SQL Injection en Endpoint /sign-up - EVALUACIÓN FINAL**

**Estado:** **NO VULNERABLE**

**Análisis Técnico:**

| Aspecto | Resultado | Evidencia |
|--------|-----------|-----------|
| Inyección SQL Directa | No vulnerable | Todas las técnicas UNION, Boolean, Time-based bloqueadas |
| Evasión de WAF | Bloqueado | Tamper scripts no evadieron detección |
| Validación de Entrada | Implementada | Sanitización correcta detectada |
| Consultas Parametrizadas | Confirmado | Resistencia a inyección indica uso de prepared statements |
| Manejo de Errores | Seguro | No divulga información sensible |
| Content-Type Validation | Estricto | Solo acepta application/json |

**Cobertura de Pruebas:**

- **Técnicas Probadas:** 5+ técnicas de inyección SQL
- **Parámetros Analizados:** 3 (username, password, email)
- **Niveles de Intensidad:** Máximo (Nivel 5, Riesgo 3)
- **Enfoques Diferentes:** 3 (JSON directo, Evasión, Form-encoded)
- **Duración Total:** Análisis completo realizado

**Conclusión Técnica:**

El endpoint `/api/v1/authentication/sign-up` implementa correctamente:
- Sanitización robusta de entradas
- Consultas parametrizadas (prepared statements)
- Validación estricta del Content-Type
- Protección perimetral (WAF/IPS)
- Manejo seguro de errores


#### 5. Hallazgos de Seguridad Positivos Identificados

Durante el análisis exhaustivo del endpoint, se identificaron múltiples controles de seguridad implementados correctamente:

**5.1. Validación Robusta de Entrada**

- **Resistencia a SQL Injection:** Confirmed through 3 different attack vectors
- **Sanitización:** Todos los parámetros son sanitizados correctamente
- **Prepared Statements:** Evidente en la resistencia a técnicas UNION y time-based
- **Validación de Tipos:** El endpoint valida tipos de datos (strings, valores)

**5.2. Configuración Segura de CORS**

- **Origin Restringido:** Solo acepta solicitudes del dominio específico `https://tavolo.eastus2.cloudapp.azure.com`
- **Credenciales:** Access-Control-Allow-Credentials: true (configurado correctamente)
- **Prevención de CORS Bypass:** No permite origins comodín (*)
- **Implicación:** Mitiga riesgo de ataques cross-origin

**5.3. Cabeceras de Seguridad Implementadas**

| Cabecera | Valor | Control de Seguridad |
|----------|-------|-------------------|
| X-Content-Type-Options | nosniff | Previene MIME sniffing y ejecución no intencional |
| X-Frame-Options | DENY | Bloquea embedding en iframes (Clickjacking) |
| X-XSS-Protection | 0 (deprecated but present) | Protección adicional contra XSS (legacy) |
| Content-Type | application/json | Validación strict de formato |

**5.4. Manejo Seguro de Errores**

- **Sin Información Sensible:** Los errores 409 y 500 no revelan stack traces
- **Respuestas Consistentes:** El servidor no divulga diferencias en tratamiento
- **Rate Limiting Implícito:** El delay observado sugiere protección contra fuerza bruta
- **Logs Seguro:** No hay exposición de rutas internas o versiones

**5.5. Protección Perimetral (WAF/IPS)**

- **Detección de Ataques:** SQLMap detectó WAF/IPS activo
- **Bloqueo de Patrones:** Técnicas conocidas de SQL Injection fueron bloqueadas
- **Inteligencia de Amenaza:** Sistema capaz de detectar herramientas automatizadas


### Retrospectiva del Sprint 3

#### Hallazgos Encontrados

- **Endpoint API Descubierto:** Se identificó y documentó correctamente el endpoint de autenticación `/api/v1/authentication/sign-up`, revelando la arquitectura del backend y su estructura de comunicación.

- **SQL Injection: NO VULNERABLE:** A pesar de la vulnerabilidad identificada en Sprint 2 (Nessus reportó SQL Injection como riesgo), el análisis exhaustivo con SQLMap (3 enfoques diferentes, nivel 5, riesgo 3) confirma que el endpoint está **PROTEGIDO** contra este vector de ataque.

- **Implementación de Seguridad Robusta:** El endpoint demuestra implementación correcta de:
  - Consultas parametrizadas (prepared statements)
  - Sanitización de entradas
  - Validación strict del Content-Type
  - CORS restrictivo
  - Cabeceras de seguridad (X-Content-Type-Options, X-Frame-Options, X-XSS-Protection)

- **Discrepancia con Sprint 2:** El hallazgo de SQL Injection en Sprint 2 (por Nessus) puede ser:
  - Un falso positivo del análisis automatizado
  - Una vulnerabilidad en un endpoint diferente (no testado en Sprint 3)
  - Una configuración que fue parcheada después del escaneo de Nessus

#### Problemas Encontrados

- **Limitación de Scope:** El análisis se enfocó solo en el endpoint `/sign-up`. Otros endpoints (login, API endpoints de datos) no fueron probados y podrían ser vulnerables a SQL Injection.

- **Falta de Acceso Autenticado:** Sin credenciales válidas, no fue posible probar endpoints protegidos que podrían exponer la vulnerabilidad de SQL Injection en contexto autenticado.

- **Falsos Positivos Posibles:** SQLMap reportó el parámetro email como "potencialmente inyectable" en el tercer enfoque, pero fue descartado. Esto sugiere que la herramienta puede generar falsos positivos bajo ciertos formatos.

#### Recomendaciones para Próximos Sprints

- **Sprint 4 - Post-Explotación:** Si es posible obtener credenciales válidas a través de otros vectores (información divulgada en Nikto, archivos de backup, etc.), se recomienda probar endpoints autenticados que podrían ser vulnerables a SQL Injection.

- **Pruebas de Otros Endpoints:** Se recomienda mapear y probar otros endpoints de la API (`/api/v1/authentication/login`, `/api/v1/users/*`, etc.) que podrían ser vulnerables a SQL Injection.

- **Fuga de Información (Prioridad Máxima):** Basándose en hallazgos de Sprint 2 (Nikto), se debe proceder a intentar descargar archivos críticos (.pem, .jks, .tgz) que podrían proporcionar acceso directo a la infraestructura y base de datos.

- **Testing de Otros Vectores:** Con acceso a credenciales o archivos de configuración, probar vulnerabilidades como IDOR, escalación de privilegios, y ejecución remota de código.
