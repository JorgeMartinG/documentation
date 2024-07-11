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

## Instalación en Linux (Debian)
> [!WARNING]
> Para instalar **Docker Engine** es necesaria la versión 64-bit de una de estas versiones de Debian:
> + Debian Bookworm 12 (_stable_)
> + Debian Bullseye 11 (_oldstable_)
### Métodos de instalación
Docker puede ser instalado de distintas maneras en base a las necesidades del usuario:
#### 1) Utilizar **Docker Engine** incluido en <a href="https://desktop.docker.com/linux/main/amd64/157355/docker-desktop-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64">Docker Desktop for Linux.</a>
> [!NOTE]
> **Docker Desktop for Linux** es un IDE que simplifica la gestión de contenedores y servicios. Incluye _Docker Engine_, _Docker CLI Client_, _Docker Compose_...
#### 2) Instalar **Docker Engine** mediante los <a href="https://docs.docker.com/engine/install/debian/#install-using-the-repository">repositorios</a> de `apt`.

#### 3) Instalar de forma manual.
Si se instala manualmente, las actualizaciones también se tendrán que gestionar de este modo.

+  Visitar la página <a href="https://download.docker.com/linux/debian/dists/.">`https://download.docker.com/linux/debian/dists/`</a>

+ Seleccionar la versión de Debian de la lista.

+ Dirigirse a _`/pool/stable/`_ y seleccionar la arquitectura correcta (`amd64`, `armhf`, `arm64` o `s390x`).

+ Descargar los paquetes _.deb_ → `containerd.io`, `docker-ce`, `docker-ce-cli`, `docker-buildx-plugin` y `docker-compose-plugin` con su correspondiente versión y arquitectura.

+ Instalar los paquetes descargados:
```sh
sudo dpkg -i ./docker-*.deb ./containerd-*.deb
```
#### 4) Utilizar un script de instalación. <ins>Recomendado únicamente para entornos de desarrollo.</ins>
Docker proporciona un **<a href="https://get.docker.com/">script</a>** para instalar Docker en entornos de desarrollo de forma no interactiva.
```sh
curl -fsSL https://get.docker.com -o get-docker.sh # Script de instalación.
sudo sh ./get-docker.sh # Con --dry-run revisar los pasos ejecutará el script.
```
Verificar que la instalación de **Docker Engine** es exitosa ejecutando la imagen `hello-world`:
```sh
sudo service docker start
sudo docker run hello-world
```
_Este comando descarga una imagen de prueba y la ejecuta en un contenedor. Al ejecutarse, muestra un mensaje de confirmación y se cierra._

### Desinstalación de Docker Engine
1) Desinstalar los paquetes _Docker Engine, CLI, containerd y Docker Compose:_
```bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```