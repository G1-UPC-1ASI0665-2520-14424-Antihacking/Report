## Capítulo III: Desarrollo del Proyecto por Sprints

### Sprint 1 - Reconocimiento y Escaneo

#### 1. Reconocimiento Pasivo

**1.1. Consulta de Registros DNS**

Se utilizó el comando nslookup  para resolver el nombre de host de Azure (tavolo.eastus2.cloudapp.azure.com) a una dirección IP, confirmando el punto de acceso inicial a la infraestructura.

**Comando Ejecutado**

nslookup tavolo.eastus2.cloudapp.azure.com

![Evidencia de Nslooup](/evidencias/nslookup_evidencia_1.png)

Resultado: La consulta confirmó que el registro A (Address) del dominio resuelve a la IP pública 40.84.58.167, la cual fue utilizada como objetivo principal en el Reconocimiento Activo.

#### 2. Reconocimiento Activo (Escaneo de puertos)

Esta sección documenta la ejecución del comando Nmap, cumpliendo con la user storie (HU01) y la identificación inicial de la superficie de ataque.

**Comando Ejecutado**

nmap -p- -sV -sC -O -A 40.84.58.167

![Evidencia del Escaneo de Puertos Nmap](/evidencias/nmap_evidencia_1.png)



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

![Evidencia de enumeración de tecnologías con curl](/evidencias/curl_evidencia_1.png)

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


![Evidencia de enumeración de seguridad con sslscan](/evidencias/sslscan_evidencia_1.png)

**3.3. Identificación con Whatweb**

Se ejecutó la herramienta WhatWeb en modo detallado para obtener un análisis de huella digital más profundo del sitio web.

**Comando Ejecutado**

whatweb -v https://40.84.58.167

**Resultado Clave:** La herramienta no detectó ningún Sistema de Gestión de Contenidos (CMS) comercial conocido (WordPress, Drupal, etc.).

**Servidor/OS:** Reconfirma HTTPServer [Ubuntu Linux] [nginx/1.24.0 (Ubuntu)].

**Título:** El título de la página es Vite App.

**Frameworks:** La detección de Script [module] y el título Vite App son fuertes indicadores de que la aplicación utiliza Vite y un framework de frontend basado en módulos.

**Detección de CMS:** La ausencia de plugins de CMS confirma que la aplicación es un desarrollo personalizado.

![Evidencia con Whatweb](/evidencias/whatweb_evidencia_1.png)

### Sprint 2 - Enumeración Profunda & Análisis de Vulnerabilidades

#### Escaneo de Vulnerabilidades Automatizado con Nessus

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

![Evidencia de nessus](/evidencias/nessus_evidencia_1.png)

![Evidencia de nessus](/evidencias/nessus_evidencia_2.png)

![Evidencia de nessus](/evidencias/nessus_evidencia_3.png)
