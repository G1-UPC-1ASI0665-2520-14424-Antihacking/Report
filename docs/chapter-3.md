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

-**Matriz de Vulnerabilidades:** Los hallazgos de Fuga de Claves/Certificados y Archivos de Backup se clasifican como CRÍTICO y deben ser la prioridad N°1 en el informe final.
