
Introduction

The Story

Desde la desaparición de McSkidy, las defensas de TBFC se han debilitado y la Plataforma de Protección de Correo Electrónico (SOC) ha caído.

Con los filtros desconectados, el personal debe clasificar manualmente cada mensaje sospechoso.
El equipo SOC sospecha que los Eggsploit Bunnies de Malhare han enviado mensajes de phishing a los usuarios de TBFC para robar credenciales e interrumpir las SOC-mas.

![[Pasted image 20251213111400.png]]

Te has unido al Grupo de Trabajo de Respuesta a Incidentes para ayudar a identificar qué correos electrónicos son legítimos o intentos de phishing.

Pero ten cuidado, algunos intentos de phishing son astutos y se disfrazan de operaciones rutinarias de TBFC, inscripciones de voluntarios o logística del evento SOC-mas. Cada llamada equivocada podría acercar a Wareville un paso más a la realización de EAST-mas.

**Objetivos de aprendizaje**

- Detección de correos electrónicos de phishing
- Aprender las técnicas de phishing más populares
- Comprender las diferencias entre spam y phishing

Inicie el equipo de destino haciendo clic en el botón "Iniciar equipo" que aparece a continuación. El equipo tardará entre 2 y 3 minutos en iniciarse por completo. A continuación, puede acceder al Inspector de amenazas de correo electrónico de Wareville en https://LAB_WEB_URL.p.thmlabs.com.

Nota: Si recibe un error 502 al acceder al enlace, espere un poco más para que el equipo se inicie por completo.

Answer the questions below

I have access to the Wareville Email Threat Inspector!

No answer needed


---

# Spotting Phishing Emails

## Resumen del phishing

El phishing puede ser uno de los trucos cibernéticos más antiguos, pero sigue siendo uno de los más efectivos. A medida que empresas como TBFC refuerzan sus defensas con filtros de correo electrónico avanzados y herramientas de seguridad, los atacantes han evolucionado sus tácticas para ir un paso por delante.

El phishing moderno se centra en la precisión y la persuasión. Los mensajes se elaboran cuidadosamente, a menudo imitando a personas reales, portales o procesos internos para engañar incluso a los usuarios más precavidos.

Intenciones comunes de los mensajes de phishing:

- **Robo de credenciales:** Engañar a los usuarios para que revelen contraseñas o datos de inicio de sesión.
- **Distribución de malware:** Disfrazar archivos adjuntos o enlaces maliciosos como contenido seguro.
- **Exfiltración de datos:** Recopilación de información confidencial de la empresa o personal.
- **Fraude financiero:** Persuadir a las víctimas para que transfieran dinero o aprueben facturas falsas.

![[Pasted image 20251213114017.png]]

En la imagen de arriba, podemos ver un ejemplo de mensaje de phishing de un atacante que intenta hacerse pasar por un empleado utilizando un dominio gratuito (gmail.com) para modificar su nómina y cometer fraude financiero.

Con los perímetros corporativos fuertemente fortificados, el phishing sigue siendo la vía más fácil para el acceso inicial. Se dirige a la única vulnerabilidad que la tecnología no puede solucionar: las personas. Incluso en Wareville, un solo correo electrónico convincente de las Eggsploit Bunnies podría abrir las puertas a EAST-mas.

## ¿Por qué el spam no es phishing?

El spam es simplemente ruido digital: molesto, pero en su mayoría inofensivo. El phishing, sin embargo, es un ataque de precisión, en este caso de las Eggsploit Bunnies de Malhare, diseñado para engañar a los empleados de TBFC y abrir una vía de escape a las defensas de la empresa.

El spam prioriza la cantidad sobre la precisión. A diferencia del phishing, cuyo objetivo es engañar a usuarios específicos, los mensajes de spam se envían masivamente para inundar las bandejas de entrada con marketing no deseado o contenido irrelevante. Su objetivo no suele ser robar datos, sino aumentar la visibilidad o la interacción.

Intenciones comunes tras los mensajes de spam:

- **Promoción:** Publicidad de productos, servicios o eventos. A menudo, no solicitados o de baja calidad.
- **Estafas:** Difundir ofertas falsas o estrategias de "enriquecimiento rápido" para atraer clics.
- **Generación de tráfico (clickbait):** Dirigir a los usuarios a sitios externos o mejorar las métricas publicitarias.
- **Recopilación de datos:** Recopilar direcciones de correo electrónico activas para futuras campañas.

