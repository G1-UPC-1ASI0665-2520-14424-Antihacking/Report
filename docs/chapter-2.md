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

### 2.4. Definición de Done (DoD)

### 2.5. Herramientas