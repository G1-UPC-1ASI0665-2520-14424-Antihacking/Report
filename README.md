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
<h3 align="center">Cliente (PyME): <em>&lt;Razón social / RUC&gt;</em></h3>
<p align="center"><em>"Securing the chain you rely on"</em></p>

<h3 align="center">Equipo de Consultoría</h3>

<div align="center">

<table>
  <thead>
    <tr>
      <th><strong>Código</strong></th>
      <th><strong>Nombre</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>U20221C936</td>
      <td>JUAN FABRITZZIO PESCORAN ANGULO</td>
    </tr>
    <tr>
      <td>U202022387</td>
      <td>ANGELO MARCIO CURI MARCELO</td>
    </tr>
    <tr>
      <td>U202102344</td>
      <td>BRENDA LUCÍA GAMIO UPIACHIHUA</td>
    </tr>
    <tr>
      <td>U202215285</td>
      <td>ALDO ALBERTO BALDEON FABIAN</td>
    </tr>
    <tr>
      <td>U202214477</td>
      <td>DIEGO ULISES SOTO QUISPE</td>
    </tr>
  </tbody>
</table>

</div>

<p align="center"><strong>Noviembre 2025</strong></p>

# Registro de Versiones del Informe

| Versión | Fecha       | Autor(es)                                                                                                                                                                                                                   | Descripción de la modificación                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TP** | 10/10/2025  | Juan Fabritzzio Pescoran Angulo <br><br> Angelo Marcio Curi Marcelo <br><br> Brenda Lucía Gamio Upiachihua <br><br> Gustavo Esau Huanca Navarro <br><br> Diego Ulises Soto Quispe | Versión inicial **TP1** (Anti-Hacking): carátula, Registro de Versiones, **Project Report Collaboration Insights**, **Tabla de Contenidos con hipervínculos**, **Student Outcome (SO2)**; **Cap. I – Introducción** (perfil del cliente y consultora, problemática, **Rules of Engagement** firmadas y escaneadas); **Cap. II – Metodología Ágil y de Pentesting** (Scrum + PTES/OWASP/NIST 800-115, Backlog de seguridad, Plan de Sprints, DoD, herramientas: Kali, Metasploit, Burp/ZAP, Nmap, sqlmap, Wireshark); **Cap. III – Desarrollo por Sprints** (Sprint 1 completo: OSINT + Nmap/Masscan; Sprint 2 en avance: enumeración + vulnerabilidades preliminares); **PoC inicial controlada (no destructiva)**. |
| **TF** | 10/10/2025  | Juan Fabritzzio Pescoran Angulo | Ajustes del **Cap. I** (expectativas del cliente, activos en alcance) y anexado del PDF de **Rules of Engagement** firmado. |

## Project Report Collaboration Insights

TP: Las tareas se gestionaron en **GitHub** (repo público del Report en Markdown), con flujo **GitFlow** y **Conventional Commits**; tablero ágil (Trello/Jira/GitHub Projects) y reuniones semanales.  
Repositorio del proyecto: **https://github.com/G2-UPC-2520-7306-Emergentes**

- **Roles (Scrum):** Product Owner; Scrum Master; Pentesters (Web, API, Móvil, Red/Infra); Documentación/Análisis.
- **Herramientas mínimas:** Kali, Metasploit, Burp/ZAP, Nmap, sqlmap, Wireshark (opcionales: Nessus/OpenVAS, Nikto, MobSF).
- **Evidencias:** capturas de Insights por miembro y PRs; salidas de herramientas; scripts; enlace a **Rules of Engagement** firmadas.

## **TP (Resumen de avance)**

