- [ ] <div style="page-break-after: always;">\</div>
## Introducción
- [Fundamentos](#fundamentos)
	* [Consolas](#consolas) 
	* [Comandos](#comandos)
	* [Variables de entorno](#variables-de-entorno)
	* [Tipos de flujo](#tipos_de_flujo)
Fundamentos
- - -


# COMANDO WATCH (BRUTAL)

# 1. Introducción
## 1.1. Software y Paquetes
En Linux todas las distribuciones traen un conjunto de aplicaciones preinstaladas. Ademas de estas, existen una serie de repositorios con una gran cantidad de paquetes disponibles para instalar a través de un gestor de paquetes (_Package Manager_).

El gestor de paquetes puede variar según la distribución. Un ejemplo serían distribuciones como Debian, Ubuntu y Linux Mint que tuilizan las herramientas `dpkg`, `apt` y `apt-get` para instalar paquetes y librerías, generalmente denominados paquetes **DEB**.\
Por el contrario, distribuciones como RedHat, Fedora o CentOS utlizan `rpm`, `yum` y `dnf`.\
Existen otros como `pacman` en sistemas ArchLinux o `zypper` en OpenSUSE.

El uso y gestión de los gestores en Linux se detalla en el punto: **URL TO PACKAGE MANAGERS**

**Gestor de paquetes en Debian**
- **dpkg**: Es el gestor de de bajo nivel en Debian y sus derivados. Se utiliza para instalar, desinstalar y gestionar paquetes individualmente. Estos tienen extensión `.deb`. Sus opciones son:
	+ `dpkg -i package.deb`: Instala un paquete DEB.
	+ `dpkg -r package`: Desinstala un paquete.
	+ `dpkg -l`: Lista todos los paquetes instalados.
	+ `dpkg -S filename`: Encuentra a qué paquete pertenece un archivo instalado.

# Consolas

**Shell**: La interfaz de línea de comandos (_CLI_), también conocida como **shell** donde el usuario introduce comandos para ejecutar funciones del kernel. Algunas son:

- **bash**: La _Bourne Again Shell GNU_ está basada en la consola Bourne de Unix, aunque la amplía de varias maneras. Es la consola más común en Linux.
	+ **rbash**: _Restricted Bash_. Versión de bash con ciertas restricciones para mejorar la seguridad en entornos donde se desea limitar las capacidades del interprete de comandos. Algunas de las restricciones comunes incluyen:
		* No se permite cambiar de directorio. (`cd` restringido).
		* Limitación de variables de entorno.
		* Algunos comandos desabilitados como `exec`, `alias`, `unset`, `chsh`...
		* No se permite la redirección de archivos.
- **bsh**: La consola _Bourne_ en la que se basa **bash**. El comando `bsh` suele ser un enlace simbólico a **bash**.
- **tcsh**: Basada en la antigua consola _C_ (`csh`).
- **zsh**: La consola _Z_ es una evolución de la consola _C_ y _Bourne_. Añadiendo numerosas funcionalidades.

Hay numerosas consolas. En Linux **bash** suele ser la consola por defecto.
El archivo `/bin/sh` suele ser un enlace simbólico a la consola por defecto del sistema.

```
ls -l /bin/sh
lrwxrwxrwx root root 8 B Sun Nov 26 22:35:05 2023 /bin/sh ⇒ /bin/zsh
```

- - -
#### Tipos de flujo

Los flujos son canales a través de los cuales los programas pueden recibir o enviar datos. Hay tres flujos estándar que son fundamentales para la comunicación entre programas y con el entorno

- **STDOUT** (Standard Output): Se representa mediante el número `1`. Es el "output" o salida de datos de un comando al ser ejecutado, mostrándose en la terminal o siendo redirigida a otro comando.

- **STDIN** (Standard Input): Representada con `0`. Representa la entrada de datos desde el teclado o desde otro programa.\ Un ejemplo del segundo caso sería `cat /ruta/archivo | grep “palabra”`. (La salida estándar del primer comando pasa como entrada del segundo mediante una tubería o _pipe_)$^1$ 

- **STDERR** (Standard Error): Representado con `2`. Es donde un comando envía los datos del error al ser ejecutado. De esta forma se separa de la salida estándar y permite gestionar los errores de forma independiente.

- - -
#### Comandos

Los comandos internos son integrados en la consola. Estos comandos también se denominan "_Built-In_". Pueden variar según la consola que se utilice.
Mediante el comando `man` se muestra el manual de cada comando, por ejemplo: `man ls`.

`man` → Proporciona acceso a los manuales del sistema, ofreciendo información detallada sobre comandos, archivos y otras funcionalidades. Los manuales se muestran al usuario mediante el paginado `less` $^2$.

> [!NOTE]
> **Secciones en los manuales:**
> Al principio de los manuales se especifica el número al que pertenece, por ejemplo `PASSWD(1)` el cual hace referencia a la sección. Algunas palabras clave hacen referencia a más de un manual por su uso. Un ejemplo es el comando `passwd` que tiene su entrada en el manual en la sección `(1)` como comando y también en la sección `(5)` como archivo de configuración `/etc/passwd`.

- `man 1` : Contiene información sobre los comandos que pueden ser ejecutados por cualquier usuario.
- `man 8` : Incluye manuales para comandos que generalmente son utilizados por el administrador. Estos suelen modificar partes críticas del sistema.
- `man 7` : Ayuda genérica y documentación.
- `man 4` : Manuales de dispositivos dedicados a su configuración y uso.
- `man 5` : Información sobre los archivos de configuración del sistema, su estructura y formato.
- `man 2` : Llamadas del sistema. Se detalla como los programas a nivel de kernel interactúan con el hardware y otros servicios.

_La herramienta `tldr` muestra una vista simplificada de los manuales y no tan densa como `man`. Suele ser necesario instalarlo primero._

> [!IMPORTANT]
> Existen comandos que no poseen un manual. No obstante, la gran mayoría contemplan la opción `--help` la cual proporciona una descripción y ayuda de forma más resumida de las opciones de un comando.

$^2$`less` → Muestra la salida estándar de forma paginada el contenido de un fichero pasado como argumento. Si este no es especificado lee de la entrada estándar.\ Algunas de las funciones son la barra `/` para buscar cadenas dentro del manual que resaltará las coincidencias encontradas.\ Si únicamente queremos mostrar las líneas que contengan una cadena concreta, haremos uso del símbolo `&` indicando la cadena que queremos filtrar.\ Mediante la tecla `q` se sale de `less` de vuelta a la consola de comandos.
- Opciones:
	+ `-c` : Limpia la pantalla antes de mostrar. 
	+ `+n` : Muestra el contenido desde la línea especificada (`n`).
	+ `-N` : Mostrar las líneas de forma numerada.
	+ `-p <str>` : Mostrar contenido de un fichero resaltando el patrón indicado.
- Atajos una vez dentro de `less`:
	+ `g` : Viajar al principio del documento.
	+ `G` : Viajar hasta el final del documento.
	+ `F` : Mostrar actualizaciones al final del archivo en tiempo real. Comportamiento similar a `tail -f`.
	+ `nG` : Ir a la línea `n` del archivo. Suele combinarse con opción `-N` para mostrar líneas numeradas.
	+ `v` : Abrir archivo con el editor en la línea actual guardado en la variable de entorno `$EDITOR`. Este puede ser modificado mediante `export EDITOR= nano / vim...`
	+ `m` : Crear una marca. Esta puede ser cualquier letra (_Case sensitive_). Para volver a la marca se indica `'` (_Simple quote_) más la letra utilizada para la marca.
	+ `h` : Mostrar ayuda con las opciones y atajos del comando `less`.

En Linux y otros sistemas _UNIX-Based_, los comandos suelen aceptar una serie de opciones que realizan determinadas tareas o modifican su comportamiento. Los formatos comunes son:
- **UNIX** : La opción es precedida por un guión. Suele ser la más común a la hora de utilizar la línea de comandos y permite agrupar las opciones. `ls -a`, `ls -l -h -A` , `ls -lAh`.
- **BSD** : A la opción no le precede un guión. No muchos comandos tienen esta posibilidad. `ps aux`, `tar cvf`.
- **GNU** : Formato largo, precedido por dos guiones. Si existe la opción, suele ser útil dentro de scripts para que sea más descriptivo. `ls --all`, `ls --format=long`.

`history` → Muestra el historial de los últimos comandos introducidos en la consola (Generalmente los últimos 500).\ Añadiendo un número entero como argumento, mostrará ese número de últimos comandos.
- `-c` y `-p`: Ambas opciones limpian el historial de la sesión actual. La opción `-c` es para _bash_ y la opción `-p` para _zsh_. 
- El historial se almacena en los archivos ocultos `~/.bash_history` y `~/.zsh_history` bajo el directorio personal del usuario actual. No obstante, no se mostrarán los últimos comandos realizados en este archivo hasta que finalice la sesión actual.

_El símbolo `~` referencia el directorio personal del usuario actual, de modo que si el usuario actual fuese por ejemplo "jorge", equivaldría a `/home/jorge`._

`which cmd` → Ver la ruta absoluta donde se encuentra un binario, comando o ejecutable en caso de existir. Por ejemplo `which grep`.\ En caso de no existir el comando `which`, existe la alternativa `command -v`. Este comando únicamente muestra la primera vez que encuentra el comando en el _PATH_. Para ver todas las coincidencias es necesario especificar la opción `-a` o la alternativa, el comando `whereis`.

_**Ruta Absoluta:**_ Especifica la ubicación completa desde la raíz del sistema de archivos. `/bin/cat`, `/home/user/file.txt`

_**Ruta Relativa:**_ Especifica la ubicación de un archivo, directorio... respecto al directorio actual. `./script.sh`, `../file`

_Cuando ejecutamos un comando normalmente no especificamos la ruta absoluta de este. 
Esto es posible ya que la ruta donde este comando está almacenado se encuentra en el `PATH`$^4$
Esto quiere decir que el sistema buscará dentro de una serie de rutas almacenadas y encontrará el binario al que hacemos referencia._
_En caso de que no se encuentre en el `PATH`, puede añadirse la ruta donde se encuentra o ser llamado mediante su ruta absoluta._

* `whatis cmd` → Buscar y mostrar breves descripciones de comandos en el sistema. Su alternativa es `man -f cmd`

* `apropos str` → Buscar en las páginas del manual cadenas y palabras clave y mostrar una lista de comandos relacionados. Su alternativa es `man -k str`.

- - -
#### Variables de entorno y variables locales

Al igual que en los lenguajes de programación, almacenan información a la que se accede mediante el nombre de la variable.

**Variables locales**: Las variables locales solo están disponibles en la _shell_ en la que han sido creadas. Para asignar un valor a la variable se realiza de la siguiente forma: `variable=value`

**Variables de entorno**: Disponible en entorno. Esto quiere decir que cualquier programa ejecutado en la terminal en la que ha sido creada, tendrá acceso a la variable.
Pueden definirse mediante el comando `export` seguido de la variable (mayúsculas por convención) igualado al valor: `export LOCALDOMAIN=nebula.local`.

Mediante `echo`$^3$ puede mostrarse el contenido de una variable seguido de la variable precedida por el símbolo `$`. Este no es necesario a la hora de definir una variable pero si cuando se referencia: `echo $LOCALDOMAIN`.

Si queremos mantener una variable fuera del entorno, está puede ser definida dentro del archivo `bashrc`, `zshrc` u otros según el tipo de shell del usuario.

> [!NOTE]
> El archivo `bashrc` (_bash run commands_) se encuentra en el directorio personal del usuario. Este se ejecuta cada vez que se ejecuta una nueva sesión de bash.
> Según el tipo de consola del usuario, este puede variar. Por ejemplo el archivo `zshrc` si el tipo de shell es **zsh** o `kshrc` si se trata de una **korn**...

Con `unset` se elimina una variable de entorno. `unset LOCALDOMAIN`. (Sin `$`).

Algunas de las variables de entorno mas relevantes pueden ser:

- $^4$`PATH` : Variable que contiene los directorios o rutas donde el sistema buscará los ejecutables. Cada directorio está separado por dos puntos (`:`).
  *Podemos añadir contenido a variables como el `PATH` de forma recursiva. Por ejemplo:*
  `PATH=$PATH:/another/path`.
- `HOME` : Contiene la ruta al directorio principal del usuario.
- `USER` o `LOGNAME` : Nombre del usuario actual.
- `SHELL` : Consola predeterminada del usuario actual.
- `PWD` : Ruta del directorio actual. La forma sencilla de mostrar la ruta actual es mediante el comando `pwd` que realiza lo mismo que `echo $PWD`.
- `TERM` : Contiene el tipo de interfaz de emulador de terminal que se está utilizando. 
  Esta proporciona una interfaz de línea de comandos en sistemas modernos
  Esta podría ser `xterm`, `gnome`, `xterm-256color`... las cuales tienen distintas capacidades como la capacidad de interpretar colores, secuencias de escape...
- `TZ` : Establece la zona horaria del sistema.
- `UID` y `GID` : Almacena el identificador de usuario y grupo del usuario actual.

_Existen muchas más variables de entorno. La manipulación de estas es fundamental para la configuración y personalización del entorno de trabajo en sistemas Linux._
##### Variable global y variable local

$^3$`echo` → Se utiliza para imprimir texto o variables en la salida estándar. Se utiliza con frecuencia en shell scripts, redirección en comandos$^5$... 

	name="Jorge" ; echo "My name is $name" > ./myName.txt
  
Algunas de sus opciones son:
+  `-e` : Habilita la interpretación de secuencias de escape como puede ser `\n` que representa un salto de línea.
+ `-E` : Deshabilita la interpretación de secuencias de escape. (Por defecto)
+ `-n` : Evita el salto de línea al final.

- - - 
#### $^5$ Redirección de comandos

Son técnicas que permiten manejar la entrada y salida de datos de los programas y comandos.

**Redirección de salida estándar (_stdout_):**
+ `cmd > file` → Enviar el _stdout_ de un comando (`cmd`) a un archivo (`file`). En caso de existir sobrescribirá el contenido del archivo.
+ `cmd >> file` → Enviar el _stdout_ de un comando (`cmd`) a un archivo (`file`) . En caso de existir añadirá el _stdout_ al contenido del archivo (_append_).
	
**Redirección de entrada estándar (_stdin_):** 
+ `cmd < file` → Redirección del contenido de un archivo como _stdin_ de un comando.
+ `cmd < cmd` → Redirección del _stdout_ del segundo comando como stdin del primero.

**Pipelines:** - Operador pipe : `|` 
+ `cmd | cmd` → Toma el _stdout_ del primer comando como _stdin_ del segundo.

**Redirección separada de salida y error estándar:**
+ `cmd 1> /dev/null` → Redirección de _stdout_ a `/dev/null`. La mención de `1` es opcional, ya que por defecto se redirige la salida estándar.
+ `cmd 2> /dev/null` → Redirección _stderr_ a `/dev/null`.
+ `cmd &> /dev/null` → Redirección tanto de _stderr_ como _stdout_ a `/dev/null`.
+ `cmd > /dev/null 2>$1` → Otra forma de redirección tanto de _stderr_ como _stdout_ a `/dev/null`. Mediante `2>&1` indicamos que el _stderr_ (`2`) pasa a formar parte del _stdout_ (`1`), por ello tanto _stdout_ como _stderr_ se redirige a `/dev/null`. Un ejemplo claro: `cmd 2>stder.txt 1>stdout.txt`

`exec` → Es un comando interno o "_built-in_" de Linux, suele utilizarse para reemplazar la terminal actual con un nuevo proceso. Esto significa que cuando se ejecuta el comando `exec cmd` el proceso de la shell actual terminará y el nuevo proceso o programa (`cmd`) comenzará.
Además de este uso, tiene otros usos avanzados. Estos pueden ser los siguientes: 

- `exec {1,2,&}> file` → Redirección del _stdout_, _stderr_ o los dos a un archivo (_Enviará la salida de todos los comandos ejecutados posteriormente_). Si se quisiera detener este comportamiento, puede redirigirse la salida de nuevo a la terminal (`TTY`) o pseudo-terminal (`pts`). Por ejemplo: `exec > /dev/pts/6` 

> [!NOTE]
> Mediante el comando `tty` puede verse el tipo de terminal y nombre del dispositivo actual.
> Cuando se trate de una **tty** (_TeleTypewriter_) el comando reportará `/dev/tty` + el número identificador de ese dispositivo. (`tty0`,`tty1`... `tty63`)
> Por otro lado, si se trata de una **pts** (_Pseudo-Terminal Slave_) reportará `/dev/pts/[n]` donde `[n]` es el número identificador de esa terminal virtual.

**Descriptores de archivo**

+ `exec 3< file` → Crear un descriptor de archivo (`3`) de lectura asociado a un archivo.
+ `exec 3> file` → Crear un descriptor de archivo (`3`) de escritura asociado a un archivo.
+ `exec 3<> file` → Crear un descriptor de archivo (`3`) de lectura y escritura asociado a un archivo.
+ `exec 3>&-` → Cerrar un descriptor de archivo (`3`). Seguirá existiendo y no perderá su contenido, solo que ya no tendrá un descriptor.
+ `exec 4>&3` → Crear un descriptor de archivo (`4`) como copia de otro (`3`).
+ `echo "str" > &3` → Escribir en un descriptor de archivo (`3`). Siempre añade, no sobrescribe.
+ `cat <&3` → Leer un descriptor de archivo (`3`).

`tee` → Este comando permite duplicar la entrada estándar y enviarla a mas de un lugar.
Si únicamente se especifica un destino, la enviará al destino y a la salida estándar. (AMPLIAR)

El dispositivo `/dev/null` es conocido como el "agujero negro" del sistema de archivos. Todo lo que se escribe aquí se descarta y no se almacena en ningún lugar. 
Se utiliza comúnmente para redirigir la salida de un comando o programa cuando no se desea mostrar esta por pantalla.

- - - 
##### Operadores

`;` → Mediante este operador podemos concatenar comandos en una sola línea.
`mkdir new_folder ; cd !$` : Creará una nueva carpeta y cambiará al directorio recién creado. Si un alguno de los comandos falla, los posteriores se ejecutarán igualmente.
  
*La variable especial `!$` representa el último argumento del comando anterior. En este caso, el nombre de la carpeta que se ha creado.*

`&&` → Al igual que el anterior, concatena comandos salvo que únicamente los ejecutará siempre y cuando el anterior comando devuelva un código de estado$^6$ exitoso (`0`). Normalmente se utiliza para concatenar comandos que dependen del éxito del comando anterior. Si el primer comando falla ya sea por ser erróneo, un error de sintaxis, fallo en la ejecución... el segundo no se ejecutará.
  
$^6$ *Para ver el **código de estado** del último comando ejecutado, podemos hacerlo mostrando el contenido de la variable `$?` → `echo $?`*

`||` → (*doble pipe*) Si concatenamos dos comandos mediante este operador, en caso de que el primer comando sea exitoso, el segundo no se ejecutará. Su uso principal es el de ejecutar un comando alternativo en caso de que el primero falle.

`|` → (*pipe*)$^1$  El _stdout_ (_No stderr, a no ser que se indique_) del primer comando se conectará a la _stdin_ del segundo comando.

`|&` → Es otra forma de representar `2>&1 |`. Es decir, el error estándar pasa a formar parte de la salida estándar y dado que hay un _pipe_ ambos pasan como entrada estándar del segundo comando a la derecha del _pipe_. 
_No debe confundirse con `&|` que ejecutará el comando a la izquierda del pipe en segundo plano y no pasará nada como stdin mediante la tubería._

`&` → El comando seguido por este operador pasará a ejecutarse en segundo plano, no esperará a que este termine. 
  Al ejecutar un comando y enviarlo a segundo plano, el _stdout_ reportará un _PID_ (Id de proceso).
	
*Cuando ejecutamos una aplicación desde la terminal, esta dependerá del proceso "padre". En este caso el proceso padre es la terminal donde se ha ejecutado.
Durante la ejecución de la aplicación, si esta se encuentra en primer plano, la terminal donde se ejecutó estará bloqueada.
Mediante el operador `&` enviaremos la aplicación o proceso "hijo" a segundo plano lo que liberará la terminal.\ A pesar de ello, en caso de cerrar el proceso "padre", en este caso la terminal, el proceso "hijo" terminará. 
Para evitar esto puede hacerse uso del comando `disown`*

`disown` → Este argumento desvincula el proceso "padre" del proceso "hijo", y este último pasa a ser un proceso único no dependiente. → `wireshark & disown`
~ *Todos los procesos del sistema, tanto los propios como los ejecutados por el usuario tienen un `id` único cuando se encuentran en ejecución. Estos se pueden ver mediante el comando `ps`* ~

- - -
##### Trabajos y procesos en Linux

En Linux es crucial comprender la diferencia entre trabajos y procesos ya que cada uno desempeña un papel específico en la gestión y ejecución del sistema.

**Trabajos**

Se refieren a las tareas o comandos que se ejecutan en la terminal actual. Al cerrar la terminal los trabajos activos en esa sesión terminarán. Un trabajo está vinculado a la existencia de la terminal que los inició.

El comando `jobs` muestra una lista de procesos en ejecución de la terminal actual que dependen de esta junto con su identificador de trabajo (_Job ID_) y estado: _Running_, _Stopped_, _Done_...
Con el parámetro `-l` mostraremos de forma mas detallada los trabajos y su _PID_.


`bg` → Destinado a enviar trabajos a segundo plano. Si un trabajo se está ejecutando en primer plano, este puede suspenderse (`Ctrl + Z`) y enviarse a segundo plano mediante `bg %` + el _Job ID_.

```bash
$ bash script.sh # Ejecución de proceso en primer plano.
^Z # Ctrl + Z -> Suspende el proceso.
zsh: suspended  bash ./script.sh
$ jobs # Mostrar los trabajos y su Job ID
[1]  + suspended  bash ./script.sh # Proceso suspendido con Job ID = 1
$ bg %1 # Enviar proceso a segundo plano con Job ID = 1
[1]  + continued  bash ./script.sh
$ jobs # Mostrar de nuevo procesos de la terminal.
[1]  + running  bash ./script.sh # Proceso ahora ejecutándose en segundo plano.
```

`fg` → Envía los procesos en segundo plano a primer plano especificando el id de trabajo. En el ejemplo anterior, para devolver el comando a primer plano, lo haríamos mediante `fg %1`.

**Atajos de control y gestión de procesos**:

- `Ctrl + C` → Interrumpir o terminar la ejecución. 
- `Ctrl + Z` → Suspender la ejecución.
- `Ctrl + S` → Detener la salida estándar (útil cuando se genera un stdout denso).
- `Ctrl + Q` → Reanudar la salida estándar.
- `Ctrl + D` → Cerrar sesión o finalizar entrada (_Exception EOFError_). Si se presiona al inicio de una línea vacía envía un `logout` y cierra la sesión del usuario.

<u>Otros atajos de utilidad</u>:

- `Ctrl + A` o `Inicio` → Mover cursor al principio de la línea.
- `Ctrl + E` o `Fin` → Mover cursor al final de la línea.
- `Ctrl + U` → Eliminar desde la posición del cursor hasta el principio de línea.
- `Ctrl + K` → Eliminar desde el cursor hasta el final de la línea.
- `Ctrl + W` → Borra la palabra que se encuentra entes del cursor en la línea actual.
- `Ctrl + R` → Búsqueda inversa en el historial de comandos. _(fzf plugin para zsh)_

**Procesos**

Los procesos pueden ejecutarse tanto por un usuario como por el sistema. Son también conocidos como _demonios_ o _daemons_. 
Los procesos del sistema, esenciales para el funcionamiento general, se inician automáticamente al inicio, sin depender de sesiones de usuarios. 
Si un usuario ejecuta un programa con procesos asociados, el cierre de la sesión los terminará, pero los del sistema seguirán en ejecución.

`ps` → Muestra información sobre los procesos en ejecución en el sistema. Si no se especifica argumento, mostrará únicamente aquellos ejecutados en la sesión del usuario actual.
+ `ps aux` → Muestra una lista mucho mas detallada de todos los procesos en ejecución en sistema. 
  + `-a` : Muestra los procesos de todos los usuarios. 
  + `-u` : Muestra información detallada del usuario propietario del proceso. 
  + `-x` : Mostrará todos los procesos y trabajos independientemente de no haber sido ejecutados por un usuario.
  + Otra opciones interesantes son `-f` para ver los procesos de forma más detallada o la opción `--forest` para aplicar sangrías y mostrar la jerarquía de procesos.
	  
<u>Otras funciones</u>

- `ps aux | grep <name>` → Mostrar información de un proceso filtrando la salida de `ps` mediante el comando `grep`$^7$.
- `ps -p PID` → Filtrar por PID _(Process ID)_.
- `pgrep <name>` → Buscar un proceso por su nombre. Este comando únicamente devuelve su PID.

**Matar procesos en Linux**:

`kill` → Envía señales a un proceso. La más común es `SIGTERM(15)` que le indica a un proceso que se cierre de manera ordenada. Si un proceso no responde a señales `SIGTERM` o necesita ser detenido de inmediato, es posible utilizar la señal `SIGKILL(9)` con el comando `kill -9` o `pkill -9`. Por ejemplo, para matar un proceso con ID 1234: `kill 1234`. Por defecto, envía una señal `SIGTERM(15)` a no ser que se especifique otra cosa. (Ej. `kill -9 4672`).

`pkill` → Permite matar procesos por nombre u otras propiedades. Ej. `pkill top` (Matar proceso por nombre), `pkill -u username` (Matar proceso por usuario).

- - -

**El comando top**

`top`  → Muestra una vista dinámica y en tiempo real de los procesos y su uso de recursos. 
[Manual top](https://man7.org/linux/man-pages/man1/top.1.html). 
Como muchos comandos de Linux, `top` admite varias opciones como:

+ `-d` + `retardo (s)` → Indicar el retardo entre actualizaciones.
+ `-p` + `PID` → Monitorizar un proceso específico.
+ `-n` + `iteraciones` → Veces que se va a actualizar antes de cerrarse.
+ `-b` → Modo por lotes. *Útil a la hora de redireccionar valores a un archivo*.

Una vez dentro del menú de top, mediante la tecla `o` se mostrará un input donde indicar un filtro por columna (`COL=nombre_proceso`). Por ejemplo, filtrar por el nombre del proceso `COMMAND=apache2` o por PID, `PID=48535`. La tecla `=` eliminará los filtros aplicados.

- Con `f` indicaremos que columnas queremos que se muestren o dejen de mostrar activando y desactivando mediante la tecla espacio.
- Mediante `k` podremos matar un proceso. El programa `top` nos solicitará un PID. También podemos ordenar los procesos por uso de CPU con `P` y por uso de memoria mediante `M`.
- Con `e` cambia la unidad de información (_Mb a Gb_, _Kb a Mb_...).

- - -

**El comando htop**

`htop` → Forma más avanzada de mostrar los procesos. A diferencia de `top` no suele venir preinstalado. [Manual htop](https://www.man7.org/linux/man-pages/man1/htop.1.html)

Dentro de `htop` se indican las teclas con las que podemos filtrar, buscar, ordenar o matar procesos...

Otras alternativas muy potentes son `bashtop` (Escrito en Bash) / `btop` (Escrito en C), `nethogs` (red), `pstree`
- - -
##### 1.6. Variables y caracteres especiales -> Bash Scripting

`"` → Las comillas dobles como delimitador, es decir, al principio y al final de una cadena, eliminan los caracteres especiales salvo
`'` → La comilla simple  elimina todos los caracteres especiales que contenga.

`\` → Escapará o ignorará el siguiente carácter seguido de la barra invertida.

`` ` `` → La comilla invertida ejecuta su contenido y no escapa caracteres especiales. 
_Si se declara una variable en la que su contenido sea el comando `ls`, por ejemplo `var="ls"`, al mostrar el contenido de esta variable delimitada por comillas invertidas provocará que se ejecute el comando. La forma recomendable es hacerlo de la siguiente manera: `$($var)`

`#` → Es el carácter destinado a crear comentarios. 
_En la línea de comandos, si se especifica este separado por al menos un espacio a cada lado, todo lo que se encuentre a la derecha se interpretará como un comentario y no se ejecutará._

`*` → El asterisco referencia todo. De este modo si se ejecuta `rm ./*` indica que se quiere borrar todo el contenido del directorio actual (`./`). 
`?` → Referencia un carácter cualquiera. Por ejemplo `ls file???` donde cada interrogante puede ser un carácter cualquiera.

`[ ]` → Asocia cualquiera de los caracteres incluidos dentro de las llaves. 
Un ejemplo sería `cp [1-5]*` que copiará todos los archivos que comiencen del 1 al 5.

_Si se especifica un rango, únicamente se toman en cuenta los caracteres inmediatos al guion. Esto quiere decir que no se puede especificar un rango, por ejemplo, de 1 a 48 `[1-48]` dado que se interpreta como rango del 1 al 4 u 8. Para asociar la segunda posición habría que especificar un nuevo filtro o conjunto. Por ejemplo: `ls file[1-3][5-6]`_
_El circunflejo o `^` representa aquellos caracteres que NO queremos asociar, un ejemplo sería `[^3]`_

Los símbolos `*`, `?` y `[]` se conocen como _wildcards_.

`$#` → Devuelve el número total de argumentos.
`$@` → Referencia todos los argumentos pasados a un comando como lista.
`$*` → Cadena que representa todos los argumentos como una sola palabra. Los espacios entre argumentos se tratan como el valor de la variable de entorno `IFS` (_Internal Field Separator_).
`$0` → Representa el nombre del script o programa.
`$1`, `$2`, `$n` → Representa argumentos individuales dada la posición en la que se han pasado.
`!!` → Representa el último comando ejecutado. Como truco, puede ser utilizado para ejecutar como sudo el último comando anterior (`sudo !!`) o agregar al último comando argumentos adicionales.

`!n` → Donde _n_ representa el número de línea del historial, ejecutará el comando ejecutado en dicha línea.
`$?` → Representa el código de salida del último comando ejecutado.
- `0` : Éxito, Indica que el comando se ejecutó correctamente y sin errores.
+ `1-127` : Errores. Suelen indicar diversos tipos de errores o problemas durante la ejecución del comando. Por ejemplo, un código de salida 127 a menudo significa que el comando no se encontró.
+  `128+` : Errores fatales o señales. Si el comando termina debido a una señal el código de salida será 128 mas el número de salida. Por ejemplo se el comando es terminado por la señal SIGSEGV (Violación de segmento), el código de salida será 128 + 11.
`!$` → Como se ha mencionado, representa el argumento del último comando introducido, muy útil para agilizar la introducción de comandos. El atajo de teclado `Alt + .`

`$!` → Representa el ID de proceso del último comando ejecutado en segundo plano.
`$$` → Representa el ID del proceso actual.
`$RANDOM` → Genera un número entero aleatorio entre 0 y 32767.
`$LINENO` → Representa el número de línea en el script actual.

- - -
#### Sistema

`lspci` → Muestra los dispositivos conectados al bus PCI (_Peripheral Component Interconnect_). Suelen ser componentes conectados a la placa base. Cuando se ejecuta este comando se reportan una serie de direcciones en notación hexadecimal las cuales son los identificadores de cada uno de los dispositivos PCI.
- `-v`, `-vv`, `-vvv` : Modo _verbose_. En los comandos de información del sistema es prácticamente necesario incluir esta opción para que se reporte más información. 
- `-t` :  Muestra la información en modo _tree-like_.
- `-s deviceId -v` : Filtrar por un dispositivo concreto y mostrar información detallada sobre este junto al modo verboso. Información como capabilities, drivers, latencia...
- `-k` : Mostrar los drivers del kernel de todos los dispositivos o por uno concreto filtrado con la opción `-s`. El modo verboso activa esta opción por defecto.
Hay otras numerosas opciones que pueden ser revisadas en en manual.

`lsusb` → Enumera los dispositivos USB (_Universal Serial Bus_) conectados a la máquina. Suelen ser dedicados a dispositivos de entrada como teclados, almacenamiento...
Al igual que `lspci`, también cuenta con el modo verboso (`-v`) o la vista en modo arbol. Además, la posibilidad de filtrar mediante un dispositivo USB concreto con la opción `-s busId:devId`, como por ejemplo `lsusb -s 01:11 -v`.

> [!NOTE]
> La información que reportan los comandos anteriores se obtiene de rutas del sistema como `/proc` o `/sys`.
> En sistemas más recientes, parte del directorio `/proc` es un enlace simbólico a `/sys`.

`uname` → Mostrar información del sistema.
- Nombre del nodo (equipo): `-n` o `--nodename`.
- Nombre del Kernel: `-s` o `--kernel-name`. *En todos los sistemas suele ser `Linux`*.
- Versión del Kernel: `-v` o `--kernel-version`. *Suele mostrar fecha y hora de compilación pero no el número de versión real*.
- Compilación del Kernel: `-r` o `--kernel-release`.
- Máquina: `-m` o `--machine`. *Muestra información sobre el equipo (CPU)*.

En la práctica lo mas común es utilizar `-a` o `--all` para conocer el sistema. El resto de opciones son útiles en scripts para obtener información concreta de forma rápida.

`date` → Comando dedicado a mostrar o establecer la fecha y hora del sistema.
Las opciones más comunes del comando date son:
- `-d "str"` / `--date="str"` : Permite operar con una fecha específica dado como string, un ejemplo sería `date -d "yesterday"`, `date -d "1 year ago"`, `date --date="next sunday"`...
- `-u` / `--utc` : Muestra o establece la fecha en UTC.
- ``
Es posible especificar el formato en el que se desea mostrar la fecha y hora utilizando secuencias. Las más comunes son:
- `%a` : Nombre del día de la semana abreviado (ej. Sun, Sat...)
- `%A` : Nombre del día de la semana completo (ej. Sunday, Saturday...)
- `%b` : Nombre del mes abreviado (ej. Jan, Feb...)
- `%B` : Nombre del mes completo (ej. January, February...)
- `%d` : Día del mes (ej. 01, 14)
- `%D` : 

`timedatectl` → Este comando mostrará información detallada sobre la hora actual, la zona horaria, etc...
- `set-time` : Actualizar el reloj del sistema a una hora específica. El formato ha de ser `"2012-10-30 18:17:16"`
- `set-timezone` : Actualizar la zona horaria a una específica.
- `list-timezones` : Listar zonas horarias disponibles.

`whoami` → Ver nuestro usuario actual.

`who` → Ver quien está logueado en este momento.
*Entre otras opciones, el parámetro `-H` nos mostrará la IP de cada usuario. Útil para revisar conexiones SSH*
`id <user>` → Ver a qué grupos pertenece un usuario. Si este no se especifica, indicará los del usuario actual.

`shutdown <args> <hour(opt)>` → Destinado a apagar o reiniciar el sistema de forma programada. Suele requerir privilegios de superusuario. Si se especifica `now` como hora el sistema se apagará o reiniciará inmediatamente. Otra forma de apagar el sistema puede ser mediante el comando `init 0`.
- `-h` : Apaga el sistema.
- `-r` : Reinicia el sistema. Es lo mismo que ejecutar el comando `reboot`.
- `-c` : Cancela un apagado o reinicio programado previamente.
- `-t <int>` : Especifica el tiempo en minutos antes del apagado o reinicio.
- `-f` : Fuerza el apagado sin consultar.
- **Ejemplos de uso:**
	+ `shutdown -r now` : Reiniciar el sistema inmediatamente.
	+ `shutdown -h 13:45 &` : Apagado planificado del sistema.

`logout` : Cerrar sesión del usuario actual.

`exit` :  Salir del intérprete de comandos actual. Si solo hay uno, equivale a cerrar sesión.
- - -

- - -
##### 2.3. Gestión y búsqueda de archivos y directorios

`pwd` → Muestra la ruta del directorio actual.

`cd` → Comando para moverse entre directorios.
- `..` : Referencia un directorio por encima o directorio padre del actual.
- `.` : Referencia al directorio actual.
	Existen referencias a rutas mediante símbolos, estas son:
- `~` : Referencia el directorio de trabajo del usuario actual.
  *Si no incluimos ni ruta ni argumentos (`cd`), el comando dirige al directorio personal del usuario actual. Este se almacena en la variable de entorno `$HOME`*
- `-` : Referencia el directorio anterior al actual.


`touch <file>` → Crear un archivo. También podemos crear un archivo redireccionando a este la salida estándar mediante el comando `echo`. 
Por ejemplo: `echo '' > file.txt`

> [!TIP]
> La opción especial `--` se puede utilizar para indicar el final de todas las opciones del comando.
> Por ejemplo, si mediante el comando `touch` se intenta crear un archivo llamado `--badname` y no se desea que el nombre sea interpretado como una opción del comando no reconocida.

`mkdir <args> <dir>` → Crear un directorio.
- `-p` : Crear varios directorios a varias profundidades. Ej. `mkdir -p /home/<dir-1>/<dir-2>`.
- `-m` : Establecer los permisos del directorio al crearlo (igual que concatenar con ` chmod `). Ej. `mkdir -m 644 <dir-name>`.

`rmdir <dir>` → Borrar un directorio (solo si este está vacío).

`rm args <dir/file>` → Elimina tanto archivos como directorios.
- `-r` : Elimina un directorio y su contenido de forma recursiva.
- `-f` : Fuerza la eliminación, sin confirmación.

`cp <dir/file> <path>` → Copiará archivo/directorio en la ruta indicada.
- `-r` : Si se especifica un directorio, copiará de forma recursiva el contenido de este y sus subdirectorios.
- `-u` : Copiar únicamente cuando el archivo o directorio es más reciente al existente o este no existe en la ruta de destino.
- `-s` : Crear enlaces simbólicos en vez de copiar.
- `-l` : Crear enlaces duros en vez de copiar.
- 

`mv` → Mover o renombrar archivos y directorios. Se podrá mover siempre que se tengan permisos en la ruta destino. Si se ejecuta  `mv file1 file2` el primero se renombra al segundo dado que está moviendo todos los _metadatos_ del primer fichero al segundo con otro nombre distinto. Es por ello que el primero dejará de existir en el sistema.
- `-i` : Solicita confirmación.
- `-f` : Fuerza la operación sin mostrar advertencias.
- `-v` (`verbose`) : Mostrar _stdout_ detallado del proceso al mover o renombrar.
- `-b` : Crear un _backup_ de los ficheros existentes en la ruta destino.
- **Ejemplos de uso:**
	+ `mv file.txt ~/Documents/` : Mover archivo a directorio destino.
	+ `mv bar.txt foo.txt` : Renombrar archivo.
	+ `mv bar.txt ~/Desktop/foo.txt` : Mover y renombrar al mismo tiempo.
	+ `mv bar/ foo/` : Renombrar un directorio.

`ln <args> <file1> <file2>` → Crear enlaces entre archivos y directorios. Pueden ser enlaces duros (*Hard links*) o simbólicos (*Symbolic link* o *Symlink*).

`type` → 

`ls` → Muestra el contenido de un directorio o propiedades de un archivo.
- `-l` : Muestra información adicional del contenido como permisos, propietario, tamaño, fecha…
- `-a` : Muestra todo el contenido incluido oculto, sin ignorar ningún fichero.
	*Los ficheros y directorios ocultos del sistema comienzan por punto `.`*
- `-A` : Es similar a la opción anterior pero omite la carpeta actual y el directorio padre, representados como `.` (Directorio actual) y `..` (Directorio padre del actual).
- `-R` : Muestra el contenido del directorio y sub-directorios de forma recursiva.
- `-d` : Muestra únicamente directorios.
- `-h` : Junto con `-l` que muestra el tamaño de archivo / directorio, muestra las unidades de forma legible.
- `-i` : Muestra el `inode` del archivo o directorio.
- `-m` : Muestra contenido separado por comas.
- `-o` : Igual que `-l` pero omite información del grupo propietario.
- `-Q` : Lista los nombres de archivos / directorios entre comillas.
- `-S` : Ordena por tamaño (Mas grandes primero).
- `-t` : Ordena por fecha de modificación (Mas nuevo primero).
- `-r` : Ordena de forma reversa. 
	*Si por ejemplo, se quisiera listar los archivos dentro de un directorio ordenados de menor a mayor según su tamaño, se puede realizar combinando `-r` y `-s`.
	En el ejemplo anterior, es lo mismo `ls -lrS` que `ls -l -r -S`. Esto se debe a que las opciones de un comando se pueden agrupar.*
	
`lsof` -> Lista ficheros abiertos. Hay que recordar que en los sistemas UNIX, todo son ficheros, por lo que al ejecutar este comando, podremos ver todos

`realpath <file/dir>` → Proporciona la ruta absoluta de un archivo o directorio. 

`tree <args> <dir>` → Muestra archivos y directorios al igual que `ls` pero de forma jerárquica o de árbol.
- `-a` : Muestra todo incluido archivos y directorios ocultos.
- `-d` : Muestra solo directorios.
- `-L <int>` : Limita la profundidad de búsqueda.
- `-h` : Muestra tamaños de archivos de forma legible.

`find <path> <args>` → Permite buscar archivos dentro de un directorio del sistema según los una enorme cantidad de parámetros. algunos pueden ser:
- `-name "*.py"` : Filtra por nombre de archivo. *El parámetro `-iname` hace lo mismo pero no case sensitive.*
- `-type <f/d/l>` : Buscar archivos en una ruta según tipo.
- `-size 1M` : Busca por tamaño de archivo redondeando por unidad. *Si se especifica `+` o `-` delante de la unidad, se filtrará por tamaños mayores o menores a esta, si no se especifica, iguales.*
	+ `c` : bytes.
	+ `k` : kibibytes.
	+ `M` : Mebibytes.
	+ `G` : Gibibytes.
- `-newerXY` : Filtra y compara por fechas de modificación. `X` Indica el tipo de archivo de referencia. `Y` Indica el tipo de archivo que se compara con el archivo de referencia. Estos parámetros pueden ser:
	+ `a` : Archivos a los que se han accedido.
	+ `B` : Archivos que se han creado.
	+ `c` : Metadatos han cambiado.
	+ `m` : Archivos que se han modificado.
	+ `t` : Último acceso a archivos.
- `-regex pattern` : Busca mediante expresiones regulares.
- `-empty` : Busca ficheros vacíos.
- `-exec <cmd> {} \;` : Se utiliza para ejecutar un comando en cada uno de los archivos o directorios encontrados. `{}` representa el marcador por el que se reemplazará el comando y `\;` indica el final de `exec`. Un ejemplo sería `find -name "*.bak" -exec gzip {} \;`
- `-maxdepth <int>` :  indicar la profundidad máxima de directorios en los que buscar.
<u>Permisos</u>
Existen múltiples formas de filtrar por permisos mediante `find` :
+ `-user <username>` : Buscar archivos y directorios cuyo propietario sea el especificado.
+ `-group <groupname>` : Buscar por archivos y directorios cuyo grupo propietario sea uno en concreto.
+ `-readable` : Buscar por archivos y directorios con capacidad de lectura para el usuario actual.
+ `-writable` : Buscará archivos o directorios con capacidad de escritura por el usuario actual.
+ `-executable` : Buscará archivos o directorios con capacidad de ejecución por el usuario actual. 
+ `-perm <args>` : Filtra por permisos de forma avanzada. Algunos ejemplos serían:
	+ `find / -type f -perm -u=w` : Buscar ficheros con permisos de escritura para el usuario actual.
	+ `find / -type d -perm -642` : Buscar directorios con unos permisos específicos de forma octal.
	+ `find / -name "*.*" -perm (-u=s / -4000)` : Buscar archivos con extensión que tengan permisos `SUID` del usuario.
	*Otros argumentos útiles pueden ser la combinación de `-print` y `-quit`. Por ejemplo: 
	`find ~/Documentos -newermt 20230101 -print -quit`. En caso de encontrar una coincidencia, terminará y no seguirá buscando.
	*Existen muchas otras formas de filtrar con `find` que pueden encontrarse en el manual (`man find`).*

`locate` → Es similar al comando `find` pero no ofrece sus filtros de búsqueda. La ventaja es la rapidez dado que trabaja mediante una base de datos local.
Para actualizar esta base de datos se ejecuta el comando `sudo updatedb` *Requiere permisos de superuser*. `locate *.conf`

`reset` / `tset` →

`cat <file>` → Mostrar el contenido de un archivo.
- `-n` : Numera todas las líneas mostradas. 
- `-A` : Muestra tabulaciones (`^I`), espacios (`·`), finales de línea (`$`)...
- `-s` : Suprime las líneas en blanco repetidas.

_El comando `tac` hace lo mismo que el comando `cat` pero muestra el contenido al revés (primera línea la final del documento y sucesivamente)._

_Existe la variante `zcat` para mostrar el contenido de archivos comprimidos sin necesidad de descomprimir estos primero. El funcionamiento es cargar en memoria el archivo y descomprimirlo primero sin que tenga que hacerlo el usuario._

`diff` → Recibe dos ficheros como parámetro y compara ambos reportando las diferencias.

`file <file>` : Determina el tipo de archivo (_ASCII_, _Json_, _Data_...).

`strings` → Imprime las secuencias de caracteres legibles de un archivo.
- `-n <int>` : Longitud mínima de la cadena.
- `-s <str>` : Especificar un delimitador entre cadenas encontradas.
- `-f` : Mostrar el nombre del archivo por cada cadena encontrada. En caso de que se reciba por entrada estándar, no indicará el nombre sino `{standard input}`.

$^7$`grep <args> <string> <file>` → Busca cadenas de texto y encuentra coincidencias dentro de un archivo o salida estándar.
- `-i` : *Ignore-case*. No diferencia entre mayúsculas y minúsculas.
    Ej. `grep -i "8B:EF:25:3A:5B:9A" <file>`
- `-n` : Muestra el número o números de línea con las palabra/s filtradas.
- `-r` : *Recursive*. Busca de forma recursiva. Ej. `grep -r "patrón" <dir>/`
- `-E` : Habilita el uso de expresiones regulares (_Regex_)
- `-v` : Muestra lo que no coincide.
- `-w` : Busca palabras exactas. Ej. `grep -w bosque <file>` -> bosque=Si / guardabosque = No.
- `-o` : En la salida estándar únicamente muestra coincidencias ignorando el resto de línea.
- `-q` : *Quiet*. No muestra salida estándar.
- `-c` : *Count*. Mostrar solo el número de coincidencias en lugar de las líneas.
- `-C <lines> / --conext <lines>` : Se utiliza para mostrar un contexto alrededor de las líneas que coinciden con un patrón. Un ejemplo sería `grep --context 2 "patrón" <file>` el cual mostrará dos líneas por encima y por debajo de la coincidencia.
- `-A <lines>` y `-B <lines>` : Muestra un número de líneas dado después (_after_) de la coincidencia o un número concreto de líneas antes (_before_) de la coincidencia.
_Al igual que `cat`, también existe la variante `zgrep` para buscar cadenas en archivos comprimidos._

`egrep` → Es un comando similar a `grep` pero permite buscar dos palabras diferentes. (`egrep -w bosques|plantas /ruta/del/archivo`)

`sort <file>/-` → Ordena el un archivo si se especifica. Si se indica `-` o no nada, lee y ordena el stdout.
- `-f` : Ignora mayúsculas y minúsculas.
- `-r` : Ordena de forma reversa.
- `-n` : Ordena de forma numérica.
- `-u` : Ordena de forma única, ignora duplicados.
- `-h` : Interpreta unidades de tamaño y compara por ellas.
- **Ejemplos de uso:**
	+ `sort messy.txt > sorted.txt` : Guardar contenido ordenado de un archivo en otro.
	+ `ls -l | sort -rh` : Ordenar contenido de un directorio por tamaño mostrando primero los mas grandes.
	+ `sort -nu numbers.txt` : Ordenar de forma numérica el contenido de un archivo descartando duplicados. 

`uniq <file>` → Reportar u omitir líneas repetidas en un archivo o desde stdin. Para que este comando considere un texto repetido, este debe estar en líneas adyacentes. Es por ello que suele utilizarse con el comando `sort`.
- `-u` : Muestra únicamente líneas que aparecen una sola vez.
- `-i` : Ignora mayúsculas y minúsculas (Ignore case).
- `-c` : Muestra un prefijo con el número de ocurrencias encontradas.
- `-d` : Muestra únicamente las líneas duplicadas una vez.
- `-D` : Muestra únicamente las líneas duplicadas tantas veces como estas se repitan.
- `-w <int>` : Compara los x primeros caracteres.
- `-s <int>` : Ignora los primeros x caracteres.
- `-f <int>` : Ignora los primeros x campos (Palabras o cadenas separadas por un espacio).

`base64 <args>` → Codifica o decodifica un archivo o entrada estándar a la salida estándar.
Si no es especificado ningún argumento, lee la entrada estándar.
- `-d` : Decodifica la data.
- `-i` : Ignora caracteres no alfabéticos.
- `-w 0` : Muestra la salida en una única línea.

`tr <args> <str-1> <str-2(opt)>` → Permite reemplazar, eliminar o traducir caracteres en una cadena de texto o en un flujo de datos. Traduce de forma secuencial, sustituyendo cada carácter del conjunto original por el correspondiente en el conjunto de destino. Por ejemplo, `tr 'abcde' '12345'` reemplaza `a` con `1`, `b` con `2`, y así sucesivamente.
Para pasar un archivo lo haremos mediante un redirección del input estándar. →  `tr '[:lower:]' '[:upper:]' < file.txt`
- `-d` : Elimina caracteres dado un estándar input o archivo. No sustituye.
- `-s` : Sustituye secuencias de caracteres repetidos por uno solo.  
- **Ejemplos de uso:**
	+ `echo 'aaaaa' | tr 'a' 'A'` : Sustitución de caracteres.
	+ `echo '123K456' | tr -d 'K'` : Eliminación de caracteres.
	+ `echo 'multiple    spaces' | tr -s ' '` : Sustitución de secuencia de caracteres repetidos por uno solo.
- **Conjuntos de caracteres:**
	+ `[:alpha:]` : Letras.
	+ `[:digit:]` : Dígitos.
	+ `[:alnum:]`: Letras y dígitos.
	+ `[:lower:]` : Letras minúsculas.
	+ `[:upper:]` : Letras mayúsculas.
	+ `[:punct:]` : Signos de puntuación.
	+ `[:blank:]` : Espacios.
	+ `[:space:]` : Espacios y saltos de línea.
	+ `[:xdigit:]` : Hexadecimales.
	+ `a-z`,  `A-Z` y `0-9`. Otra forma de referenciar minúsculas, mayúsculas y dígitos. Por ejemplo: `tr 'a-z' 'A-Z'` (Remplazar minúsculas por mayúsculas). De esta forma también pueden representarse rangos, por ejemplo: `a-e` = `abcde` o `1-5` = `12345`.

`sed <args> <script> <input/file>` → Realiza transformaciones de texto en flujos de datos o archivos de texto. 
*`tr` es más sencillo de usar para realizar tareas de transliteración de caracteres básicas para las cuales a menudo es más eficiente.*
Algunas de las transformaciones más comunes de `sed` son:
**Sustitución:** 
- `sed 's/bar/foo/' file.txt` : Sustituye la primera aparición de `bar` por `foo` en el stdout.
- `sed 's/bar/foo/g' file.txt` : Sustituye todas las apariciones de `foo` por `bar` en el stdout.
**Eliminación:**
- `sed '/bar/d' file.txt` : Elimina todas las coincidencias que coinciden con el patrón en el stdout.
**Agregación:**
- `sed 's/^/ bar/' file.txt` : Agregar texto al principio de cada línea. `^` es la etiqueta de principio de línea.
- `sed 's/$/ foo/' file.txt` : Agregar texto al final de cada línea. `$` es la etiqueta de fin de línea. 
**Parámetros:**
- `-e` : Permite especificar múltiples transformaciones en una sola línea. 
  *Hay que especificar `-e` por cada transformación a aplicar.*
  `sed -e 's/bar/foo/' -e 's/foo/bar/' file.txt`
- `-i` : Este parámetro indica que `sed` guardará los cambios en vez de mostrarlos en stdout.
  *Es posible realizar una copia de seguridad del archivo antes de aplicar los reemplazos mediante `-i` añadiendo un sufijo. `sed -i.bak 's/bar/foo/g' file.txt` guardará el archivo original como `file.txt.bak` y `file.txt` será el archivo reemplazado.*
El comando `sed` es muy extenso y ofrece muchas mas opciones de transformación. → [Guía sed](https://www.gnu.org/software/sed/manual/sed.html)

`rev` → Invierte el orden de forma reversa de cada línea dado un input estándar o pasando un archivo como argumento. 
*La principal diferencia con `sort -r` es que este **no ordena** antes de revertir el orden de las líneas.*
- `cat file.txt | rev`
- `rev file.txt`

##### 2.5 Archivar, comprimir y descomprimir archivos

Existen varios métodos para comprimir y descomprimir archivos. Cada uno tiene sus ventajas y desventajas frente a los tipos de archivos. Siendo algunos más eficientes a la hora de reducir el tamaño con determinados tipos de archivos.

`tar`  (`tar <args> <file/dir/>`) → Son las siglas de _tape archive_. Se utiliza para crear archivos de archivo y extraer los archivos de archivo.
- `-c` : Crea un nuevo archivo _tar_ agrupando juntos ficheros y directorios.
- `-x` : Extrae ficheros y directorios de un archivo existente.
- `-f` : Especifica el nombre del fichero que se va a crear o del que se va a extraer. 
- `-t` : Lista el contenido de un archivo comprimido.
- `-u` : Añade archivos y directorios a un comprimido existente.
- `-r` : Añade o actualiza archivos y directorios a un comprimido existente sin recrear este.
- `-v` : Modo verboso. Muestra información detallada en el proceso.
- `-z` : Utiliza compresión `gzip`.
- `-j` : Utiliza compresión `bzip2`.
- `-W` : Verifica la integridad del archivo asegurando que este no esté corrupto.

`gzip <args> <file/dir/>` → Únicamente comprime archivos y no directorios.
- `gzip file.txt` : Comprimir el archivo `file.txt` que pasará a `file.txt.gz`.
- `gzip -d file.txt.gz` / `gunzip file` : Descomprimir el archivo `file.txt.gz` que pasará a `file.txt`.
- `gzip -r dir/` : Comprime todos los archivos del interior de un directorio y subdirectorios del primero de forma recursiva. El comando `gzip -rd dir/` hará lo mismo pero al revés (descomprimiendo).
- `gzip -k file.txt` : Comprime conservando el archivo original.

`bzip2 <args> <file/dir/>` → Mismo funcionamiento y sintaxis que _gzip_
- `bzip2 file.txt` : Comprimir el archivo `file.txt` que pasará a `file.txt.bz2`.
- `bzip2 -d file.bz2` / `bunzip2 file.bz2`: Descomprimir el archivo `file.txt.bz2` que pasará a `file.txt`.
- `bzip2 -r dir/` : Comprime todos los archivos del interior de un directorio y subdirectorios del primero de forma recursiva.
- `bzip2 -k file.txt` : Comprime conservando el archivo original.

`xz <args> <file/dir/>`
- `unxz` : descomprimir el archivo

`7z` → 

`xargs` → Se utiliza para tomar una lista de elementos (por lo general, obtenida a través de la salida de otro comando) y ejecutar un comando en cada uno de esos elementos de manera iterativa.
- `-d` : Delimita los input mediante caracteres especificados.
- `-I <str>` : Reemplaza ocurrencias de un string, normalmente indicado como `{}`. 

**Ejemplos de uso:**
+  `find . -name "*.tmp" | xargs rm`. En este ejemplo, buscará todos los archivos temporales y borrará cada uno de ellos.
+ `cat files.txt | xargs -I {} cp {} /ruta/destino`. Leer lista de archivos y copiar cada uno de ellos a una ruta destino. *`xargs` toma cada argumento y lo sustituye por la cadena que le indiquemos con el parámetro `-I` y en el siguiente comando sustituirá la cadena por los argumentos en la posición de `{}`**.
+ `sudo find ./ -name ".sh" | xargs -I {} chown root:root ~{}`. Procesamiento por lotes el cual cambia el propietario de archivos según su extensión en un directorio. 
+ `find dir/ -type -f -name ".txt" | xargs -P 4 -I {} gzip {}`. Ejecución paralela. El parámetro `-P` indica el número de procesos en paralelo que se ejecutarán a la hora de comprimir cada uno de los archivos.
+ El comando `find` con la opción de -exec ejecutará un comando pero si este fallase devolvería igualmente un código de estado 0. Es donde `xargs` es extremadamente útil si es necesario saber el resultado del comando ejecutado mediante su código de estado. `find ./ -type f -iname "*.json" -print0 | xargs -0 -I {} sh -c 'jq empty "{}"'`
`nc <args> <host> <port>` (netcat) → 

`curl` -> Es una herramienta muy potente de línea de comandos, utilizada para transferir datos desde o hacia un servidor, utilizando diversos protocolos como HTTP, HTTPS, FTP, entre otros.

**Opciones más relevantes**:
- `-X`, `--request <method>`: Especifica el método HTTP a utlizar (GET, POST, PUT, DELETE, etc.)
- `-d`, `--data <data>`: Envía datos en una solicitud POST.
- `-H`, `--header <header>`: Permite añadir un encabezado personalizado a la solicitud.
- `-o`, `--output <file>`: Guarda el contenido de la respuesta en un archivo.
- `-L`, `--location`: Sigue las redirecciones HTTP automáticamente.
- `-u`, `--user <user:password>`: Especifica el nombre de usuario y contraseña para autenticación.
- `-v`, `--verbose`: Muestra detalles adicionales de la operación, útil para la depuración.
- `-i`, `--include`: Incluye los encabezados HTTP en la salida.
- `-s`, `--silent`: Modo silencioso; no muestra el progreso ni los mensajes de error.
- `-S`, `--show-error`: Muestra los errores incluso cuando `-s` se haya especificado.
- `-k`, `--insecure`: Permite conexiones a servidores con certificados SSL no verificados.
- `-b`, `--cookie <data|filename>`: Envía cookies desde un archivo o cadena.
- `-c`, `--cookie-jar <filename>`: Fuarda las cookies en un archivo después de la operación.
- `-I`, `--head`: Muestra solo la información del encabezado del documento.
- `-T`, `--upload-file <file>`: Sube un archivo al servidor destino.
- `-G`, `--get`: Convierte datos POST en parámetros de URL y usa el método GET.
- `-C`, `--continue-at <offset>`: Continúa una descarga en el punto donde se interrumpió.
- `--compressed`: Solicita una respuesta comprimida del servidor.
- `--retry <num>`: Reintenta la solicitud un número de veces.
- `--max-time <seconds>`: Tiempo máximo permitido para la transferencia.
- `--rate <max-request-rate>`: Limita la tasa de transferencia.
- `--interface <name>`: Utiliza una interfaz de red específica para la solicitud.

Para mas información de todas las posibilidades que ofrece -> `curl --help all`

```bash
systemctl list-units --type=service --state=failed
```
```bash
systemctl list-units --type=service --state=running
```
`base64 <args>`



`nmap` : Comando cojonudo!

       \\     backslash

       \a     alert (BEL)

       \b     backspace

       \c     produce no further output

       \e     escape

       \f     form feed

       \n     new line

       \r     carriage return

       \t     horizontal tab

       \v     vertical tab

       \0NNN  byte with octal value NNN (1 to 3 digits)

Montar una carpeta remota mediante ssh en la máquina local. (sshfs)
Neceista instalarse previamente en maquina local.
sshfs user@address:/path/to/folder /local/path

`dpkg-reconfigure tzdata` Configurar la hora del servidor (Zona horaria)

`ip link set dev <iface> down` -> Apagar interfaz
`ip link set dev <iface> up` -> Levantar interfaz


true && { echo success;} || { echo failed; } -> `ping -c1 machine && { echo success;log-timestamp.sh }|| { echo failed; email-admin.sh; }`


`lsof` Importante añadir a manual

apt-cache policy es-webserver -> ver las versiones de este paquete (es-webserver)

/bin/false -> Retorna un codigo de estado falso, negativo, erroneo (1)
/bin/true -> Retorna un código de estado verdadero (0)


free -h => Consultar cantidad de memoria instalada, utilizada y disponible
