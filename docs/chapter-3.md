## Capítulo III: Desarrollo del Proyecto por Sprints

### Sprint 1 - Reconocimiento y Escaneo

#### Reconocimiento Pasivo

**Consulta de Registros DNS**

Se utilizó el comando nslookup  para resolver el nombre de host de Azure (tavolo.eastus2.cloudapp.azure.com) a una dirección IP, confirmando el punto de acceso inicial a la infraestructura.

**Comando Ejecutado**

nslookup tavolo.eastus2.cloudapp.azure.com

![Evidencia de Nslooup](/evidencias/nslookup_evidencia_1.png)

Resultado: La consulta confirmó que el registro A (Address) del dominio resuelve a la IP pública 40.84.58.167, la cual fue utilizada como objetivo principal en el Reconocimiento Activo.

#### Reconocimiento Activo (Escaneo de puertos)

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

