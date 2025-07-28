---
title: "Checklist personal OTG"
description: "Checklist práctica y personal basada en OWASP Testing Guide, adaptada a entornos reales de auditoría web. Ítems editables según proyecto y contexto."
date: 2025-07-27
showBreadcrumbs: true
showTableOfContents: true
---

## Checklist personal OTG

Esta checklist está basada en la OWASP Testing Guide (OTG) y adaptada a los escenarios reales que enfrento como pentester web.  
Marca, adapta o expande cada ítem según el contexto y alcance de tu auditoría.

| ID OTG           | Título oficial (inglés)                                                | Título español propuesto                                         | Hallazgo |
| ---------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------- | -------- |
| OTG-INFO-001     | Conduct Search Engine Discovery Reconnaissance for Information Leakage | Reconocimiento con buscadores (búsqueda de fugas de información) |          |
| OTG-INFO-002     | Fingerprint Web Server                                                 | Huella digital del servidor web                                  |          |
| OTG-INFO-003     | Review Webserver Metafiles for Information Leakage                     | Revisar metarchivos del servidor en busca de fugas de info       |          |
| OTG-INFO-004     | Enumerate Applications on Webserver                                    | Enumerar aplicaciones en el servidor web                         |          |
| OTG-INFO-005     | Review Webpage Content for Information Leakage                         | Revisar contenido de páginas por fugas de información            |          |
| OTG-INFO-006     | Identify Application Entry Points                                      | Identificar puntos de entrada de la aplicación                   |          |
| OTG-INFO-007     | Map Execution Paths Through Application                                | Trazar rutas de ejecución en la aplicación                       |          |
| OTG-INFO-008     | Fingerprint Web Application Framework                                  | Huella del framework de la aplicación web                        |          |
| OTG-INFO-009     | Fingerprint Web Application                                            | Huella de la aplicación web                                      |          |
| OTG-INFO-010     | Map Application Architecture                                           | Mapear la arquitectura de la aplicación                          |          |
| OTG-CONFIG-001   | Test Network Infrastructure Configuration                              | Probar configuración de infraestructura de red                   |          |
| OTG-CONFIG-002   | Test Application Platform Configuration                                | Probar configuración de la plataforma de aplicación              |          |
| OTG-CONFIG-003   | Test File Extensions Handling for Sensitive Information                | Probar manejo de extensiones de archivo sensibles                |          |
| OTG-CONFIG-004   | Review Old Backup and Unreferenced Files for Sensitive Information     | Revisar copias y archivos sin referencia                         |          |
| OTG-CONFIG-005   | Enumerate Infrastructure and Application Admin Interfaces              | Enumerar interfaces administrativas                              |          |
| OTG-CONFIG-006   | Test HTTP Methods                                                      | Probar métodos HTTP                                              |          |
| OTG-CONFIG-007   | Test HTTP Strict Transport Security                                    | Probar HSTS                                                      |          |
| OTG-CONFIG-008   | Test RIA Cross Domain Policy                                           | Probar política cross-domain (RIA)                               |          |
| OTG-CONFIG-009   | Test File Permission                                                   | Probar permisos de archivos                                      |          |
| OTG-CONFIG-010   | Test for Subdomain Takeover                                            | Probar toma de subdominios                                       |          |
| OTG-CONFIG-010   | Test Cloud Storage                                                     | Probar almacenamiento en la nube                                 |          |
| OTG-CONFIG-012   | Test for Content Security Policy                                       | Probar política CSP                                              |          |
| OTG-CONFIG-013   | Test for Path Confusion                                                | Probar confusión de rutas                                        |          |
| OTG-CONFIG-014   | Test for Other HTTP Security Header Misconfigurations                  | Probar otras cabeceras HTTP de seguridad                         |          |
| OTG-IDENT-001    | Test Role Definitions                                                  | Probar definición de roles                                       |          |
| OTG-IDENT-002    | Test User Registration Process                                         | Probar registro de usuarios                                      |          |
| OTG-IDENT-003    | Test Account Provisioning Process                                      | Probar aprovisionamiento de cuentas                              |          |
| OTG-IDENT-004    | Testing for Account Enumeration and Guessable User Account             | Probar enumeración de cuentas y usuarios predecibles             |          |
| OTG-IDENT-005    | Testing for Weak or Unenforced Username Policy                         | Probar políticas débiles de nombres de usuario                   |          |
| OTG-AUTHN-001    | Testing for Credentials Transported over an Encrypted Channel          | Verificar transporte cifrado de credenciales                     |          |
| OTG-AUTHN-002    | Testing for Default Credentials                                        | Probar credenciales por defecto                                  |          |
| OTG-AUTHN-003    | Testing for Weak Lock Out Mechanism                                    | Probar mecanismos de bloqueo débiles                             |          |
| OTG-AUTHN-004    | Testing for Bypassing Authentication Schema                            | Probar bypass de autenticación                                   |          |
| OTG-AUTHN-005    | Testing for Vulnerable Remember Password                               | Probar “recordar contraseña” vulnerable                          |          |
| OTG-AUTHN-006    | Testing for Browser Cache Weaknesses                                   | Probar debilidades de caché del navegador                        |          |
| OTG-AUTHN-007    | Testing for Weak Password Policy                                       | Probar políticas de contraseña débiles                           |          |
| OTG-AUTHN-008    | Testing for Weak Security Question Answer                              | Probar preguntas de seguridad débiles                            |          |
| OTG-AUTHN-009    | Testing for Weak Password Change or Reset Functionalities              | Probar cambio/restablecimiento de contraseña débil               |          |
| OTG-AUTHN-010    | Testing for Weaker Authentication in Alternative Channel               | Probar canal alternativo de autenticación más débil              |          |
| OTG-AUTHN-011    | Testing Multi-Factor Authentication                                    | Probar autenticación multifactor                                 |          |
| OTG-AUTHZ-001    | Testing Directory Traversal File Include                               | Probar LFI/Traversal                                             |          |
| OTG-AUTHZ-002    | Testing for Bypassing Authorization Schema                             | Probar bypass de autorización                                    |          |
| OTG-AUTHZ-003    | Testing for Privilege Escalation                                       | Probar escalada de privilegios                                   |          |
| OTG-AUTHZ-004    | Testing for Insecure Direct Object References                          | Probar IDOR                                                      |          |
| OTG-AUTHZ-005    | Testing for OAuth Weaknesses                                           | Probar debilidades OAuth                                         |          |
| OTG-AUTHZ-006    | Testing for OAuth Authorization Server Weaknesses                      | Probar servidor de autorización OAuth                            |          |
| OTG-AUTHZ-007    | Testing for OAuth Client Weaknesses                                    | Probar cliente OAuth                                             |          |
| OTG-SESS-001     | Testing for Session Management Schema                                  | Probar esquema de gestión de sesión                              |          |
| OTG-SESS-002     | Testing for Cookies Attributes                                         | Probar atributos de cookies                                      |          |
| OTG-SESS-003     | Testing for Session Fixation                                           | Probar fijación de sesión                                        |          |
| OTG-SESS-004     | Testing for Exposed Session Variables                                  | Probar variables de sesión expuestas                             |          |
| OTG-SESS-005     | Testing for Cross Site Request Forgery                                 | Probar CSRF                                                      |          |
| OTG-SESS-006     | Testing for Logout Functionality                                       | Probar funcionalidad de cierre de sesión                         |          |
| OTG-SESS-007     | Testing Session Timeout                                                | Probar expiración de sesión                                      |          |
| OTG-SESS-008     | Testing for Session Puzzling                                           | Probar “session puzzling”                                        |          |
| OTG-SESS-009     | Testing for Session Hijacking                                          | Probar secuestro de sesión                                       |          |
| OTG-SESS-010     | Testing JSON Web Tokens                                                | Probar JSON Web Tokens                                           |          |
| OTG-SESS-011     | Testing for Concurrent Sessions                                        | Probar sesiones concurrentes                                     |          |
| OTG-INPVAL-001   | Testing for Reflected Cross Site Scripting                             | XSS reflejado                                                    |          |
| OTG-INPVAL-002   | Testing for Stored Cross Site Scripting                                | XSS almacenado                                                   |          |
| OTG-INPVAL-003   | Testing for HTTP Verb Tampering                                        | Manipulación de verbo HTTP                                       |          |
| OTG-INPVAL-004   | Testing for HTTP Parameter Pollution                                   | Contaminación de parámetros HTTP                                 |          |
| OTG-INPVAL-005   | Testing for SQL Injection                                              | Inyección SQL                                                    |          |
| OTG-INPVAL-017   | Testing for Oracle                                                     | Pruebas en Oracle                                                |          |
| OTG-INPVAL-018   | Testing for MySQL                                                      | Pruebas en MySQL                                                 |          |
| OTG-INPVAL-019   | Testing for SQL Server                                                 | Pruebas en SQL Server                                            |          |
| OTG-INPVAL-020   | Testing PostgreSQL                                                     | Pruebas en PostgreSQL                                            |          |
| OTG-INPVAL-021   | Testing for MS Access                                                  | Pruebas en MS Access                                             |          |
| OTG-INPVAL-022   | Testing for NoSQL Injection                                            | Inyección NoSQL                                                  |          |
| OTG-INPVAL-007   | Testing for ORM Injection                                              | Inyección ORM                                                    |          |
| OTG-INPVAL-023   | Testing for Client-side                                                | Inyección SQL en cliente                                         |          |
| OTG-INPVAL-006   | Testing for LDAP Injection                                             | Inyección LDAP                                                   |          |
| OTG-INPVAL-008   | Testing for XML Injection                                              | Inyección XML                                                    |          |
| OTG-INPVAL-009   | Testing for SSI Injection                                              | Inyección SSI                                                    |          |
| OTG-INPVAL-010   | Testing for XPath Injection                                            | Inyección XPath                                                  |          |
| OTG-INPVAL-011   | Testing for IMAP SMTP Injection                                        | Inyección IMAP/SMTP                                              |          |
| OTG-INPVAL-012   | Testing for Code Injection                                             | Inyección de código                                              |          |
| OTG-AUTHZ-001    | Testing for Local File Inclusion                                       | Inclusión de archivo local                                       |          |
| OTG-AUTHZ-008    | Testing for Remote File Inclusion                                      | Inclusión de archivo remoto                                      |          |
| OTG-INPVAL-013   | Testing for Command Injection                                          | Inyección de comandos                                            |          |
| OTG-INPVAL-014   | Testing for Format String Injection                                    | Inyección de formato                                             |          |
| OTG-INPVAL-015   | Testing for Incubated Vulnerability                                    | Vulnerabilidad incubada                                          |          |
| OTG-INPVAL-016   | Testing for HTTP Splitting Smuggling                                   | HTTP splitting/smuggling                                         |          |
| OTG-INPVAL-024   | Testing for HTTP Incoming Requests                                     | Pruebas de peticiones HTTP entrantes                             |          |
| OTG-INPVAL-025   | Testing for Host Header Injection                                      | Inyección Host Header                                            |          |
| OTG-INPVAL-026   | Testing for Server-side Template Injection                             | Inyección de plantillas del lado servidor                        |          |
| OTG-INPVAL-027   | Testing for Server-Side Request Forgery                                | SSRF                                                             |          |
| OTG-INPVAL-028   | Testing for Mass Assignment                                            | Asignación masiva                                                |          |
| OTG-ERR-001      | Testing for Improper Error Handling                                    | Manejo incorrecto de errores                                     |          |
| OTG-ERR-002      | Testing for Stack Traces                                               | Trazas de pila expuestas                                         |          |
| OTG-CRYPST-001   | Testing for Weak Transport Layer Security                              | TLS débil                                                        |          |
| OTG-CRYPST-002   | Testing for Padding Oracle                                             | Padding Oracle                                                   |          |
| OTG-CRYPST-003   | Testing for Sensitive Information Sent via Unencrypted Channels        | Info sensible por canales sin cifrar                             |          |
| OTG-CRYPST-004   | Testing for Weak Encryption                                            | Cifrado débil                                                    |          |
| OTG-BUSLOGIC-001 | Test Business Logic Data Validation                                    | Validación de datos de negocio                                   |          |
| OTG-BUSLOGIC-002 | Test Ability to Forge Requests                                         | Capacidad de forjar peticiones                                   |          |
| OTG-BUSLOGIC-003 | Test Integrity Checks                                                  | Comprobaciones de integridad                                     |          |
| OTG-BUSLOGIC-004 | Test for Process Timing                                                | Tiempos de proceso                                               |          |
| OTG-BUSLOGIC-005 | Test Number of Times a Function Can Be Used Limits                     | Límites de uso de funciones                                      |          |
| OTG-BUSLOGIC-006 | Testing for the Circumvention of Work Flows                            | Eludir flujos de trabajo                                         |          |
| OTG-BUSLOGIC-007 | Test Defenses Against Application Misuse                               | Defensas contra uso indebido                                     |          |
| OTG-BUSLOGIC-008 | Test Upload of Unexpected File Types                                   | Subida de tipos de archivo inesperados                           |          |
| OTG-BUSLOGIC-009 | Test Upload of Malicious Files                                         | Subida de archivos maliciosos                                    |          |
| OTG-BUSLOGIC-010 | Test Payment Functionality                                             | Probar funcionalidad de pagos                                    |          |
| OTG-CLIENT-001   | Testing for DOM-Based Cross Site Scripting                             | XSS basado en DOM                                                |          |
| OTG-CLIENT-013   | Testing for Self DOM Based Cross-Site Scripting                        | XSS DOM auto-infligido                                           |          |
| OTG-CLIENT-002   | Testing for JavaScript Execution                                       | Ejecución de JavaScript                                          |          |
| OTG-CLIENT-003   | Testing for HTML Injection                                             | Inyección HTML                                                   |          |
| OTG-CLIENT-004   | Testing for Client-side URL Redirect                                   | Redirección URL en cliente                                       |          |
| OTG-CLIENT-005   | Testing for CSS Injection                                              | Inyección CSS                                                    |          |
| OTG-CLIENT-006   | Testing for Client-side Resource Manipulation                          | Manipulación de recursos en cliente                              |          |
| OTG-CLIENT-007   | Testing Cross Origin Resource Sharing                                  | Probar CORS                                                      |          |
| OTG-CLIENT-008   | Testing for Cross Site Flashing                                        | Cross-Site Flashing                                              |          |
| OTG-CLIENT-009   | Testing for Clickjacking                                               | Clickjacking                                                     |          |
| OTG-CLIENT-010   | Testing WebSockets                                                     | Probar WebSockets                                                |          |
| OTG-CLIENT-011   | Testing Web Messaging                                                  | Probar Web Messaging                                             |          |
| OTG-CLIENT-012   | Testing Browser Storage                                                | Probar almacenamiento del navegador                              |          |
| OTG-CLIENT-014   | Testing for Cross Site Script Inclusion                                | Inclusión de scripts cruzados                                    |          |
| OTG-CLIENT-015   | Testing for Reverse Tabnabbing                                         | Reverse Tabnabbing                                               |          |
| OTG-API-001      | API Reconnaissance                                                     | Reconocimiento de API                                            |          |
| OTG-API-002      | API Broken Object Level Authorization                                  | Autorización rota a nivel de objeto API                          |          |
| OTG-API-003      | Testing GraphQL                                                        | Probar GraphQL                                                   |          |

