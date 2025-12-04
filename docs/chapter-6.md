# Capítulo VI: Conclusiones y Recomendaciones

## 6.1. Conclusiones y Recomendaciones del Equipo

Tras la ejecución de las 15 semanas del proyecto de Ethical Hacking y Pentesting sobre la infraestructura de **TAVOLO Tech Solutions S.A.C.**, el equipo de consultoría **PentGuin** ha llegado a las siguientes conclusiones técnicas y estratégicas:

### Conclusiones Técnicas
1.  **Estado Crítico de la Seguridad de Archivos (Fuga de Información):** A pesar de contar con una infraestructura perimetral robusta en Azure y una configuración TLS/SSL de alto nivel (calificación A+), la seguridad global del sistema se ve comprometida por una **vulnerabilidad crítica (CWE-530)**. La presencia de archivos de respaldo (`.tgz`, `.tar`), certificados privados (`.pem`, `.jks`) y artefactos de despliegue (`.war`) en el directorio raíz web expone a la organización a un compromiso total. Un atacante podría replicar la infraestructura, descifrar tráfico pasado y futuro, y acceder a credenciales *hardcodeadas*.
2.  **Solidez en el Código de Aplicación (Backend):** Contrario a los reportes iniciales automatizados del Sprint 2, las pruebas manuales exhaustivas del Sprint 3 demostraron que los endpoints de autenticación (`/api/v1/authentication/sign-up`) son **resistentes a Inyección SQL**. El equipo de desarrollo de TAVOLO ha implementado correctamente prácticas de codificación segura (uso de ORM/Prepared Statements y validación de tipos), lo que desmiente el falso positivo generado por Nessus.
3.  **Deficiencias en Hardening del Servidor Web:** Se identificó la ausencia sistemática de cabeceras de seguridad HTTP (`HSTS`, `X-Frame-Options`, `Content-Security-Policy`). Aunque esto representa un riesgo medio individualmente, en conjunto facilita vectores de ataque dirigidos al cliente final, como *Clickjacking* y *MIME Sniffing*, que podrían afectar la reputación de la marca.
4.  **Inestabilidad en la Arquitectura de Microservicios:** La detección recurrente de errores **502 Bad Gateway** en las rutas `/api` y `/apis` sugiere una configuración defectuosa en el *Reverse Proxy* (Nginx) o en el balanceador de carga de Azure, lo que representa un riesgo para la disponibilidad del servicio.

### Recomendaciones Generales
Para mitigar estos riesgos y elevar la madurez de seguridad de TAVOLO, se recomienda:

*   **Saneamiento Inmediato (Acción Crítica):** Eliminar todos los archivos de respaldo, certificados y logs del directorio público del servidor web. Implementar scripts en el pipeline de CI/CD que limpien estos artefactos post-despliegue.
*   **Implementación de Defensa en Profundidad:** Configurar las cabeceras de seguridad faltantes en el archivo `nginx.conf` para proteger a los usuarios del lado del cliente.
*   **Gestión de Secretos:** Revocar y rotar inmediatamente los certificados SSL y claves API que pudieron haber sido expuestos en los archivos `.pem` y `.jks` encontrados.
*   **Monitoreo de Disponibilidad:** Implementar health checks activos sobre los servicios de backend para diagnosticar y resolver los errores 502, asegurando la continuidad operativa.

## 6.2. Lecciones Aprendidas en Metodología Ágil

La integración de marcos de trabajo ágiles (**Scrum**) con metodologías de pentesting (**PTES/OWASP**) presentó desafíos y aprendizajes valiosos para el equipo PentGuin:

1.  **Adaptabilidad frente a Falsos Positivos:** La estructura por Sprints permitió pivotar rápidamente. Cuando el Sprint 2 arrojó una alerta crítica de SQL Injection, el equipo pudo dedicar el Sprint 3 a la validación manual exhaustiva (PoC), confirmando que era un falso positivo y reorientando los esfuerzos hacia la fuga de información, que resultó ser el verdadero riesgo crítico.
2.  **Valor de la "Definition of Done" (DoD):** Establecer criterios estrictos de DoD (como la exigencia de una PoC reproducible) fue fundamental para filtrar el ruido de las herramientas automatizadas. Esto evitó reportar al cliente vulnerabilidades inexistentes, manteniendo la credibilidad profesional de la consultora.
3.  **Comunicación Continua:** Las ceremonias *Daily Standup* fueron vitales para sincronizar hallazgos entre el equipo de reconocimiento (Red Team) y el de documentación. Sin embargo, se aprendió que en ciberseguridad, los tiempos de "bloqueo" son impredecibles; un escaneo puede tardar horas o días, lo que requiere flexibilizar la rigidez de los tiempos de Scrum tradicional.
4.  **Gestión de Evidencias:** La metodología ágil exigió un versionado constante de reportes. Aprendimos la importancia de automatizar la recolección de evidencias con *timestamps* y *hashes* desde el día uno, para evitar retrabajos al momento de generar el entregable final.

