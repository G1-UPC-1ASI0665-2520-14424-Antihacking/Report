## Capítulo I: Introducción 

### 1.1. Startup Profile (Cliente) 
### 1.1.1 Descripción de la PYME - TAVOLO

**Razón Social:** TAVOLO Tech Solutions S.A.C.
<br>
**Sector:** Tecnología aplicada al sector gastronómico (FoodTech)
<br>
**Tipo de empresa:** Startup tecnológica - Pequeña empresa
<br>
**Año de fundación:** 2024
<br>
**Ubicación:** Lima, Perú
<br>
**Número de empleados:** 8-12 colaboradores (equipo técnico y comercial)
<br><br>
**Descripción del Negocio**
<br>
TAVOLO es una startup peruana que desarrolla soluciones tecnológicas basadas en Internet of Things (IoT) para la transformación digital del sector gastronómico. Su producto principal consiste en un sistema integral que combina hardware (sensores de peso embebidos en mesas) con software (aplicaciones web y móviles) para la gestión inteligente del aforo en cafeterías.<br>
La empresa nació como respuesta a una problemática identificada durante la pandemia de COVID-19, cuando el control de aforo se volvió crítico, y ha evolucionado hacia una solución que mejora la experiencia del cliente y optimiza la operación de los establecimientos gastronómicos.
<br><br>
**Modelo de Negocio**
<br>
TAVOLO opera bajo un modelo B2B2C (Business-to-Business-to-Consumer):<br>

**B2B (Clientes directos):** <br> 
- Cafeterías independientes en zonas urbanas de alta demanda
- Cadenas de cafeterías con múltiples sedes
- Espacios de coworking con áreas de cafetería
- Restaurantes de tamaño mediano
<br>

**B2C (Usuarios finales):** <br> 
- Comensales que utilizan la aplicación móvil para consultar disponibilidad y realizar reservas
<br>

**Modelo de ingresos:** <br> 
- Venta inicial del hardware (sensores IoT + instalación)
- Licenciamiento mensual del software (SaaS por sede)
- Soporte técnico y mantenimiento
- Planes premium con analytics avanzados
<br>

### 1.1.2 Expectativas del Cliente
Entregables esperados:
- **Informe Técnico Detallado:**
  - Vulnerabilidades identificadas con severidad CVSS
  - Proof of Concepts reproducibles
  - Pasos exactos de explotación
  - Recomendaciones técnicas específicas con ejemplos de código
- **Informe Ejecutivo:**
  - Resumen para presentar a inversionistas
  - Impacto en negocio traducido a términos comerciales
  - Roadmap de seguridad priorizado
  - Métricas de mejora esperada
- **Plan de Remediación Ejecutable:**
  - Priorización clara
  - Esfuerzo estimado por correción
  - Guías de implementación para el equipo de desarrollo
  - Quick wins vs. proyectos a largo plazo
- **Sesión de Transferencia de Conocimiento:**
  - Presentación al equipo técnico de TAVOLO
  - Demo en vivo de explotaciones críticas
  - QA técnico
  - Recomendaciones de herramientas


### 1.2. Consultora de Ciberseguridad (Equipo)
### 1.2.1 Descripción de la Consultora

**Razón Social:** PentGuin Cybersecurity Consulting
<br>
**Tipo de empresa:** Consultora de seguridad ofensiva (Ethical Hacking & Penetration Testing)
<br>
**Especialización:** Pentesting de aplicaciones web, APIs y aplicaciones móviles
<br>
**Ubicación:** Lima, Perú
<br>
**Formación:** Estudiantes de Ingeniería de Software de la Universidad Peruana de Ciencias Aplicadas
<br><br>
**Misión de la Consultora**
<br>
Proporcionar servicios especializados de Ethical Hacking y Penetration Testing con un enfoque académico-profesional, aplicando metodologías reconocidas internacionalmente (PTES, OWASP) y herramientas de código abierto, para identificar vulnerabilidades en sistemas informáticos y ofrecer soluciones de remediación efectivas que protejan los activos digitales de nuestros clientes, con especial énfasis en startups tecnológicas y empresas en proceso de transformación digital.
<br><br>

**Misión de la Consultora**
¿Por qué contratar a neustra consultora?

1. **Perspectiva Fresca:** Como equipo en formación, aportamos conocimientos actualizados en las últimas tendencias de ciberseguridad, frameworks modernos y vectores de ataque emergentes.
2. **Enfoque Metodológico Riguroso:** Aplicamos metodologías ágiles (Scrum) combinadas con estándares de pentesting (PTES, OWASP), garantizando un proceso estructurado, documentado y reproducible.
3. **Especialización en Tecnologías Emergentes:** Experiencia práctica en testing de soluciones IoT, aplicaciones móviles nativas, arquitecturas cloud y APIs RESTful modernas.
4. **Documentación Exhaustiva:** Entregables con estándares académico-profesionales, incluyendo evidencias visuales, PoCs funcionales, código comentado y recomendaciones accionables.
5. **Relación Costo-Beneficio:** Servicios de calidad profesional adaptados a presupuestos de startups y PyMEs, sin comprometer la profundidad del análisis.
6. **Ética y Confidencialidad Absoluta:** Compromiso total con el código de ética de ACM/IEEE/CIP, respeto estricto de Rules of Engagement y confidencialidad de información sensible.

**Servicios Ofrecidos en este Proyecto:**

| Componente             | Tipo de Prueba                 | Herramientas Principales         |
| ---------------------- | ------------------------------ | -------------------------------- |
| Aplicaciones Web       | Web Application Pentesting     | Burp Suite Pro, OWASP ZAP, Nikto |
| APIs REST              | API Security Testing           | Postman, Burp Suite, Arjun, ffuf |
| Aplicación Móvil       | Mobile App Security Assessment | MobSF, Frida, APKTool, Jadx      |
| Infraestructura de Red | Network Pentesting             | Nmap, Masscan, Metasploit        |
| Social Engineering     | Phishing SImulation            | GoPhish, SET                     |


### 1.2.2 Perfiles de los integrantes y roles Scrum

### 1.3. Solution Profile
### 1.3.1 1.3.1 Antecedentes y Problemática desde la Perspectiva de Seguridad
**Estructura usando 5 'W's y 2 'H's:**

- **What (¿Qué necesita ser evaluado?)**

| Activo | Descripción | Datos Sensibles | Impacto si Comprometido |
|--------|-------------|-----------------|-------------------------|
| **API REST** | Backend que procesa solicitudes de apps y sensores | Tokens de autenticación, datos de usuarios, info de reservas | CRÍTICO - Acceso total a la plataforma |
| **App Móvil Android** | Aplicación del comensal | Credenciales, datos personales, tokens JWT | ALTO - Robo de identidad, acceso no autorizado |
| **Portal Web Administrativo** | Panel de gestión de sedes | Credenciales admin, métricas de negocio, configuración de mesas | CRÍTICO - Control total de operación |
| **Landing Page** | Sitio informativo público | Formularios de contacto, información corporativa | MEDIO - Phishing, defacement |
| **Infraestructura IoT** | Sensores y gateway | Datos de ocupación en tiempo real, configuración de red | ALTO - Manipulación de disponibilidad, DDoS |
| **Base de Datos** | PostgreSQL/MongoDB | Todos los datos de usuarios, reservas, sedes | CRÍTICO - Pérdida total de información |
| **Sistema de Autenticación** | JWT/OAuth | Tokens de sesión, hashes de contraseñas | CRÍTICO - Acceso masivo no autorizado |

**Vectores de Ataque Potenciales:**

1. **OWASP Top 10 Web Applications:**
   - A01:2021 - Broken Access Control (IDOR en APIs)
   - A02:2021 - Cryptographic Failures (Datos en tránsito sin encriptar)
   - A03:2021 - Injection (SQLi, NoSQL Injection, Command Injection)
   - A04:2021 - Insecure Design (Lógica de negocio vulnerable)
   - A05:2021 - Security Misconfiguration (Configuraciones por defecto, CORS abierto)
   - A07:2021 - XSS (Cross-Site Scripting en dashboards)
   - A08:2021 - Software and Data Integrity Failures (Falta de validación de firmware)
   - A10:2021 - SSRF (Server-Side Request Forgery en integraciones)

2. **OWASP API Security Top 10:**
   - API1:2023 - Broken Object Level Authorization
   - API2:2023 - Broken Authentication
   - API3:2023 - Broken Object Property Level Authorization
   - API5:2023 - Broken Function Level Authorization
   - API6:2023 - Unrestricted Access to Sensitive Business Flows
   - API7:2023 - Server Side Request Forgery
   - API8:2023 - Security Misconfiguration
   - API9:2023 - Improper Inventory Management

