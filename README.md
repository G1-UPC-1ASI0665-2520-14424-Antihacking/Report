# **COURSE PROJECT**

<p align="center">
  <img src="https://www.upc.edu.pe/static/img/logo_upc_red.png" alt="Logo de la UPC" />
</p>

<p align="center"><strong>Universidad Peruana de Ciencias Aplicadas</strong></p>

<p align="center"><strong>Ingeniería de Software</strong><br>
<strong>1ASI0665 - Anti-Hacking y Nuevas Tendencias de Seguridad</strong> - NRC: 14424 <br>
Ciclo Académico: 202520 <br>
<strong>Profesor(es):</strong> Vera Olivera, David Carlos</p>

<h2 align="center">INFORME DE TRABAJO FINAL – ANTI-HACKING Y NUEVAS TENDENCIAS DE SEGURIDAD</h2>

<h3 align="center">Consultora de Ciberseguridad: <em>CyberChain</em></h3>
<h3 align="center">Cliente (PyME): <em>TAVOLO Tech Solutions S.A.C.</em></h3>
<p align="center"><em>"Securing the chain you rely on"</em></p>

<h3 align="center">Equipo de Consultoría</h3>

<div align="center">

<table>
  <thead>
    <tr>
      <th><strong>Código</strong></th>
      <th><strong>Apellidos, Nombres</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>U20221C936</td>
      <td>Pescoran Angulo, Juan Fabritzzio</td>
    </tr>
    <tr>
      <td>U202022387</td>
      <td>Curi Marcelo, Angelo Marcio</td>
    </tr>
    <tr>
      <td>U202102344</td>
      <td>Gamio Upiachihua, Brenda Lucía</td>
    </tr>
    <tr>
      <td>U202215285</td>
      <td>Baldeon Fabian, Aldo Alberto</td>
    </tr>
    <tr>
      <td>U202214477</td>
      <td>Soto Quispe, Diego Ulises</td>
    </tr>
  </tbody>
</table>

</div>

<p align="center"><strong>Noviembre 2025</strong></p>

# Registro de Versiones del Informe

| Versión | Fecha       | Autor(es) | Descripción de la modificación |
|--------|-------------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TP** | 26/10/2025  | **Pescoran Angulo, Juan Fabritzzio**<br><br>**Curi Marcelo, Angelo Marcio**<br><br>**Gamio Upiachihua, Brenda Lucía**<br><br>**Baldeon Fabian, Aldo Alberto**<br><br>**Soto Quispe, Diego Ulises** | Versión inicial **TP1** (Anti‑Hacking): incluye carátula; Registro de Versiones; **Project Report Collaboration Insights**; **Tabla de Contenidos con hipervínculos**; **Student Outcome (SO2)**. Contenido incluido en esta versión: <br>**Cap. I – Introducción** (perfil del cliente y consultora; problemática; **Rules of Engagement** firmadas y escaneadas); <br>**Cap. II – Metodología Ágil y de Pentesting** (Scrum; PTES/OWASP/NIST 800-115; backlog de seguridad; plan de sprints; DoD; herramientas: Kali, Metasploit, Burp/ZAP, Nmap, sqlmap, Wireshark); <br>**Cap. III – Desarrollo por Sprints** (Sprint 1: OSINT y reconocimiento con Nmap/Masscan; Sprint 2: enumeración y análisis preliminar de vulnerabilidades); <br>**Cap. IV – Resultados Consolidados**; <br>**PoC inicial controlada (no destructiva)**. |

## Project Report Collaboration Insights

La coordinación del proyecto se realizó mediante un repositorio en GitHub (documentación pública para el informe), aplicando un flujo GitFlow y la convención de commits 'Conventional Commits' para asegurar trazabilidad de cambios y facilitar revisiones.