---

### 1. Reconocimiento y mapeo

- Identificación de subdominios y hosts relacionados
- Detección de tecnologías, frameworks y lenguajes backend/frontend
- Enumeración de endpoints, rutas y recursos ocultos
- Identificación de puntos de entrada para usuarios y datos

---

### 2. Revisión de configuración

- Análisis de cabeceras HTTP relevantes (CSP, HSTS, CORS, etc.)
- Revisión de cookies: flags, scope y atributos de seguridad
- Evaluación de configuración de servidores web, proxies y load balancers
- Revisión de mensajes de error y banners expuestos

---

### 3. Testing de autenticación y sesiones

- Verificación de mecanismos de login (2FA, lockout, enumeración de usuarios)
- Pruebas de fuerza bruta y control de intentos
- Validación de gestión de sesiones (expiración, regeneración, tokens)
- Revisión de recuperación de contraseñas y flujos de registro

---

### 4. Testing de autorización y control de acceso

- Pruebas de acceso horizontal y vertical (privilegios, roles)
- Bypass de controles en endpoints sensibles
- Manipulación de parámetros de referencia (IDs, objetos, tokens)
- Revisión de endpoints administrativos y recursos restringidos

---

### 5. Testing de entrada y validaciones

- Pruebas de inyección (SQLi, XSS, XXE, SSTI, etc.)
- Validación del input en cliente y servidor
- Manipulación de payloads, encoding y sanitización
- Comprobación de gestión de archivos, uploads y descargas

---

### 6. Testing de lógica de negocio y flujo de aplicación

- Pruebas de procesos críticos (pagos, transferencias, workflows internos)
- Identificación de race conditions y condiciones de carrera
- Comprobación de lógica insuficiente o saltos de paso
- Testing de manipulación de lógica de negocio (precios, descuentos, cantidades)

---

### 7. Testing de otros vectores

- Revisión de exposición de información sensible (logs, backups, .git, etc.)
- Evaluación de uso y configuración de cifrado (TLS, almacenamiento)
- Testing de APIs y endpoints externos/integraciones
- Revisión de configuraciones de seguridad adicionales (WAF, CSP, MFA, etc.)

---

> *Josfull — Creador, escritor y pentester detrás de cada línea de este sitio.*