3. **OWASP IoT Top 10:**
   - Weak passwords en dispositivos
   - Insecure network services (MQTT sin TLS)
   - Insecure data transfer and storage
   - Lack of secure update mechanism (firmware)
   - Use of insecure or outdated components
   - Insufficient privacy protection

4. **OWASP Mobile Top 10:**
   - M1: Improper Platform Usage
   - M2: Insecure Data Storage (credenciales en SharedPreferences)
   - M3: Insecure Communication (HTTP en lugar de HTTPS)
   - M4: Insecure Authentication
   - M5: Insufficient Cryptography
   - M6: Insecure Authorization
   - M8: Code Tampering (APK sin ofuscación)
   - M9: Reverse Engineering

- **Why (¿Por qué es crítico realizar este pentesting AHORA?)**<br>
**Razones de Urgencia:**

1. **Fase de Expansión Comercial:**
   - TAVOLO está en conversaciones con cadenas de cafeterías que exigen auditorías de seguridad
   - Potenciales clientes corporativos solicitan certificaciones ISO 27001
   - Próxima ronda de inversión requiere due diligence de seguridad

2. **Superficie de Ataque en Crecimiento:**
   - Cada nueva sede instalada incrementa el número de dispositivos IoT expuestos
   - Mayor base de usuarios = mayor atractivo para atacantes
   - Datos acumulados incrementan el valor del objetivo

3. **Riesgos Regulatorios:**
   - Ley de Protección de Datos Personales (Ley N° 29733) - Multas de hasta 100 UIT
   - Obligación de notificar brechas de seguridad en 72 horas
   - Directiva de Seguridad de la Información en la Administración Pública (si venden a entidades públicas)

4. **Precedentes en el Sector IoT:**
   - Mirai Botnet (2016): 600,000 dispositivos IoT comprometidos
   - Ring Security Cameras (2019): Cámaras hackeadas por credenciales débiles
   - Tesla Hack (2020): Vulnerabilidades en API permitieron desbloqueo remoto
   - **Lección:** Los dispositivos IoT son objetivos frecuentes y la reputación se pierde rápidamente

5. **Window of Opportunity:**
   - Es más económico encontrar y corregir vulnerabilidades AHORA (fase temprana)
   - Costo de breach post-producción: 10-100x más caro que prevención
   - Reputación de startup se construye desde el inicio

**Impactos Potenciales de No Actuar:**

| Amenaza | Probabilidad | Impacto | Consecuencias Estimadas |
|---------|--------------|---------|-------------------------|
| **Data Breach (robo de datos de usuarios)** | Alta | Crítico | - Multa ARPDP: S/ 500,000<br>- Pérdida de confianza<br>- Cancelación de contratos B2B |
| **Manipulación de sensores IoT** | Media | Alto | - Mesas reportadas como disponibles cuando están ocupadas<br>- Pérdida de credibilidad del servicio<br>- Churn de usuarios |
| **Ransomware en infraestructura** | Media | Crítico | - Indisponibilidad del servicio 48-72h<br>- Pago de rescate: $20,000-$50,000<br>- Pérdida de ingresos mensuales |
| **Account Takeover (secuestro de cuentas admin)** | Alta | Crítico | - Control total de operación<br>- Eliminación maliciosa de datos<br>- Extorsión a la empresa |
| **API Abuse (scraping masivo de datos)** | Alta | Medio | - Competidores obtienen datos de demanda<br>- Sobrecarga de infraestructura<br>- Costos adicionales de cloud |
| **Robo de propiedad intelectual** | Media | Alto | - Algoritmos de optimización expuestos<br>- Clonación del producto<br>- Ventaja competitiva perdida |


- **Who (¿Quién está involucrado?)** <br>
**Equipo de la Consultora:**
  - [Listado de roles Scrum según sección 1.2]
  - 

**Contactos del Cliente (TAVOLO):**

| Rol | Nombre | Email | Teléfono | Responsabilidad |
|-----|--------|-------|----------|-----------------|
| **CEO/CTO** | [Nombre] | cto@tavolo.pe | +51 XXX XXX XXX | Autorización final, decisiones estratégicas |
| **Tech Lead** | [Nombre] | tech@tavolo.pe | +51 XXX XXX XXX | Contacto técnico principal, acceso a infraestructura |
| **DevOps Engineer** | [Nombre] | devops@tavolo.pe | +51 XXX XXX XXX | Provisión de accesos, logs, respaldo técnico |
| **Product Manager** | [Nombre] | product@tavolo.pe | +51 XXX XXX XXX | Coordinación de alcance, prioridades de negocio |

**Escalation Path:**
1. **Vulnerabilidad Baja/Media:** Reporte en Sprint Review
2. **Vulnerabilidad Alta:** Email + Slack en < 24h
3. **Vulnerabilidad Crítica (Explotación exitosa):** Llamada inmediata + Email + Freeze del ambiente

**Stakeholders Indirectos:**
- Cafeterías clientes de TAVOLO (notificación si sus datos son afectados)
- Usuarios comensales (notificación de breach si aplica Ley 29733)
- Inversionistas de TAVOLO (presentación de resultados si se requiere)

- **Where (¿Dónde están las vulnerabilidades esperadas?)**
<br>
  - Périmtetro externo:
    - Landing Page (www.tavolo.pe)
    -    App Web del Comensal (app.tavolo.pe)
    - API Gateway (api.tavolo.pe)
    - Endpoints de descarga de APK  
  - Zona DMZ (Cloud)
    - API REST Backend
    - WebSockets Server
    - Message Broker
  - Zona interna (Backend)
    - Servidores de Aplicación
    - Base de Datos
    - File Storage
    - Admin Panel Backend
  - Aplicación móvil
    - APK Android
    - Comunicación con API
    - Tokens almacenados
<br>

- **When (Cuándo):** Contextualiza temporalemente

**Timeline del Proyecto:**
| Fase | Semanas | Fechas Tentativas | Hitos |
|------|---------|-------------------|-------|
| **Pre-engagement** | S1 | [Fecha inicio] | Firma de RoE, NDA, configuración de entorno |
| **Sprint 1: Reconocimiento** | S2-S3 | [Fechas] | Mapeo de superficie de ataque, OSINT |
| **Sprint 2: Análisis de Vulnerabilidades** | S4-S6 | [Fechas] | Escaneo automatizado, enumeración |
| **Sprint 3: Explotación** | S7-S9 | [Fechas] | PoCs de vulnerabilidades críticas, **TP1** |
| **Sprint 4: Post-explotación** | S10-S12 | [Fechas] | Escalamiento, movimiento lateral |
| **Sprint 5: Informe y Remediación** | S13-S15 | [Fechas] | Consolidación, **TF1**, presentación final |


- **How (¿Cómo se ejecutará el pentesting?)** 
**Metodología Integrada:**

PTES (Penetration Testing Execution Standard) + OWASP + Scrum

- **Phase 1: Pre-engagement Interactions**
  - Rules of Engagement (RoE) firmadas
  - Non-Disclosure Agreement (NDA)
  - Alcance definido (in-scope / out-of-scope)
  - Emergency contacts
  - Backout procedures

- **Phase 2: Intelligence Gathering (Sprint 1)**
  - Passive Reconnaissance
    - OSINT: Google Dorking, Shodan, LinkedIn
    - DNS enumeration (subfinder, amass)
    - GitHub/GitLab leaks
    - Public exploit databases
  - Active Reconnaissance
    - Nmap full TCP/UDP scan
    - Service fingerprinting
    - Technology stack identification (Wappalyzer, WhatWeb)
    - SSL/TLS analysis
  - Deliverable: Mapa de superficie de ataque

- **Phase 3: Threat Modeling (Sprint 2)**
  - Identificación de activos críticos
  - Análisis de confianza entre componentes
  - Construcción de árboles de ataque
  - Priorización de objetivos
  - Deliverable: Matriz de amenazas

- **Phase 4: Vulnerability Analysis (Sprint 2)**
  - Automated Scanning
    - Web: Nikto, OWASP ZAP
    - Network: Nessus/OpenVAS
    - Mobile: MobSF static analysis
    - API: Fuzzing con ffuf, Arjun
  - Manual Testing
    - Authentication bypass attempts
    - Authorization flaws (IDOR, privilege escalation)
    - Business logic flaws
    - Input validation (SQLi, XSS, Command Injection)
    - Session management
  - Deliverable: Matriz preliminar de vulnerabilidades

