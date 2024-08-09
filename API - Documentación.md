---
tags:
  - DevOps
  - Documentation
---
## ¿Qué es una API?

El término **API** (Interfaz de programación de Aplicaciones) es un conjunto de protocolos, funciones y reglas que permiten que diferentes programas de software se comuniquen entre sí.

En otras palabras, una API es un intermediario que permite que dos aplicaciones interactúen, facilitando la integración de diferentes sistemas y servicios.

- Permiten la integración de diferentes sistemas y servicios.
- Facilitan el desarrollo de aplicaciones, al permitir reutilizar funcionalidades ya existentes.

## Componentes de una API

### Endpoints

Son las URLs específicas a las que se puede hacer una solicitud. Cada endpoint realiza una función específica.

### Métodos HTTP

Los métodos HTTP indican la acción que desea se desea realizar en un recurso determinado de una API. Los métodos más comunes son los siguientes:

- **CONNECT**  
	Utilizado par abrir un túnel de comunicación entre el cliente y el servidor, generalmente usado con proxies.
    
- **HEAD**  
    Solicita solo las cabeceras que serían devueltas si la solicitud fuese realizada mediante el método  _GET_. Útil para comprobar detalles como el tamaño de un archivo sin descargarlo.

- **OPTIONS**  
    Solicita las opciones de comunicacion permitidas para un determinado recurso. Puede usarse para conocer qué métodos soporta un servidor.
    
    >**Ejemplo**
    > Para conocer los métodos soportados por un servidor, puede utilizarse `curl` de la siguiente forma:
    >```bash
    >curl -X OPTIONS https://example.org -i  
    >```
    >_La opción `-X`  o `--request` permite especificar el método de la solicitud y la opción `-i` o `--include` incluye las cabeceras en la salida estandar._
    
- **GET**
    Obtiene datos del servidor. Estas solicitudes solo deben usarse para recuperar datos y o deben modificar el estado del servidor (No incluyen datos en la petición).  
    
