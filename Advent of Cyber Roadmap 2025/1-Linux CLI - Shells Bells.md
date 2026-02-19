
Introduction

![[Pasted image 20251201164334.png]]

Lo impensable ha sucedido: McSkidy ha sido secuestrada. Sin ella, las defensas de Wareville flaquean y la Navidad misma pende de un hilo. Pero el pánico no salvará la temporada. Queda un largo camino por delante para descubrir qué sucedió realmente. El equipo de TBFC (La Mejor Compañía de Festivales) ya está pensando en qué hacer a continuación, y su primera pista apunta a tbfc-web01, un servidor Linux que procesa listas de deseos navideños. En algún lugar de sus datos podría estar la verdad: rastros de las últimas acciones de McSkidy, o quizás las pistas sobre la retorcida visión del Rey Malhare para EASTMAS.

![[Pasted image 20251201164401.png]]

Objetivos de aprendizaje
Aprender los conceptos básicos de la interfaz de línea de comandos (CLI) de Linux
Explorar su uso para objetivos personales y administración de TI
Aplicar sus conocimientos para desvelar los misterios navideños
Conexión a la máquina

Antes de continuar, revise las preguntas de la tarjeta de conexión que se muestra a continuación:

![[Pasted image 20251201164429.png]]

Inicie el laboratorio haciendo clic en el botón "Iniciar máquina" a continuación. La máquina se iniciará en vista dividida y tardará unos dos minutos en cargarse. Si la máquina no está visible, haga clic en el botón "Mostrar vista dividida" en la parte superior de la página. Una vez cargada, aparecerá una ventana de terminal: su CLI de Linux. ¡Deberá escribir los comandos allí!

![[Pasted image 20251201164508.png]]

Alternativamente, puede utilizar las credenciales a continuación para conectarse a la máquina de destino a través de SSH desde su propia máquina conectada a THM VPN:

![[Pasted image 20251201164530.png]]


---

**==Linux CLI==**

**Trabajando con la CLI de Linux**

- ¡Pero el servidor no tiene interfaz gráfica (GUI)! ¿Cómo buscaremos pistas?
- ¿Quién necesita una GUI cuando tenemos una terminal de línea de comandos de Linux? ¡Es aún mejor!

Linux cuenta con una potente interfaz de línea de comandos que permite usar y administrar el sistema simplemente escribiendo comandos en el teclado. No es tan difícil como parece; una vez que te acostumbres, quizá te guste más la CLI que la interfaz gráfica. Además, la mayoría de los expertos en TI y ciberseguridad trabajan con la CLI a diario, ¡así que comencemos a aprender!

- Para ejecutar tu primer comando de la CLI, escribe ``echo "Hello World!"`` y pulsa Intro. Esto hará un ``echo`` del texto.
- Luego, escribe ``ls`` para listar el contenido del directorio actual. Este comando te mostrará los archivos de McSkidy.
- Después, escribe ``cat README.txt`` para mostrar el contenido del archivo. Verás su contenido en la salida a continuación.

![[Pasted image 20251201164633.png]]

**Navegando por el sistema de archivos**

Parece que McSkidy dejó una guía de seguridad antes de ser secuestrado. ¡Sería de gran ayuda! Quizás hayas visto el directorio "Guides" la última vez que ejecutaste ``ls``; probablemente sea el directorio que necesitamos. Tu experiencia con la CLI comenzó en el directorio de inicio de McSkidy (puedes verificarlo ejecutando ``pwd``), pero ahora cambiemos al directorio de guías.

Cambia de directorio ejecutando ``cd Guides``. Aparecerás en ``/home/mcskidy/Guides``.
Ejecuta el comando ``ls`` de nuevo para ver el contenido del directorio de guías (estará vacío).

![[Pasted image 20251201164821.png]]

**Buscando la Guía Oculta**

¡Vaya! Parece que las guías no están. ¿O sí? En Linux, los archivos y directorios se pueden ocultar a simple vista si empiezan con un punto (p. ej., ``.secret.txt``). Esta función suele ser utilizada por administradores de TI para ocultar archivos del sistema, por atacantes para ocultar malware y, ahora, por McSkidy para ocultar la valiosa guía de los malos.