- Mejora de alcance con el cliente (dominios, subdominios, APIs, sistemas en ambiente de pruebas).
- **Sprint 1** finalizado (OSINT + reconocimiento y escaneo inicial con Nmap/Masscan).
- **Sprint 2** en curso (enumeración de servicios y vulnerabilidades preliminares con Nessus/Nikto/Burp); elaboración de **PoC inicial controlada**.
- Redacción en Markdown + control de versiones (rama `develop`, PRs por capítulo).

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
    - [Sprint 2 – Enumeración y Vulnerabilidades](#sprint-2--enumeración-y-vulnerabilidades)
    - [Sprint 3 – Explotación](#sprint-3--explotación)
    - [Sprint 4 – Post-explotación y Persistencia](#sprint-4--post-explotación-y-persistencia)
    - [Sprint 5 – Informe Final y Recomendaciones](#sprint-5--informe-final-y-recomendaciones)
- [**Capítulo IV: Resultados Consolidados**](#capítulo-iv-resultados-consolidados)
- [**Capítulo V: Recomendaciones y Plan de Mitigación**](#capítulo-v-recomendaciones-y-plan-de-mitigación)
- [**Capítulo VI: Conclusiones y Video About-the-Team**](#capítulo-vi-conclusiones-y-video-about-the-team)
- [**Bibliografía (APA 7)**](#bibliografía-apa-7)
- [**Anexos**](#anexos)

# Student Outcome 2 - ABET - EAC 

Criterio: La capacidad de funcionar efectivamente en un equipo cuyos miembros juntos
proporcionan liderazgo, crean un entorno de colaboración e inclusivo, establecen objetivos,
planifican tareas y cumplen objetivos.
En el siguiente cuadro se describe las acciones realizadas y enunciados de conclusiones por
parte del grupo, que permiten sustentar el haber alcanzado el logro del ABET – EAC - Student
Outcome 2.

| Criterio específico | Acciones realizadas | Conclusiones |
|---|---|---|
| **Diseña soluciones en ingeniería de software (productos, procesos y/o servicios) que satisfagan necesidades específicas considerando el impacto en salud pública, seguridad, bienestar, así como factores globales, culturales, sociales, ambientales y económicos.** | **TP**<br>• **JUAN FABRITZZIO PESCORAN ANGULO:** Definió alcance autorizado con la PyME (dominios/sistemas/APIs) y activos críticos; matriz de riesgos inicial.<br>• **ANGELO MARCIO CURI MARCELO:** Backlog de seguridad y DoD con criterios reproducibles; mapeo objetivos → entregables.<br>• **BRENDA LUCÍA GAMIO UPIACHIHUA:** Necesidades de negocio/usuarios y restricciones legales; lineamientos de tratamiento de datos.<br>• **ALDO ALBERTO BALDEON FABIAN:** OSINT y reconocimiento con Nmap/Masscan; consolidación de superficie de ataque inicial.<br>• **DIEGO ULISES SOTO QUISPE:** PoC controlada (no destructiva) y pautas éticas/confidencialidad.<br><br>**TF**<br>• **JUAN:** Ajuste de objetivos de mitigación con el cliente y validación de impacto en continuidad operativa.<br>• **ANGELO:** Priorización de vulnerabilidades con CVSS y definición de acciones tácticas/de negocio.<br>• **BRENDA:** Recomendaciones alineadas a políticas internas y normativa local.<br>• **ALDO:** Evidencia de mejoras en postura de seguridad tras remediaciones parciales.<br>• **DIEGO:** Integración de resultados finales, riesgos residuales y roadmap. | **TP:** El diseño del servicio de pentesting responde a riesgos reales y prioriza continuidad/confidencialidad; decisiones justificadas por el contexto económico y cultural del cliente.<br>**TF:** La solución propuesta equilibra seguridad y operatividad con un plan de mejora continua y priorización costo–beneficio. |
| **Valida que el diseño de la solución de software considere aspectos en salud pública, seguridad, bienestar, así como factores globales, culturales, sociales, ambientales y económicos.** | **TP**<br>• **JUAN:** Reglas de compromiso acordadas (sin DoS, ventanas de prueba); control de impacto en disponibilidad.<br>• **ANGELO:** Métricas de validación (evidencias, reproducibilidad, criterios de aceptación).<br>• **BRENDA:** Checklist de cumplimiento/privacidad y buenas prácticas de manejo de datos.<br>• **ALDO:** Verificación no intrusiva de hallazgos y documentación de falsos positivos.<br>• **DIEGO:** Trazabilidad y resguardo de evidencias con hashes.<br><br>**TF**<br>• **JUAN:** Validación con TI/negocio y cierre de alcance.<br>• **ANGELO:** Comparación *before/after* de métricas y riesgos residuales.<br>• **BRENDA:** Evaluación de alineamiento con políticas internas y marco legal vigente.<br>• **ALDO:** Verificación de que remediaciones no afecten procesos críticos ni UX.<br>• **DIEGO:** Lecciones aprendidas y criterios para iteraciones futuras. | **TP:** El diseño y las pruebas respetaron salud, seguridad y continuidad del servicio; trabajo colaborativo y ético.<br>**TF:** Se valida integralmente el impacto de las mejoras considerando factores técnicos y socioeconómicos; se establecen controles sostenibles y medibles. |