![[Pasted image 20251213114148.png]]

En la captura de pantalla anterior, se muestra un ejemplo de correo electrónico de marketing que ofrece soluciones logísticas para el evento SOC-mas. Se observa que la intención detrás del mensaje es puramente comercial.
Debe analizar cada mensaje con cuidado. Busque la intención subyacente. No todos los correos electrónicos no deseados son una amenaza; a veces son simplemente spam que no representan un riesgo real para TBFC.

## El ataque de Phishmas

Los atacantes utilizan técnicas comunes en casi todos los intentos de phishing. En un ataque de phishing, se utiliza al menos una de las siguientes técnicas:

**Impersonation**

Algunos atacantes pueden hacerse pasar por una persona, un departamento o incluso un servicio para atraer a los usuarios. Esta es una forma de ganar credibilidad haciéndose pasar por el gerente del destinatario o una persona importante de la empresa.

Abra el correo electrónico con el asunto "**URGENT: McSkidy VPN access for incident response**" y revise el campo "From:" del mensaje.

![[Pasted image 20251213114308.png]]

Podemos detectar fácilmente los intentos de suplantación de identidad al comprobar si el correo electrónico del remitente coincide con el dominio interno o la estructura estándar de la empresa. En este caso, el dominio del remitente es un dominio gratuito de Gmail, que no está alineado con el dominio de TBFC.

## Ingeniería social

La ingeniería social en el phishing consiste en manipular a las personas en lugar de descifrar tecnología. Los atacantes crean historias, correos electrónicos, llamadas o mensajes de chat creíbles que explotan las emociones (miedo, ayuda, curiosidad, urgencia) y el contexto real para atraer a los destinatarios.

Ahora, lee el contenido del correo electrónico anterior que abriste. Podemos detectar múltiples técnicas de ingeniería social:

- **Suplantación de identidad:** Es un tipo de ingeniería social. ¡El atacante se hace pasar por McSkidy!
- **Sentido de urgencia:** Podemos observar palabras como "urgente" e "inmediatamente" para presionar al destinatario.
- **Canal lateral:** El atacante intenta disuadir a los destinatarios de contactar con McSkidy utilizando sus canales de comunicación habituales (teléfono y correo electrónico). 
- **Intención maliciosa:** El atacante intenta engañar al usuario para que proporcione sus credenciales de VPN. También puede intentar solicitar la aprobación de pagos, abrir malware o compartir datos confidenciales.


![[Pasted image 20251213114443.png]]


**Typosquatting y Punycode**

Has aprendido que revisar el dominio del remitente es una buena manera de detectar intentos de suplantación de identidad de remitentes externos. Pero ¿qué pasa si el atacante crea un dominio muy similar?
En ese caso, el typosquatting y el punycode permiten a los atacantes aprovecharse de la falta de atención (o de conocimiento) de los usuarios.

El typosquatting se produce cuando un atacante registra un error ortográfico común en el dominio de una organización. Por ejemplo, "glthub.com" en lugar de "github.com" (observa que hay una L en lugar de una i).

![[Pasted image 20251213114557.png]]

Por otro lado, punycode es un sistema de codificación especial que convierte caracteres Unicode (usados ​​en sistemas de escritura como el chino, el cirílico y el árabe) en ASCII. Al escribir punycodes en la barra de direcciones del navegador, estos se traducirán al formato ASCII, el formato aceptado por DNS.
Con este recurso, los atacantes pueden reemplazar letras latinas idénticas; por ejemplo, una "a" latina estándar podría reemplazarse por una "α" griega.

A continuación, se muestra una imagen del dominio tryhackme.com escrito con "тrу" (t cirílica, г cirílica, y cirílica):

![[Pasted image 20251213114657.png]]

Ambas técnicas permiten a los atacantes registrar dominios maliciosos y engañar a los usuarios haciéndoles creer que reciben correos electrónicos del dominio legítimo o que acceden a sitios web auténticos.

Ahora, abramos el correo electrónico con el asunto "**TBFC-IT shared "Christmas Laptop Upgrade Agreement" with you**".
Si prestamos atención al remitente de este mensaje, podemos identificar una letra latina ƒ en lugar de la f normal. Es un claro uso de punycode para un dominio de correo electrónico.

![[Pasted image 20251213114838.png]]