- Vuelve a ver el directorio ejecutando ``ls -la``. El indicador ``-a`` muestra los archivos ocultos. El indicador ``-l`` muestra detalles adicionales, como los permisos y el propietario del archivo.
- Lee la guía oculta ejecutando ``cat .guide.txt``. No olvides el punto inicial.

![[Pasted image 20251201164842.png]]

**Explorando los registros**

En su guía, McSkidy hace referencia a ``/var/log/``, un directorio de Linux donde se almacenan todos los eventos de seguridad (registros). De hecho, cualquier analista de SOC en TBFC confirmará que la mejor manera de encontrar conejos malvados es revisar los registros. Los archivos de registro suelen ser muy grandes, y revisarlos con ``cat`` no es lo ideal. Por lo tanto, usemos ``grep``, un comando para buscar un texto específico dentro de un archivo.

Navegue al directorio de registros con ``cd /var/log`` y explore su contenido con ``ls``.
Ejecute ``grep "Failed password" auth.log`` para buscar los inicios de sesión fallidos dentro de ``auth.log``.

![[Pasted image 20251201164903.png]]

![[Pasted image 20251201164926.png]]

**Encontrando los Archivos**

Puedes ver muchos inicios de sesión fallidos en la cuenta "socmas", ¡todos desde la ubicación HopSec! Claramente intentaban acceder a SOC-mas, la plataforma de pedidos navideños de Wareville. ¿Y si alguien dejó malware allí? Sigamos la guía de McSkidy y busquemos Eggsploits y Eggshells con ``find``, un comando que busca archivos con parámetros específicos, como ``-name``:

