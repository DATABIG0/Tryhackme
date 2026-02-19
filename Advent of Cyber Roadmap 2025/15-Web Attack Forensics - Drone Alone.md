
  
Introduction

![[Pasted image 20251217180019.png]]

La interfaz web del programador de drones de TBFC recibe solicitudes HTTP largas y extrañas que contienen fragmentos Base64. Splunk genera una alerta: "Apache generó un proceso inusual". En algunos endpoints, estas solicitudes hacen que el servidor web ejecute código shell, ofuscado y oculto dentro de las cargas útiles Base64. En esta sala, su trabajo como miembro del Equipo Azul consiste en clasificar el incidente, identificar los hosts comprometidos, extraer y decodificar las cargas útiles y determinar el alcance.

Utilizará Splunk para alternar entre los registros web (Apache) y la telemetría a nivel de host (Sysmon).

Siga los pasos de investigación a continuación; cada uno corresponde a una consulta de Splunk y un objetivo de investigación.

Objetivos de aprendizaje

- Detectar y analizar actividad web maliciosa a través de los registros de acceso y errores de Apache
- Investigar las acciones de los atacantes a nivel de sistema operativo utilizando datos de Sysmon
- Identificar y decodificar cargas útiles sospechosas u ofuscadas de los atacantes
- Reconstruir la cadena de ataque completa utilizando Splunk para la investigación del Equipo Azul

Answer the questions below

I have successfully started the AttackBox and the target machine!

No answer needed


---

# Web Attack Forensics


## Iniciar sesión en Splunk

Después de iniciar AttackBox y la máquina de destino en la tarea anterior, espere unos 3 minutos para que el sistema arranque por completo. Luego, use Firefox en AttackBox para acceder al panel de Splunk en http://MACHINE_IP:8000 con las credenciales que aparecen a continuación.

![[Pasted image 20251217180151.png]]

La página de inicio de sesión de Splunk debería verse similar a la captura de pantalla que se muestra a continuación.

![[Pasted image 20251217180210.png]]

Después de iniciar sesión correctamente, será llevado a la página de búsqueda como se muestra en la captura de pantalla a continuación.

![[Pasted image 20251217180229.png]]

Asegúrese de ajustar el rango de tiempo de Splunk para que incluya la hora de los eventos (p. ej., "Últimos 7 días" o "Siempre"). Si el rango predeterminado es demasiado estrecho, podría aparecer el mensaje "No se encontraron resultados".

Un Blue Teamer exploraría diversos ángulos de ataque a través de Splunk. En esta tarea, seguiremos al elfo Log McBlue, quien usa la magia de Splunk para desentrañar la ruta de ataque.

## Detectar comandos web sospechosos

En el primer paso, buscaremos solicitudes HTTP que puedan mostrar actividad maliciosa. La siguiente consulta busca en los registros de acceso web cualquier solicitud HTTP que incluya indicios de intentos de ejecución de comandos, como ``cmd.exe``, ``PowerShell`` o ``Invoke-Expression``. Esta consulta ayuda a identificar posibles ataques de inyección de comandos, donde el atacante intenta ejecutar comandos del sistema a través de un script CGI vulnerable (``hello.bat``).

``index=windows_apache_access (cmd.exe OR powershell OR "powershell.exe" OR "Invoke-Expression") | table _time host clientip uri_path uri_query status``

![[Pasted image 20251217183509.png]]

En este paso, nos interesan principalmente las cadenas codificadas en base64, que pueden revelar diversos tipos de actividad. Una vez que detecte los comandos de PowerShell codificados, decodifíquelos con base64decode.org o su decodificador de base64 preferido para comprender qué intentaba hacer el atacante. Con base en los resultados obtenidos, copiemos la cadena de PowerShell codificada ``VABoAGkAcwAgAGkAcwAgAG4AbwB3ACAATQBpAG4AZQAhACAATQBVAEEASABBAEEASABBAEEA`` y péguela en el campo superior de https://www.base64decode.org/. Luego, haga clic en "Decodificar", como se muestra en la captura de pantalla a continuación.

![[Pasted image 20251217183605.png]]

