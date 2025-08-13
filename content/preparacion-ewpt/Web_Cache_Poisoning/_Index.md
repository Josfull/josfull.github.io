---
title: " Hacking Web Socket"
description: "agrega una descripcion basado en la informacion de la nota."
showBreadcrumbs: true
showTableOfContents: false
---

# da una breve explicacion de la vulnerabilidad

En este laboratorio se analiza una vulnerabilidad de Web Cache Poisoning provocada por el uso inseguro de una cabecera HTTP que no es tenida en cuenta como parte de la clave de caché (unkeyed header). Esto permite a un atacante modificar el contenido que será servido a futuros usuarios desde la caché del servidor.

La aplicación utiliza la cabecera ‘**X-Forwarded-Host’** para generar URLs absolutas de recursos JavaScript. Al modificar esta cabecera, es posible hacer que el navegador del usuario intente cargar un script desde un dominio arbitrario, como el exploit server.

Al comprobar que la respuesta modificada se almacena en caché (gracias a la cabecera ‘**X-Cache: hit**‘), se confirma que es posible envenenar la caché con contenido controlado por el atacante. Esta técnica establece la base del ataque y demuestra una lógica defectuosa en la gestión de cabeceras en el backend.