- Roles (Scrum): Product Owner; Scrum Master; Pentesters (Web, API, Móvil, Red/Infra); Documentación y Análisis.
- Herramientas principales: Kali Linux, Metasploit, Burp Suite / ZAP, Nmap, sqlmap, Wireshark (complementarias: Nessus/OpenVAS, Nikto, MobSF).
- Evidencias y gobernanza:
  - Capturas y registros por miembro que documentan resultados de reconocimiento, escaneo y hallazgos (Nmap, Masscan, Burp), incluidos en los anexos y referenciados en los Pull Requests.
  - Pull Requests, diffs y comentarios que evidencian revisión entre pares y control de calidad editorial.
  - Salidas y logs estructurados (texto/JSON) y scripts reproducibles que permiten la replicación de pruebas de reconocimiento y enumeración.
  - Documento firmado de Rules of Engagement (anexo) y valores hash (SHA256) asociados a artefactos críticos para garantizar integridad.
  - Nota sobre ética y trazabilidad: todas las pruebas se ejecutaron conforme a las Rules of Engagement acordadas; las evidencias cuentan con metadatos (autor, fecha, descripción) y valores de integridad, y se aplicaron controles de acceso para preservar confidencialidad y cumplimiento legal.

- Repositorio: [G1-UPC-1ASI0665-2520-14424-Antihacking](https://github.com/G1-UPC-1ASI0665-2520-14424-Antihacking) (repositorio principal de documentación y evidencias del proyecto)

Las evidencias están descritas y referenciadas tanto en el cuerpo del informe como en los anexos; se recomienda mantener un manifiesto de evidencias (`evidence_manifest.csv`) con mapeo nombre–archivo, autor, fecha y hash para facilitar auditoría y trazabilidad.

## **TP (Resumen de avance)**

- Mejora de alcance con el cliente (dominios, subdominios, APIs, sistemas en ambiente de pruebas).
- **Sprint 1** finalizado: OSINT, reconocimiento y escaneo inicial con Nmap / Masscan; recopilación de superficie de ataque.
- **Sprint 2** en curso: enumeración de servicios y análisis preliminar de vulnerabilidades (Nessus/Nikto/Burp) y priorización inicial de hallazgos.
- Consolidación de resultados preliminares y preparación de evidencias para su inclusión en el informe; los resultados consolidados se presentan en **Cap. IV – Resultados Consolidados**.
- Redacción y control de versiones del informe en Markdown (rama `develop`, PRs por capítulo) con revisión entre pares.

# Contenido

## Tabla de Contenidos

- [**Capítulo I: Introducción**](#capítulo-i-introducción)
    - [1.1. Client Profile (PyME)](#11-client-profile-pyme)
        - [1.1.1. Descripción de la PyME](#111-descripción-de-la-pyme)
        - [1.1.2. Expectativas del cliente](#112-expectativas-del-cliente)
    - [1.2. Consultora de Ciberseguridad (Equipo)](#12-consultora-de-ciberseguridad-equipo)
        - [1.2.1. Perfiles y roles Scrum](#121-perfiles-y-roles-scrum)
    - [1.3. Solution Profile](#13-solution-profile)
        - [1.3.1. Antecedentes y problemática](#131-antecedentes-y-problemática)
        - [1.3.2. Objetivos del pentesting](#132-objetivos-del-pentesting)
    - [1.4. Aceptación del Servicio (Rules of Engagement)](#14-aceptación-del-servicio-rules-of-engagement)
- [**Capítulo II: Metodología Ágil y de Pentesting**](#capítulo-ii-metodología-ágil-y-de-pentesting)
    - [2.1. Marco de referencia (Scrum + PTES/OWASP/NIST 800-115)](#21-marco-de-referencia-scrum--ptesowaspnist-800-115)
    - [2.2. Backlog inicial (User Stories de seguridad)](#22-backlog-inicial-user-stories-de-seguridad)
    - [2.3. Planificación de Sprints](#23-planificación-de-sprints)
    - [2.4. Definition of Done (DoD)](#24-definition-of-done-dod)
    - [2.5. Herramientas](#25-herramientas)
- [**Capítulo III: Desarrollo del Proyecto por Sprints**](#capítulo-iii-desarrollo-del-proyecto-por-sprints)
    - [Sprint 1 – Reconocimiento y Escaneo](#sprint-1--reconocimiento-y-escaneo)
    - [Sprint 2 – Enumeración y Vulnerabilidades](#sprint-2--enumeracion-y-vulnerabilidades)
    - [Sprint 3 – Explotación](#sprint-3--explotacion)
    - [Sprint 4 – Post-explotación y Persistencia](#sprint-4--post-explotacion-y-persistencia)
    - [Sprint 5 – Informe Final y Recomendaciones](#sprint-5--informe-final-y-recomendaciones)
- [**Capítulo IV: Resultados Consolidados**](#capítulo-iv-resultados-consolidados)
- [**Capítulo V: Recomendaciones y Plan de Mitigación**](#capítulo-v-recomendaciones-y-plan-de-mitigacion)
- [**Capítulo VI: Conclusiones y Video About-the-Team**](#capítulo-vi-conclusiones-y-video-about-the-team)
- [**Bibliografía (APA 7)**](#bibliografía-apa-7)
- [**Anexos**](#anexos)

# Student Outcome 2 - ABET - EAC 

Criterio: La capacidad de aplicar el diseño de ingeniería para producir soluciones que satisfagan necesidades específicas con consideración de salud pública, seguridad y bienestar, así como factores globales, culturales, sociales, ambientales y económicos. En el siguiente cuadro se describe las acciones realizadas y enunciados de conclusiones por parte del grupo, que permiten sustentar el logro del ABET – EAC – Student Outcome 2.


| Criterio específico | Acciones realizadas (TP) | Conclusiones |
|---|---|---|
| Diseña soluciones en ingeniería de software (productos, procesos y/o servicios) que satisfagan necesidades específicas considerando el impacto en salud pública, seguridad, bienestar, así como factores globales, culturales, sociales, ambientales y económicos. | **TP**<br>• Pescoran Angulo, Juan Fabritzzio: definición del alcance autorizado (dominios, sistemas, APIs) y elaboración de la matriz inicial de riesgos.<br>• Curi Marcelo, Angelo Marcio: desarrollo del backlog de seguridad, Definition of Done y mapeo objetivo–entregable.<br>• Gamio Upiachihua, Brenda Lucía: identificación de necesidades del negocio, restricciones legales y lineamientos de tratamiento de datos.<br>• Baldeon Fabian, Aldo Alberto: actividades de OSINT y reconocimiento (Nmap, Masscan); consolidación de la superficie de ataque.<br>• Soto Quispe, Diego Ulises: elaboración de PoC controladas y establecimiento de pautas éticas y de confidencialidad. | El equipo diseñó y ejecutó soluciones de pentesting coherentes con los riesgos identificados; las decisiones de priorización y las medidas propuestas consideraron el impacto en salud, seguridad y continuidad operativa, y están sustentadas por evidencia verificable. |
| Valida que el diseño de la solución de software considere aspectos en salud pública, seguridad, bienestar, así como factores globales, culturales, sociales, ambientales y económicos. | **TP**<br>• Pescoran Angulo, Juan Fabritzzio: establecimiento de reglas de compromiso (sin DoS, ventanas de prueba) y control de impacto en disponibilidad.<br>• Curi Marcelo, Angelo Marcio: definición de métricas de validación y criterios reproducibles de aceptación.<br>• Gamio Upiachihua, Brenda Lucía: creación de checklist de cumplimiento y buenas prácticas de manejo de datos.<br>• Baldeon Fabian, Aldo Alberto: verificación no intrusiva de hallazgos y documentación de falsos positivos.<br>• Soto Quispe, Diego Ulises: trazabilidad y resguardo de evidencias con registros y hashes. | Las actividades de validación incorporaron criterios técnicos y de gobernanza; la evidencia recopilada (logs, capturas y manifiesto) permite auditar hallazgos y verificar la eficacia de las medidas de mitigación. |