## Búsqueda de errores del servidor o de ejecución de comandos en los registros de errores de Apache

En esta etapa, nos centraremos en inspeccionar los registros de errores del servidor web, ya que esto nos ayudará a detectar cualquier actividad maliciosa. Utilizaremos la siguiente consulta:

``index=windows_apache_error ("cmd.exe" OR "powershell" OR "Internal Server Error")``

Esta consulta inspecciona los registros de errores de Apache en busca de indicios de intentos de ejecución o fallos internos causados ​​por solicitudes maliciosas. Como puede ver, buscamos mensajes de error con términos específicos como ``cmd.exe`` y ``powershell``.

Asegúrese de seleccionar "View: Raw" en el menú desplegable sobre el campo "Event".

![[Pasted image 20251217183742.png]]

Si una solicitud como ``/cgi-bin/hello.bat?cmd=powershell`` genera un error interno del servidor 500, suele significar que la entrada del atacante fue procesada por el servidor, pero falló durante la ejecución, una señal clave de intentos de explotación.

Comprobar estos resultados ayuda a confirmar si el ataque llegó al backend o permaneció bloqueado en la capa web.

## Rastrear la creación de procesos sospechosos desde Apache

Exploremos Sysmon en busca de otros archivos ejecutables maliciosos que el servidor web podría haber generado. Lo haremos mediante la siguiente consulta de Splunk:

``index=windows_sysmon ParentImage="*httpd.exe"``

Esta consulta se centra en las relaciones entre procesos de los registros de Sysmon, específicamente cuando el proceso principal es Apache (``httpd.exe``).

Seleccione "View: Table" en el menú desplegable sobre el campo "Event".

![[Pasted image 20251217183856.png]]

Normalmente, Apache solo debería generar subprocesos de trabajo, no procesos del sistema como ``cmd.exe`` o ``powershell.exe``.

Si los resultados muestran procesos secundarios como:

``ParentImage = C:\Apache24\bin\httpd.exe``

``Image = C:\Windows\System32\cmd.exe``

Esto indica una inyección de comandos exitosa donde Apache ejecutó un comando del sistema.

El hallazgo anterior es uno de los indicadores más sólidos de que el ataque web penetró el sistema operativo.

## Confirmar la actividad de enumeración del atacante

En este paso, buscamos descubrir qué hacen los programas específicos que encontramos en consultas anteriores. Usemos la siguiente consulta:

``index=windows_sysmon *cmd.exe* *whoami*``

Esta consulta busca **registros de ejecución de comandos** donde ``cmd.exe`` ejecutó el comando ``whoami``.

Los atacantes suelen usar el comando whoami inmediatamente después de obtener la ejecución del código para determinar en qué cuenta de usuario se ejecuta su proceso malicioso.

El hallazgo de estos eventos confirma el **reconocimiento posterior a la explotación** del atacante y muestra que el comando inyectado se ejecutó en el host.

![[Pasted image 20251217184042.png]]

## Identificar cargas útiles de PowerShell codificadas en Base64

En este último paso, buscaremos todos los comandos codificados correctamente. Para buscar cadenas codificadas, podemos usar la siguiente consulta de Splunk:

``index=windows_sysmon Image="*powershell.exe" (CommandLine="*enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*Base64*")``

Esta consulta detecta comandos de PowerShell que contienen texto en Base64 o en -EncodedCommand, una técnica común que utilizan los atacantes para **ocultar sus comandos reales**.

Si sus defensas están configuradas correctamente, esta consulta no debería devolver **ningún resultado**, lo que significa que la carga útil codificada (como el mensaje "Muahahaha") nunca se ejecutó.

Si aparecen resultados, puede decodificar el comando en Base64 para verificar la verdadera intención del atacante.

![[Pasted image 20251217184104.png]]

**Answer the questions below**

What is the reconnaissance executable file name?

Respuesta: whoami.exe
![[Pasted image 20251217190122.png]]

What executable did the attacker attempt to run through the command injection?

Respuesta: PowerShell.exe


decodificamos el string
![[Pasted image 20251217190546.png]]
