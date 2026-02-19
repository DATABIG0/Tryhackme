
**Introduction**

Ante las recientes amenazas de ciberseguridad contra The Best Festival Company (TBFC), el equipo rojo local ha programado varias pruebas de penetración. Los miembros del equipo rojo realizaron pruebas de penetración periódicas contra su TBFC. Parte de este ejercicio consiste en garantizar que los empleados sean diligentes al hacer clic en enlaces y que la empresa esté bien protegida contra los últimos ataques de phishing. Este tipo de phishing autorizado es una forma comprobada de comprobar si la formación en ciberseguridad ha dado sus frutos.

En esta tarea, formarás parte del equipo rojo local de TBFC junto con los elfos Recon McRed, Exploit McRed y Pivot McRed. Les ayudarás a planificar y ejecutar su campaña de phishing. Es hora de determinar si se requiere más formación en ciberseguridad.

Objetivos de aprendizaje

- Comprender qué es la ingeniería social
- Aprender los tipos de phishing
- Explorar cómo los equipos rojos crean páginas de inicio de sesión falsas
- Usar el kit de herramientas de ingeniería social para enviar un correo electrónico de phishing


Conexión a la máquina

Antes de continuar, revisa las preguntas de la tarjeta de conexión que se muestra a continuación:

![[Pasted image 20251202163643.png]]


Inicie su máquina virtual de destino haciendo clic en el botón "Iniciar máquina" a continuación. La máquina tardará unos 2 minutos en arrancar por completo. Además, inicie su AttackBox haciendo clic en el botón "Iniciar AttackBox" a continuación. AttackBox se iniciará en vista dividida. Si no puede verla, haga clic en el botón "Mostrar vista dividida" en la parte superior de la página.

![[Pasted image 20251202163704.png]]

---

==**Phishing Exercise for TBFC**==

**Ingeniería social**

La ingeniería social se refiere a manipular a un usuario para que cometa un error. Ejemplos de estos errores incluyen compartir una contraseña, abrir un archivo malicioso y aprobar un pago. El término "social" significa que el objetivo de este tipo de ataque son seres humanos, no sistemas informáticos. Por lo tanto, el atacante recurre a trucos psicológicos para lograr la cooperación del usuario objetivo. Algunos factores psicológicos que pueden desempeñar un papel clave en el éxito de estos ataques son la urgencia, la curiosidad y la autoridad. Por eso, algunos se refieren a la ingeniería social como "hackeo humano".

![[Pasted image 20251202175915.png]]

**Phishing**

El phishing es un subconjunto de la ingeniería social en el que el medio de comunicación son principalmente mensajes. En su momento, los ataques de phishing más comunes se realizaban por correo electrónico; sin embargo, la proliferación de smartphones, junto con el acceso omnipresente a internet, ha extendido el phishing a mensajes de texto cortos (smishing), llamadas de voz (vishing), códigos QR (quishing) y mensajes directos en redes sociales. El objetivo del atacante es que el usuario haga clic, abra o responda a un mensaje para robarle información, dinero o acceso.

