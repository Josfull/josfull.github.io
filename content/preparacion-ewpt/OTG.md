---
title: "Metodología OTG (OWASP Testing Guide)"
description: "Explicación técnica y práctica de la Metodología OWASP OTG, utilizada en mis auditorías web y formación continua. Aprende cómo aplico cada fase en pentesting profesional."
showBreadcrumbs: true
showTableOfContents: true
---

## ¿Qué es la Metodología OTG?

La **OWASP Testing Guide** (OTG) es el estándar más reconocido y práctico para auditorías de seguridad en aplicaciones web.  
Su enfoque sistemático y su cobertura exhaustiva la convierten en mi referencia principal para análisis, documentación y formación en pentesting web.

---

### ¿Por qué uso OTG?

Como pentester web y creador de contenido técnico, aplico la OTG porque:

- **Asegura cobertura total:** Nada se pasa por alto; cada área del sistema es evaluada de forma metódica.
- **Facilita reporting profesional:** El reporte se estructura siguiendo las mismas fases y controles, facilitando la comprensión para el cliente.
- **Establece mejores prácticas:** Permite justificar y documentar procedimientos ante cualquier auditoría externa.
- **Es actualizable y mantenida por la comunidad:** Siempre alineada a los nuevos riesgos y tecnologías.

---

### Fases y controles principales

La OTG divide el proceso de pentesting web en **fases y controles específicos**. Estas son las principales:

1. **Reconocimiento y mapeo**  
   - Identificación de objetivos, subdominios, tecnologías, endpoints y vectores de ataque potenciales.

2. **Revisión de configuración**  
   - Evaluación de cabeceras HTTP, gestión de cookies, tecnologías expuestas, configuración de servidores y frameworks.

3. **Testing de autenticación y sesiones**  
   - Análisis de controles de login, políticas de contraseñas, gestión de tokens, logout, persistencia y seguridad de sesión.

4. **Testing de autorización y controles de acceso**  
   - Validación de permisos, segregación de roles, acceso horizontal y vertical, endpoints protegidos y bypasses comunes.

5. **Testing de entrada y validaciones**  
   - Pruebas de inyección (SQLi, XSS, XXE, SSTI, etc.), validación en cliente y servidor, encoding y sanitización.

6. **Testing de lógica de negocio y flujo de aplicación**  
   - Detección de fallos en procesos, race conditions, manipulación de parámetros, vulnerabilidades no técnicas.

7. **Testing de otros vectores**  
   - Exposición de información sensible, falta de cifrado, configuración de APIs, integraciones externas, etc.

---

### ¿Cómo la aplico en mi trabajo?

- **Checklist personalizada:** Utilizo la OTG como base para crear listas de verificación adaptadas a cada cliente y proyecto.
- **Documentación y evidencia:** Cada hallazgo es referenciado a su control OTG correspondiente para máxima claridad y trazabilidad.
- **Formación continua:** Mis labs, artículos y series “0 a 100” están alineados a la estructura OTG, facilitando el aprendizaje a quienes siguen el sitio.
- **Optimización del tiempo:** Automatizo pruebas repetitivas pero mantengo el análisis manual en áreas críticas.

---

### Recursos recomendados

- [OTG-CHECKLIST](/preparacion-ewpt/otg-checklist/)
  *(Adaptada y optimizada a partir de mi experiencia en auditorías reales y labs, actualizada constantemente a medida que evolucionan las técnicas y controles)*

- [Guía Oficial OTG (OWASP)](https://github.com/OWASP/wstg/releases/download/v4.2/wstg-v4.2.pdf)


---

> **En resumen:**  
La Metodología OTG es el hilo conductor de mis auditorías y contenido. Permite abordar el pentesting de forma profesional, documentada y reproducible.

---

> *Josfull — Creador, escritor y pentester detrás de cada línea de este sitio.*