Una forma sencilla de identificar punycodes es consultar el campo "Return-Path" en los encabezados del correo electrónico. En el correo electrónico abierto, vaya a la vista previa de los encabezados y verá el prefijo ACE y los caracteres no ASCII codificados.

**Spoofing**

La suplantación de identidad de correo electrónico es otra forma en que los atacantes pueden engañar a los usuarios haciéndoles creer que reciben correos de un dominio legítimo.
El mensaje parece provenir de un remitente confiable (el nombre para mostrar y el campo "From:" se ven en la vista previa), pero los encabezados subyacentes cuentan una historia diferente. Los clientes de correo electrónico modernos pueden rechazar fácilmente los intentos de suplantación de identidad, pero debido a que la protección de correo electrónico de Wareville no funciona, algunos intentos de suplantación de identidad pueden pasar desapercibidos.

Abra el correo electrónico con el asunto "**New Audio Message from McSkidy**" y revise el campo "From:".

![[Pasted image 20251213115000.png]]

Parece un dominio real de TBFC, pero revisemos algunos campos esenciales en los encabezados de correo electrónico:

- `Authentication-Results`
- `Return-Path`

![[Pasted image 20251213115031.png]]

En "Authentication-Results", SPF, DKIM y DMARC son comprobaciones de seguridad que ayudan a confirmar si un correo electrónico proviene realmente de quien dice ser:

- **SPF:** Indica qué servidores tienen permiso para enviar correos electrónicos para un dominio (como una lista de remitentes aprobados).
- **DKIM:** Añade una firma digital para demostrar que el mensaje no se modificó y que realmente proviene de ese dominio.
- **DMARC:** Utiliza SPF y DKIM para decidir qué hacer si un correo electrónico parece falso (por ejemplo, enviarlo a la carpeta de spam o bloquearlo).

Si tanto SPF como DMARC fallan, es una clara señal de que el correo electrónico es falso, lo que significa que el remitente no es quien dice ser. En este caso, ¡todo falló!

En la Return-Path podemos ver la dirección de correo electrónico real zxwsedr@easterbb.com. Esto confirma el intento de suplantación de identidad en el correo electrónico de llamadas perdidas de TBFC.

**Archivos adjuntos maliciosos**

La forma más clásica de phishing es adjuntar archivos maliciosos a un correo electrónico. Normalmente, estos archivos adjuntos se envían mediante algún tipo de técnica de ingeniería social en el cuerpo del correo.

En el correo electrónico anterior que analizamos, el cuerpo del correo intentaba engañar a los usuarios haciéndoles creer que el archivo adjunto era un mensaje de voz de McSkidy.
En realidad, el archivo es un archivo ".html"

![[Pasted image 20251213115223.png]]

Los archivos adjuntos maliciosos pueden tener múltiples objetivos. Una vez abiertos, estos archivos pueden instalar malware, robar contraseñas o dar a los atacantes acceso al dispositivo o la red. En este caso, los archivos HTA/HTML se utilizan comúnmente para el phishing porque se ejecutan sin sandbox del navegador, lo que significa que los scripts tienen acceso completo al endpoint en el que se ejecutan.

## Phishing en tendencia

Dado que las plataformas de correo electrónico y las herramientas de seguridad han mejorado considerablemente el bloqueo de mensajes y archivos adjuntos sospechosos, los Eggsploit Bunnies de Malhare y otros atacantes tuvieron que cambiar su estrategia:

- En lugar de enviar archivos de malware (que son fáciles de detectar), ahora se centran en engañar a los usuarios para que abandonen el entorno seguro de la empresa.
- A menudo utilizan herramientas o sitios web legítimos para que sus señuelos parezcan fiables y que los usuarios proporcionen sus credenciales o descarguen archivos maliciosos.

En resumen, la mayoría de los ataques de phishing no se centran en la instalación directa de malware, sino en el robo de acceso.
A continuación, puede ver un diagrama de este flujo de tendencias:

![[Pasted image 20251213115305.png]]

**Aplicaciones legítimas**

Podemos observar que los atacantes se esconden tras servicios de confianza como Dropbox, Google Drive/Docs y OneDrive, ya que esos enlaces parecen legítimos y suelen superar los filtros de correo electrónico.
El escenario más común implica un archivo compartido que contiene una propuesta muy atractiva, como un documento de aumento de sueldo de RR. HH. o una actualización de portátil.
Al hacer clic en él, el usuario redirige a un documento compartido con contenido falso. El objetivo es atraer a los usuarios a páginas de inicio de sesión falsas para robar credenciales o descargar archivos maliciosos.

