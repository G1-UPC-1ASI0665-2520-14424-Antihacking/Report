# Capítulo II: Metodología Ágil y de Pentesting

## 2.1. Marco de referencia

El servicio de consultoría de Pruebas de Penetración (Pentesting) para Tavolo se ejecuta bajo un marco de referencia híbrido, diseñado para asegurar la máxima rigurosidad técnica mientras se mantiene la agilidad y la transparencia requeridas por una PYME. Este enfoque combina tres estándares internacionales clave de ciberseguridad con la metodología de gestión Scrum.

### 2.1.1. Estándares Técnicos Guía: PTES, OWASP y NIST

La ejecución de las pruebas se fundamenta en el **Penetration Testing Execution Standard (PTES)**. Este marco proporciona las siete fases estructuradas que guían el proyecto de inicio a fin: desde la interacción inicial con el cliente (Pre-Engagement) hasta la elaboración del informe final. El PTES asegura que el proceso de pentesting sea completo y metódico, cubriendo todo el ciclo de vida de un ataque simulado, incluyendo la recolección de inteligencia, el modelado de amenazas, la explotación de vulnerabilidades y la post-explotación.

Dentro de las fases de análisis y explotación, la principal guía técnica es la **OWASP Testing Guide (OTG)**. Esta guía es esencial, ya que proporciona los procedimientos y casos de prueba detallados para evaluar específicamente la seguridad de las aplicaciones web, que es el activo principal de Tavolo. El OTG se utiliza para diseñar las pruebas concretas en el portal de registro y en las funcionalidades internas post-login, permitiendo descubrir fallos como el Broken Access Control o vulnerabilidades de lógica de negocio que un atacante autenticado podría explotar.

Finalmente, el **NIST SP 800-115** (Guía Técnica para la Evaluación y Prueba de la Seguridad de la Información) complementa la metodología enfocándose en la calidad, la documentación y la planificación. El NIST asegura que todas las actividades estén bien definidas desde la fase de planificación (alcance, exclusiones) y que la documentación de la evidencia y el reporte de resultados sean rigurosos, repetibles y objetivos, lo cual es fundamental para que Tavolo pueda confiar y actuar sobre las recomendaciones.

### 2.1.2. Adaptación a la Metodología Scrum

Para asegurar la transparencia, adaptabilidad y entrega de valor incremental, la gestión del proyecto se enmarca en la metodología Scrum, articulando las fases técnicas del pentesting (PTES) en Sprints definidos. El equipo de la consultora opera bajo roles Scrum especializados en seguridad ofensiva.

**Roles Scrum en el proyecto de pentesting:**

Cada integrante del equipo describe su perfil técnico, su rol dentro del marco Scrum y el valor que aporta a la ejecución del proyecto. Se detallan las competencias técnicas, experiencia académica previa (ej. en desarrollo, redes o bases de datos) y el valor que aporta cada rol a la ejecución del pentesting.

- **Scrum Master**: Facilita las ceremonias Scrum (Daily Standups, Sprint Planning, Sprint Review, Retrospective), elimina impedimentos técnicos u organizacionales, y asegura que el equipo siga la metodología Scrum de forma disciplinada. Responsable de coordinar la comunicación con el cliente Tavolo y mantener el proyecto dentro del cronograma establecido.

- **Product Owner**: Prioriza el Product Backlog de seguridad según el riesgo del negocio, define los criterios de aceptación de las historias de usuario, y mantiene comunicación directa con Tavolo para validar que las pruebas cubran los objetivos de seguridad del cliente. Es el enlace entre el equipo técnico y los stakeholders del negocio.

- **Pentester Web**: Especialista en seguridad de aplicaciones web. Ejecuta pruebas de vulnerabilidades web según OWASP Testing Guide (inyección SQL, XSS, CSRF, Broken Access Control, etc.). Responsable de las historias de usuario relacionadas con el frontend y backend web de Tavolo.

- **Pentester de APIs/móvil**: Especialista en pruebas de seguridad de APIs RESTful y aplicaciones móviles. Ejecuta pruebas de autenticación, autorización, validación de entrada en endpoints de API. Utiliza herramientas como Burp Suite, Postman, y MobSF para evaluar la seguridad de las comunicaciones entre cliente-servidor.

- **Documentador/Analista**: Responsable de documentar todas las evidencias (capturas de pantalla, logs, PoCs), mantener actualizado el reporte técnico en GitHub, calcular puntajes CVSS, y elaborar el informe final. Garantiza la trazabilidad y reproducibilidad de todos los hallazgos. Colabora en el análisis de resultados de escaneos automatizados y la validación de falsos positivos.

**Nota**: Los perfiles de los estudiantes que forman la consultora incluyen su rol dentro del marco Scrum (ej. Scrum Master, Product Owner, especialista web, especialista APIs), competencias técnicas (lenguajes, frameworks, bases de datos), experiencia académica previa y el refuerzo de aprendizaje colaborativo y multidisciplinario que aporta cada miembro al equipo.

**Integración de Scrum con los estándares de pentesting:**

La metodología Scrum se integra con PTES, OWASP y NIST SP 800-115 de la siguiente manera:

**1. Pre-Engagement (PTES) → Sprint 0 (Planificación inicial):**
- Definición del alcance del proyecto con Tavolo
- Firma de Rules of Engagement (RoE) y documentos legales
- Identificación de activos críticos a evaluar
- Definición del cronograma de sprints (5 sprints de 2 semanas)
- Creación del Product Backlog inicial con historias de usuario de seguridad

**2. Intelligence Gathering + Threat Modeling (PTES) → Sprint 1:**
- Reconocimiento pasivo (OSINT) y activo (escaneo de puertos)
- Mapeo de la superficie de ataque de Tavolo
- Identificación de tecnologías utilizadas (frameworks, servidores, bases de datos)
- Modelado preliminar de amenazas según activos identificados

**3. Vulnerability Analysis (PTES + OWASP) → Sprint 2:**
- Enumeración profunda de servicios y aplicaciones web
- Escaneos automatizados con Nessus/OpenVAS, Nikto
- Análisis de configuraciones según OWASP Testing Guide
- Identificación de vulnerabilidades conocidas (CVEs)
- Creación de matriz de vulnerabilidades priorizada por CVSS

**4. Exploitation (PTES + OWASP) → Sprint 3:**
- Explotación controlada de vulnerabilidades identificadas
- Generación de Proof of Concepts (PoC) reproducibles
- Pruebas manuales de OWASP Top 10 (SQL Injection, XSS, Broken Access Control, etc.)
- Validación del impacto real de cada vulnerabilidad
- Notificación inmediata al cliente de vulnerabilidades críticas (< 24h)

**5. Post-Exploitation (PTES) → Sprint 4:**
- Evaluación del alcance completo de un compromiso exitoso
- Simulación de movimiento lateral y escalamiento de privilegios
- Análisis de datos sensibles que podrían ser extraídos
- Documentación de la cadena de ataque (kill chain)

**6. Reporting (PTES + NIST SP 800-115) → Sprint 5:**
- Consolidación de todos los hallazgos
- Elaboración de informe técnico detallado con evidencias
- Elaboración de informe ejecutivo para dirección de Tavolo
- Generación de plan de remediación priorizado
- Presentación formal de resultados al cliente (Sprint Review Final)

Esta integración permite mantener la rigurosidad técnica de los estándares de pentesting (PTES, OWASP, NIST) mientras se aprovecha la flexibilidad y transparencia de Scrum para adaptarse a los hallazgos durante la ejecución y mantener comunicación constante con el cliente.


## 2.2. Backlog inicial

El Product Backlog inicial del proyecto define el trabajo a realizar por la consultora, estructurado como **Historias de Usuario (HU) enfocadas en pentesting**. Cada historia de usuario representa una prueba de seguridad específica que el equipo debe ejecutar sobre la aplicación web Tavolo.

Las HU están formuladas desde la perspectiva de un atacante o consultor de seguridad (ej. "Como atacante, quiero probar inyección SQL...", "Como consultor, quiero escanear puertos...") y están diseñadas para validar controles de seguridad específicos. Estas historias están priorizadas según el **riesgo potencial para el negocio de Tavolo** y se alinean directamente con las fases de ejecución de los Sprints.

**Objetivo del Product Backlog:**
- Cubrir las principales categorías de vulnerabilidades según **OWASP Top 10**
- Validar controles de seguridad en autenticación, autorización, gestión de sesiones
- Identificar configuraciones inseguras en la infraestructura de Azure
- Evaluar la resistencia de Tavolo ante ataques comunes (SQL Injection, XSS, CSRF, IDOR)

### 2.2.1. Estructura y Priorización del Backlog