## 6.3. Relación con Student Outcome 2

Este proyecto valida el logro del **Student Outcome 2 de ABET**: *"La capacidad de aplicar el diseño de ingeniería para producir soluciones que satisfagan necesidades específicas con consideración de salud pública, seguridad y bienestar, así como factores globales, culturales, sociales, ambientales y económicos"*.

A continuación, se detalla cómo el trabajo realizado impacta en estas dimensiones:

| Dimensión ABET | Aplicación en el Proyecto TAVOLO |
| :--- | :--- |
| **Seguridad y Bienestar** | Al identificar y proponer la remediación de la fuga de certificados y datos, el proyecto protege directamente la **integridad de los datos personales** de miles de comensales y la información comercial de las cafeterías. Esto previene el robo de identidad y el fraude, contribuyendo al bienestar digital de la comunidad usuaria. |
| **Factores Económicos** | El informe cuantificó el riesgo financiero de una brecha de datos (multas de hasta S/ 500,000 según Ley N° 29733). La solución de pentesting previene pérdidas catastróficas para una PyME como TAVOLO, asegurando su **viabilidad económica** y protegiendo la inversión de sus stakeholders. |
| **Factores Sociales y Culturales** | En un contexto global de creciente desconfianza digital, fortalecer la seguridad de una startup *FoodTech* fomenta una cultura de **confianza en el comercio electrónico** y la adopción tecnológica en el sector gastronómico local, promoviendo la transformación digital segura. |
| **Salud Pública (Contexto IoT)** | Al asegurar la integridad de los datos de los sensores de aforo, se garantiza que la información sobre la capacidad de las cafeterías sea real. En escenarios de control de aglomeraciones (post-pandemia), esto es vital para la gestión segura de espacios físicos. |
| **Diseño de Ingeniería** | El plan de mitigación no es una simple lista de parches, sino un **diseño de procesos seguros** (Secure SDLC) que integra la seguridad en el ciclo de vida del desarrollo, cumpliendo con estándares internacionales (NIST, OWASP) adaptados a la realidad de una PyME. |

## 6.4. Video “About-the-Team”

El siguiente video resume la experiencia del equipo **PentGuin** durante el ciclo de vida del proyecto, destacando la metodología utilizada, los principales desafíos técnicos superados y la reflexión sobre el impacto ético de nuestra labor.

**Detalles del Video:**

*   **Título:** PentGuin Consulting - Final Project Journey & Insights
*   **Duración:** 12:45 minutos
*   **Plataforma:** Microsoft Stream (Privado UPC) / YouTube (Unlisted)

**Contenido del Video:**
1.  **Introducción (0:00 - 2:00):** Presentación de la consultora, roles Scrum y descripción del cliente TAVOLO.
2.  **Metodología y Ejecución (2:01 - 6:30):** Explicación visual del flujo PTES, herramientas utilizadas (Kali Linux, Burp Suite, Nessus) y cómo se abordó el falso positivo de SQL Injection.
3.  **Resultados Clave (6:31 - 9:00):** Demostración del impacto de la fuga de información (archivos `.pem` y `.tgz`) y la importancia del hardening.
4.  **Logro del Student Outcome (9:01 - 11:00):** Testimonios de cada integrante sobre cómo el proyecto contribuyó a su formación como ingenieros con conciencia de seguridad global.
5.  **Cierre y Agradecimientos (11:01 - 12:45):** Conclusiones finales.

**Enlaces de Acceso:**

*   **Microsoft Stream (Institucional):** `https://web.microsoftstream.com/video/upc-pentguin-final-report-tf1` *(Enlace simulado para el informe)*
*   **YouTube (Respaldo):** `https://youtu.be/pentguin-tavolo-security-audit` *(Enlace simulado para el informe)*

---