- **Phase 5: Exploitation (Sprint 3)**
  - Proof of Concept Development
    - SQLi → Database extraction
    - XSS → Session hijacking
    - IDOR → Acceso a datos de otros usuarios
    - JWT manipulation → Privilege escalation
    - API rate limiting bypass
  - Safe Exploitation (NO destructivo)
    - Dump de 10 registros (no toda la DB)
    - Create dummy user (no borrar usuarios)
    - Read files (no modificar)
    - PoC screenshots + videos
  - Deliverable: PoCs documentados + TP1

- **Phase 6: Post-Exploitation (Sprint 4)**
  - Privilege Escalation
    - Horizontal (user → user)
    - Vertical (user → admin)
  - Persistence Simulation (sin implementar realmente)
  - Pivoting & Lateral Movement
    - Desde web app → backend → DB
  - Data Exfiltration (simulado)
  - Deliverable: Cadenas de ataque completas

- **Phase 7: Reporting (Sprint 5)**
  - Technical Report
  - Executive Summary
  - Remediation Roadmap
  - Presentation + TF1

- **How much (¿Cuánto impacto/esfuerzo?)**
<br>
  Esfuerzo Estimado del Proyecto:
<br>

| Fase                             | Horas por Integrante | Total Equipo (5 personas) | Semanas |
| -------------------------------- | -------------------- | ------------------------- | ------- |
| Pre-engagement                   | 5h                   | 30h                       | 0.5     |
| Sprint 1: Reconnaissance         | 20h                  | 120h                      | 2       |
| Sprint 2: Vulnerability Analysis | 25h                  | 150h                      | 2-3     |
| Sprint 3: Exploitation           | 30h                  | 180h                      | 3       |
| Sprint 4: Post-exploitation      | 25h                  | 150h                      | 3       |
| Sprint 5: Reporting              | 20h                  | 120h                      | 2-3     |
| **TOTAL**                        | **125h**             | **750h**                  | **15**  |

<br>
  Inversión del Cliente (TAVOLO):
<br>

| Concepto                          | Estimado                                    |
| --------------------------------- | ------------------------------------------- |
| **Servicio de Pentesting**        | S/ 15,000 - S/ 25,000 (académico-comercial) |
| **Horas de coordinación interna** | 40-60 horas (Tech Lead + DevOps)            |
| **Recursos de infraestructura**   | S/ 500 (ambientes de prueba adicionales)    |
| **Remediación post-pentesting**   | S/ 10,000 - S/ 50,000 (según hallazgos)     |
| **TOTAL INVERSIÓN**               | S/ 25,500 - S/ 75,500                       |

<br>
  Retorno de Inversión (ROI):
<br>

| Beneficio                              | Ahorro Estimado                                   |
| -------------------------------------- | ------------------------------------------------- |
| **Evitar data breach**                 | S/ 500,000 - S/ 2,000,000 (multas + reputación)   |
| **Certificación ISO 27001 futura**     | S/ 30,000 (costos reducidos con evidencia previa) |
| **Cierre de contratos B2B**            | S/ 100,000+ (confianza de clientes corporativos)  |
| **Reducción de riesgos operacionales** | S/ 50,000 (downtime evitado)                      |
| **ROI Estimado**                       | **800% - 2,600%**                                 |

<br>
  Métricas de Éxito del Pentesting:
<br>

| Métrica                               | Objetivo                       |
| ------------------------------------- | ------------------------------ |
| **Cobertura de superficie de ataque** | ≥ 95%                          |
| **Vulnerabilidades identificadas**    | ≥ 30 (expectativa)             |
| **Vulnerabilidades críticas**         | Identificar todas las posibles |
| **False positives**                   | < 10%                          |
| **Reproducibilidad de PoCs**          | 100%                           |
| **Satisfacción del cliente**          | ≥ 4.5/5                        |
| **Tiempo de respuesta a críticas**    | < 4 horas                      |

### 1.4. Aceptación del Servicio de Pentesting (Rules of Engagement)
Las Reglas de Compromiso (Rules of Engagement - RoE) constituyen el marco legal y técnico que autoriza formalmente la ejecución de pruebas de penetración ética sobre la infraestructura de TAVOLO. Este acuerdo establece los límites, responsabilidades y procedimientos que regirán todas las actividades del pentesting, garantizando que las pruebas se realicen de manera controlada, ética y profesional.

### 1.4.1 Partes Involucradas

### **Cliente (Empresa Objetivo)**
**TAVOLO TECH SOLUTIONS S.A.C.** es una startup peruana especializada en soluciones IoT para el sector gastronómico. La empresa desarrolla y comercializa un sistema integral de gestión de aforo en cafeterías basado en sensores inteligentes, aplicaciones web y móviles.

### **Consultora (Proveedor del Servicio)**
**PentGuin Cybersecurity Consulting** es un equipo de estudiantes de Ingeniería de Software de la Universidad Peruana de Ciencias Aplicadas, especializado en Ethical Hacking y Penetration Testing, formado en el curso 1ASI0665 - Anti-Hacking y Nuevas Tendencias de Seguridad.

### 1.4.2 Objetivo del Servicio
El servicio de Ethical Hacking y Penetration Testing tiene como propósito fundamental evaluar la postura de seguridad de la plataforma TAVOLO mediante la identificación sistemática de vulnerabilidades en su infraestructura tecnológica, siguiendo metodologías reconocidas internacionalmente.

### **Objetivos Específicos:**
**1. Evaluación Integral de Seguridad:** Realizar un análisis exhaustivo de todos los componentes tecnológicos de TAVOLO (aplicaciones web, APIs, aplicación móvil, dispositivos IoT e infraestructura de red) para identificar debilidades que puedan ser explotadas por actores maliciosos.

**2. Validación mediante Proof of Concepts:** Desarrollar y ejecutar pruebas de concepto (PoCs) controladas que demuestren el impacto real de las vulnerabilidades críticas identificadas, sin causar daños permanentes a los sistemas ni comprometer datos de usuarios reales.

**3. Clasificación y Priorización de Riesgos:** Evaluar cada vulnerabilidad identificada utilizando el sistema Common Vulnerability Scoring System (CVSS) v3.1, considerando tanto el impacto técnico como el impacto en el negocio de TAVOLO.

**4. Plan de Remediación Accionable:** Proporcionar recomendaciones técnicas específicas y priorizadas para la corrección de cada vulnerabilidad, incluyendo ejemplos de código seguro, configuraciones recomendadas y referencias a mejores prácticas de la industria (OWASP, CIS Benchmarks, etc.).

**5. Transferencia de Conocimiento:** Capacitar al equipo técnico de TAVOLO en seguridad ofensiva y defensiva mediante la presentación de hallazgos, demostración de técnicas de explotación y recomendaciones de secure coding.

**6. Evaluación de Cumplimiento:** Verificar el cumplimiento con estándares de seguridad relevantes para el sector, incluyendo OWASP Top 10 (Web, API, Mobile, IoT), normativas de protección de datos personales (Ley N° 29733) y mejores prácticas de seguridad en la nube.

### **Alcance de la Evaluación:**

El pentesting seguirá las fases del **Penetration Testing Execution Standard (PTES)** adaptadas a una metodología ágil:

1. **Pre-engagement:** Definición de alcance, firma de acuerdos, configuración de entornos
2. **Intelligence Gathering:** Reconocimiento pasivo y activo
3. **Threat Modeling:** Identificación de vectores de ataque
4. **Vulnerability Analysis:** Escaneo automatizado y pruebas manuales
5. **Exploitation:** Explotación controlada con desarrollo de PoCs
6. **Post-Exploitation:** Evaluación de escalamiento de privilegios y movimiento lateral
7. **Reporting:** Documentación exhaustiva y presentación de resultados
8. 
### 1.4.2 Alcance Técnico Autorizado
### **Activos Incluidos en el Alcance (IN-SCOPE)**

El cliente TAVOLO autoriza expresamente la realización de pruebas de penetración sobre los siguientes activos digitales:

#### **a) Aplicaciones Web**

**Landing Page Corporativa:**

- **URL:** https://www.tavolo.pe
- **Descripción:** Sitio web informativo público con información sobre el producto TAVOLO
- **Componentes autorizados:** Formularios de contacto, newsletter, información corporativa
- **Tecnologías:** HTML5, CSS3, JavaScript (React/Vue/Angular - a confirmar)