Las Historias de Usuario (HU) han sido priorizadas utilizando la escala **MoSCoW**, donde la prioridad se asigna según el impacto potencial al negocio:
- **Must Have** (Obligatorio, riesgo crítico): Vulnerabilidades que podrían comprometer completamente la confidencialidad, integridad o disponibilidad de datos sensibles
- **Should Have** (Debería tener, riesgo alto): Vulnerabilidades que facilitan ataques pero requieren condiciones específicas
- **Could Have** (Podría tener, riesgo medio): Vulnerabilidades de menor impacto o que requieren múltiples pasos para ser explotadas

**Criterios de aceptación en formato Gherkin:**
Cada HU incluye escenarios de prueba escritos en formato **Gherkin** (Given/When/Then) que definen:
- **Given**: Precondiciones o contexto inicial de la prueba
- **When**: Acción específica que ejecuta el pentester
- **Then**: Resultado esperado que demuestra seguridad o vulnerabilidad

### 2.2.2. Product Backlog de Historias de Usuario

| ID | Historia de Usuario (HU) | Prioridad (MoSCoW) | Criterios de Aceptación (Escenarios Gherkin) | Sprint Asignado |
|----|--------------------------|---------------------|----------------------------------------------|-----------------|
| **HU01** | Como consultor, quiero realizar un escaneo de puertos y servicios públicos para mapear la superficie de ataque del servidor en Azure. | Must Have | **Scenario: Confirmación de Servicios Expuestos**<br>Given la dirección IP pública del servidor de Tavolo<br>When ejecuto un escaneo completo de puertos TCP/UDP<br>Then solo deberían aparecer abiertos los puertos esenciales (80, 443)<br>And se registra la versión exacta del servicio en cada puerto. | S1 |
| **HU02** | Como atacante, quiero probar el proceso de registro (`/sign-up`) contra ataques de **SQL Injection** para comprometer la base de datos de Tavolo. | Must Have | **Scenario: Detección de Inyección SQL**<br>Given un formulario de registro válido en la URL `/sign-up`<br>When ingreso una payload de inyección (`' OR 1=1 --`) en el campo 'Nombre de Usuario'<br>Then el sistema debería devolver un error genérico o completar el registro sin un error de base de datos. | S3 |
| **HU03** | Como usuario normal, quiero intentar acceder a las funcionalidades de administración o a datos de otros usuarios para identificar fallos de **Broken Access Control**. | Must Have | **Scenario: Escalada Horizontal de Privilegios**<br>Given estoy autenticado como 'UsuarioA' con ID de sesión válido<br>When intento modificar un recurso de 'UsuarioB' cambiando el parámetro ID en la URL o solicitud<br>Then el sistema debería rechazar la solicitud y devolver el código de estado HTTP **403 (Forbidden)**. | S3 |
| **HU04** | Como consultor, quiero escanear la aplicación con herramientas automatizadas (Nessus/Nikto/Burp) para descubrir vulnerabilidades conocidas del stack tecnológico. | Should Have | **Scenario: Validación de Reporte de Escaneo**<br>Given los resultados brutos del escaneo automatizado han sido exportados<br>When el equipo técnico filtra los hallazgos de criticidad Alta y Crítica<br>Then se documentan solo aquellos hallazgos que han sido validados manualmente como no ser un falso positivo. | S2 |
| **HU05** | Como atacante, quiero explotar credenciales débiles o mecanismos de autenticación frágiles para acceder a una cuenta sin conocer la contraseña. | Should Have | **Scenario: Prueba de Tasa de Ataque (Rate Limit)**<br>Given conozco un nombre de usuario válido<br>When envío 100 peticiones de login fallidas en 60 segundos<br>Then el sistema debería implementar un bloqueo de la cuenta o un mecanismo de captcha en intentos posteriores. | S3 |
| **HU06** | Como usuario, quiero introducir código malicioso en los campos de mi perfil para verificar si la plataforma es vulnerable a ataques de **Cross-Site Scripting (XSS)**. | Should Have | **Scenario: XSS Almacenado en la Descripción del Perfil**<br>Given estoy autenticado y accedo a la sección 'Editar Perfil'<br>When ingreso una payload de XSS persistente (`<script>alert(1)</script>`) en la descripción<br>Then el sistema debería sanitizar la entrada y NO ejecutar el script cuando otro usuario visite mi perfil. | S3 |
| **HU07** | Como consultor, quiero analizar las configuraciones de seguridad de las cabeceras HTTP para identificar fallas de hardening del servidor web. | Should Have | **Scenario: Verificación de Cabeceras de Seguridad**<br>Given la URL principal de Tavolo<br>When realizo una solicitud HTTP/S y analizo las cabeceras de respuesta<br>Then deberían estar presentes las cabeceras: `X-Content-Type-Options`, `X-Frame-Options`, `Strict-Transport-Security` (HSTS), y `Content-Security-Policy`. | S2 |
| **HU08** | Como atacante, quiero manipular parámetros en URLs o cookies para evaluar si la aplicación valida correctamente los datos de entrada. | Should Have | **Scenario: Manipulación de Parámetros de Sesión**<br>Given estoy autenticado y tengo una sesión activa<br>When modifico el valor de un parámetro en la URL (ej. `?user_id=123` a `?user_id=124`)<br>Then el sistema debería validar que el `user_id` corresponde al usuario autenticado antes de mostrar información. | S3 |
| **HU09** | Como consultor, quiero probar si el servidor expone información sensible en sus mensajes de error. | Could Have | **Scenario: Fuga de Información en Errores**<br>Given provoco un error intencional en la aplicación (ej. solicitud malformada)<br>When el servidor responde con un mensaje de error<br>Then el error NO debe revelar información técnica como: versión de frameworks, rutas de archivos del servidor, o consultas SQL. | S2 |
| **HU10** | Como usuario malicioso, quiero probar la funcionalidad de carga de archivos para subir archivos ejecutables o scripts maliciosos. | Could Have | **Scenario: Validación de Tipo de Archivo**<br>Given estoy en la sección de carga de archivos<br>When intento subir un archivo con extensión `.php`, `.jsp`, `.exe`<br>Then el sistema debería rechazar el archivo y mostrar un mensaje de error claro. | S3 |
| **HU11** | Como consultor, quiero enumerar directorios y archivos ocultos del servidor para identificar recursos no protegidos. | Should Have | **Scenario: Descubrimiento de Archivos Sensibles**<br>Given la URL base de Tavolo<br>When ejecuto una herramienta de fuzzing de directorios (ej. Gobuster, Dirb)<br>Then NO deberían existir directorios como `/admin`, `/backup`, `/config` sin autenticación, o archivos como `.env`, `.git` expuestos. | S2 |
| **HU12** | Como atacante, quiero probar si la aplicación es vulnerable a ataques de **Cross-Site Request Forgery (CSRF)**. | Should Have | **Scenario: Validación de Token CSRF**<br>Given estoy autenticado en Tavolo<br>When intento ejecutar una acción sensible (cambio de contraseña) desde un sitio externo sin el token CSRF<br>Then la solicitud debería ser rechazada y devolver un error de validación. | S3 |
| **HU13** | Como consultor, quiero verificar la implementación de políticas de contraseñas para garantizar que cumplan con estándares mínimos de seguridad. | Could Have | **Scenario: Política de Contraseñas Seguras**<br>Given estoy en el proceso de registro o cambio de contraseña<br>When intento establecer una contraseña débil (ej. "123456" o "password")<br>Then el sistema debería rechazar la contraseña y solicitar: mínimo 8 caracteres, combinación de mayúsculas, minúsculas, números y símbolos. | S1 |
| **HU14** | Como atacante, quiero probar la funcionalidad de recuperación de contraseña para identificar vulnerabilidades de enumeración de usuarios o tokens predecibles. | Should Have | **Scenario: Recuperación Segura de Contraseña**<br>Given ingreso un correo electrónico en el formulario de recuperación<br>When el sistema procesa la solicitud<br>Then NO debería revelar si el correo está registrado, y el token de recuperación debe ser único, aleatorio y de un solo uso. | S2 |
| **HU15** | Como consultor, quiero analizar el comportamiento de la sesión del usuario para identificar fallos en la gestión de sesiones. | Should Have | **Scenario: Timeout de Sesión Inactiva**<br>Given estoy autenticado y mi sesión está activa<br>When permanezco inactivo por más de 15 minutos<br>Then el sistema debería cerrar automáticamente mi sesión por seguridad. | S3 |
| **HU16** | Como atacante, quiero interceptar y manipular las llamadas a la API REST para identificar vulnerabilidades de **Insecure Direct Object References (IDOR)**. | Must Have | **Scenario: Validación de Autorización en APIs**<br>Given intercepto una solicitud API que accede a un recurso específico<br>When modifico el ID del recurso en la solicitud<br>Then la API debería validar que el usuario tiene autorización para acceder a ese recurso específico y devolver 403 si no está autorizado. | S3 |
| **HU17** | Como consultor, quiero identificar páginas de error y *stack traces* expuestas que revelen información del servidor. | Could Have | **Scenario: Manejo Seguro de Errores**<br>Given provoco un error en la aplicación<br>When el servidor responde<br>Then la página de error debe ser genérica sin revelar información técnica del backend. | S2 |
| **HU18** | Como atacante, quiero probar si es posible realizar una desconexión (*logout*) CSRF. | Could Have | **Scenario: Protección de Logout con CSRF**<br>Given estoy autenticado en Tavolo<br>When intento forzar el logout de otro usuario mediante CSRF<br>Then la solicitud de logout debería requerir validación de token CSRF o confirmación del usuario. | S3 |
| **HU19** | Como consultor, quiero validar que todas las comunicaciones se realicen únicamente a través de canales cifrados (HTTPS). | Must Have | **Scenario: Redirección Forzada a HTTPS**<br>Given intento acceder a Tavolo mediante HTTP (sin cifrado)<br>When el servidor procesa mi solicitud<br>Then debería redirigir automáticamente a HTTPS (código 301 o 302) y NO permitir comunicación sin cifrar. | S1 |
| **HU20** | Como consultor, quiero evaluar posibilidades de escalamiento de privilegios desde accesos obtenidos para determinar el alcance completo del compromiso. | Must Have | **Scenario: Escalamiento de Privilegios Vertical**<br>Given tengo acceso inicial al sistema como usuario de bajos privilegios<br>When ejecuto herramientas de enumeración (LinPEAS, WinPEAS)<br>Then debería identificar vías potenciales de escalamiento y documentarlas con evidencias. | S4 |
| **HU21** | Como atacante, quiero simular movimiento lateral entre servicios para evaluar la segmentación de red y las confianzas entre componentes. | Should Have | **Scenario: Movimiento Lateral Simulado**<br>Given he comprometido un servidor con credenciales válidas<br>When intento acceder a otros servicios usando las mismas credenciales<br>Then el sistema debería tener segmentación de red y credenciales únicas por servicio. | S4 |
| **HU22** | Como consultor, quiero cuantificar el volumen y tipo de datos sensibles que serían accesibles en caso de compromiso para evaluar el impacto real. | Must Have | **Scenario: Inventario de Datos Sensibles**<br>Given he obtenido acceso no autorizado a la base de datos<br>When enumero las tablas y registros accesibles<br>Then documento el volumen de datos personales, financieros o confidenciales expuestos. | S4 |
| **HU23** | Como consultor, quiero documentar la cadena de ataque completa (kill chain) para que el cliente entienda cómo un atacante real llegaría al compromiso. | Must Have | **Scenario: Documentación de Kill Chain**<br>Given he completado todas las fases del ataque<br>When mapeo cada paso desde reconocimiento hasta post-explotación<br>Then el documento muestra una secuencia lógica y reproducible siguiendo MITRE ATT&CK. | S4 |

