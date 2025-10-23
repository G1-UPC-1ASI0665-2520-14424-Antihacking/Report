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

### 2.3. Planificación de sprints (Sprint Planning)

### 2.4. Definición de Done (DoD)

### 2.5. Herramientas