**Portal Web del Comensal:**

- **URL:** https://app.tavolo.pe
- **Descripción:** Aplicación web para que comensales consulten disponibilidad y realicen reservas
- **Funcionalidades a evaluar:**
    - Sistema de autenticación (registro, login, recuperación de contraseña)
    - Visualización de disponibilidad de mesas en tiempo real
    - Sistema de reservas
    - Menú digital por sede
    - Perfil de usuario
    - Historial de reservas
- **Usuarios de prueba proporcionados:** 2 cuentas (usuario regular + usuario premium)

**Panel Administrativo por Sede:**

- **URL:** https://admin.tavolo.pe
- **Descripción:** Dashboard para administradores de cafeterías
- **Funcionalidades a evaluar:**
    - Autenticación con roles (admin de sede)
    - Gestión de mesas (agregar, editar, eliminar)
    - Visualización de reservas activas
    - Consulta de sede asignada
    - Panel de estadísticas (si está implementado)
- **Credenciales de prueba:** 1 cuenta de administrador de sede en ambiente staging

**Super Admin Dashboard:**

- **URL:** https://superadmin.tavolo.pe (o subdirectorio)
- **Descripción:** Panel de control total del sistema para equipo TAVOLO
- **Funcionalidades a evaluar:**
    - Gestión de múltiples sedes
    - Gestión de usuarios y roles
    - Configuración global del sistema
    - Analytics y reportes globales
- **Acceso:** Solo con autorización expresa para pruebas específicas

**Subdominios Autorizados:**

- Cualquier subdominio bajo `*.tavolo.pe` descubierto durante el reconocimiento que esté relacionado con la infraestructura de TAVOLO (previa confirmación con el contacto técnico)

#### **b) APIs REST**

**API Gateway Principal:**

- **Base URL:** https://api.tavolo.pe
- **Versión:** v1 (o la versión actual en producción/staging)
- **Documentación:** Swagger/OpenAPI (si está disponible)

**Endpoints Autorizados para Pruebas:**
| **Categoría**      | **Endpoints**                                                                                                                       | **Métodos**             | **Funcionalidad**                          |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------- | ----------------------- | ------------------------------------------ |
| **Autenticación**  | `/api/v1/auth/register`<br>`/api/v1/auth/login`<br>`/api/v1/auth/logout`<br>`/api/v1/auth/refresh`<br>`/api/v1/auth/reset-password` | POST                    | Gestión de autenticación y sesiones        |
| **Usuarios**       | `/api/v1/users/{id}`<br>`/api/v1/users/profile`<br>`/api/v1/users/preferences`                                                      | GET, PUT, PATCH, DELETE | Gestión de perfiles de comensales          |
| **Mesas**          | `/api/v1/tables`<br>`/api/v1/tables/{id}`<br>`/api/v1/tables/availability`                                                          | GET, POST, PUT, DELETE  | CRUD de mesas y consulta de disponibilidad |
| **Reservas**       | `/api/v1/bookings`<br>`/api/v1/bookings/{id}`<br>`/api/v1/bookings/cancel`                                                          | GET, POST, PUT, DELETE  | Sistema de reservas                        |
| **Sedes**          | `/api/v1/venues`<br>`/api/v1/venues/{id}`<br>`/api/v1/venues/{id}/menu`                                                             | GET                     | Información de cafeterías y menús          |
| **Sensores IoT**   | `/api/v1/sensors/data`<br>`/api/v1/sensors/{id}/status`                                                                             | POST, GET               | Recepción de datos de sensores             |
| **Administración** | `/api/v1/admin/venues`<br>`/api/v1/admin/tables`<br>`/api/v1/admin/bookings`                                                        | GET, POST, PUT, DELETE  | Funciones administrativas                  |

**Aspectos a Evaluar en las APIs:**

- Autenticación y autorización (JWT, OAuth 2.0, API Keys)
- Validación de entrada (injection attacks)
- Control de acceso (IDOR, privilege escalation)
- Rate limiting y throttling
- Manejo de errores y logging
- Exposición de información sensible
- CORS configuration
- Parámetros ocultos (parameter pollution)

#### **c) Aplicación Móvil**

**Plataforma Android:**

- **Package Name:** com.tavolo.app (o el nombre real del package)
- **Versión:** [X.X.X] (versión de QA/Staging proporcionada)
- **Entrega:** APK proporcionado por el cliente via email seguro o repositorio privado

**Funcionalidades de la App Móvil a Evaluar:**

1. Sistema de autenticación (login, registro, biometría si aplica)
2. Comunicación con APIs backend
3. Visualización de mesas disponibles en tiempo real
4. Sistema de reservas
5. Menú digital
6. Notificaciones push
7. Geolocalización de sedes cercanas
8. Almacenamiento local de datos (caché, tokens, preferencias)

**Tipos de Análisis Autorizados:**

- **Análisis Estático (SAST):**
    
    - Decompilación del APK (APKTool, Jadx)
    - Análisis de código fuente Java/Kotlin
    - Revisión de AndroidManifest.xml
    - Búsqueda de credenciales hardcodeadas
    - Análisis de bibliotecas de terceros vulnerables
    - Evaluación de ofuscación de código
- **Análisis Dinámico (DAST):**
    
    - Ejecución en emulador Android (Android Studio)
    - Instrumentación con Frida
    - Interceptación de tráfico (Burp Suite + Proxy)
    - Análisis de almacenamiento local (SharedPreferences, SQLite)
    - Bypass de certificate pinning (si está implementado)
    - Evaluación de root detection

**Plataforma iOS (Opcional - si se proporciona):**

- **Bundle ID:** com.tavolo.ios
- **Formato:** IPA file
- **Análisis limitado:** Solo análisis estático (el equipo no cuenta con dispositivos iOS físicos)

#### **d) Infraestructura de Red y Servidores**

**Ambiente Autorizado:** STAGING/QA únicamente (NO producción)

**Servidores de Aplicación:**

- **Hostnames/IPs:** staging-web-01, staging-api-01, staging-db-01 (o IPs específicas)
- **Sistema Operativo:** Linux (Ubuntu/CentOS/Debian) o Windows Server
- **Servicios expuestos:** HTTP/HTTPS (80, 443), SSH (22), PostgreSQL/MongoDB (5432/27017)

**Base de Datos:**

- **Tipo:** PostgreSQL / MongoDB / MySQL
- **Versión:** [X.X]
- **Acceso:** Solo desde red interna o VPN (no expuesta públicamente)
- **Nota:** Datos de staging con información ficticia o anonimizada

**Infraestructura Cloud:**

- **Proveedor:** AWS / Azure / Google Cloud / DigitalOcean
- **Servicios en scope:**
    - EC2 instances / VMs
    - S3 Buckets / Blob Storage (con datos de prueba)
    - RDS / Managed Databases (staging)
    - Load Balancers
    - API Gateways
    - Lambda Functions / Azure Functions

**Rango de IPs Autorizadas:**

- Red interna de staging: [X.X.X.0/24]
- IPs públicas específicas: [Lista de IPs]

**Aspectos a Evaluar:**

- Escaneo de puertos (Nmap full TCP/UDP scan)
- Enumeración de servicios y versiones
- Vulnerabilidades conocidas (CVEs)
- Configuraciones inseguras (SSH con password, puertos innecesarios abiertos)
- Weak passwords / default credentials
- Seguridad de S3 buckets (public access)
- IAM permissions misconfigurations
- Security groups overly permissive

#### **e) Repositorios de Código (Opcional)**

**Solo si el cliente autoriza explícitamente:**

- **Plataforma:** GitHub / GitLab / Bitbucket
- **Repositorios:** Privados de TAVOLO
- **Acceso:** Read-only para análisis de código fuente
- **Objetivo:** Identificar credenciales expuestas, vulnerabilidades en código, secretos hardcodeados

### **Activos Excluidos del Alcance (OUT-OF-SCOPE)**

**IMPORTANTE:** Los siguientes activos están estrictamente PROHIBIDOS de realizar pruebas. Cualquier actividad sobre ellos sin autorización expresa constituiría una violación del RoE y podría tener consecuencias legales.

#### **Ambiente de Producción**

- Base de datos de producción con datos reales de clientes B2B y comensales
- Servidores de producción (prod-web-_, prod-api-_, prod-db-*)
- Sensores IoT instalados en cafeterías reales operativas
- Red WiFi de cafeterías clientes de TAVOLO
- Cualquier sistema que procese transacciones o datos reales en tiempo real