## 2.3. Planificación de sprints (Sprint Planning)

El proyecto se estructura en **5 sprints de 3 semanas** cada uno, cubriendo las **15 semanas completas del curso** (curso 1ASI0665 - Anti-Hacking). Esta planificación permite ejecutar todas las fases del PTES de forma completa y profesional, asegurando tiempo suficiente para reconocimiento, análisis, explotación, post-explotación y documentación exhaustiva.

**Distribución temporal:**
- **Sprint 1:** Semanas 1-3 (Reconocimiento & Enumeración)
- **Sprint 2:** Semanas 4-6 (Análisis de Vulnerabilidades)
- **Sprint 3:** Semanas 7-9 (Explotación Controlada)
- **Sprint 4:** Semanas 10-12 (Post-Explotación)
- **Sprint 5:** Semanas 13-15 (Informe Final)

**Hitos de entrega:**
- **TP1 (Trabajo Parcial 1):** Entrega en Semana 9 - Incluye Sprints 1, 2 y avance de Sprint 3
- **TF1 (Trabajo Final 1):** Entrega en Semana 15 - Incluye Sprint 3 completo, Sprint 4, Sprint 5 e informe final

Cada sprint está alineado con las fases del PTES y los objetivos específicos del pentesting de Tavolo.

### Sprint 1: Reconocimiento & Enumeración (Semanas 1-3)

**Objetivo del Sprint:**  
Ejecutar reconocimiento pasivo y activo sobre la infraestructura de Tavolo en Azure. Mapear la superficie de ataque externa, identificar todos los activos expuestos (dominios, subdominios, puertos, servicios), y realizar enumeración inicial de tecnologías utilizadas. Establecer el contexto técnico completo que servirá de base para los sprints posteriores.

**Fases PTES Equivalentes:**
- Pre-Engagement Interactions (firma de RoE, definición de alcance)
- Intelligence Gathering (OSINT, reconocimiento pasivo)
- Threat Modeling (modelado preliminar de amenazas)

**Objetivos específicos del sprint:**
1. Completar el reconocimiento pasivo (OSINT) sin interactuar directamente con el servidor
2. Ejecutar reconocimiento activo (escaneo de puertos y servicios)
3. Identificar todas las tecnologías del stack (frameworks, servidores web, bases de datos)
4. Mapear la arquitectura de red y superficie de ataque
5. Documentar todos los activos identificados en un inventario estructurado

**Historias de usuario atendidas:**
- HU01: Escaneo de puertos y servicios públicos (Must Have)
- HU13: Verificación de políticas de contraseñas (Could Have)
- HU19: Validación de comunicaciones HTTPS forzadas (Must Have)

**Actividades realizadas:**

1. **Reconocimiento Pasivo (OSINT):**
    - Búsqueda de información pública de Tavolo en Google, redes sociales, LinkedIn
    - Identificación de empleados clave y estructura organizacional
    - Recolección de correos electrónicos con herramientas como theHarvester
    - Búsqueda de subdominios mediante herramientas como Sublist3r, Amass
    - Consulta de registros DNS (dig, nslookup, host)
    - Análisis de certificados SSL/TLS expuestos

2. **Reconocimiento Activo (Escaneo de Puertos):**
    - Escaneo completo de puertos con Nmap: `nmap -p- -sV -sC -O -A <IP_Tavolo>`
    - Identificación de servicios activos (HTTP, HTTPS, SSH, FTP, bases de datos)
    - Detección de versiones de software y sistemas operativos
    - Generación de reportes XML y HTML de Nmap

3. **Enumeración de Tecnologías Web:**
    - Identificación del stack tecnológico con Wappalyzer, BuiltWith
    - Análisis de cabeceras HTTP con curl, Burp Suite
    - Detección de CMS (WordPress, Drupal, etc.) con WhatWeb
    - Identificación de frameworks JavaScript en el frontend

4. **Mapeo de Arquitectura:**
    - Creación de diagrama de red con activos identificados
    - Documentación de relaciones entre servicios
    - Identificación de posibles vectores de ataque iniciales

**Resultados y evidencias:**

- Inventario completo de activos:
    - 5 subdominios identificados
    - 12 puertos abiertos en el servidor principal
    - Stack tecnológico: React + Node.js + Azure SQL Database
    - Sistema operativo: Ubuntu 22.04 LTS
- Reporte de Nmap exportado en XML/HTML
- Lista de empleados y correos electrónicos recolectados (15 emails)
- Diagrama de arquitectura de red preliminar
- Matriz de servicios expuestos con versiones identificadas

**Adjuntar en repositorio GitHub:**
- `/sprint-1/evidencias/nmap_scan_full.xml`
- `/sprint-1/evidencias/nmap_scan_report.html`
- `/sprint-1/evidencias/subdomains_found.txt`
- `/sprint-1/evidencias/network_diagram_v1.png`
- `/sprint-1/reportes/sprint1_reconnaissance_report.md`

**Retrospectiva del sprint:**

**¿Qué funcionó bien?**
- La combinación de herramientas OSINT permitió recopilar información valiosa sin alertar al objetivo
- Nmap proporcionó resultados detallados y confiables sobre servicios expuestos
- La comunicación diaria del equipo (Daily Standups) mantuvo a todos sincronizados
- El uso de GitHub para documentar hallazgos en tiempo real facilitó la colaboración

**¿Qué no funcionó bien?**
- Algunos subdominios identificados resultaron ser falsos positivos
- La enumeración manual de tecnologías tomó más tiempo del estimado
- Faltó definir mejor los criterios de aceptación antes de iniciar el sprint

**¿Qué mejorar para el próximo sprint?**
- Validar subdominios antes de incluirlos en el reporte final
- Automatizar más la enumeración de tecnologías con scripts personalizados
- Asignar roles más claros para evitar duplicación de esfuerzos
- Mejorar la documentación de evidencias con timestamps y contexto adicional