- Ejecuta ``find /home/socmas -name *egg*`` para buscar "eggs" en el directorio de inicio de socmas.
- Ten en cuenta que ``find`` es un comando potente. Consulta su [documentación](https://man7.org/linux/man-pages/man1/find.1.html) para más detalles.

![[Pasted image 20251201164957.png]]

**Analizando Eggstrike**

¡Parece que has encontrado algo, ``eggstrike.sh``! Los archivos con la extensión ``.sh`` contienen comandos CLI y se denominan scripts de shell. Estos scripts son utilizados tanto por equipos de TI para automatizar tareas como por atacantes para ejecutar rápidamente comandos maliciosos. Veamos el contenido del script sospechoso e intentemos comprenderlo:

![[Pasted image 20251201165021.png]]

1. Las líneas que empiezan con ``#`` son solo comentarios y no son los comandos reales.
2. El comando `cat wishlist.txt | sort | uniq` enumera los artículos únicos del archivo `wishlist.txt`.
3. El comando envía la salida (pedidos únicos) al archivo `/tmp/dump.txt`.
4. El comando `rm wishlist.txt` elimina el archivo de la lista de deseos (que contiene los deseos navideños).
5. El comando `mv eastmas.txt wishlist.txt` reemplaza el archivo original con `eastmas.txt`.

**Características de la CLI**

¡El script de Eggstrike que leíste parece estar robando felicitaciones navideñas y reemplazándolas con las falsas! Quizás hayas notado que los comandos del script son un poco complejos, pero no es inusual, ya que el autor del script es nada menos que Sir Carrotbane, el líder del equipo rojo de HopSec. Exploremos los símbolos especiales a continuación:

| Special Symbol             | Description                                                | Example                                             |
| -------------------------- | ---------------------------------------------------------- | --------------------------------------------------- |
| Pipe symbol (``\|``)       | Send the output from the first command to the second       | `cat unordered-list.txt \| sort \| uniq`            |
| Output redirect (`>`/`>>`) | Use `>` to overwrite a file, and `>>` to append to the end | `some-long-command > /home/mcskidy/output.txt`      |
| Double ampersand (`&&`)    | Run the second command if the first was successful         | `grep "secret" message.txt && echo "Secret found!"` |

## Sir Carrotbane Attacks

![[Pasted image 20251201165124.png]]

Ahora está claro que el servidor ha sido vulnerado y la lista de deseos de Navidad ha sido reemplazada por una de EASTMAS. Aunque no has encontrado ninguna pista de lo que le ocurrió a McSkidy, al menos sabes que los atacantes estaban allí. Puedes ver cómo Sir Carrotbane reemplazó la lista de deseos visitando http://MACHINE_IP:8080 desde el navegador web de la máquina virtual. Puedes abrirlo haciendo clic en el icono de Firefox en el escritorio.

**Utilidades del sistema**

Hay cientos de comandos CLI para ver y administrar tu sistema. Por ejemplo, ``uptime`` para ver cuánto tiempo lleva funcionando el sistema, ``ip addr`` para comprobar tu dirección IP y ``ps aux`` para listar todos los procesos. También puedes comprobar los nombres de usuario y las contraseñas hash de usuarios, como McSkidy, ejecutando ``cat /etc/shadow``. Sin embargo, necesitarás permisos de root para hacerlo.

![[Pasted image 20251201165149.png]]

**Usuario root**

El usuario root es el usuario predeterminado de Linux, con capacidad para realizar cualquier acción en el sistema. Puedes cambiarlo a root con ``sudo su`` y regresar a McSkidy con el comando ``exit``. Solo el usuario root puede abrir ``/etc/shadow`` y editar la configuración del sistema, por lo que suele ser un objetivo principal para los atacantes. Si en algún momento quieres verificar tu usuario actual, ¡simplemente ejecuta ``whoami``!

- Cambia al usuario root ejecutando el comando ``sudo su``.
- Puedes verificar tu usuario actual ejecutando ``whoami``.

![[Pasted image 20251201165219.png]]

**Historial de Bash**

¿Sabías que cada comando que ejecutas se guarda en un archivo de historial oculto, también llamado historial de Bash? Se encuentra en el directorio personal de cada usuario: ``/home/mcskidy/.bash_history`` para McSkidy y ``/root/.bash_history`` para root. Puedes consultarlo con el práctico comando ``history`` o leer los archivos directamente con ``cat``. ¡Comprobemos si Sir Carrotbane y sus conejos malos dejaron rastro en el historial!

- Familiarízate con el historial de Bash ejecutando el comando ``history``.
- Ten en cuenta que tus comandos también se guardan en un archivo (``cat .bash_history``).

![[Pasted image 20251201165249.png]]

**Answer the questions below**

Which CLI command would you use to list a directory?

Respuesta:  ls

What flag did you see inside of the McSkidy's guide?

Respuesta:  THM{learning-linux-cli}

![[Pasted image 20251201170057.png]]

Which command helped you filter the logs for failed logins?

Respuesta:  grep

What flag did you see inside the Eggstrike script?

Respuesta:  THM{sir-carrotbane-attacks}

![[Pasted image 20251201171053.png]]

Which command would you run to switch to the root user?

Respuesta:  sudo su

Finally, what flag did Sir Carrotbane leave in the root bash history?

Respuesta:  THM{until-we-meet-again}

![[Pasted image 20251201172121.png]]

For those who consider themself intermediate and want another challenge, check McSkidy's hidden note in `/home/mcskidy/Documents/` to get access to the key for **Side Quest 1**!

No necesita respuesta

nos movemos a la carpeta dada
![[Pasted image 20251201172732.png]]
leemos el archivo 
![[Pasted image 20251201172910.png]]
en el mensaje nos dan las credenciales de una cueta de usuario, iniciamos sesion en la cuenta
![[Pasted image 20251201175239.png]]
nos moveremos al directorio donde dejaron otra nota 
![[Pasted image 20251201175424.png]]
listanamos y leemos el contenido de los archivos
![[Pasted image 20251201180657.png]]
el segundo archivo tiene doble extension y la principal es la .gpg que es una encriptacion
![[Pasted image 20251201180737.png]]
vamos a buscar los tres huevos para encontrar la llave para descrifrar el archivo







Enjoyed investigating in a Linux environment? Check out our [Linux Logs Investigations](https://tryhackme.com/room/linuxlogsinvestigations) room for more like this!

No necesita respuesta