**Razón:** Riesgo de impacto en operaciones reales, pérdida de datos de clientes, incumplimiento de SLAs con clientes B2B.

#### **Sistemas de Terceros**

- Infraestructura compartida de proveedores de cloud (AWS/Azure/GCP) que no sea específica de TAVOLO
- Servicios de terceros integrados:
    - Proveedores de pago (Stripe, PayPal, Culqi, Niubiz)
    - Servicios de email (SendGrid, Mailgun, AWS SES)
    - Servicios de SMS/notificaciones push (Twilio, Firebase Cloud Messaging)
    - CDN (CloudFlare, Fastly, Akamai)
    - Analytics (Google Analytics, Mixpanel)
- APIs públicas de terceros consumidas por TAVOLO

**Razón:** Violación de términos de servicio de terceros, posibles consecuencias legales, afectación a otros clientes de esos servicios.

#### **Personal y Dispositivos Personales**

- Cuentas personales de empleados de TAVOLO (email, redes sociales)
- Dispositivos personales del equipo (laptops, smartphones personales)
- Cuentas de redes sociales personales de fundadores o empleados
- Información personal no relacionada con la empresa (domicilios, vehículos, etc.)

**Razón:** Respeto a la privacidad individual, separación entre ámbito laboral y personal.

#### **Infraestructura Física**

- Oficinas físicas de TAVOLO
- Data centers físicos (si aplica)
- Routers, switches y equipos de red físicos en oficinas
- Dispositivos de seguridad física (cámaras, alarmas, control de acceso)

**Razón:** Fuera del alcance técnico del pentesting, requeriría autorización de seguridad física separada.

#### **Ataques Destructivos o de Denegación de Servicio**

- DoS/DDoS attacks contra cualquier componente
- Stress testing que pueda causar indisponibilidad
- Modificación o eliminación de datos (salvo cuentas de prueba específicamente creadas para el pentesting)
- Corrupción de sistemas de archivos
- Eliminación de logs

**Razón:** Pueden causar downtime, pérdida de datos, impacto en la reputación de TAVOLO.

#### **Ingeniería Social No Autorizada**

- Phishing contra empleados de TAVOLO (salvo campaña específicamente autorizada)
- Vishing (llamadas telefónicas de engaño)
- Pretexting o suplantación de identidad
- Physical social engineering (tailgating, dumpster diving)

**Razón:** Requiere autorización legal y de RRHH separada, posible impacto psicológico en empleados.

### **Procedimiento para Activos No Listados**

Durante el reconocimiento, es posible que se descubran activos adicionales no explícitamente mencionados en este documento (ej. subdominios no documentados, servicios internos expuestos).

**Protocolo a seguir:**

1. **DETENER** cualquier prueba sobre el activo descubierto
2. **DOCUMENTAR** el hallazgo:
    - URL/IP/hostname exacto
    - Cómo fue descubierto (herramienta, técnica)
    - Información visible sin interacción (ej. página de login, banner de servicio)
3. **NOTIFICAR** al contacto técnico de TAVOLO vía email:
    - Asunto: "[TAVOLO Pentest] Activo no listado descubierto - Solicitud de autorización"
    - Descripción del activo
    - Screenshot (si aplica)
    - Pregunta: ¿Está autorizado realizar pruebas sobre este activo?
4. **ESPERAR** respuesta por escrito (email) del contacto técnico
5. **PROCEDER** solo si se recibe autorización explícita

**Tiempo de respuesta esperado:** 24-48 horas hábiles

### 1.4.4. Tipos de Pruebas Autorizadas y Prohibidas
### **Técnicas y Pruebas PERMITIDAS**

#### **a) Fase de Reconocimiento (Intelligence Gathering)**

**Reconocimiento Pasivo (No intrusivo):**

- OSINT (Open Source Intelligence) mediante búsquedas públicas
- Google Dorking (site:tavolo.pe, inurl:, intitle:, filetype:)
- Búsquedas en Shodan, Censys, ZoomEye
- Análisis de DNS público (dig, nslookup, host)
- Enumeración de subdominios (subfinder, amass, assetfinder)
- Búsqueda en repositorios públicos de GitHub (leaks de credenciales)
- Análisis de metadatos en documentos públicos (FOCA, exiftool)
- Revisión de archive.org (WaybackMachine)
- LinkedIn reconnaissance (empleados, tecnologías mencionadas)

**Reconocimiento Activo (Intrusivo controlado):**

- Escaneo de puertos TCP/UDP completo (Nmap, Masscan)
- Service fingerprinting y version detection
- OS fingerprinting
- Enumeración de directorios y archivos web (Gobuster, ffuf, Dirbuster)
- Análisis de certificados SSL/TLS (testssl.sh, SSLScan)
- DNS zone transfer attempts (dig axfr)
- Email enumeration (Hunter.io, theHarvester)
- WAF detection (wafw00f)
- Technology stack identification (Wappalyzer, WhatWeb, Builtwith)

#### **b) Análisis de Vulnerabilidades**

**Escaneo Automatizado:**

- Vulnerability scanning con Nessus/OpenVAS
- Web application scanning con Nikto, OWASP ZAP, Burp Suite Scanner
- Fuzzing de parámetros (ffuf, wfuzz)
- API endpoint discovery y fuzzing (Arjun, Kiterunner)
- Mobile app static analysis (MobSF)
- Dependency checking (OWASP Dependency-Check, Snyk)
- Configuration scanning (Lynis para servidores Linux)

**Pruebas Manuales Detalladas:** Todas las categorías del OWASP Top 10 Web Application Security Risks:

- A01:2021 - Broken Access Control
- A02:2021 - Cryptographic Failures
- A03:2021 - Injection
- A04:2021 - Insecure Design
- A05:2021 - Security Misconfiguration
- A06:2021 - Vulnerable and Outdated Components
- A07:2021 - Identification and Authentication Failures
- A08:2021 - Software and Data Integrity Failures
- A09:2021 - Security Logging and Monitoring Failures
- A10:2021 - Server-Side Request Forgery (SSRF)

#### **c) Pruebas de Explotación Controlada**

**Injection Attacks:**

- SQL Injection (In-band, Blind, Time-based) con sqlmap, manual testing
- NoSQL Injection (MongoDB, CouchDB) en APIs
- LDAP Injection
- Command Injection (OS Command Injection)
- XML External Entity (XXE) Injection
- Template Injection (SSTI - Server-Side Template Injection)

**Cross-Site Scripting (XSS):**

- Reflected XSS
- Stored XSS
- DOM-based XSS
- Bypassing filters y WAF
- XSS to Session Hijacking PoC

**Broken Authentication & Authorization:**

- Brute force attacks (controlado: máximo 50 intentos por minuto)
- Password spraying (contraseñas comunes)
- Session fixation attacks
- JWT manipulation (algoritmo confusion, weak secret)
- OAuth2 flow vulnerabilities
- Insecure Direct Object References (IDOR)
- Privilege escalation (horizontal y vertical)
- Broken Function Level Authorization en APIs

**Business Logic Flaws:**

- Race conditions en reservas (2 usuarios reservando misma mesa simultáneamente)
- Price manipulation
- Bypass de validaciones del lado del cliente
- Parameter tampering

**Server-Side Request Forgery (SSRF):**

- SSRF para acceder a metadata de cloud (AWS, Azure)
- SSRF para port scanning interno
- Blind SSRF detection

**Security Misconfiguration:**

- Exposición de archivos sensibles (.env, .git, backups)
- Directory listing enabled
- Default credentials en servicios
- Missing security headers (CSP, HSTS, X-Frame-Options)
- Verbose error messages con stack traces
- CORS misconfiguration

**API-Specific Attacks:**

- Broken Object Level Authorization (BOLA/IDOR en APIs)
- Broken User Authentication
- Excessive Data Exposure (APIs que devuelven más info de la necesaria)
- Lack of Resources & Rate Limiting (sin causar DoS)
- Broken Function Level Authorization
- Mass Assignment vulnerabilities
- Security Misconfiguration en APIs
- API endpoint fuzzing

**Mobile Application Attacks:**

- Insecure Data Storage (SharedPreferences, SQLite sin encriptación)
- Weak Cryptography (claves hardcodeadas, algoritmos débiles)
- Insecure Communication (HTTP en lugar de HTTPS)
- Certificate Pinning bypass
- Code Tampering / Runtime manipulation con Frida
- Reverse Engineering (decompilación, análisis de código ofuscado)
- Deeplink exploitation


