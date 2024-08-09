---
tags:
  - Documentation
  - GitLab
  - DevOps
---
## Runners

Un **GitLab Runner** es un proceso que se ejecuta en los trabajos _(jobs)_ definidos en un pipeline de CI/CD en GitLab.

Cada Runner puede estar configurado para trabajar con múltiples proyectos y puede ejecutar varios trabajos simultáneamente, dependiendo de su configuración.

### Tipos de Runners

- **Shared Runners** : Son runners que estan disponibles para todos los proyectos en una instancia de GitLab.
- **Group Runners** : Son runners compartidos entre todos los proyectos dentro de un grupo específico en GitLab.
- **Specific Runners** : Son runners asignados a un proyecto en particular.

### Funcionamiento de un Runner

- **Pipeline definition**
	   Se define un pipeline en el archivo `.gitlab-ci.yml` dentro de un proyecto. Cada job dentro dle pipeline puede especificar una imagen concreta o utilizar la imagen por defecto del runner.
	   
- **Job Execution**
	   Cuando un pipeline se ejecuta, GitLab envía los trabajos a los runners disponibles o a uno concreto especificado mediante `tags`.
	   
- **Docker in Docker**
	   Si se hace uso del executor Docker, el runner se comunica con el demonio de Docker de la maquina anfitrión para crear contenedores y ejecutar trabajos en estos.

### Configuración de un GitLab Runner

**Instalación de Docker** (Si no está instalado) -> [[DOCKER - Installation|DOCKER - Installation]]

**Ejecución del contenedor de GitLab Runner**
```bash
docker run -d --name my-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner-latest
```

   - `docker run -d` : Crea y ejecuta un contenedor. 
     Mediante `-d` se ejecuta en modo _"deatached"_ o segundo plano.
   - `--name <name>` : Asigna un nombre al contenedor lo que facilita posteriormente su referencia.
   - `--restart <str>` : Configura la política de reinicio de un contenedor.

>|<div style="width:210px">Flag</div>|Descripción|
>|:-----|:-----|
>|`no`|No reiniciará automáticamente el contenedor|
>|`on-failure[:max-retries]`|Reinicia, únicamente cuando falle, un número de veces |
>|`always`|Reiniciará siempre si se detiene, salvo manualmente que iniciará si el demonio es reiniciado.|
>|`unless-stopped`|Similar a `always` salvo que, si es detenido manualmente, no iniciará si el demonio de docker es reiniciado.|
   
   - `-v <conf-path>:<conf-path>` : Monta la configuración dentro del contenedor.
   - `-v <sock-path>:<sock-path>` : Monta el socket en el contenedor, lo que permite al runner controlar y crear otros contenedores en la máquina anfitriona. Es crucial para que el runner pueda ejecutar trabajos _(jobs)_ en Docker.
   - `gitlab/<gitlab-image>` : Especifica la imagen de Docker que se usará. En este caso, la imagen oficial de GitLab Runner.

**Registro del runner en GitLab**
```bash
# docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
   docker exec -it my-runner gitlab-runner register
```

El comando `docker exec` permite ejecutar comandos en un contenedor en ejecución.
La opción `-i` o `--interactive` ejecuta el contenedor en modo interactivo, lo que deja abierta la entrada estandar permitiendo el envío de comandos. 
Con la opción `-t` o `--tty` invoca una pseudoterminal.

El comando `register` ejecuta un formulario que solicita lo siguiente:

- **GitLab instance URL** : URL de la instancia de GitLab
- **Registration token** : El token específico que se puede encontrar / crear en las configuraciónes CI/CD de GitLab.
- **Description** : Descripción del runner.
- **Tags** : Tags de identificación del runner.
- **Executor** : El modo en el que el runner ejecutará los jobs. (Mas detalles adelante)
- **Docker Image** : La imagen que Docker utilizará por defecto si no se especificase ninguna en el job.

**Roles o configuración del Runner**

- **Shell** : Ejecuta los comandos directamente en la consola del servidor que ejecuta el runner. No utiliza contenedores por lo que es más rápido, pero menos aislado.
- **Docker** : Ejecuta los trabajos dentro de contenedores Docker. Proporciona aislamiento y consistencia.
- **Docker+Machine** : Similar a Docker, pero también permite la creación dinámica de máquinas virtuales (VMs).
- **Kubernetes** : Ejecuta los trabajos en un clúster Kubernetes, ideal para entornos con escalabilidad y microservicios.
- **SSH** : Conecta a un servidor remoto mediante SSH y ejecuta los trabajos ahí.
- **Custom** : Permite la definición de un executor personalizado.