Reabramos el correo electrónico con el asunto "**TBFC-IT shared "Christmas Laptop Upgrade Agreement" with you**" y analicemos cómo lo utilizan los atacantes:

![[Pasted image 20251213115436.png]]

En la imagen superior, podemos observar el uso de un dominio falso con punycodes para engañar a los usuarios, así como el uso de una herramienta legítima (OneDrive), seguido de una propuesta muy atractiva. Todas estas señales tienen como objetivo principal ganar credibilidad y hacer creer a los usuarios que provienen del equipo de TI real de TBFC.

**Páginas de inicio de sesión falsas**

Como vimos, las credenciales son el principal objetivo de los atacantes hoy en día, y las páginas de inicio de sesión falsas son su truco favorito para lograrlo.
Es simple e imita las páginas de inicio de sesión de diversas aplicaciones habituales con las que los usuarios interactúan en su día a día. En la mayoría de los casos, crean plataformas de correo electrónico falsas y portales de inicio de sesión como Microsoft Office 365 y Google.

![[Pasted image 20251213115509.png]]

Arriba se muestra un ejemplo de una página de inicio de sesión falsa de Microsoft. Podemos observar el dominio falso microsoftonline.login444123.com/signin en la parte superior.

**Comunicaciones de canal lateral**

La comunicación de canal lateral ocurre cuando un atacante traslada la conversación del correo electrónico a otro canal, como SMS, WhatsApp/Telegram, una llamada telefónica o videollamada, un enlace de SMS o una plataforma de documentos compartidos, para continuar la ingeniería social en una plataforma fuera del control de la empresa.

![[Pasted image 20251213115536.png]]

## ¡Es hora de detectar el phishing y salvar el SOC-mas!

**Tu misión:** Clasifica los correos electrónicos, separa el spam del phishing e identifica tres señales claras (por ejemplo: suplantación de identidad, ingeniería social) para cada correo electrónico de phishing que marques.
Obtendrás una bandera tras seleccionar las señales correctas para un correo electrónico de phishing. Reúne banderas para todos los correos de phishing para completar la sala y proteger el SOC-mas de TBFC.

¡Sigue investigando los correos electrónicos y consigue las banderas para cada correo enviado correctamente! Mantente alerta, verifica antes de actuar y que tus instintos sean más agudos que los trucos de los Eggsploit Bunnies. ¡Mucha suerte!

**Answer the questions below**

Classify the 1st email, what's the flag?

Respuesta:  THM{yougotnumber1-keep-it-going}
![[Pasted image 20251213130220.png]]
![[Pasted image 20251213130233.png]]
![[Pasted image 20251213130242.png]]
![[Pasted image 20251213130252.png]]

Classify the 2nd email. What's the flag?

Respuesta: THM{nmumber2-was-not-tha-thard!}
![[Pasted image 20251213130537.png]]
![[Pasted image 20251213130546.png]]
![[Pasted image 20251213130555.png]]
![[Pasted image 20251213130603.png]]

Classify the 3rd email. What's the flag?

Respuesta: THM{Impersonation-is-areal-thing-keepIt}
![[Pasted image 20251213130708.png]]
![[Pasted image 20251213130738.png]]
![[Pasted image 20251213130747.png]]
![[Pasted image 20251213130817.png]]

Classify the 4th email. What's the flag?

Respuesta: THM{Get-back-SOC-mas!!}
![[Pasted image 20251213131427.png]]
![[Pasted image 20251213131437.png]]
![[Pasted image 20251213131445.png]]
![[Pasted image 20251213131452.png]]

Classify the 5th email. What's the flag?

Respuesta: THM{It-was-just-a-sp4m!!}
![[Pasted image 20251213131600.png]]
![[Pasted image 20251213131610.png]]
![[Pasted image 20251213131617.png]]
![[Pasted image 20251213131622.png]]

Classify the 6th email. What's the flag?

Respuesta: THM{number6-is-the-last-one!-DX!}
![[Pasted image 20251213131718.png]]
![[Pasted image 20251213131742.png]]
![[Pasted image 20251213131751.png]]
![[Pasted image 20251213131824.png]]


If you enjoyed today's room, you can explore the [Phishing Analysis Tools](https://tryhackme.com/room/phishingemails3tryoe) room in detail!

Check

![[Pasted image 20251213125506.png]]