#### **d) Post-Explotación (Simulada y Controlada)**

**Estas actividades se realizan SOLO en ambiente de staging y con objetivo educativo:**

- Privilege escalation (user → admin)
- Lateral movement simulation (webapp → database server)
- Credential harvesting (extracción de hashes, no cracking masivo)
- Persistence techniques (evaluación teórica, NO implementación real)
- Data exfiltration simulation (identificar qué datos podrían ser robados, sin extraerlos realmente)
- Pivoting (uso de sistema comprometido para acceder a otros sistemas en scope)

**Limitaciones estrictas:**

- NO establecer persistencia real (backdoors, reverse shells persistentes)
- NO extraer grandes volúmenes de datos (máximo 10 registros por tabla)
- NO modificar configuraciones de seguridad permanentemente
- NO eliminar logs de auditoría

### **Técnicas y Pruebas PROHIBIDAS**

#### **a) Ataques de Denegación de Servicio**

**Estrictamente prohibido:**

- DoS (Denial of Service) attacks
- DDoS (Distributed Denial of Service) attacks
- Application-layer DoS (slowloris, HTTP flood)
- Resource exhaustion attacks
- Fork bombs
- Zip bombs
- XML bombs (Billion Laughs Attack) que puedan causar crash

**Rate limiting testing:**

- PERMITIDO: Validar existencia de rate limiting con requests moderados (100 req/min max)
- PROHIBIDO: Stress testing que sature recursos

#### **b) Destrucción o Modificación de Datos**

**Prohibido:**

- Eliminar registros de bases de datos (DELETE sin WHERE clause)
- Modificar datos de usuarios reales
- Truncar tablas
- DROP de bases de datos o tablas
- Modificar configuraciones de producción
- Sobrescribir archivos del sistema
- Corromper backups
- Modificar códigos fuente en repositorios
- Alterar logs del sistema para ocultar actividades

#### **c) Ingeniería Social Sin Autorización**

**Prohibido sin autorización expresa por escrito:**

- Phishing campaigns contra empleados de TAVOLO
- Spear phishing dirigido a ejecutivos
- Vishing (voice phishing) por teléfono
- Smishing (SMS phishing)
- Pretexting (creación de escenarios falsos para obtener información)
- Impersonation de soporte técnico, proveedores o clientes
- Baiting (dejar USBs con malware en oficinas)
- Tailgating o acceso físico no autorizado
- Dumpster diving (búsqueda en basura física)

**Nota:** Si en fases posteriores se desea incluir ingeniería social, se requerirá:

- Addenda al RoE específica
- Autorización de RRHH de TAVOLO
- Definición de empleados objetivo (consentimiento informado)
- Protocolo de debriefing post-ejercicio

#### **d) Uso de Exploits Peligrosos o No Validados**

**Prohibido:**

- Exploits de día cero (0-day) no revelados públicamente
- Exploits que puedan causar corrupción de memoria permanente
- Kernel exploits que puedan crashear el sistema
- Exploits sin entender completamente su funcionamiento
- Malware real (trojans, ransomware, worms)
- Cryptominers o software de minería
- Keyloggers o spyware en sistemas de producción

**Permitido:**

- Exploits de Metasploit Framework validados y documentados
- PoCs públicos de CVEs conocidos
- Custom exploits desarrollados por el equipo (revisados y validados)
- Todos los exploits deben ser ejecutados primero en ambiente local controlado

#### **e) Pivoting No Autorizado**

**Prohibido:**

- Usar sistemas comprometidos para atacar infraestructura fuera del alcance
- Intentar acceder a redes de clientes B2B de TAVOLO desde sistemas TAVOLO
- Lateral movement hacia sistemas explícitamente OUT-OF-SCOPE
- Uso de sistemas TAVOLO como proxy para ataques a terceros
- Establecer túneles hacia internet externo desde red interna

**Permitido:**

- Lateral movement entre sistemas IN-SCOPE en ambiente de staging
- Pivoting documentado y controlado para demostrar cadenas de ataque
- Requiere notificación previa al contacto técnico

#### **f) Acciones Ilegales o Antiéticas**

**Prohibido:**

- Venta o divulgación de vulnerabilidades a terceros antes de notificar al cliente
- Extorsión o amenazas basadas en hallazgos
- Uso de información obtenida para beneficio personal
- Acceso a sistemas después de finalizado el periodo autorizado
- Mantener puertas traseras activas post-proyecto
- Compartir credenciales con personas fuera del equipo autorizado
- Uso de datos personales para fines distintos al pentesting
- Publicación de hallazgos sin autorización escrita

### 1.4.5. Limitaciones Operacionales y Técnicas
### **a) Limitaciones de Tráfico y Tasa de Requests**

Para evitar impactar la disponibilidad de los servicios de TAVOLO:

**APIs REST:**

- **Rate limit de pruebas:** Máximo 100 requests por minuto por endpoint
- **Concurrencia:** Máximo 10 threads concurrentes en fuzzing
- **Payload size:** Máximo 10 MB por request en pruebas de file upload
- **Timeout:** Respetar timeouts configurados, no enviar requests infinitos

**Aplicaciones Web:**

- **Spider/Crawler:** Velocidad moderada (1-2 requests/segundo)
- **Fuzzing de directorios:** Wordlists medianas (máx 50,000 líneas), no diccionarios masivos
- **Login brute force:** Máximo 50 intentos por usuario, pausa de 5 min entre intentos

**Escaneo de Puertos:**

- **Nmap timing:** Usar `-T3` o `-T4` (no `-T5 insane`)
- **Parallel hosts:** Máximo 5 hosts simultáneos
- **Port range:** Completo permitido, pero en ventanas de mantenimiento


### **b) Limitaciones de Extracción de Datos**

**Bases de Datos:**

- **Registros extraídos:** Máximo 10 filas por tabla como evidencia
- **Tablas consultadas:** Documentar todas las tablas accedidas
- **Dumps completos:** PROHIBIDO (ni siquiera en staging con datos ficticios, por buenas prácticas)

**Archivos del Sistema:**

- **Lectura:** Permitida para archivos de configuración públicos (nginx.conf, package.json)
- **Descarga:** Solo metadatos y primeras líneas, no archivos completos de logs (GB)
- **Prohibido:** Descargar código fuente completo sin autorización explícita

**Credenciales:**

- **Almacenamiento:** En gestor de contraseñas encriptado del equipo (1Password/LastPass)
- **Uso:** Solo para validación de vulnerabilidad, no uso prolongado
- **Documentación:** Registrar en informe de forma segura (hash o asteriscos)
- **Post-proyecto:** Eliminación segura obligatoria

### **c) Ventanas de Ejecución y Horarios**

**Ambiente de Staging/QA:**

- **Disponibilidad:** 24/7 para cualquier tipo de prueba
- **Coordinación:** No requerida para pruebas estándar
- **Notificación:** Solo para pruebas potencialmente disruptivas (ej. fuzzing masivo)

**Ambiente de Producción (solo consultas no intrusivas):**

- **Días:** Lunes a Viernes
- **Horario:** 9:00 AM - 6:00 PM (UTC-5, hora de Lima)
- **Actividades permitidas:** Reconocimiento pasivo, consultas GET públicas, análisis de headers
- **Prohibido:** POST/PUT/DELETE, fuzzing, ataques de cualquier tipo

**Ventanas de Mantenimiento (para pruebas invasivas):**

- **Día:** Domingos
- **Horario:** 2:00 AM - 6:00 AM (UTC-5)
- **Coordinación:** Notificar con 48h de anticipación al contacto técnico
- **Actividades:** Escaneo completo de puertos, pruebas de explotación en infraestructura, firmware analysis

**Días NO laborables:**

- No se realizarán pruebas en feriados nacionales peruanos
- El cliente notificará días específicos de indisponibilidad (ej. mantenimientos programados)

### **d) Notificación de Hallazgos Según Severidad**

**CRÍTICO (CVSS 9.0 - 10.0):**

- **Ejemplos:** Remote Code Execution, SQL Injection con acceso total a DB, Authentication Bypass completo
- **Tiempo de notificación:** Inmediata (< 2 horas desde descubrimiento)
- **Canal:** Llamada telefónica + Email detallado + Mensaje Slack
- **Destinatario:** Contacto técnico + Contacto de emergencia
- **Acción:** Suspender pruebas en ese componente hasta coordinación
- **Documentación preliminar:** Email con:
    - Descripción técnica resumida
    - URL/endpoint/sistema afectado
    - Severidad y justificación CVSS
    - Impacto potencial
    - Screenshot de evidencia
    - Recomendación de mitigación inmediata (ej. desactivar endpoint)