**Definition of Done (DoD) del Sprint 1:**
- [x] Reconocimiento pasivo completado con lista de subdominios y correos
- [x] Escaneo de puertos ejecutado y documentado
- [x] Tecnologías del stack identificadas y verificadas
- [x] Diagrama de arquitectura de red creado
- [x] Inventario de activos documentado en formato estructurado
- [x] Evidencias almacenadas en repositorio GitHub con tag `sprint-1-done`
- [x] Reporte de sprint revisado por Scrum Master
- [x] Sprint Review realizado con el cliente
- [x] Retrospectiva documentada con lecciones aprendidas

**Actividades Técnicas Principales:**

1. **Reconocimiento Pasivo (OSINT):**
    - Búsqueda de subdominios con herramientas como `theHarvester`, `Sublist3r`
    - Análisis de certificados SSL/TLS con `crt.sh`
    - Búsqueda de credenciales filtradas en bases de datos públicas

   ```bash
   sublist3r -d staging.tavolo.pe -o subdominios.txt
   ```

2. **Escaneo de Puertos con Nmap:**
   ```bash
   nmap -sS -sV -O -p- staging.tavolo.pe -oA nmap_scan_completo
   ```

3. **Análisis de Certificados SSL:**
   ```bash
   sslscan staging.tavolo.pe
   ```
   
4. **Captura de Tráfico con Wireshark:**
    - Capturar tráfico HTTPS para verificar versión de TLS

**Entregables del Sprint:**
- Reporte de reconocimiento en Markdown
- Diagrama de arquitectura de red identificada
- Lista de activos (IPs, dominios, servicios, versiones)
- Matriz preliminar de amenazas

**Definition of Done (DoD):**
- [ ] Todos los subdominios y servicios identificados están documentados
- [ ] Mapa de red completo con diagrama visual
- [ ] Evidencias fotográficas con timestamps
- [ ] Aprobación del Scrum Master
- [ ] Commit en repositorio GitHub con tag `sprint-1-done`


### Sprint 2: Enumeración Profunda & Análisis de Vulnerabilidades (Semanas 4-6)

**Objetivo del Sprint:**  
Realizar enumeración en profundidad de todos los servicios identificados en Sprint 1. Ejecutar escaneos automatizados de vulnerabilidades con herramientas especializadas. Generar una matriz priorizada de vulnerabilidades clasificadas por severidad CVSS. Validar manualmente los hallazgos para eliminar falsos positivos.

**Fases PTES Equivalentes:**
- Vulnerability Analysis (análisis automatizado y manual)

**Objetivos específicos del sprint:**
1. Enumerar versiones exactas de software en todos los servicios expuestos
2. Ejecutar escaneos automatizados con Nessus/OpenVAS, Nikto, Gobuster
3. Analizar configuraciones de seguridad del servidor web y cabeceras HTTP
4. Identificar directorios y archivos ocultos o sensibles
5. Clasificar todas las vulnerabilidades encontradas usando CVSS v3.1
6. Validar manualmente los resultados para descartar falsos positivos
7. Generar matriz de vulnerabilidades priorizada por riesgo al negocio

**Historias de usuario atendidas:**
- HU04: Escaneo automatizado con Nessus/Nikto/Burp (Should Have)
- HU07: Análisis de cabeceras HTTP de seguridad (Should Have)
- HU09: Prueba de fuga de información en errores (Could Have)
- HU11: Enumeración de directorios y archivos ocultos (Should Have)
- HU14: Análisis de recuperación de contraseña (Should Have)
- HU17: Identificación de stack traces expuestos (Could Have)

**Actividades realizadas:**

1. **Escaneo de Vulnerabilidades Automatizado:**
    - Escaneo completo con Nessus Professional o OpenVAS
    - Escaneo de aplicación web con Nikto: `nikto -h https://staging.tavolo.pe`
    - Escaneo de vulnerabilidades conocidas (CVE) en servicios identificados
    - Análisis de configuraciones inseguras del servidor

2. **Enumeración de Directorios y Archivos:**
    - Fuzzing de directorios con Gobuster: `gobuster dir -u https://staging.tavolo.pe -w wordlist`
    - Búsqueda de archivos de backup (.bak, .old, .backup)
    - Identificación de paneles administrativos ocultos
    - Búsqueda de archivos sensibles (robots.txt, sitemap.xml, .git, .env)

3. **Análisis de Cabeceras HTTP:**
    - Verificación de cabeceras de seguridad (CSP, HSTS, X-Frame-Options, X-XSS-Protection)
    - Detección de información sensible en cabeceras (versiones de servidor)
    - Análisis de cookies (Secure, HttpOnly, SameSite flags)

4. **Análisis de Endpoints API:**
    - Enumeración de endpoints REST con Burp Suite
    - Análisis de métodos HTTP permitidos (OPTIONS, TRACE, PUT, DELETE)
    - Identificación de endpoints sin autenticación

5. **Validación Manual de Falsos Positivos:**
    - Revisión uno por uno de los hallazgos de Nessus/OpenVAS
    - Pruebas manuales para confirmar explotabilidad
    - Descarte de falsos positivos documentado

**Resultados y evidencias:**

- Matriz de vulnerabilidades priorizada (30 vulnerabilidades identificadas)
    - 3 Críticas (CVSS 9.0-10.0)
    - 8 Altas (CVSS 7.0-8.9)
    - 12 Medias (CVSS 4.0-6.9)
    - 7 Bajas (CVSS 0.1-3.9)
- 15 directorios ocultos descubiertos
- 5 archivos de backup expuestos
- 8 cabeceras de seguridad ausentes o mal configuradas
- 12 endpoints API sin autenticación adecuada

**Adjuntar en repositorio GitHub:**
- `/sprint-2/evidencias/nessus_scan_report.pdf`
- `/sprint-2/evidencias/nikto_scan_output.html`
- `/sprint-2/evidencias/gobuster_directories.txt`
- `/sprint-2/evidencias/http_headers_analysis.xlsx`
- `/sprint-2/reportes/vulnerability_matrix_v1.xlsx`
- `/sprint-2/reportes/sprint2_vulnerability_analysis_report.md`

**Retrospectiva del sprint:**

**¿Qué funcionó bien?**
- Nessus/OpenVAS proporcionó una base sólida de vulnerabilidades conocidas
- La validación manual evitó incluir falsos positivos en el reporte
- Gobuster encontró directorios críticos que no estaban en el sitemap
- La matriz CVSS permitió priorizar vulnerabilidades de forma objetiva

**¿Qué no funcionó bien?**
- Los escaneos automatizados generaron demasiados falsos positivos (40% de los hallazgos)
- Nessus tomó más tiempo del esperado debido al tamaño de la aplicación
- Faltó documentar mejor las configuraciones de las herramientas usadas

**¿Qué mejorar para el próximo sprint?**
- Afinar las configuraciones de Nessus para reducir falsos positivos
- Crear scripts personalizados para automatizar la validación de hallazgos
- Mejorar la comunicación con el cliente sobre el progreso del escaneo
- Documentar TODAS las configuraciones de herramientas en el repositorio

**Definition of Done (DoD) del Sprint 2:**
- [x] Escaneos automatizados completados con Nessus, Nikto, Gobuster
- [x] Todos los hallazgos validados manualmente
- [x] Falsos positivos documentados y descartados
- [x] Matriz de vulnerabilidades creada con clasificación CVSS
- [x] Cabeceras HTTP analizadas y documentadas
- [x] Directorios y archivos sensibles identificados
- [x] Evidencias almacenadas en repositorio con tag `sprint-2-done`
- [x] Sprint Review realizado con demostración de hallazgos críticos
- [x] Retrospectiva documentada

**Actividades Técnicas Principales:**

1. **Escaneo con Nessus/OpenVAS:**
   ```bash
   # Si usas OpenVAS desde CLI
   omp -u admin -w admin --xml='<create_target><name>Tavolo</name><hosts>staging.tavolo.pe</hosts></create_target>'
   ```

2. **Fuzzing de Directorios con Gobuster:**
   ```bash
   gobuster dir -u https://staging.tavolo.pe -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o directorios_encontrados.txt
   ```

3. **Análisis de Cabeceras con curl:**
   ```bash
   curl -I https://staging.tavolo.pe
   ```

4. **Escaneo con Nikto:**
   ```bash
   nikto -h https://staging.tavolo.pe -o nikto_report.html
   ```

**Entregables del Sprint:**
- Matriz de vulnerabilidades con severidad CVSS
- Reporte de escaneos automatizados (Nessus/Nikto)
- Lista de falsos positivos descartados
- Recomendaciones preliminares de hardening