- **POST**
    Envía datos al servidor para crear un nuevo recurso o realizar alguna acción en este.
    _El tipo de cuerpo de la solicitud se indica con la cabecera [Content-Type](https://developer.mozilla.org/es/docs/Web/HTTP/Headers/Content-Type)._
    
- **PUT**
    Actualiza datos existentes o crea un nuevo elemento.  
    El método `PUT` es **idempotente**, lo que significa que llamarlo varias veces tiene el mismo efecto.
    >Un ejemplo es una base de datos donde múltiples `UPDATE` no cambian el resultado después de la primera ejecución. Sin embargo, un `POST` repetido como subir un recurso al servidor puede crear múltiples copias del mismo recurso.
    
- **DELETE**
	  Elimina el recurso especificado en el servidor.
	  
- **PATCH**
    Aplica modificaciones parciales a un recurso. A diferencia de `PUT` no requiere que se envíe el recurso completo.
    
- **TRACE**
    Realiza una prueba de bucle de solicitud para depurar la comunicación entre el cliente y el servidor.

### Códigos de estado HTTP

Los códigos de estado de respuesta HTTP indican si se ha completado satisfactoriamente una solicitud HTTP específica. Las respuestas se agrupan en cinco clases:

1. **Respuestas informativas (100 - 199)** : Indican que el servidor ha recibido la solicitud y está en proceso.
	- [100 - Continue](https://developer.mozilla.org/es/docs/Web/HTTP/Status/100) → Respuesta provisional que indica que todo va correctamente.
	
2. **Respuestas satisfactorias (200 - 299)** : Indican que la solicitud se ha completado exitosamente.
	- [200 - OK](https://developer.mozilla.org/es/docs/Web/HTTP/Status/200) → La solicitud ha tenido éxito. Su significado depende del método de solicitud.
	- [201 - Created](https://developer.mozilla.org/es/docs/Web/HTTP/Status/201) → La solicitud ha tenido éxito y se ha creado un nuevo recurso. Respuesta típica de petición `PUT`.
	- [202 - Accepted](https://developer.mozilla.org/es/docs/Web/HTTP/Status/202) → La solicitud se ha recibido, pero aún no se ha actuado.
	- [203 - Non-Authoritative Information](https://developer.mozilla.org/es/docs/Web/HTTP/Status/203) → La petición se ha completado pero su contenido no se ha obtenido de la fuente originalmente solicitada.
	- [204 - No Content](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204) → La petición se ha completado con éxito pero su respuesta no tiene ningún contenido.
	- [206 - Partial Content](https://developer.mozilla.org/es/docs/Web/HTTP/Status/206) → La petición ha devuelto el contenido de forma parcial.
	>[!INFO]
	>La respuesta **206 - Partial Content** es utilizada por herramientas de descarga como `wget` para continuar una transferencia o descarga si esta ha sido anterioremente interrumpida.
	
3. **Redirecciones (300 - 399)** : Indican que se neceista realizar una acción adicional para completar la solicitud.
	
4. **Errores del clientes (400 - 499)** : Indican que la solicitud contiene un error o no puede ser procesada.
	- [400 - Bad Request](https://developer.mozilla.org/es/docs/Web/HTTP/Status/400) → El servidor no ha podido interpretar la solicitud por una sintaxis inválida.
	- [401 - Unauthorized](https://developer.mozilla.org/es/docs/Web/HTTP/Status/401) → Es necesario autenticación para obtener la solicitud.
	- [403 - Forbidden](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403) → El cliente no posee los permisos necesarios.
	- [404 - Not Found](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404) → Recurso no encontrado.
	- [405 - Method Not Allowed](https://developer.mozilla.org/es/docs/Web/HTTP/Status/405) → Método solicitado ha sido deshabilitado. No puede ser utilizado.
1. **Errores del servidor (500 - 599)** : Indican que el servidor ha encontrado un error mientras procesaba la solicitud.
	- [500 - Internal Server Error](https://developer.mozilla.org/es/docs/Web/HTTP/Status/500)→ Error en el servidor.
	  
### Anatomía de una API Request
Una solicitud a una API (API Request) se compone de varios elementos clave:
1. **URL (Uniform Resource Locator)** : Dirección del endpoint donde se realizará la solicitud.
2. **Método HTTP** : Define la acción que se desea realizar (GET, POST, PUT, etc.).
3. **Headers** : Información adicional enviada al servidor, como el tipo de contenido (Content-Type), tokens de autenticación, etc.
4. **Body** : Contenido enviado en la solicitud, generalmente en solicitudes POST, PUT o PATCH. Puede ser en formato JSON, XML, etc.
5. **Params** : Datos enviados como parte de la URL, que pueden ser opcionales o requeridos.

```bash
POST /users HTTP/1.1
Host: api.ejemplo.com
Content-Type: application/json
Autorization: Bearer access_token
```

## Ver peticiones de APIs en el navegador

Mediante las herramientas de desarrollador de un navegador pueden verse las peticiones de APIs que realiza una determinada página web.

1. Abrir herramientas de desarrollador → `F12` o `Ctrl+Shift+I`.
2. Ir a la pestaña de **red** (Network).
3. Filtrar por **XHR** o **Fetch**.
4. Aquí hay detalles como _URL_, método HTTP, encabezados, cuerpo o respuesta.

## CURL [[cURL]]

## API Rest
Existen distintos tipos de APIs, entre ellas se encuentran las API Rest (Representational State Transfer) las cuales ==son un tipo específico de API que permite la comunicación entre sistemas a través de HTTP==. Sigue una serie de principios y restricciones que son los siguientes:
1. **Cliente-Servidor** : Basada en arquitectura ==cliente-servidor==.
2. **Sin estado (Stateless)** : Cada solicitud debe contener la información necesaria para entender y procesar la solicitud. ==El servidor no guarda ningún estado de la sesión== del cliente (no recuerda las solicitudes anteriores).
3. **Cacheable** : Las respuestas pueden ser marcadas como cacheables. 
   >[!INFO]
   >Si el mismo u otro cliente vuelve a solicitar un recurso ya solicitado, el servidor, el cual que incluye un encabezado en la respuesta `Cache-Control: max-age=86400` (La respuesta se almacena 24h), utiliza la versión cacheada, reduciendo la carga en el servidor y mejorando la velocidad.
4. **Interfaz uniforme** : REST utiliza un conjunto limitado y predefinido de operaciones (`GET`, `POST`, `PUT` y `DELETE`)