**ALTO (CVSS 7.0 - 8.9):**

- **Ejemplos:** XSS almacenado, IDOR con acceso a datos sensibles, Privilege Escalation
- **Tiempo de notificación:** < 24 horas hábiles
- **Canal:** Email detallado + Mensaje Slack
- **Destinatario:** Contacto técnico
- **Acción:** Continuar con otras pruebas, documentar exhaustivamente
- **Documentación:** Email estructurado con secciones de descripción, impacto, evidencia, recomendación

**MEDIO (CVSS 4.0 - 6.9):**

- **Ejemplos:** XSS reflejado, Information Disclosure, Missing security headers
- **Tiempo de notificación:** En Sprint Review semanal
- **Canal:** Documentación en herramienta de gestión (Jira/Trello) + Mención en reunión
- **Acción:** Continuar pruebas normalmente

**BAJO (CVSS 0.1 - 3.9):**

- **Ejemplos:** Verbose error messages, Clickjacking en páginas no críticas
- **Tiempo de notificación:** En informe de Sprint Review
- **Canal:** Documentación en repositorio del proyecto
- **Acción:** Continuar pruebas normalmente

**INFORMATIVO (CVSS 0.0):**

- **Ejemplos:** Recomendaciones de hardening, mejores prácticas no implementadas
- **Tiempo de notificación:** En informe final
- **Documentación:** Sección de recomendaciones generales

### **e) Uso de Herramientas y Software**

**Herramientas Aprobadas (lista no exhaustiva):**

- Sistema operativo: Kali Linux, Parrot Security OS
- Proxy/Interceptor: Burp Suite Community/Pro, OWASP ZAP
- Scanners: Nmap, Masscan, Nessus, OpenVAS, Nikto
- Exploitation: Metasploit Framework, sqlmap, BeEF
- Mobile: MobSF, Frida, APKTool, Jadx, Objection
- Fuzzing: ffuf, wfuzz, Gobuster, Arjun
- Password: John the Ripper, Hashcat (solo hashes obtenidos legítimamente)
- Recon: subfinder, amass, theHarvester, Shodan, Censys
- Post-exploitation: Mimikatz (solo staging), BloodHound (si AD está en scope)

**Herramientas Prohibidas:**

- Malware real o ransomware
- Exploits de propósito destructivo
- Herramientas de DDoS (LOIC, HOIC)
- Cryptominers
- Cualquier herramienta ilegal o de distribución prohibida

**Desarrollo de Scripts Personalizados:**

- Permitido y recomendado para automatizar pruebas específicas
- Deben ser revisados por el equipo antes de ejecución
- Compartir con cliente si solicita (como parte de entregables)
- Documentar claramente su funcionamiento

### 1.4.6. Responsabilidades de las Partes

### **Responsabilidades del Cliente (TAVOLO)**

#### **1. Provisión de Accesos y Recursos**

**Credenciales de Prueba:**

- Proporcionar al menos 2 cuentas de usuario comensal en ambiente staging:
    - 1 usuario regular
    - 1 usuario premium/VIP (si aplica diferenciación de roles)
- 1 cuenta de administrador de sede:
    - Con permisos completos para gestión de mesas y reservas
    - Asignada a una sede ficticia de prueba
- 1 cuenta de super administrador (solo si se autoriza evaluar ese panel)
- Todas las contraseñas deben ser seguras pero documentadas

**Acceso a Infraestructura:**

- VPN credentials (si se requiere acceso a red interna)
- Acceso SSH a servidores de staging (con IP whitelisting del equipo)
- Credenciales de base de datos de staging (read-only preferentemente)

**Materiales Técnicos:**

- APK de la aplicación móvil (versión de QA, firmado para testing)
- Documentación de API (Swagger/Postman collection)
- Diagrama de arquitectura de alto nivel
- Lista de IPs/hostnames de servidores en scope

#### **2. Preparación del Ambiente**

**Ambiente de Staging Representativo:**

- Configuración idéntica o muy similar a producción
- Datos ficticios pero realistas (volumetría representativa)
- Servicios completamente funcionales
- Aislado de producción (sin conexión a DB real, sin sensores reales)

**Backups y Recuperación:**

- Realizar backup completo antes del inicio del pentesting
- Mantener snapshots de VMs durante las 15 semanas del proyecto
- Capacidad de restaurar ambiente en < 4 horas si es necesario

**Monitoreo y Logging:**

- Activar logs centralizados (syslog, application logs, access logs)
- Proporcionar acceso a logs al equipo (para validar detección)
- Configurar alertas para actividad anómala (sin bloquear al equipo de pentesting)

**Comunicación de Cambios:**

- Notificar al equipo cualquier cambio en infraestructura (deploys, mantenimientos)
- Informar sobre nuevas funcionalidades desplegadas en staging
- Avisar con 48h de anticipación si habrá indisponibilidad de servicios

#### **3. Manejo de Hallazgos**

**Durante el Pentesting:**

- No implementar correcciones de vulnerabilidades sin notificar al equipo
    - Razón: Puede invalidar evidencias en proceso de documentación
    - Excepción: Vulnerabilidades críticas con riesgo inmediato (coordinado)
- Mantener vulnerabilidades en staging para permitir validación y PoC development
- Responder consultas de clarificación sobre hallazgos en < 48 horas

**Post-Pentesting:**

- Revisar informe final y proporcionar feedback en < 7 días
- Priorizar remediación de vulnerabilidades críticas y altas
- Permitir re-testing de vulnerabilidades críticas corregidas (1 sesión incluida)

#### **4. Protección Legal de la Consultora**

**No tomar acciones legales contra el equipo por:**

- Hallazgos reportados de buena fe dentro del alcance
- Vulnerabilidades identificadas que afecten la imagen de la empresa
- Accesos no autorizados descubiertos accidentalmente y reportados inmediatamente

**Indemnización:**

- Defender a la consultora contra reclamos de terceros derivados de pruebas autorizadas
- Asumir responsabilidad si un cliente B2B se ve afectado (si las pruebas estuvieron dentro del alcance)

### **Responsabilidades de la Consultora**

#### **1. Conducta Ética y Profesional**

**Respeto Estricto del Alcance:**

- Realizar pruebas SOLO sobre activos explícitamente autorizados en este RoE
- Detener actividades inmediatamente si se descubre impacto en sistemas OUT-OF-SCOPE
- Consultar antes de proceder con activos descubiertos no listados

**Código de Ética:**

- Cumplir con el código de ética de ACM (Association for Computing Machinery)
- Cumplir con el código de ética de IEEE Computer Society
- Respetar los principios del Colegio de Ingenieros del Perú (CIP)
- Actuar con integridad, honestidad y transparencia en todo momento

**No Uso Indebido de Información:**

- No utilizar información obtenida para beneficio personal o de terceros
- No acceder a sistemas después de finalizado el periodo autorizado
- No vender, compartir o publicar vulnerabilidades sin autorización

#### **2. Ejecución Técnica Profesional**

**Aplicación de Metodologías:**

- Seguir Penetration Testing Execution Standard (PTES)
- Aplicar OWASP Testing Guide para aplicaciones web
- Usar OWASP API Security Project para APIs
- Seguir OWASP Mobile Security Testing Guide para app móvil
- Aplicar OWASP IoT Security Testing Guide para dispositivos IoT

**Uso de Herramientas Estándar:**

- Utilizar herramientas reconocidas de la industria (Kali Linux, Metasploit, Burp Suite, etc.)
- Documentar todas las herramientas utilizadas en el informe
- Validar exploits en ambiente controlado antes de usarlos contra TAVOLO

**Documentación Exhaustiva:**

- Mantener logs detallados de todas las actividades (comandos, timestamps, resultados)
- Capturar screenshots con timestamp visible
- Grabar videos de explotaciones críticas (si es posible)
- Usar herramienta de note-taking (CherryTree, Notion, Obsidian)

#### **3. Seguridad y No Destructividad**

**Pruebas Controladas:**

- Realizar pruebas de forma incremental (validar impacto antes de escalar)
- Tener plan de rollback para cada acción potencialmente disruptiva
- Mantener respaldos de datos extraídos para evidencia

**Detención Inmediata en Caso de Incidente:**