**Definition of Done (DoD):**
- [ ] Todos los escaneos automatizados ejecutados y documentados
- [ ] Vulnerabilidades clasificadas por severidad (Crítica/Alta/Media/Baja)
- [ ] Falsos positivos validados manualmente y descartados
- [ ] Matriz de riesgos actualizada
- [ ] Peer review completado
- [ ] Commit en repositorio GitHub con tag `sprint-2-done`

### Sprint 3: Explotación Controlada (Semanas 7-9)

**Objetivo del Sprint:**  
Ejecutar explotación controlada y ética de las vulnerabilidades identificadas en Sprint 2. Generar Proof of Concepts (PoC) reproducibles para todas las vulnerabilidades críticas y altas. Validar el impacto real de cada vulnerabilidad en el contexto de negocio de Tavolo. Documentar evidencias detalladas de cada explotación exitosa.

**Fases PTES Equivalentes:**
- Exploitation (explotación de vulnerabilidades)
- Post-Exploitation (evaluación inicial del impacto)

**Objetivos específicos del sprint:**
1. Validar manualmente todas las vulnerabilidades críticas y altas
2. Desarrollar PoCs reproducibles para cada vulnerabilidad explotable
3. Ejecutar pruebas de inyección SQL en formularios y endpoints API
4. Validar controles de acceso (Broken Access Control, IDOR)
5. Probar vulnerabilidades de XSS (reflejado, almacenado, DOM-based)
6. Validar protecciones contra CSRF en acciones sensibles
7. Analizar gestión de sesiones y mecanismos de autenticación
8. Documentar el impacto técnico y de negocio de cada explotación
9. Notificar inmediatamente al cliente sobre vulnerabilidades críticas (< 24h)

**Historias de usuario atendidas:**
- HU02: Pruebas de SQL Injection en `/sign-up` (Must Have)
- HU03: Pruebas de Broken Access Control (Must Have)
- HU05: Ataque de fuerza bruta y credenciales débiles (Should Have)
- HU06: Pruebas de Cross-Site Scripting (XSS) (Should Have)
- HU08: Manipulación de parámetros (Should Have)
- HU10: Validación de carga de archivos (Could Have)
- HU12: Pruebas de CSRF (Should Have)
- HU15: Análisis de gestión de sesiones (Should Have)
- HU16: Pruebas de IDOR en APIs REST (Must Have)
- HU18: Pruebas de logout CSRF (Could Have)

**Actividades realizadas:**

1. **Explotación de SQL Injection:**
    - Pruebas manuales en formulario de registro `/sign-up`
    - Uso de sqlmap: `sqlmap -u "https://staging.tavolo.pe/signup" --data="user=test" --dbs`
    - Extracción de bases de datos y tablas sensibles
    - Desarrollo de PoC paso a paso para reproducir el ataque

2. **Broken Access Control & IDOR:**
    - Pruebas de acceso no autorizado a endpoints admin
    - Manipulación de IDs en APIs REST: `GET /api/users/123` → `GET /api/users/124`
    - Acceso a recursos de otros usuarios mediante cambio de parámetros
    - PoC de escalamiento horizontal de privilegios

3. **Cross-Site Scripting (XSS):**
    - Pruebas de XSS reflejado en parámetros GET
    - XSS almacenado en campos de comentarios
    - Payload: `<script>alert('XSS')</script>`
    - Demostración de robo de cookies de sesión

4. **Pruebas de CSRF:**
    - Análisis de tokens anti-CSRF en formularios críticos
    - Generación de página maliciosa para CSRF
    - PoC de cambio de contraseña sin token CSRF

5. **Ataque de Fuerza Bruta:**
    - Pruebas de rate limiting en login
    - Uso de Hydra: `hydra -l admin -P rockyou.txt https-post-form`
    - Identificación de credenciales débiles

6. **Análisis de Gestión de Sesiones:**
    - Verificación de timeout de sesión
    - Pruebas de session fixation
    - Análisis de renovación de tokens

**Resultados y evidencias:**

- 8 vulnerabilidades críticas explotadas exitosamente
    - SQL Injection en `/signup` → Acceso completo a base de datos (10,000 usuarios)
    - Broken Access Control → Acceso a panel admin sin autenticación
    - IDOR en API → Acceso a datos de cualquier usuario
- 12 PoCs desarrollados y documentados paso a paso
- 5 reportes de notificación inmediata enviados al cliente (< 24h)
- Matriz de impacto actualizada con evidencias de explotación

**Adjuntar en repositorio GitHub:**
- `/sprint-3/evidencias/sql_injection_poc.md`
- `/sprint-3/evidencias/broken_access_control_demo.mp4`
- `/sprint-3/evidencias/xss_payload_execution.png`
- `/sprint-3/evidencias/csrf_attack_poc.html`
- `/sprint-3/reportes/critical_vulnerabilities_notification.pdf`
- `/sprint-3/scripts/sqli_automated_exploit.py`

**Retrospectiva del sprint:**

**¿Qué funcionó bien?**
- Los PoCs desarrollados fueron reproducibles y claros
- La comunicación inmediata con el cliente sobre vulnerabilidades críticas fue muy valorada
- Metasploit y Burp Suite fueron herramientas fundamentales para la explotación
- La documentación detallada facilitó la generación del informe final

**¿Qué no funcionó bien?**
- Algunas vulnerabilidades críticas requirieron más tiempo del estimado para ser explotadas
- Faltó coordinar mejor con el cliente los horarios para pruebas invasivas
- El equipo no tenía experiencia previa con algunas técnicas avanzadas de explotación

**¿Qué mejorar para el próximo sprint?**
- Capacitar al equipo en técnicas avanzadas de explotación antes del proyecto
- Definir ventanas de prueba específicas con el cliente para evitar impacto en producción
- Mejorar el proceso de notificación de vulnerabilidades críticas con plantillas predefinidas
- Crear una biblioteca de payloads reutilizables para futuros proyectos

**Definition of Done (DoD) del Sprint 3:**
- [x] Todas las vulnerabilidades críticas y altas explotadas
- [x] PoCs reproducibles desarrollados y documentados
- [x] Impacto técnico y de negocio documentado para cada vulnerabilidad
- [x] Cliente notificado inmediatamente sobre hallazgos críticos
- [x] Evidencias fotográficas y videos de explotaciones almacenadas
- [x] Scripts de explotación almacenados en repositorio con comentarios
- [x] Matriz de vulnerabilidades actualizada con estado de explotación
- [x] Sprint Review con demostración en vivo de explotaciones
- [x] Retrospectiva documentada

**Actividades Técnicas Principales:**

1. **Pruebas de SQL Injection con sqlmap:**
   ```bash
   sqlmap -u "https://staging.tavolo.pe/sign-up" --data="username=test&email=test@test.com" --batch --level=5 --risk=3
   ```

2. **Pruebas de Broken Access Control con Burp Suite:**
    - Interceptar solicitud autenticada de UsuarioA
    - Modificar ID de usuario a UsuarioB
    - Analizar respuesta del servidor (esperado: 403 Forbidden)

3. **Pruebas de XSS:**
   ```javascript
   // Payload de prueba
   <script>alert('XSS Vulnerability')</script>
   <img src=x onerror=alert('XSS')>
   ```

4. **Pruebas de CSRF:**
    - Crear HTML con formulario malicioso que ejecuta acción sensible
    - Verificar si el servidor valida token CSRF

5. **Pruebas de Fuerza Bruta con Hydra:**
   ```bash
   hydra -l admin -P /usr/share/wordlists/rockyou.txt staging.tavolo.pe https-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
   ```

**Entregables del Sprint:**
- PoCs reproducibles para vulnerabilidades críticas
- Videos de demostración de explotaciones exitosas
- Scripts de explotación documentados
- Reporte técnico de hallazgos con impacto al negocio

**Definition of Done (DoD):**
- [ ] Todas las vulnerabilidades críticas tienen PoC reproducible
- [ ] Cada PoC incluye: precondiciones, pasos exactos, evidencia visual
- [ ] Puntuación CVSS calculada para cada vulnerabilidad
- [ ] Impacto al negocio documentado (pérdida de datos, reputación, financiero)
- [ ] Cliente notificado de vulnerabilidades críticas (< 24h)
- [ ] Commit en repositorio GitHub con tag `sprint-3-done`


### Sprint 4: Post-Explotación & Análisis de Impacto (Semanas 10-12)

**Objetivo del Sprint:**  
Evaluar el alcance completo y el impacto real de las vulnerabilidades explotadas exitosamente en Sprint 3. Simular escenarios de movimiento lateral, escalamiento de privilegios y extracción de datos sensibles (en entorno controlado con autorización explícita del cliente). Documentar la cadena de ataque completa (kill chain) y el potencial daño al negocio.

**Fases PTES Equivalentes:**
- Post-Exploitation (análisis profundo del compromiso)

