## Instalación en Linux (Debian)
> [!WARNING]
> Para instalar **Docker Engine** es necesaria la versión 64-bit de una de estas versiones de Debian:
> + Debian Bookworm 12 (_stable_)
> + Debian Bullseye 11 (_oldstable_)
### Métodos de instalación
Docker puede ser instalado de distintas maneras en base a las necesidades del usuario:
#### 1. Utilizar Docker Engine incluido en <a href="https://desktop.docker.com/linux/main/amd64/157355/docker-desktop-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64">Docker Desktop for Linux.</a>

> [!NOTE]
> **Docker Desktop for Linux** es un IDE que simplifica la gestión de contenedores y servicios. Incluye _Docker Engine_, _Docker CLI Client_, _Docker Compose_...

#### 2. Instalar Docker Engine mediante los <a href="https://docs.docker.com/engine/install/debian/#install-using-the-repository">repositorios</a> de `apt`.

#### 3. Instalar y gestionar las actualizaciones de forma manual.
+ Visitar la página <a href="https://download.docker.com/linux/debian/dists/.">`https://download.docker.com/linux/debian/dists/`</a>

+ Seleccionar la versión de Debian de la lista.

+ Dirigirse a _`/pool/stable/`_ y seleccionar la arquitectura correcta (`amd64`, `armhf`, `arm64` o `s390x`).

+ Descargar los paquetes _.deb_ → `containerd.io`, `docker-ce`, `docker-ce-cli`, `docker-buildx-plugin` y `docker-compose-plugin` con su correspondiente versión y arquitectura.

+ Instalar los paquetes descargados:
```sh
sudo dpkg -i ./docker-*.deb ./containerd-*.deb
```

#### 4. Utilizar un script de instalación.
_(Recomendado únicamente para entornos de desarrollo)._

Docker proporciona un **<a href="https://get.docker.com/">script</a>** para instalar Docker en entornos de desarrollo de forma no interactiva.
```sh
curl -fsSL https://get.docker.com -o get-docker.sh # Script de instalación.
sudo sh ./get-docker.sh # Con --dry-run revisar los pasos ejecutará el script.
```

Para verificar que la instalación de **Docker Engine** es exitosa ejecutando la imagen `hello-world`:
```sh
sudo service docker start && sudo docker run hello-world
```
Este comando descarga una imagen de prueba y la ejecuta en un contenedor. Al ejecutarse, muestra un mensaje de confirmación y se cierra.

### Desinstalación de Docker Engine
Desinstalar los paquetes _Docker Engine, CLI, containerd y Docker Compose:_
```bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```
Eliminar imágenes, contenedores, volúmenes y archivos de configuración:
```sh
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```
### Post-instalación
#### Incluir usuario en grupo `docker`
El demonio de Docker se vincula a un socket y el propietario por defecto es `root`.\
Para acceder desde otro usuario solo es posible mediante `sudo` o agregando al usuario al grupo `docker`. _(En caso de no existir, será necesario crearlo)_ → `sudo groupadd docker`
```sh
cat /etc/group | grep "docker"
sudo usermod -aG docker $USER
```
#### Configurar inicio de Docker al arrancar el sistema
En Debian y Ubuntu Docker inicia en el arranque por defecto.
Puede activar o desactivarse este comportamiento mediante `systemd`.
```sh
# Activar Docker en el arranque
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```
```sh
# Desactivar Docker en el arranque
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```