- Si un servicio se cae inesperadamente: STOP ALL TESTING
- Documentar exactamente qué se estaba haciendo (comando, herramienta, timestamp)
- Notificar al contacto de emergencia en < 15 minutos
- Esperar instrucciones antes de continuar

**No Causar Daños:**

- NO eliminar datos (salvo registros de test creados por el equipo)
- NO modificar configuraciones de producción
- NO causar indisponibilidad de servicios
- NO comprometer datos de usuarios reales

#### **4. Comunicación Proactiva y Transparente**

**Notificación de Hallazgos Críticos:**

- Seguir protocolo de escalamiento según severidad (ver sección 1.4.5.D)
- No "guardar" hallazgos para el informe final si son críticos
- Proporcionar recomendaciones de mitigación inmediata junto con el hallazgo

**Participación en Sprints:**

- Asistir a todas las ceremonias programadas (Sprint Planning, Reviews)
- Proporcionar updates diarios asíncronos del progreso
- Comunicar bloqueos o impedimentos al Scrum Master

**Transparencia en Dificultades:**

- Si no se encuentra vulnerabilidades en un área: reportarlo honestamente
- Si una herramienta falla: documentarlo y usar alternativas
- Si se necesita más tiempo: negociar extensión con anticipación

#### **5. Confidencialidad Absoluta**

**Durante el Proyecto:**

- No divulgar a terceros que se está realizando pentesting para TAVOLO
- No compartir capturas de pantalla, URLs o información en redes sociales
- Mantener credenciales en gestor de contraseñas encriptado
- No trabajar en espacios públicos con información sensible visible

**Post-Proyecto:**

- No publicar hallazgos en blogs, Twitter, conferencias sin autorización escrita
- No usar vulnerabilidades específicas de TAVOLO como ejemplos en otros trabajos
- Versión pública del informe (para portfolio): completamente anonimizada

**Manejo de Datos Sensibles:**

- Encriptar todos los archivos relacionados con el proyecto (VeraCrypt, GPG)
- Usar comunicaciones encriptadas (Signal, ProtonMail si se requiere alta confidencialidad)
- Eliminar datos de forma segura post-proyecto (sobrescritura múltiple, no solo borrado)

#### **6. Entregables de Calidad**

**Informe Técnico:**

- Formato profesional (Markdown en GitHub + PDF exportado)
- Estructura clara siguiendo el template del curso
- Evidencias reproducibles (screenshots, comandos, outputs)
- Clasificación CVSS correcta y justificada
- Recomendaciones técnicas específicas y accionables

**Informe Ejecutivo:**

- Lenguaje no técnico para dirección
- Resumen de riesgos de negocio
- Priorización clara
- Roadmap de remediación con timeline

**Proof of Concepts:**

- Scripts funcionales y documentados
- Instrucciones paso a paso de reproducción
- Requisitos y dependencias listados
- Código comentado y limpio

**Plan de Mitigación:**

- Recomendaciones priorizadas por urgencia e impacto
- Esfuerzo estimado (horas/días)
- Referencias a documentación oficial (OWASP, CWE, vendor docs)
- Quick wins vs. proyectos a largo plazo identificados

**Presentaciones:**

- PowerPoint/Google Slides profesional
- Videos de exposición editados (máx 15 min)
- Demos en vivo de explotaciones en Sprint Reviews

#### **7. Post-Proyecto**

**Soporte Post-Entrega:**

- Responder consultas de clarificación: 30 días post-entrega
- Canal: Email (respuesta en < 72 horas hábiles)
- No incluye: Nuevas pruebas o desarrollo de PoCs adicionales

**Re-Testing Incluido:**

- 1 sesión de re-testing de vulnerabilidades críticas corregidas
- Duración: Máximo 1 día (8 horas)
- Timeline: Dentro de 60 días post-entrega del informe final
- Entregable: Addendum al informe confirmando correcciones o identificando bypasses

**Eliminación Segura de Datos:**

- Plazo: 7 días post-cierre del proyecto
- Alcance: Credenciales, datos extraídos, capturas con PII
- Método: Sobrescritura múltiple (shred en Linux, sdelete en Windows)
- Certificado: Email confirmando destrucción de datos sensibles
- Retención: Solo versión final del informe (anonimizada si es para portfolio)

### 1.4.7. Confidencialidad y Uso de Información
### **Acuerdo de No Divulgación (NDA Integrado)**

Ambas partes reconocen que durante el pentesting se accederá a información altamente sensible y propietaria. Por tanto, se establecen los siguientes términos de confidencialidad:

#### **Información Considerada Confidencial:**

- **Técnica:**
    
    - Vulnerabilidades identificadas y su severidad
    - Arquitectura de sistemas y diagramas de red
    - Código fuente (si se proporciona acceso)
    - Credenciales y secretos (API keys, tokens, certificados)
    - Configuraciones de servidores y servicios
    - Algoritmos propietarios y lógica de negocio
- **Comercial:**
    
    - Datos de clientes B2B (cafeterías)
    - Métricas de negocio y volúmenes de transacciones
    - Estrategia de producto y roadmap
    - Información financiera o de inversión
- **Personal:**
    
    - Datos personales de comensales (nombres, emails, teléfonos)
    - Información de empleados de TAVOLO

#### **Obligaciones de Confidencialidad de la Consultora:**

**Durante el Proyecto:**

- Limitar acceso a información solo a miembros del equipo con need-to-know
- No discutir el proyecto en espacios públicos o con personas no autorizadas
- No publicar en redes sociales (LinkedIn, Twitter) sin autorización
- Usar dispositivos personales encriptados para almacenar información del proyecto

**Comunicaciones:**

- Email: Usar TLS/StartTLS (verificar cifrado)
- Archivos grandes: Usar servicios con cifrado end-to-end (Tresorit, SpiderOak)
- Videollamadas: Usar plataformas seguras (Zoom con waiting room, Google Meet)
- Mensajería: Slack workspace privado o Signal para temas sensibles

**Almacenamiento:**

- Repositorio GitHub: Privado (no público hasta autorización)
- Notas y documentos: En carpeta encriptada (VeraCrypt container)
- Screenshots: Almacenar en carpeta local encriptada, no en cloud público
- Backups: Encriptados con contraseña robusta

**Post-Proyecto - Uso Permitido:**

- Incluir a TAVOLO como cliente en portfolio (solo con autorización escrita)
- Mencionar tipo de proyecto realizado ("Pentesting para startup FoodTech")
- Uso académico en UPC: Permitido con datos anonimizados

**Post-Proyecto - Uso Prohibido:**

- Publicar detalles técnicos específicos de vulnerabilidades
- Compartir PoCs de vulnerabilidades de TAVOLO públicamente
- Usar en presentaciones o conferencias sin previa aprobación
- Mencionar nombres de vulnerabilidades críticas no parcheadas

#### **Excepciones de Confidencialidad (Divulgación Autorizada):**

**Contexto Académico:**

- El informe completo será presentado a docentes de UPC como Trabajo Final
- Los docentes están sujetos a confidencialidad académica
- Para repositorio institucional UPC: Versión anonimizada

**Versión Pública Anonimizada (Portfolio):** Solo si TAVOLO aprueba por escrito, se puede publicar versión donde:

- Nombre de la empresa: "Empresa Cliente - Startup de Tecnología IoT para sector gastronómico"
- URLs reales: Reemplazadas por "example.com", "target.local"
- IPs: Reemplazadas por IPs privadas (10.0.0.x, 192.168.x.x)
- Nombres de personas: Removidos o anonimizados
- Datos de negocio: Generalizados o eliminados
- Screenshots: Redactados para ocultar información identificable

**Divulgación Responsable (Responsible Disclosure):** Si se descubre vulnerabilidad que afecta también a terceros (ej. librería open source):

1. Notificar primero a TAVOLO
2. Coordinador con TAVOLO para notificar a vendor de software afectado
3. Seguir timeline de divulgación responsable (típicamente 90 días)
4. No publicar hasta que TAVOLO y vendor hayan parchado

#### **Duración del Acuerdo de Confidencialidad:**

- **Vigencia:** Indefinida
- **Inicio:** Desde la fecha de aceptación de este RoE
- **Obligaciones persisten:** Incluso después de terminado el proyecto
- **No expira:** Salvo autorización escrita explícita de TAVOLO

#### **Consecuencias de Incumplimiento:**

- Responsabilidad civil por daños y perjuicios
- Posible responsabilidad penal (Ley N° 30096 - Delitos Informáticos)
- Reporte a autoridades académicas de UPC (puede afectar calificaciones)
- Exclusión de certificado de pentesting completado