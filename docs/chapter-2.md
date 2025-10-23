## Capítulo II: Metodología Ágil y de Pentesting

### 2.1. Marco de referencia

El servicio de consultoría de Pruebas de Penetración (Pentesting) para Tavolo se ejecuta bajo un marco de referencia híbrido, diseñado para asegurar la máxima rigurosidad técnica mientras se mantiene la agilidad y la transparencia requeridas por una PYME. Este enfoque combina tres estándares internacionales clave de ciberseguridad con la metodología de gestión Scrum.

##### Estándares Técnicos Guía: PTES, OWASP y NIST

La ejecución de las pruebas se fundamenta en el Penetration Testing Execution Standard (PTES). Este marco proporciona las siete fases estructuradas que guían el proyecto de inicio a fin: desde la interacción inicial con el cliente (Pre-Engagement) hasta la elaboración del informe final. El PTES asegura que el proceso de pentesting sea completo y metódico, cubriendo todo el ciclo de vida de un ataque simulado, incluyendo la recolección de inteligencia, el modelado de amenazas, la explotación de vulnerabilidades y la post-explotación.

Dentro de las fases de análisis y explotación, la principal guía técnica es la OWASP Testing Guide (OTG). Esta guía es esencial, ya que proporciona los procedimientos y casos de prueba detallados para evaluar específicamente la seguridad de las aplicaciones web, que es el activo principal de Tavolo. El OTG se utiliza para diseñar las pruebas concretas en el portal de registro y en las funcionalidades internas post-login, permitiendo descubrir fallos como el Broken Access Control o vulnerabilidades de lógica de negocio que un atacante autenticado podría explotar.

Finalmente, el NIST SP 800-115 (Guía Técnica para la Evaluación y Prueba de la Seguridad de la Información) complementa la metodología enfocándose en la calidad, la documentación y la planificación. El NIST asegura que todas las actividades estén bien definidas desde la fase de planificación (alcance, exclusiones) y que la documentación de la evidencia y el reporte de resultados sean rigurosos, repetibles y objetivos, lo cual es fundamental para que Tavolo pueda confiar y actuar sobre las recomendaciones.

##### Adaptación a la Metodología Scrum

Para asegurar la transparencia, adaptabilidad y entrega de valor incremental, la gestión del proyecto se enmarca en la metodología Scrum, articulando las fases técnicas del pentesting (PTES) en Sprints definidos. El equipo de la consultora opera bajo roles Scrum para optimizar el flujo de trabajo.

La integración se manifiesta en tres etapas clave que vinculan directamente la gestión con el plan de ejecución:

1. Planificación y Definición del Backlog: Al inicio, el equipo y el Product Owner (representante de Tavolo) colaboran para transformar los objetivos de seguridad y el Modelado de Amenazas en el Sprint Backlog. Esto asegura que las pruebas más críticas —como la seguridad del login y el control de acceso a las funciones internas— se prioricen desde el principio, cumpliendo con los requisitos de la fase de Pre-Engagement (PTES).

2. Ejecución Ágil y Comunicación: Durante la ejecución de las pruebas técnicas (Enumeración, Explotación y Post-Explotación), se realizan Daily Stand-ups para que el equipo comunique el progreso, las barreras y, lo más importante, los hallazgos de alta criticidad. Esta agilidad es fundamental, dado que si una vulnerabilidad es explotada con éxito (PoC), el equipo tiene la capacidad de pivotar inmediatamente el enfoque de la prueba para evaluar el impacto total (Post-Explotación) y notificar al contacto de emergencia de Tavolo, superando la rigidez de las metodologías secuenciales.

3. Reporte y Cierre: El cierre del proyecto culmina con la Sprint Review, donde se presenta el informe final (guiado por los estándares de documentación de NIST SP 800-115). Esta revisión es una sesión colaborativa donde se explica la criticidad real del riesgo empresarial y se trabaja conjuntamente con Tavolo para validar y refinar el Plan de Remediación. De esta manera, se garantiza que los resultados técnicos se traduzcan directamente en una hoja de ruta de acciones claras y priorizadas para el equipo de desarrollo del cliente.


### 2.2. Backlog inicial

El Product Backlog inicial del proyecto define el trabajo a realizar por la consultora, estructurado como Historias de Usuario (HU) enfocadas en las pruebas de seguridad. Estas historias están priorizadas según el riesgo potencial para Tavolo y se alinean directamente con las fases de ejecución de los Sprints.

##### Estructura y Priorización del Backlog