Desafortunadamente, los ataques de phishing son cada vez más difíciles de detectar. Incluso las personas más precavidas pueden ser víctimas de estos ataques si no actúan con la debida precaución. La formación en ciberseguridad de TBFC enseña a los usuarios dos mnemotécnicas antiphishing escritas como S.T.O.P. La primera es de[ All Things Secured](https://www.allthingssecured.com/tips/email-phishing-scams-stop-method/), que indica a los usuarios que se hagan las siguientes preguntas antes de responder a un correo electrónico:

- ¿Sospechoso?
- ¿Me pide que haga clic en algo?
- ¿Me ofrece una oferta increíble? 
- ¿Me estás presionando para que haga algo ahora?

El segundo S.T.O.P. recuerda a los usuarios que sigan las siguientes instrucciones:

- Tranquilo. Los estafadores se dejan llevar por la adrenalina.
- Escribe la dirección tú mismo. No uses el enlace del mensaje.
- No abras nada inesperado. Verifica primero.
- Comprueba quién es el remitente. Comprueba la dirección/número de remitente real, no solo el nombre para mostrar.

Tras horas de formación periódica en ciberseguridad, el equipo rojo comprueba si el personal de TBFC puede esquivar correos electrónicos sospechosos.

**Construyendo la trampa**

Debes sonar muy convincente como experto en pruebas de penetración para que un ataque de phishing tenga éxito. No solo importa cómo escribas el correo o los mensajes de phishing, sino también cómo prepares la trampa para el objetivo. La trampa puede ser cualquier cosa, dependiendo de tus objetivos y de la investigación que realices sobre el objetivo. A veces, los atacantes intentan comprometer el equipo del objetivo, y lo consiguen adjuntando un archivo malicioso a su correo electrónico de phishing. Los atacantes a veces crean una página web que imita una página de inicio de sesión legítima para robar las credenciales del objetivo.

En esta tarea, buscamos obtener las credenciales de inicio de sesión del usuario objetivo. Nuestra trampa sería una página de inicio de sesión falsa del portal TBFC, que adjuntamos al correo electrónico de phishing y enviamos al objetivo. Sin embargo, una página de inicio de sesión por sí sola no es suficiente. Necesitamos alojarla e implementar cierta lógica para capturar las credenciales ingresadas por el objetivo. Para facilitar su tarea, ya hemos configurado un script que, al ejecutarse, alojará una página de inicio de sesión falsa. Esta página de inicio de sesión falsa que creamos capturará todas las credenciales ingresadas en la página.

El script ya está ubicado en AttackBox en ~/Rooms/AoC2025/Day02. Si desea usar su propio equipo conectado a THM VPN, puede descargar el script mediante el botón "Descargar archivos de tarea" que aparece a continuación. Asegúrese de mantener ambos archivos en el mismo directorio.

Para ejecutar el script, use ./server.py y comenzará a escuchar las credenciales. Si el objetivo es interceptado e ingresa las credenciales, se mostrarán en la misma terminal.

![[Pasted image 20251202180054.png]]

El mensaje anterior indica que la aplicación web de phishing está escuchando en el puerto 8000; además, el puerto 0.0.0.0 implica que está vinculada a todas las interfaces. Para confirmar lo que verá el usuario, use Firefox en AttackBox y navegue a http://CONNECTION_IP:8000 o http://127.0.0.1:8000; cualquiera de estas direcciones le mostrará lo que verá el usuario. Con esto configurado, es hora de enviar este enlace por correo electrónico para comprobar la vigilancia de nuestros usuarios.

**Envío mediante el kit de herramientas de ingeniería social (SET)**

Una vez que nuestra página de phishing esté lista, podemos preparar y enviar el correo electrónico de phishing a nuestros usuarios objetivo. Enviarlo desde nuestro correo electrónico personal es la peor idea. Idealmente, el correo electrónico debería parecer provenir de un remitente aparentemente legítimo; por ejemplo, podemos fingir ser alguien en quien el usuario objetivo confía o de quien espera recibir dicho correo. Cuanto más realista parezca un correo electrónico de phishing, más probable será que el usuario objetivo lo crea y sea víctima de phishing. La pregunta es cómo podemos enviar un correo electrónico de apariencia realista que contenga nuestra página de inicio de sesión falsa.

Una solución es usar el kit de herramientas de ingeniería social ([SET](https://github.com/trustedsec/social-engineer-toolkit)). Es una herramienta de código abierto diseñada principalmente por David Kennedy para ataques de ingeniería social. Ofrece una amplia gama de funciones. En particular, permite redactar y enviar un correo electrónico de phishing. En este caso, usaremos esta herramienta para crear y enviar un correo electrónico de phishing al usuario objetivo.

Comencemos a crear el correo electrónico de phishing mediante la herramienta SET. Antes de usar esta herramienta, recuerde que consta de varios pasos, cada uno con preguntas diferentes sobre el correo electrónico de phishing que desea enviar. Por lo tanto, tenga paciencia y siga el proceso.

Para iniciar la herramienta, escriba "setoolkit" en la terminal y se le mostrará un menú con varias opciones. En la parte inferior, verá "set>", donde puede introducir el número de opción deseado. En nuestro caso, seleccionaríamos la opción 1 (Ataques de Ingeniería Social). Si se equivoca en algún momento, la opción 99 le devolverá al menú principal, donde podrá volver a empezar. Sin embargo, si comete algún error al escribir el correo electrónico de phishing, deberá presionar Ctrl + C para volver al menú principal. Los ataques de ingeniería social abarcan diversos tipos de ataques, desde phishing selectivo y correo masivo hasta ataques a puntos de acceso inalámbricos.

![[Pasted image 20251202180202.png]]

Al seleccionar 1, se mostrará otro menú con el tipo de ataque de ingeniería social que queremos usar. En este caso, seleccionaremos "Ataque de correo masivo" escribiendo 5.

![[Pasted image 20251202180223.png]]

Ahora, se nos pedirá que elijamos entre dos opciones. Una nos permite enviar el correo electrónico de phishing a una sola dirección, mientras que la otra nos permite enviarlo a varias personas. En este caso, seleccionaríamos la opción 1: "Ataque de correo electrónico a una sola dirección".

![[Pasted image 20251202180308.png]]

Ahora, tendremos varias preguntas que responder y varios campos que completar. El primer grupo de preguntas se refiere a las direcciones de correo electrónico y cómo se enrutará y entregará el correo. Después de cada entrada, podemos presionar Enter para pasar a la siguiente pregunta.

- Enviar correo electrónico a: Empecemos por dirigirnos a factory@wareville.thm
- Cómo enviar el correo electrónico: Elegiremos "Usar su propio servidor" o "Open Relay"
- Dirección de remitente: Sabemos que el personal de la fábrica de juguetes se comunica regularmente con Flying Deer, la empresa de transporte, por lo que usaremos updates@flyingdeer.thm como dirección de correo electrónico de origen
- Nombre de remitente: Usaremos el nombre Flying Deer
- Nombre de usuario para open-relay: Lo dejaremos en blanco y simplemente presionaremos Enter
- Contraseña para open-relay: Lo dejaremos en blanco y simplemente presionaremos Enter
- Dirección del servidor de correo electrónico SMTP: Enviaremos el correo directamente al servidor de correo de TBFC ingresando MACHINE_IP
- Número de puerto del servidor SMTP: Dejamos el valor predeterminado de 25 y simplemente pulsamos Intro.

El siguiente grupo de preguntas le preguntará si desea enviarlo con alta prioridad o adjuntar un archivo.

- Marcar este mensaje como alta prioridad: La decisión es suya, según su conocimiento de las circunstancias, pero responderemos "no".
- ¿Desea adjuntar un archivo?: Responderemos "n".
- ¿Desea adjuntar un archivo en línea?: De nuevo, respondamos "n".

Finalmente, elegimos un asunto del correo electrónico e ingresamos el contenido del mensaje en texto plano o HTML.

- Asunto del correo electrónico: Necesitamos algo convincente, por ejemplo, "Cambios en el horario de envío".
- Enviar el mensaje en HTML o sin formato: Mantenemos la opción predeterminada de texto plano y simplemente pulsamos Intro.
- Ingrese el cuerpo del mensaje y escriba "END" (en mayúsculas) al terminar: Cree y escriba un mensaje convincente. Asegúrese de incluir la URL http://CONNECTION_IP:8000 para comprobar si el destinatario cae en esta trampa. 

En la terminal a continuación se muestra un ejemplo de interacción.

![[Pasted image 20251202180500.png]]

Ahora, el correo electrónico de phishing se ha enviado al objetivo. El botón "Presione ``<return>`` para continuar" es simplemente la tecla Enter para reiniciar la herramienta. Abra la terminal donde se ejecuta nuestro script server.py para ver si el usuario es interceptado e ingresa sus credenciales.

Nota: Puede que tenga que esperar de 1 a 2 minutos y observar la terminal para ver si el usuario ha ingresado alguna credencial.

Para sorpresa del equipo rojo de TBFC, recibieron al menos un conjunto de credenciales que funcionaban. Este resultado es alarmante; significa que un adversario podría tener éxito en un ataque similar si aún no lo ha hecho. Considerando las credenciales recibidas, si un adversario obtiene dicho acceso, podría fácilmente destruir todo el sistema de entrega de regalos. Es vital verificar si se ha producido un ataque de este tipo y actuar en consecuencia.

**Answer the questions below**

What is the password used to access the TBFC portal?

Respuesta:  unranked-wisdom-anthem

Browse to `http://MACHINE_IP` from within the AttackBox and try to access the mailbox of the `factory` user to see if the previously harvested `admin` password has been reused on the email portal. What is the total number of toys expected for delivery?

Respuesta:  1984000

If you enjoyed today's room, feel free to check out the [Phishing Prevention](https://tryhackme.com/room/phishingemails4gkxh) room.

No necesita respuesta.

![[Pasted image 20251202181657.png]]

![[Pasted image 20251202181711.png]]

![[Pasted image 20251202181936.png]]
seleccionamos la opcion 1
![[Pasted image 20251202181919.png]]
nos aparecera lo siguiente
![[Pasted image 20251202182120.png]]
seleccionamos la opcion 5
![[Pasted image 20251202182239.png]]
seleccionamos la opcion 1
![[Pasted image 20251202182345.png]]
acontinuacion nos saldra el primer grupo de preguntas
![[Pasted image 20251202182711.png]]segundo grupo de preguntas
![[Pasted image 20251202182842.png]]
tercer grupo
![[Pasted image 20251202183344.png]]
todo junto
![[Pasted image 20251202183410.png]]
al finalizar con setoolkit nos dirigimos a nuestra terminal donde se ejecuta el script.py y esperamos hasta que captura unas credenciales
![[Pasted image 20251202183716.png]]
navegamos a la pagina  de fabrica y accedemos con las credenciales
![[Pasted image 20251202183933.png]]
![[Pasted image 20251202184725.png]]
logramos acceder
![[Pasted image 20251202184751.png]]
leemos el correo de las unidades
![[Pasted image 20251202184834.png]]
y vemos que nuestro correo llego
![[Pasted image 20251202184856.png]]


