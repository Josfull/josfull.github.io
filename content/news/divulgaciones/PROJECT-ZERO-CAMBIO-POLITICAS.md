---
title: "🛡️ Google Project Zero anuncia nueva política de transparencia en divulgación de vulnerabilidades"
description: "El equipo **Project Zero de Google** ha anunciado un cambio importante en su política de divulgación de fallas de seguridad."
showBreadcrumbs: true
showTableOfContents: false
---


#### El equipo **Project Zero de Google** ha anunciado un cambio importante en su política de divulgación de fallas de seguridad. Tim Willis publicó la entrada _“Policy and Disclosure: 2025 Edition”_ donde presenta la iniciativa experimental **Transparencia en los Reportes**.

> 📌 **Objetivo**: Acelerar la corrección de vulnerabilidades y reducir la brecha entre la creación del parche y su llegada al dispositivo del usuario final.

---

## 📉 Antecedentes: La “brecha de parches” y el desafío actual

Desde 2021, Project Zero adoptó el modelo **“90+30”**:
- _90 días_: para que el proveedor desarrolle el parche.
- _30 días adicionales_: para facilitar su adopción por los usuarios.

Pese a esto, persiste una demora crítica: la **“patch gap”**, es decir, el tiempo real entre que se publica un parche y el usuario lo instala.

A esto se suma una brecha anterior:
- 🔁 **Patch gap upstream**: cuando el proveedor principal tiene la corrección lista, pero los distribuidores aún no la integran.
- Esto prolonga el ciclo de vida de las vulnerabilidades, especialmente en componentes fundamentales como chipsets y drivers.

---

## 🧪 Nueva política experimental: “Transparencia en los Reportes”

A partir de ahora:
- **1 semana después** de reportar una vulnerabilidad, Project Zero publicará su existencia.
- Sin incluir detalles técnicos ni PoC.
- Se comunicarán únicamente:
  - 🔹 Proyecto o empresa notificada.
  - 🔹 Producto afectado.
  - 🔹 Fecha del reporte y plazo de 90 días para divulgación completa.

📅 La política original de **90+30 días** se mantiene intacta.  
🧠 Incluso el proyecto colaborativo **Google Big Sleep** aplicará este protocolo de transparencia temprana.

---

## 🕵️ ¿Por qué este cambio? Más transparencia para acortar la brecha

> “Acortar la brecha upstream mediante una mayor transparencia” — *Tim Willis*

La idea es que los actores **downstream** reciban señales tempranas sobre fallos reportados upstream y puedan:
- Preparar sus parches con anticipación.
- Coordinar mejoras con proveedores principales.
- Mejorar la adopción de actualizaciones por parte de los usuarios.

Además, se busca **rastrear los tiempos reales** desde el reporte hasta la corrección efectiva en el dispositivo.

---

## 🔐 ¿Transparencia vs ventaja para atacantes?

Una inquietud razonable:  
¿Publicar que existe una vulnerabilidad antes de tener un parche da ventajas a atacantes?

✋ Según Project Zero: **No.**  
La divulgación inicial no incluye nada que permita la explotación:
- ❌ Sin detalles técnicos.
- ❌ Sin código.
- ✅ Solo una alerta de existencia, sin vectores de ataque revelados.

Algunos proveedores sin ecosistema downstream podrían ver esto como “ruido innecesario”, pero **representan una minoría**. La mayoría utiliza componentes compartidos, y ahí la transparencia sí marca la diferencia.

---

## ✅ Conclusión

La nueva política de **Transparencia en los Reportes** busca acelerar todo el ciclo de seguridad:
- 🚀 Reducción de tiempos entre hallazgo, parche y adopción.
- 🧩 Mejor coordinación entre proveedores.
- 🔎 Más visibilidad para la comunidad sobre qué parches llegan —y cuáles no— a los usuarios.

> La existencia de vulnerabilidades **no debe causar pánico**, sino facilitar respuestas más rápidas y ecosistemas más seguros.

📊 Project Zero evaluará el impacto de esta medida experimental durante 2025 y ajustará su enfoque según los resultados.

---

**🌐 Fuente oficial**: [Google Project Zero Blog](https://googleprojectzero.blogspot.com)