Las Historias de Usuario (HU) han sido priorizadas utilizando la escala MoSCoW, donde la prioridad se asigna como Must Have (Obligatorio, riesgo crítico), Should Have (Debería tener, riesgo alto) y Could Have (Podría tener, riesgo medio).

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Historia de Usuario (HU)</th>
            <th>Prioridad (MoSCoW)</th>
            <th>Criterios de Aceptación (Escenarios Gherkin)</th>
            <th>Sprint Asignado</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HU01</td>
            <td>Como consultor, quiero realizar un escaneo de puertos y servicios públicos para mapear la superficie de ataque del servidor en Azure.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Confirmación de Servicios Expuestos</strong><br>
                Given la dirección IP pública del servidor de Tavolo<br>
                When ejecuto un escaneo completo de puertos TCP/UDP<br>
                Then solo deberían aparecer abiertos los puertos esenciales (80, 443)<br>
                And se registra la versión exacta del servicio en cada puerto.
            </td>
            <td>S1</td>
        </tr>
        <tr>
            <td>HU02</td>
            <td>Como atacante, quiero probar el proceso de registro (<code>/sign-up</code>) contra ataques de **SQL Injection** para comprometer la base de datos de Tavolo.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Detección de Inyección SQL</strong><br>
                Given un formulario de registro válido en la URL <code>/sign-up</code><br>
                When ingreso una payload de inyección (<code>' OR 1=1 --</code>) en el campo 'Nombre de Usuario'<br>
                Then el sistema debería devolver un error genérico o completar el registro sin un error de base de datos.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU03</td>
            <td>Como usuario normal, quiero intentar acceder a las funcionalidades de administración o a datos de otros usuarios para identificar fallos de **Broken Access Control**.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Escalada Horizontal de Privilegios</strong><br>
                Given estoy autenticado como 'UsuarioA' con ID de sesión válido<br>
                When intento modificar un recurso de 'UsuarioB' cambiando el parámetro ID en la URL o solicitud<br>
                Then el sistema debería rechazar la solicitud y devolver el código de estado HTTP <strong>403 (Forbidden)</strong>.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU04</td>
            <td>Como consultor, quiero escanear la aplicación con herramientas automatizadas (Nessus/Nikto/Burp) para descubrir vulnerabilidades conocidas del stack tecnológico.</td>
            <td>Should Have</td>
            <td>
                <strong>Scenario: Validación de Reporte de Escaneo</strong><br>
                Given los resultados brutos del escaneo automatizado han sido exportados<br>
                When el equipo técnico filtra los hallazgos de criticidad Alta y Crítica<br>
                Then se documentan solo aquellos hallazgos que han sido validados manualmente como no ser un falso positivo.
            </td>
            <td>S2</td>
        </tr>
        <tr>
            <td>HU05</td>
            <td>Como atacante, quiero explotar credenciales débiles o mecanismos de autenticación frágiles para acceder a una cuenta sin conocer la contraseña.</td>
            <td>Should Have</td>
            <td>
                <strong>Scenario: Prueba de Tasa de Ataque (Rate Limit)</strong><br>
                Given conozco un nombre de usuario válido<br>
                When envío 100 peticiones de login fallidas en 60 segundos<br>
                Then el sistema debería implementar un bloqueo de la cuenta o un mecanismo de captcha en intentos posteriores.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU06</td>
            <td>Como usuario, quiero introducir código malicioso en los campos de mi perfil para verificar si la plataforma es vulnerable a ataques de **Cross-Site Scripting (XSS)**.</td>
            <td>Should Have</td>
            <td>
                <strong>Scenario: XSS Almacenado en la Descripción del Perfil</strong><br>
                Given estoy autenticado y accedo a la sección 'Editar Perfil'<br>
                When ingreso una payload de XSS persistente (<code>&lt;script&gt;alert(1)&lt;/script&gt;</code>) en la descripción<br>
                Then la payload no debería ejecutarse, sino mostrarse como texto plano en la vista del perfil de la víctima.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU07</td>
            <td>Como consultor, quiero documentar el acceso a información sensible tras la explotación para medir el impacto total del riesgo.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Acceso a Archivos Críticos</strong><br>
                Given se ha obtenido una <em>shell</em> o acceso al sistema de archivos del servidor (Post-Explotación)<br>
                When se navega al directorio de configuración de la aplicación<br>
                Then se obtiene una captura de pantalla verificable del archivo que contiene <strong>credenciales de bases de datos internas</strong>.
            </td>
            <td>S4</td>
        </tr>
        <tr>
            <td>HU08</td>
            <td>Como consultor, quiero redactar el informe técnico, ejecutivo y el plan de remediación para entregar a Tavolo la hoja de ruta para corregir las vulnerabilidades.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Revisión de la Entrega Final</strong><br>
                Given todos los hallazgos han sido validados y documentados con PoC<br>
                When el equipo de Tavolo recibe el informe final y el plan de remediación<br>
                Then el documento cumple con los requisitos de formato <strong>NIST</strong> y las recomendaciones son suficientemente específicas para que el desarrollador pueda actuar.
            </td>
            <td>S5</td>
        </tr>
        <tr>
            <td>HU09</td>
            <td>Como consultor, quiero evaluar la lógica de negocio en funcionalidades clave (gestión de perfiles o creación de eventos) para encontrar fallos que permitan la manipulación de datos.</td>
            <td>Could Have</td>
            <td>
                <strong>Scenario: Manipulación de Parámetros de Negocio</strong><br>
                Given estoy creando un evento y capturo la solicitud HTTP<br>
                When modifico el parámetro <em>price</em> a un valor negativo o no permitido en la solicitud <em>proxy</em><br>
                Then el backend debería invalidar la solicitud y no permitir la creación del evento con el precio modificado.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU10</td>
            <td>Como consultor, quiero examinar los encabezados y *cookies* de respuesta HTTP para identificar configuraciones de seguridad faltantes o débiles.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Verificación de Encabezados de Seguridad</strong><br>
                Given realizo una solicitud HTTP a la página principal y a los endpoints de login/registro<br>
                When reviso los encabezados de respuesta del servidor<br>
                Then el encabezado <code>Strict-Transport-Security</code> (HSTS) debe estar presente con una directiva adecuada<br>
                And se verifica la existencia de <code>X-Content-Type-Options: nosniff</code> y <code>X-Frame-Options: DENY</code>.
            </td>
            <td>S2</td>
        </tr>
        <tr>
            <td>HU11</td>
            <td>Como atacante, quiero abusar de la funcionalidad de "Olvidé mi Contraseña" para tomar control de una cuenta o causar una denegación de servicio a la cuenta.</td>
            <td>Should Have</td>
            <td>
                <strong>Scenario: Prueba de Tasa de Ataque (Rate Limit)</strong><br>
                Given he solicitado un código de restablecimiento de contraseña para un usuario válido<br>
                When envío 100 intentos fallidos de código de 6 dígitos en un período de 5 minutos<br>
                Then el sistema debe invalidar el código, bloquear temporalmente la funcionalidad o requerir un *captcha* después de un número limitado de fallos.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU12</td>
            <td>Como consultor, quiero revisar el manejo de archivos subidos por el usuario (foto de perfil) para detectar fallos de **Unrestricted File Upload**.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Subida de Shell Inversa a Través de Imagen</strong><br>
                Given tengo acceso a la funcionalidad de subir una foto de perfil<br>
                When intento subir un archivo con extensión <code>php</code> o <code>asp</code> con código malicioso<br>
                Then el sistema debe rechazar el archivo basándose en la lista blanca de tipos MIME y la extensión, y no permitir su ejecución.
            </td>
            <td>S4</td>
        </tr>
        <tr>
            <td>HU13</td>
            <td>Como atacante, quiero inyectar entradas maliciosas en los logs, comentarios o campos de búsqueda para verificar la vulnerabilidad a **Server-Side Template Injection (SSTI)**.</td>
            <td>Could Have</td>
            <td>
                <strong>Scenario: Inyección en Campo de Búsqueda</strong><br>
                Given la aplicación utiliza un motor de plantillas para renderizar contenido (Twig, Jinja2)<br>
                When ingreso una <em>payload</em> de SSTI (<code>${{7*7}}</code>) en un campo que es renderizado dinámicamente<br>
                Then el sistema no debería ejecutar la operación matemática y en su lugar mostrar la <em>payload</em> como texto plano o un error seguro.
            </td>
            <td>S4</td>
        </tr>
        <tr>
            <td>HU14</td>
            <td>Como consultor, quiero analizar la estructura de los tokens de sesión (JWT, etc.) para identificar si son predecibles, caducan o contienen información sensible.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Exposición de Datos en JWT (JSON Web Tokens)</strong><br>
                Given capturo un token de autenticación después de un inicio de sesión exitoso<br>
                When decodifico las tres partes del token (Header, Payload, Signature)<br>
                Then el Payload no debe contener información sensible (contraseñas, información financiera) sino solo identificadores de usuario y permisos, y el token debe tener una fecha de expiración (<code>exp</code>).
            </td>
            <td>S2</td>
        </tr>
        <tr>
            <td>HU15</td>
            <td>Como consultor, quiero evaluar si los logs de la aplicación registran eventos de seguridad críticos para permitir la detección de intrusiones y respuesta a incidentes.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Verificación de Registro de Eventos Críticos</strong><br>
                Given un ataque de SQL Injection fallido ha ocurrido<br>
                When se revisan los logs del servidor y de la aplicación<br>
                Then se debe encontrar una entrada detallada que registre el intento de inyección, la IP de origen y la hora, para fines de auditoría.
            </td>
            <td>S4</td>
        </tr>
        <tr>
            <td>HU16</td>
            <td>Como atacante, quiero interceptar y manipular las llamadas a la **API REST** para acceder a recursos de otros usuarios mediante *IDOR* (Insecure Direct Object Reference).</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Acceso a Datos de Terceros en API</strong><br>
                Given estoy autenticado como Usuario A y conozco el formato de ID de recurso (<code>/api/v1/user/101</code>)<br>
                When modifico la solicitud a <code>/api/v1/user/102</code><br>
                Then la API debe validar que el token de sesión pertenece solo al Usuario A y devolver un código <strong>403 (Forbidden)</strong> o <strong>401 (Unauthorized)</strong>.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU17</td>
            <td>Como consultor, quiero identificar si existen páginas de **Error y *Stack Traces*** detalladas expuestas públicamente.</td>
            <td>Should Have</td>
            <td>
                <strong>Scenario: Exposición de Información Sensible en Errores</strong><br>
                Given provoco un error de aplicación conocido (ej. parámetro inválido)<br>
                When reviso la página de respuesta y el código HTTP (ej. 500 Internal Server Error)<br>
                Then la respuesta no debe mostrar rutas de archivos, variables de entorno o *stack traces* del servidor, sino una página de error genérica.
            </td>
            <td>S2</td>
        </tr>
        <tr>
            <td>HU18</td>
            <td>Como atacante, quiero probar si puedo realizar una desconexión (Logout) en una sesión de otro usuario (**Session Fixation/CSRF**) para causar Denegación de Servicio (DoS).</td>
            <td>Could Have</td>
            <td>
                <strong>Scenario: Desconexión Forzada por CSRF</strong><br>
                Given un usuario está autenticado y tiene una sesión activa<br>
                When el atacante induce al usuario a hacer clic en un enlace de Logout sin token CSRF<br>
                Then el sistema debe requerir un token de validación de sesión (CSRF token) para cualquier acción crítica como el cierre de sesión, y la sesión del usuario no debe ser terminada.
            </td>
            <td>S3</td>
        </tr>
        <tr>
            <td>HU19</td>
            <td>Como consultor, quiero validar que todas las comunicaciones se realicen únicamente a través de canales cifrados para proteger la integridad y confidencialidad de los datos.</td>
            <td>Must Have</td>
            <td>
                <strong>Scenario: Forzar Conexión Insegura</strong><br>
                Given intento acceder al sitio usando la URL <code>https://tavolo.eastus2.cloudapp.azure.com/</code><br>
                When el navegador envía la solicitud HTTP<br>
                Then el servidor debe redirigir inmediatamente la conexión a <code>https://tavolo.eastus2.cloudapp.azure.com/</code> con el código HTTP 301 o 302, sin servir contenido sobre HTTP.
            </td>
            <td>S1</td>
        </tr>
    </tbody>
</table>


### 2.3. Planificación de sprints (Sprint Planning)

A continuación, se presenta la planificación de los 5 Sprints, estructurada para cubrir de manera incremental las fases de un Pentesting profesional (Reconocimiento, Escaneo, Enumeración, Explotación, Post-Explotación e Informe Final). Cada Sprint define sus Objetivos, las Actividades Técnicas a realizar, las Historias de Usuario (HU) que se comprometen a completar y los Entregables clave.


<table>
    <thead>
        <tr>
            <th>Sprint</th>
            <th>Objetivo del Sprint</th>
            <th>Actividades Técnicas</th>
            <th>Historias de Usuario (HU) Cubiertas</th>
            <th>Entregables (Artefactos)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>S1: Reconocimiento &amp; Escaneo</strong></td>
            <td>Mapear la superficie de ataque del objetivo, obteniendo información pasiva y activa de su infraestructura externa.</td>
            <td>
                <ul>
                    <li>Instalación y Configuración del entorno de laboratorio (Kali Linux).</li>
                    <li>Reconocimiento Pasivo (Google Hacking, Whois) para obtener dominios, IPs y contactos.</li>
                    <li>Escaneo de Puertos y Servicios (TCP/UDP) usando <code>Nmap</code> y <code>Masscan</code> para identificar puertos abiertos y versiones.</li>
                    <li>Validación de la configuración HTTPS y la directiva HSTS.</li>
                </ul>
            </td>
            <td>HU01, HU02, HU19</td>
            <td>
                <ul>
                    <li>Documento de Recolección de Información Pasiva (incluye IPs, dominios, contactos).</li>
                    <li>Reporte de Escaneo Activo (Listado de puertos abiertos y versiones de servicio con <code>Nmap</code>).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><strong>S2: Enumeración &amp; Vulnerabilidades</strong></td>
            <td>Profundizar en la información de los servicios activos e identificar vulnerabilidades conocidas, configuraciones erróneas y defensas débiles.</td>
            <td>
                <ul>
                    <li>Enumeración de Servicios específicos (DNS, SMB, SNMP) para obtener información detallada de la red.</li>
                    <li>Análisis Automatizado de Vulnerabilidades (Nessus, Burp) para descubrir vulnerabilidades conocidas (CVE, CVSS).</li>
                    <li>Análisis de Tokens de Sesión (JWT) y encabezados HTTP.</li>
                    <li>Pruebas de Configuración de Errores para evitar la exposición de <em>stack traces</em>.</li>
                </ul>
            </td>
            <td>HU04, HU05, HU10, HU14, HU17</td>
            <td>
                <ul>
                    <li>Matriz de Vulnerabilidades (Hallazgos verificados, incluyendo CVE y CVSS).</li>
                    <li>Reporte de Configuraciones Erradas (Encabezados HTTP, Tokens y Manejo de Errores).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><strong>S3: Explotación</strong></td>
            <td>Obtener acceso inicial al sistema mediante la explotación controlada de las vulnerabilidades más críticas identificadas.</td>
            <td>
                <ul>
                    <li>Explotación de Inyecciones (SQLi, XSS) en <em>endpoints</em> clave (ej. registro, login).</li>
                    <li>Pruebas de Broken Access Control (Horizontal y Vertical) y ataques IDOR en APIs.</li>
                    <li>Evaluación de la autenticación: Rate Limiting y lógica de negocio.</li>
                    <li>Uso de Frameworks de Explotación (Metasploit) y pruebas de Buffer Overflow para obtener acceso.</li>
                </ul>
            </td>
            <td>HU02, HU03, HU05, HU06, HU09, HU11, HU16, HU18</td>
            <td>
                <ul>
                    <li>Evidencia de Acceso Inicial (Captura de <em>shell</em> o sesión Meterpreter).</li>
                    <li>PoC (Proof of Concept) de Ataques Web (SQLi, BAC, XSS, etc.) exitosos.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><strong>S4: Post-Explotación &amp; Emergentes</strong></td>
            <td>Evaluar el impacto real al sistema y a los datos sensibles tras la explotación inicial, e integrar la seguridad en la nube y el análisis de logs.</td>
            <td>
                <ul>
                    <li>Escalada de Privilegios y Mantenimiento de Acceso para persistencia.</li>
                    <li>Extracción y <em>Dumping</em> de credenciales y <em>hashes</em>.</li>
                    <li>Pruebas de Unrestricted File Upload y Server-Side Template Injection (SSTI).</li>
                    <li>Evaluación de la seguridad en Entornos Cloud (AWS, Azure) para <em>misconfigurations</em>.</li>
                    <li>Verificación de Logging de eventos de seguridad para la detección de anomalías.</li>
                </ul>
            </td>
            <td>HU07, HU12, HU13, HU15</td>
            <td>
                <ul>
                    <li>Reporte de Post-Explotación (Evidencia de credenciales <em>dumped</em>, escalada).</li>
                    <li>Análisis de Seguridad en la Nube (Identificación de <em>misconfigurations</em>).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td><strong>S5: Informe Final</strong></td>
            <td>Documentar todos los hallazgos y generar un informe técnico y ejecutivo de alta calidad, proporcionando una hoja de ruta para la mitigación.</td>
            <td>
                <ul>
                    <li>Estructuración y Redacción del informe, incluyendo informe ejecutivo y técnico detallado.</li>
                    <li>Desarrollo del Plan de Remediación con recomendaciones específicas y prioritarias.</li>
                    <li>Incorporación de conceptos de Inteligencia Artificial aplicados a la detección de anomalías (como tendencia emergente).</li>
                    <li>Revisión y Edición Final del documento para asegurar cumplimiento con estándares (ej. NIST/PTES).</li>
                </ul>
            </td>
            <td>HU08</td>
            <td>
                <ul>
                    <li>Informe Final de Pentesting Profesional (Documento técnico y ejecutivo).</li>
                    <li>Presentación de Resultados (para el cliente/equipo de Tavolo).</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>


### 2.4. Definición de Done (DoD)


A continuación, se define la Definición de 'Done' (DoD) para cada Historia de Usuario, estableciendo los criterios de calidad y verificación que deben cumplirse para que un hallazgo de seguridad sea considerado terminado. Este proceso asegura que cada resultado esté respaldado por evidencia clara, sea reproducible y contenga un análisis de impacto válido para su posterior remediación.

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Historia de Usuario (HU)</th>
            <th>Criterios de "Done" (DoD)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HU01</td>
            <td>Escaneo de puertos y servicios públicos.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla del reporte de <code>Nmap</code> o <code>Masscan</code> con puertos y versiones.</li>
                    <li>Reproducibilidad: El comando de escaneo exacto utilizado está registrado.</li>
                    <li>Documentación: Se documentan todos los puertos abiertos y se establece la superficie de ataque.</li>
                    <li>Impacto: Se determina la reducción o expansión de la superficie de ataque inicial.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU02</td>
            <td>Prueba de SQL Injection en el registro (<code>/sign-up</code>).</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla de la solicitud/respuesta de Burp Suite que muestre la <em>payload</em> inyectada.</li>
                    <li>Reproducibilidad: La <em>payload</em> de inyección (<code>' OR 1=1 --</code>) y el campo exacto están registrados.</li>
                    <li>Documentación: Se registra si la prueba resultó en error seguro o en error de base de datos.</li>
                    <li>Impacto: Crítico si es vulnerable (acceso a DB).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU03</td>
            <td>Identificación de fallos de Broken Access Control.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla de la solicitud/respuesta que muestre la modificación del parámetro (ej. <code>id=102</code>) y el código de respuesta (idealmente 403).</li>
                    <li>Reproducibilidad: El parámetro modificado y el token de sesión están documentados.</li>
                    <li>Documentación: El fallo se clasifica como Horizontal o Vertical.</li>
                    <li>Impacto: Alto a Crítico (fuga de datos o acceso administrativo).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU04</td>
            <td>Escaneo con herramientas automatizadas.</td>
            <td>
                <ul>
                    <li>Evidencia: Reporte exportado de la herramienta (ej. Nessus) con hallazgos de criticidad Alta/Crítica.</li>
                    <li>Reproducibilidad: La configuración del escaneo está guardada.</li>
                    <li>Documentación: Solo los hallazgos validados manualmente (NO falsos positivos) se transfieren a la matriz final.</li>
                    <li>Impacto: Los hallazgos se priorizan según su puntuación CVSS.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU05</td>
            <td>Prueba de Tasa de Ataque (<em>Rate Limit</em>).</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de la respuesta del servidor (ej. código 429) o la aparición de un <em>captcha</em> después del límite de intentos.</li>
                    <li>Reproducibilidad: El script o configuración de Burp Intruder utilizado está guardado.</li>
                    <li>Documentación: Se registra si el sistema implementó bloqueo temporal o falló.</li>
                    <li>Impacto: Alto (permite fuerza bruta de credenciales) si el límite falla.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU06</td>
            <td>Vulnerabilidad a Cross-Site Scripting (XSS).</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla que muestre la <em>payload</em> no ejecutada, sino renderizada como texto plano (si es seguro).</li>
                    <li>Reproducibilidad: La <em>payload</em> XSS (ej. <code>&lt;script&gt;alert(1)&lt;/script&gt;</code>) y el campo de entrada están registrados.</li>
                    <li>Documentación: Se clasifica el tipo de XSS (Almacenado, Reflejado o DOM).</li>
                    <li>Impacto: Alto/Crítico si se ejecuta código arbitrario.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU07</td>
            <td>Documentar el acceso a información sensible (Post-Explotación).</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla verificable del archivo crítico (ej. <code>config.php</code>) que contiene credenciales de bases de datos.</li>
                    <li>Reproducibilidad: La ruta exacta del archivo y el método de acceso están registrados.</li>
                    <li>Documentación: Se registra la sensibilidad de la información expuesta.</li>
                    <li>Impacto: Crítico (compromiso total de sistemas internos).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU08</td>
            <td>Redactar el informe técnico, ejecutivo y plan de remediación.</td>
            <td>
                <ul>
                    <li>Evidencia: Archivo PDF final del Informe de Pentesting, completo y finalizado.</li>
                    <li>Reproducibilidad: El informe incluye todos los PoC validados y las referencias a las evidencias de cada HU.</li>
                    <li>Documentación: El informe cumple con la estructura profesional (NIST/PTES) y las recomendaciones son específicas.</li>
                    <li>Impacto: Documento final que consolida y mide el riesgo total.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU09</td>
            <td>Evaluar la lógica de negocio.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla de la solicitud modificada (ej. <code>price=-100</code>) y la respuesta del servidor (rechazo de lógica).</li>
                    <li>Reproducibilidad: Se registra el parámetro exacto manipulado y el valor no permitido.</li>
                    <li>Documentación: Se verifica que el <em>backend</em> realiza validaciones de negocio.</li>
                    <li>Impacto: Alto (pérdida financiera o corrupción de datos) si la manipulación es exitosa.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU10</td>
            <td>Examinar encabezados y <em>cookies</em> HTTP.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla de Burp Suite que muestre la presencia de encabezados de seguridad críticos (ej. <code>HSTS</code>, <code>X-Frame-Options</code>).</li>
                    <li>Reproducibilidad: La solicitud HTTP utilizada está registrada.</li>
                    <li>Documentación: Se lista si los encabezados críticos están presentes y configurados correctamente.</li>
                    <li>Impacto: Medio (riesgo de <em>clickjacking</em> o degradación de seguridad) si faltan.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU11</td>
            <td>Abuso de la funcionalidad "Olvidé mi Contraseña".</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla que demuestre el bloqueo de la cuenta o la aparición de un <em>captcha</em> después del límite de intentos.</li>
                    <li>Reproducibilidad: La secuencia de prueba de fuerza bruta del código de restablecimiento está documentada.</li>
                    <li>Documentación: Se registra el número de intentos antes de que se active la defensa.</li>
                    <li>Impacto: Alto (permite toma de cuenta si el código es débil o no hay límite).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU12</td>
            <td>Revisar el manejo de archivos subidos.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla que muestre la respuesta de rechazo del servidor al intentar subir un archivo de tipo no permitido (ej. <code>shell.php</code>).</li>
                    <li>Reproducibilidad: El nombre de archivo y el <em>MIME type</em> de prueba están registrados.</li>
                    <li>Documentación: Se verifica la validación por lista blanca de tipos MIME.</li>
                    <li>Impacto: Crítico (RCE - Ejecución Remota de Código) si la subida es exitosa.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU13</td>
            <td>Vulnerabilidad a Server-Side Template Injection (SSTI).</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla que muestre la <em>payload</em> inyectada (ej. <code>${{7*7}}</code>) y el resultado.</li>
                    <li>Reproducibilidad: La <em>payload</em> de prueba y el campo inyectado están registrados.</li>
                    <li>Documentación: Se identifica el motor de plantillas sospechoso.</li>
                    <li>Impacto: Crítico (RCE) si el servidor ejecuta la <em>payload</em> correctamente.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU14</td>
            <td>Analizar la estructura de los tokens de sesión (JWT).</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla de la herramienta de decodificación JWT que muestre el contenido del <em>Payload</em> decodificado.</li>
                    <li>Reproducibilidad: El token capturado está registrado.</li>
                    <li>Documentación: Se verifica que el <em>Payload</em> no contenga datos sensibles y que el campo <code>exp</code> esté presente.</li>
                    <li>Impacto: Alto (suplantación de identidad) si el token es débil o contiene datos sensibles.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU15</td>
            <td>Evaluar si los logs registran eventos de seguridad.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla de la consola o archivo de logs que muestre la entrada detallada del intento de ataque (SQLi o similar), incluyendo IP y hora.</li>
                    <li>Reproducibilidad: Se documenta el evento de seguridad generado por el consultor.</li>
                    <li>Documentación: Se registra qué sistema (WAF, App, OS) capturó la anomalía.</li>
                    <li>Impacto: Alto (incapacidad para detectar, auditar o responder a incidentes) si los logs son deficientes.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU16</td>
            <td>Interceptar y manipular las llamadas a la API REST (IDOR).</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de la solicitud/respuesta de Burp Suite que muestre la modificación del ID de recurso y la respuesta 403 o 401.</li>
                    <li>Reproducibilidad: La URL exacta del <em>endpoint</em> API y el ID de recurso modificado están registrados.</li>
                    <li>Documentación: Se verifica que la validación del token de sesión se extienda a la propiedad del recurso.</li>
                    <li>Impacto: Crítico (fuga de datos masiva o manipulación de datos de terceros) si la prueba es exitosa.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU17</td>
            <td>Identificar páginas de Error y <em>Stack Traces</em> expuestas.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla que muestre el error provocado (ej. HTTP 500) y que la página de error es genérica, sin mostrar información del servidor.</li>
                    <li>Reproducibilidad: Se registra el método exacto para provocar el error.</li>
                    <li>Documentación: Se verifica que la respuesta del servidor no filtre información interna.</li>
                    <li>Impacto: Medio (fuga de información del <em>stack</em> tecnológico del servidor).</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU18</td>
            <td>Probar si se puede realizar una desconexión (<em>Logout</em>) CSRF.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de pantalla que demuestre que la sesión de la víctima NO fue terminada, o que la solicitud de <em>logout</em> requiere un CSRF token.</li>
                    <li>Reproducibilidad: Se documenta la forma en que se intentó forzar el <em>logout</em>.</li>
                    <li>Documentación: Se verifica la presencia del token CSRF en acciones críticas de gestión de sesión.</li>
                    <li>Impacto: Bajo (DoS a un usuario) si la prueba es exitosa.</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>HU19</td>
            <td>Validar que todas las comunicaciones se realicen únicamente a través de canales cifrados.</td>
            <td>
                <ul>
                    <li>Evidencia: Captura de la respuesta HTTP que muestre el código de redirección 301 o 302 al acceder por <code>http://</code>.</li>
                    <li>Reproducibilidad: El comando de <code>curl</code> o el intento de acceso HTTP están registrados.</li>
                    <li>Documentación: Se verifica que toda la comunicación obligue a usar HTTPS.</li>
                    <li>Impacto: Alto (riesgo de <em>sniffing</em>) si la comunicación HTTP simple no es redirigida o bloqueada.</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### 2.5. Herramientas

La ejecución exitosa de los Sprints de Pentesting requiere el uso de herramientas específicas que se alinean con las fases de la metodología. A continuación, se enumeran las herramientas obligatorias y las recomendadas, explicando su contribución a las fases del proyecto.


<table>
    <thead>
        <tr>
            <th>Herramienta</th>
            <th>Tipo</th>
            <th>Fases de Contribución</th>
            <th>Explicación de la Contribución</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Kali Linux</strong> </td>
            <td>Sistema Operativo / Plataforma</td>
            <td>S1 a S5 (Todo el Proyecto)</td>
            <td>Es la <strong>plataforma base</strong> que integra todas las utilidades. Proporciona el entorno preconfigurado para ejecutar las pruebas, desde el escaneo hasta la post-explotación.</td>
        </tr>
        <tr>
            <td><strong>Nmap</strong></td>
            <td>Escáner de Red</td>
            <td>S1: Reconocimiento &amp; Escaneo</td>
            <td>Fundamental para el <strong>mapeo de la infraestructura</strong>. Identifica hosts activos, escanea puertos abiertos, detecta versiones de servicios y sistemas operativos (HU01).</td>
        </tr>
        <tr>
            <td><strong>Wireshark</strong></td>
            <td>Analizador de Protocolos</td>
            <td>S1: Reconocimiento &amp; Escaneo</td>
            <td>Permite la <strong>captura y análisis del tráfico de red</strong> en tiempo real. Es crucial para identificar información sensible o debilidades en los protocolos de comunicación.</td>
        </tr>
        <tr>
            <td><strong>Burp Suite</strong></td>
            <td>Proxy Web Interceptor</td>
            <td>S2: Enumeración &amp; S3: Explotación</td>
            <td>Esencial para la <strong>intercepción y modificación de solicitudes HTTP/S</strong>. Se usa para la prueba manual de vulnerabilidades en aplicaciones web, como Inyecciones, XSS, y Broken Access Control (HU02, HU03).</td>
        </tr>
        <tr>
            <td><strong>Metasploit</strong></td>
            <td>Framework de Explotación</td>
            <td>S3: Explotación &amp; S4: Post-Explotación</td>
            <td>Proporciona una amplia base de datos de <strong>exploits y payloads</strong> para obtener <strong>acceso inicial</strong> al sistema y realizar tareas de post-explotación, como el *dumping* de credenciales.</td>
        </tr>
        <tr>
            <td><strong>sqlmap</strong></td>
            <td>Inyección SQL Automatizada</td>
            <td>S3: Explotación</td>
            <td>Herramienta especializada para la <strong>detección y explotación automatizada de fallas de inyección SQL</strong> (HU02), permitiendo la enumeración de bases de datos y la extracción de datos sensibles.</td>
        </tr>
        <tr>
            <td><strong>Nessus / OpenVAS</strong> (Recomendadas)</td>
            <td>Escáner de Vulnerabilidades</td>
            <td>S2: Enumeración &amp; Vulnerabilidades</td>
            <td>Ejecutan <strong>escaneos automatizados y profundos</strong> (HU04). Identifican software obsoleto, configuraciones erróneas y mapean vulnerabilidades conocidas con su respectivo puntaje CVSS.</td>
        </tr>
        <tr>
            <td><strong>MobSF (Mobile Security Framework)</strong> (Recomendada)</td>
            <td>Análisis de Aplicaciones Móviles</td>
            <td>S3: Explotación &amp; S4: Post-Explotación</td>
            <td>Recomendado para escenarios móviles, facilita el <strong>análisis estático y dinámico de aplicaciones</strong> (APKs/ZIPs), evaluando el manejo de tokens, APIs y el almacenamiento de datos sensibles.</td>
        </tr>
    </tbody>
</table>