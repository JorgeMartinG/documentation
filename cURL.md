`curl` -> Es una herramienta muy potente de línea de comandos, utilizada para transferir datos desde o hacia un servidor, utilizando diversos protocolos como HTTP, HTTPS, FTP, entre otros.

**Opciones más relevantes**:

- `-X`, `--request <method>`: Especifica el método HTTP a utlizar (GET, POST, PUT, DELETE, etc.)
- `-d`, `--data <data>`: Envía datos en una solicitud POST.
- `-H`, `--header <header>`: Permite añadir un encabezado personalizado a la solicitud.
- `-o`, `--output <file>`: Guarda el contenido de la respuesta en un archivo.
- `-L`, `--location`: Sigue las redirecciones HTTP automáticamente.
- `-u`, `--user <user:password>`: Especifica el nombre de usuario y contraseña para autenticación.
- `-v`, `--verbose`: Muestra detalles adicionales de la operación, útil para la depuración.
- `-i`, `--include`: Incluye los encabezados HTTP en la salida.
- `-s`, `--silent`: Modo silencioso; no muestra el progreso ni los mensajes de error.
- `-k`, `--insecure`: Permite conexiones a servidores con certificados SSL no verificados.
- `-b`, `--cookie <data|filename>`: Envía cookies desde un archivo o cadena.
- `-c`, `--cookie-jar <filename>`: Fuarda las cookies en un archivo después de la operación.
- `-I`, `--head`: Muestra solo la información del encabezado del documento.
- `-T`, `--upload-file <file>`: Sube un archivo al servidor.
- `-G`, `--get`: Convierte datos POST en parámetros de URL y usa el método GET.
- `-C`, `--continue-at <offset>`: Continúa una descarga en el punto donde se interrumpió.
- `--compressed`: Solicita una respuesta comprimida del servidor.
- `--retry <num>`: Reintenta la solicitud un número de veces.
- `--max-time <seconds>`: Tiempo máximo permitido para la transferencia.
- `--rate <max-request-rate>`: Limita la tasa de transferencia.
- `--interface <name>`: Utiliza una interfaz de red específica para la solicitud.

Para mas información de todas las posibilidades que ofrece:
```python
curl --help all
```

# Encabezado 1
## Encabezad 2
### Encabezado 3
|dato|valor|
|---|---|
|1|hola|
|2|adios|

