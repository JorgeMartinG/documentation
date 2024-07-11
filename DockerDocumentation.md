## ¿Qué es Docker?
Docker es una herramienta para crear, desplegar y ejecutar aplicaciones mediante contenedores.
Los contenedores permiten empaquetar una aplicación con todas las partes que necesita. 
Están aislados entre sí y cada uno contiene su propio software, bibliotecas y archivos de configuración.

## Características de Docker
* Contienen únicamente **binarios, bibliotecas y archivos de configuración** junto con la aplicación en sí.
* No contienen un sistema operativo como tal sino que **hacen uso del núcleo del sistema anfitrión**.
* **Comparten recursos con otros contenedores** y proporcionan **aislamiento de procesos** a nivel de sistema.

## Conceptos Básicos
### Imagen Docker
Una plantilla inmutable que define el contenido y configuración de un contenedor. Las imágenes se construyen a partir de un archivo _Dockerfile_.
### Contenedor Docker
Una instancia ejecutable de una imagen. Son entornos aislados que conienen todo lo necesario para ejecutar una aplicación.
### Dockerfile
Es un archivo de texto con instrucciones para construir una imagen Docker.
Aquí se define como se configurará el contenedor y que software incluirá.
### Docker Engine
Es el motor que ejecuta y gestiona los contenedores Docker.
    1) **Servidor**: Responsable de crear y gestionar imágenes Docker, contenedores, redes y volúmenes en Docker. Se le conoce como proceso demonio.
    2) **REST API**: Especifica como la aplicación puede interactuar con el servidor y que instucciones ejecutará.
    3) **Cliente**: La interfaz de línea de comandos (CLI), que permite interactuar con Docker.
### Docker Hub
Un repositorio de imágenes para contenedores. Es el repositorio por defecto de la plataforma Docker Engine. Pueden encontrarse imágenes oficiales o de proveedores externos.