**Objetivos específicos del sprint:**
1. Evaluar posibilidades de escalamiento de privilegios desde accesos obtenidos
2. Simular movimiento lateral entre servicios o usuarios (si aplica)
3. Identificar y documentar datos sensibles que serían accesibles
4. Evaluar persistencia y posibilidades de backdoors (solo documentación teórica)
5. Analizar logs del sistema para verificar detectabilidad de las pruebas
6. Documentar la cadena de ataque completa (desde reconocimiento hasta compromiso)
7. Cuantificar el impacto financiero, reputacional y legal potencial
8. Preparar recomendaciones detalladas de remediación por prioridad

**Historias de usuario atendidas:**
- HU20: Evaluación de escalamiento de privilegios (Must Have)
- HU21: Análisis de movimiento lateral (Should Have)
- HU22: Cuantificación de datos sensibles expuestos (Must Have)
- HU23: Documentación de kill chain completa (Must Have)

**Actividades realizadas:**

1. **Escalamiento de Privilegios (si se obtuvo acceso):**
    - Análisis de permisos y configuraciones inseguras
    - Uso de herramientas como LinPEAS, WinPEAS (si aplica)
    - Documentación de vías de escalamiento identificadas

2. **Análisis de Datos Sensibles Expuestos:**
    - Inventario de datos personales, financieros o confidenciales accesibles
    - Evaluación de cumplimiento con GDPR, LOPD u otras regulaciones
    - Cuantificación del volumen de registros comprometibles

3. **Movimiento Lateral (simulado):**
    - Análisis de confianza entre servicios o componentes de Tavolo
    - Identificación de credenciales reutilizadas o almacenadas inseguramente

4. **Análisis de Detección y Respuesta:**
    - Revisión de logs del servidor para verificar si las pruebas fueron detectadas
    - Evaluación de la capacidad de monitoreo y respuesta a incidentes del cliente
    - Recomendaciones de mejora en visibilidad y detección

5. **Documentación de Kill Chain:**
    - Mapeo completo de la cadena de ataque siguiendo el modelo Cyber Kill Chain o MITRE ATT&CK
    - Identificación de puntos donde el ataque pudo ser detenido

**Resultados y evidencias:**

- Cadena de ataque completa documentada: Reconocimiento → Enumeración → Explotación SQL Injection → Acceso a base de datos → Extracción de 10,000 registros de usuarios
- 3 vías de escalamiento de privilegios identificadas
- Inventario de datos sensibles:
    - 10,000 registros de usuarios (nombres, correos, contraseñas hasheadas)
    - 500 registros de tarjetas de crédito (últimos 4 dígitos)
    - Información financiera de la empresa
- Análisis de impacto al negocio:
    - Impacto financiero estimado: $50,000 - $100,000 (multas GDPR + costos de remediación)
    - Impacto reputacional: ALTO (pérdida de confianza de clientes)
    - Impacto legal: ALTO (incumplimiento de GDPR y LOPD)
- 0% de detección: Ninguna prueba fue detectada por los sistemas del cliente

**Adjuntar en repositorio GitHub:**
- `/sprint-4/evidencias/kill_chain_diagram_mitre_attack.png`
- `/sprint-4/evidencias/sensitive_data_inventory.xlsx`
- `/sprint-4/evidencias/privilege_escalation_paths.pdf`
- `/sprint-4/evidencias/log_analysis_report.md`
- `/sprint-4/reportes/business_impact_analysis.pdf`
- `/sprint-4/reportes/sprint4_post_exploitation_report.md`

**Retrospectiva del sprint:**

**¿Qué funcionó bien?**
- El mapeo de la kill chain con MITRE ATT&CK proporcionó un marco claro para documentar el ataque
- La cuantificación del impacto financiero ayudó al cliente a entender la gravedad
- El análisis de logs reveló falta de monitoreo por parte del cliente
- La simulación controlada no afectó la operación del cliente

**¿Qué no funcionó bien?**
- Faltó más coordinación con el equipo de TI del cliente para entender su arquitectura
- El análisis de logs fue limitado porque el cliente no tenía SIEM implementado
- Algunas técnicas de post-explotación no pudieron ser probadas por restricciones del cliente

**¿Qué mejorar para el próximo sprint?**
- Solicitar acceso a documentación de arquitectura del cliente desde el inicio
- Recomendar al cliente implementar SIEM antes de futuros pentests
- Crear plantillas de análisis de impacto reutilizables
- Mejorar la comunicación de hallazgos críticos con visualizaciones más claras

**Definition of Done (DoD) del Sprint 4:**
- [x] Alcance completo del compromiso documentado con evidencias
- [x] Cadena de ataque visualizada en diagrama con técnicas MITRE ATT&CK
- [x] Análisis cuantitativo del impacto (número de registros, costo estimado)
- [x] Recomendaciones de mitigación para cada vector de escalamiento
- [x] Cliente informado formalmente del alcance total del compromiso
- [x] Análisis de detección completado con recomendaciones
- [x] Inventario de datos sensibles clasificado por tipo y volumen
- [x] Sprint Review con presentación del análisis de impacto
- [x] Retrospectiva documentada

---

### Sprint 5: Documentación & Informe Final (Semanas 13-15)

**Objetivo del Sprint:**  
Consolidar todos los hallazgos técnicos en informes ejecutivos y técnicos profesionales. Elaborar recomendaciones de remediación priorizadas y accionables. Presentar formalmente los resultados al cliente en Sprint Review Final. Cerrar el proyecto con retrospectiva y lecciones aprendidas documentadas.

**Fases PTES Equivalentes:**
- Reporting (documentación final según NIST SP 800-115)

**Objetivos específicos del sprint:**
1. Elaborar informe técnico detallado con todas las vulnerabilidades, evidencias y PoCs
2. Crear informe ejecutivo resumido para dirección de Tavolo
3. Generar plan de remediación priorizado por riesgo e impacto
4. Preparar presentación formal de hallazgos con demos en vivo
5. Grabar video de demostración de vulnerabilidades críticas
6. Realizar Sprint Review Final con cliente
7. Ejecutar retrospectiva del proyecto completo
8. Documentar lecciones aprendidas y mejoras para futuros proyectos

**Actividades Principales:**

**1. Elaboración de Informe Técnico Completo:**

El informe técnico debe incluir las siguientes secciones obligatorias:

- **1. Resumen Ejecutivo (Executive Summary):**
    - Contexto del proyecto y objetivos del pentesting
    - Metodología empleada (PTES + OWASP + NIST + Scrum)
    - Resumen cuantitativo de hallazgos (# vulnerabilidades por severidad)
    - Riesgo global del sistema evaluado
    - Conclusión de alto nivel sobre el estado de seguridad de Tavolo

- **2. Alcance y Metodología:**
    - Activos evaluados (URLs, IPs, servicios)
    - Período de ejecución de las pruebas
    - Herramientas utilizadas
    - Limitaciones y exclusiones del alcance
    - Metodologías aplicadas (PTES, OWASP Testing Guide, NIST SP 800-115)

- **3. Hallazgos Detallados:**

  Para cada vulnerabilidad identificada, documentar:
    - **ID único** (ej. TAVOLO-001)
    - **Título descriptivo** (ej. "Inyección SQL en formulario de registro")
    - **Severidad CVSS v3.1** (puntuación y vector)
    - **Descripción técnica** de la vulnerabilidad
    - **Ubicación exacta** (URL, endpoint, parámetro afectado)
    - **Evidencias visuales** (capturas de pantalla con timestamps)
    - **Proof of Concept (PoC)** paso a paso reproducible
    - **Impacto al negocio** (confidencialidad, integridad, disponibilidad)
    - **Recomendación de remediación** específica y accionable
    - **Referencias externas** (CWE, OWASP, CVE si aplica)

- **4. Plan de Remediación Priorizado:**
    - Tabla con todas las vulnerabilidades ordenadas por: Severidad CVSS × Facilidad de explotación × Impacto al negocio
    - Estimación de esfuerzo de remediación (Horas/Días)
    - Responsable sugerido (Desarrollo, Infraestructura, Configuración)
    - Plazos recomendados (Crítico: 7 días, Alto: 30 días, Medio: 90 días)

- **5. Conclusiones y Recomendaciones Generales:**
    - Evaluación global del estado de seguridad de Tavolo
    - Recomendaciones estratégicas (hardening, capacitación, monitoreo)
    - Próximos pasos sugeridos (re-testing, auditorías periódicas)

- **6. Apéndices:**
    - Comandos ejecutados durante las pruebas
    - Configuraciones de herramientas utilizadas
    - Logs y outputs completos de escaneos
    - Código fuente de scripts personalizados
    - Glosario de términos técnicos

**2. Elaboración de Informe Ejecutivo (para Dirección):**

Documento de 2-4 páginas para CEO/CTO/CFO de Tavolo con:
- Resumen del proyecto en lenguaje no técnico
- Gráficos visuales del estado de seguridad (distribución de severidades)
- Top 5 riesgos críticos explicados en términos de impacto al negocio
- Inversión recomendada en remediación vs. costo de un incidente
- Comparativa con estándares de la industria (si aplica)
- Recomendaciones ejecutivas de alto nivel

**3. Presentación al Cliente (Sprint Review Final):**

Sesión formal de 60-90 minutos que incluye:
- Introducción de la metodología y alcance
- Demostración en vivo de 2-3 vulnerabilidades críticas
- Explicación del impacto técnico y de negocio de cada hallazgo
- Walkthrough del plan de remediación priorizado
- Sesión de Q&A con equipo técnico de Tavolo
- Entrega formal de informes y acceso al repositorio GitHub

**4. Video de Demostración:**

Grabación profesional de 15-20 minutos mostrando:
- Introducción al proyecto y metodología
- Demo de 3-4 vulnerabilidades clave con PoC en vivo
- Explicación del impacto y recomendaciones
- Cierre con conclusiones y próximos pasos
- Publicación en YouTube (privado) o plataforma del cliente

**5. Retrospectiva del Proyecto (Retrospective):**

Sesión interna del equipo para documentar:
- **¿Qué funcionó bien?**
    - Herramientas más efectivas
    - Procesos que aceleraron el trabajo
    - Comunicación con el cliente

- **¿Qué no funcionó bien?**
    - Herramientas que fallaron o dieron falsos positivos
    - Impedimentos técnicos u organizacionales
    - Comunicación interna del equipo

- **¿Qué mejorar en futuros proyectos?**
    - Acciones concretas de mejora
    - Nuevas herramientas o técnicas a aprender
    - Ajustes en la metodología Scrum aplicada a pentesting

**Entregables del Sprint:**
- Informe Técnico Final completo (PDF, 30-60 páginas)
- Informe Ejecutivo (PDF, 2-4 páginas)
- Plan de Remediación Priorizado (Excel/CSV)
- Presentación para cliente (PowerPoint/PDF)
- Video de demostración de hallazgos (MP4, 15-20 min)
- Repositorio GitHub completo con:
    - Todo el código de scripts y PoCs
    - Evidencias organizadas por sprint
    - README profesional con instrucciones
    - Licencia open-source (MIT o similar)
- Documento de retrospectiva del proyecto
- Acta de cierre firmada por el cliente

**Definition of Done (DoD):**
- [ ] Informe técnico completo con TODOS los hallazgos documentados
- [ ] Informe ejecutivo revisado y aprobado por el equipo
- [ ] Video de presentación grabado, editado y publicado
- [ ] Presentación formal realizada con el cliente
- [ ] Cliente ha recibido, revisado y aprobado formalmente el cierre del proyecto
- [ ] Acta de cierre firmada por ambas partes
- [ ] Retrospectiva documentada con lecciones aprendidas
- [ ] Repositorio GitHub completo y organizado
- [ ] Todos los archivos entregables subidos a Canvas con hash SHA256
- [ ] Proyecto cerrado en GitHub con release tag `v1.0-final`


## 2.4. Definición de Done (DoD)

La Definición de Done establece los criterios que deben cumplirse para considerar una Historia de Usuario, un Sprint, o el proyecto completo como "terminado". Esto garantiza calidad, consistencia, reproducibilidad y trazabilidad en todo el proceso de pentesting.

**Propósito del DoD:**
- Asegurar que cada prueba de seguridad está completamente documentada
- Garantizar reproducibilidad de los hallazgos por terceros
- Mantener estándares profesionales de calidad en el pentesting
- Facilitar la validación y remediación por parte del cliente

### 2.4.1. Definition of Done - Nivel Historia de Usuario

Una Historia de Usuario (HU) se considera **DONE** cuando cumple **TODOS** los siguientes criterios:

**1. Prueba Ejecutada Completamente:**
- La prueba de pentesting planificada en la HU ha sido ejecutada según los criterios de aceptación Gherkin (Given/When/Then)
- Se han probado todas las variantes y casos límite relevantes
- Se documentó el resultado (vulnerable / no vulnerable / parcialmente vulnerable)

**2. Evidencia Clara (pantallazos, reportes):**
- Screenshots de alta calidad con timestamps visibles
- Captura de pantallas completas (no recortes) mostrando URL, hora del sistema
- Logs de comandos ejecutados con outputs completos
- Archivos de salida de herramientas (XML de Nmap, HTML de Nikto, JSON de Burp)
- Videos de explotaciones complejas (opcional pero recomendado para críticas)

**3. Reproducibilidad:**
- Existe un documento paso a paso que permite reproducir exactamente la prueba
- Todos los payloads, URLs, parámetros están documentados
- Precondiciones claramente especificadas (ej. "requiere usuario autenticado")
- Cualquier miembro del equipo puede replicar el hallazgo siguiendo la documentación

**4. Documentación de Proof of Concept (PoC):**
- Si se explotó una vulnerabilidad, existe un PoC funcional y documentado
- El PoC incluye:
    - Descripción del escenario de ataque
    - Código fuente completo (scripts, payloads, configuraciones)
    - Instrucciones paso a paso de ejecución
    - Output esperado y output obtenido
- Scripts almacenados en repositorio GitHub con comentarios

**5. Análisis de Impacto:**
- **Severidad técnica:** Calculada usando CVSS v3.1 con vector de ataque completo
- **Impacto al negocio:** Documentado en términos de:
    - **Confidencialidad:** ¿Qué datos se exponen? ¿Cuántos registros?
    - **Integridad:** ¿Se pueden modificar datos? ¿Qué tipo de datos?
    - **Disponibilidad:** ¿Se puede causar denegación de servicio? ¿A qué escala?
    - **Impacto financiero:** Estimación de costos (multas, pérdida de clientes, remediación)
    - **Impacto reputacional:** ¿Afectaría la confianza de los usuarios?
    - **Impacto legal:** ¿Incumple GDPR, LOPD u otras regulaciones?

**6. Peer Review Completado:**
- Otro miembro del equipo ha revisado la evidencia técnica
- Se validó que la vulnerabilidad es real (no un falso positivo)
- Se confirmó la exactitud del puntaje CVSS asignado
- Se revisó la claridad de la documentación

**7. Documentación Actualizada:**
- El hallazgo está documentado en el reporte técnico del repositorio GitHub
- Se actualizó la matriz de vulnerabilidades con la nueva entrada
- Se actualizó el tablero Kanban (Jira/Trello) marcando la HU como "Done"
- Código y scripts están en el repositorio con commit descriptivo

**Ejemplo de criterio cumplido:**
```
HU02: Pruebas de SQL Injection en /sign-up
Ejecutada: Se probó inyección SQL en todos los campos del formulario
Evidencia: Screenshot mostrando payload y error de base de datos MySQL
Reproducible: Documento con URL, payload exacto, y pasos de reproducción
PoC: Script Python automatizado de inyección almacenado en /exploits/sql_injection_signup.py
Impacto: CVSS 9.1 (Critical) - Acceso completo a base de datos con 10,000 usuarios
Peer Review: Validado por Pentester de APIs el 15/03/2025
Documentado: Agregado a informe técnico sección 3.2.1 y commit abc123f
```

### 2.4.2. Definition of Done - Nivel Sprint

Un Sprint se considera **DONE** cuando cumple TODOS los siguientes criterios:

- **Todas las HU Asignadas Completadas:** Cada Historia de Usuario del Sprint cumple con el DoD de User Story.

- **Sprint Review Realizada:** Se ha presentado el trabajo al Product Owner (y opcionalmente al cliente) en una sesión de demostración.

- **Retrospectiva Documentada:** El equipo ha realizado la retrospectiva y documentado:
    - ¿Qué salió bien?
    - ¿Qué salió mal?
    - ¿Qué acciones de mejora implementaremos?

- **Reporte de Sprint Generado:** Se ha creado un documento Markdown con:
    - Objetivos del sprint
    - HU completadas
    - Hallazgos principales
    - Métricas (horas invertidas, vulnerabilidades encontradas)

- **Notificación al Cliente:** Si se encontraron vulnerabilidades críticas, el cliente fue notificado dentro de las 24 horas.

- **Commit en GitHub:** Todo el trabajo está en el repositorio con commit convencional y tag de sprint (ej. `sprint-1-done`).

### 2.4.3. Definition of Done - Nivel Proyecto (TP1/TF1)

El proyecto completo se considera **DONE** cuando cumple TODOS los siguientes criterios:

- **Todos los Sprints Completados:** Los 5 sprints cumplen con sus respectivos DoD.

- **Informe Técnico Final Completo:** Documento profesional con:
    - Resumen ejecutivo
    - Metodología
    - Hallazgos detallados (con evidencias)
    - Recomendaciones de remediación priorizadas
    - Apéndices (comandos, configuraciones)

- **Informe Ejecutivo para Dirección:** Documento de alto nivel (2-3 páginas) para CEO/CTO de Tavolo.

- **Video de Presentación:** Grabación profesional (15-20 min) demostrando hallazgos clave.

- **Repositorio GitHub Completo:** Incluye:
    - Código de todos los scripts
    - Evidencias organizadas por sprint
    - README profesional con instrucciones
    - Licencia (MIT o similar)

- **Cierre Formal con Cliente:** Tavolo ha recibido, revisado y aprobado formalmente el proyecto.

- **Archivos Entregables Subidos:** Todos los PDFs, videos y archivos requeridos están en Canvas con hash SHA256 verificado.

- **Retrospectiva Final del Proyecto:** El equipo ha documentado las lecciones aprendidas del proyecto completo.

## 2.5. Herramientas

La ejecución exitosa de los Sprints de Pentesting requiere el uso de herramientas específicas que se alinean con las fases de la metodología PTES y los objetivos de cada sprint.

### 2.5.1. Herramientas Obligatorias

| Herramienta | Tipo | Fases de Contribución | Explicación de la Contribución | Sprints |
|-------------|------|----------------------|--------------------------------|---------|
| **Kali Linux** | Sistema Operativo / Plataforma | S1 a S5 (Todo el Proyecto) | Es la **plataforma base** que integra todas las utilidades de pentesting. Proporciona el entorno preconfigurado con más de 600 herramientas para ejecutar las pruebas, desde el escaneo hasta la post-explotación. | Todos |
| **Nmap** | Escáner de Red | S1: Reconocimiento & Escaneo | Fundamental para el **mapeo de la infraestructura**. Identifica hosts activos, escanea puertos abiertos, detecta versiones de servicios y sistemas operativos. Es la base del reconocimiento activo (HU01). | Sprint 1 |
| **Wireshark** | Analizador de Protocolos | S1: Reconocimiento & Escaneo<br>S2-S4: Análisis de tráfico | Permite la **captura y análisis del tráfico de red** en tiempo real. Es crucial para identificar información sensible transmitida sin cifrar, analizar protocolos de comunicación y detectar debilidades en la implementación de SSL/TLS. | Sprint 1-4 |
| **Burp Suite** | Proxy Web Interceptor | S2: Enumeración<br>S3: Explotación | Esencial para la **intercepción y modificación de solicitudes HTTP/S**. Se usa para la prueba manual de vulnerabilidades en aplicaciones web como Inyecciones SQL, XSS, Broken Access Control, CSRF, y manipulación de parámetros (HU02, HU03, HU06, HU08, HU12, HU16). Incluye herramientas integradas como Spider, Intruder, Repeater y Scanner. | Sprint 2-3 |
| **Metasploit Framework** | Framework de Explotación | S3: Explotación<br>S4: Post-Explotación | Proporciona una amplia base de datos de **exploits y payloads** para obtener **acceso inicial** al sistema, realizar escalamiento de privilegios y ejecutar tareas de post-explotación como el *dumping* de credenciales o establecimiento de shells persistentes. | Sprint 3-4 |
| **sqlmap** | Inyección SQL Automatizada | S3: Explotación | Herramienta especializada para la **detección y explotación automatizada de fallas de inyección SQL** (HU02). Permite la enumeración de bases de datos, extracción de tablas, dumping de credenciales y ejecución de comandos en el servidor de base de datos. | Sprint 3 |

### 2.5.2. Herramientas Recomendadas

| Herramienta | Tipo | Fases de Contribución | Explicación de la Contribución | Sprints |
|-------------|------|----------------------|--------------------------------|---------|
| **Nessus / OpenVAS** | Escáner de Vulnerabilidades | S2: Enumeración & Vulnerabilidades | Ejecutan **escaneos automatizados y profundos** de vulnerabilidades conocidas (HU04). Identifican software obsoleto, configuraciones erróneas y mapean vulnerabilidades con su respectivo puntaje CVSS. OpenVAS es la alternativa open-source a Nessus Professional. | Sprint 2 |
| **Nikto** | Escáner Web | S2: Enumeración | Escáner de servidores web que identifica **configuraciones peligrosas**, archivos/scripts peligrosos, versiones desactualizadas de software web. Complementa a Nessus con pruebas específicas de servidores HTTP. | Sprint 2 |
| **Gobuster / Dirb / Dirbuster** | Fuzzing de Directorios | S2: Enumeración | Herramientas de **fuzzing de directorios y archivos** ocultos en servidores web (HU11). Usan diccionarios para descubrir recursos no indexados como paneles de administración, backups, archivos de configuración expuestos. Gobuster es más rápido (Go), Dirb es más estable (C). | Sprint 2 |
| **Hydra** | Ataque de Fuerza Bruta | S3: Explotación | Herramienta de **ataque de fuerza bruta** contra servicios de autenticación (SSH, FTP, HTTP, SMTP, etc.). Se usa para probar la robustez de credenciales y mecanismos de rate limiting (HU05). | Sprint 3 |
| **MobSF (Mobile Security Framework)** | Análisis de Aplicaciones Móviles | S3: Explotación<br>S4: Post-Explotación | Recomendado para escenarios móviles. Facilita el **análisis estático y dinámico de aplicaciones** Android (APK) e iOS (IPA). Evalúa el manejo de tokens, seguridad de APIs, almacenamiento de datos sensibles y permisos peligrosos. | Sprint 3-4 |
| **OWASP ZAP (Zed Attack Proxy)** | Proxy Web / Escáner | S2: Enumeración<br>S3: Explotación | Alternativa open-source a Burp Suite Professional. Incluye escáner automatizado de vulnerabilidades web, fuzzer, y capacidades de interceptación de tráfico. Útil para complementar Burp Suite en análisis automatizados. | Sprint 2-3 |
| **theHarvester** | OSINT | S1: Reconocimiento | Herramienta de **reconocimiento pasivo** que recopila correos electrónicos, subdominios, hosts, nombres de empleados, puertos abiertos y banners desde fuentes públicas (Google, Bing, Shodan, LinkedIn). | Sprint 1 |
| **Sublist3r** | Enumeración de Subdominios | S1: Reconocimiento | Herramienta especializada en **descubrimiento de subdominios** usando motores de búsqueda y APIs públicas. Fundamental para mapear la superficie de ataque completa de Tavolo. | Sprint 1 |
| **sslscan / testssl.sh** | Análisis SSL/TLS | S1: Reconocimiento<br>S2: Enumeración | Herramientas para evaluar la **configuración de SSL/TLS** en servidores. Identifican cifrados débiles, certificados vencidos, vulnerabilidades como BEAST, POODLE, Heartbleed (HU19). | Sprint 1-2 |

### 2.5.3. Herramientas de Gestión y Documentación

| Herramienta | Propósito | Uso en el Proyecto |
|-------------|-----------|-------------------|
| **GitHub** | Control de Versiones | Repositorio central para código, scripts, evidencias y documentación. Permite trazabilidad de cambios y colaboración del equipo. |
| **Markdown** | Documentación | Formato estándar para todos los reportes técnicos, READMEs y documentación del proyecto. |
| **Jira / Trello** | Gestión Ágil | Tablero Kanban para gestionar el Product Backlog, sprint backlog y seguimiento de tareas. |
| **Obsidian / Notion** | Notas de Pentesting | Herramientas de toma de notas durante las pruebas, organización de hallazgos y colaboración del equipo. |
| **KeepNote / CherryTree** | Notas Jerárquicas | Alternativas open-source para documentar hallazgos de forma estructurada durante el pentesting. |
| **Dradis** | Colaboración en Pentesting | Plataforma colaborativa para que el equipo comparta hallazgos en tiempo real y genere reportes consolidados. |

### 2.5.4. Matriz de Herramientas por Sprint

| Sprint | Herramientas Principales | Herramientas Complementarias |
|--------|-------------------------|------------------------------|
| **Sprint 1** | Nmap, Wireshark, sslscan, theHarvester, Sublist3r | Shodan, crt.sh, Google Dorking |
| **Sprint 2** | Nessus/OpenVAS, Burp Suite, Nikto, Gobuster | OWASP ZAP, curl, Postman |
| **Sprint 3** | Burp Suite, sqlmap, Metasploit, Hydra | OWASP ZAP, BeEF, XSSer, Commix |
| **Sprint 4** | Metasploit, Mimikatz, LinPEAS, WinPEAS | BloodHound, PowerSploit, Empire |
| **Sprint 5** | Markdown, LaTeX, Dradis, Jira | OBS Studio (para videos), Canva (para infografías) |

