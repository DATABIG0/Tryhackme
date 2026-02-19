**==Introducción==**

¿Qué es SIEM?

SIEM significa Sistema de Gestión de Información y Eventos de Seguridad. Es una herramienta que recopila datos de diversos endpoints/dispositivos de red, los almacena en un lugar centralizado y los correlaciona. En esta sesión se abordarán los conceptos básicos necesarios para comprender SIEM y su funcionamiento.

Answer the questions below

What does SIEM stand for?
respuesta Security Information and Event Management system

---

**==Visibilidad de la red mediante SIEM==**

Antes de explicar la importancia de SIEM, entendamos por qué es crucial tener una mejor visibilidad de todas las actividades dentro de una red. La imagen a continuación muestra un ejemplo de una red simple que comprende varios endpoints basados ​​en Linux/Windows, un servidor de datos y un sitio web. Cada componente se comunica con los demás o accede a internet a través de un router.

![[Pasted image 20250827213442.png]]

Como sabemos, cada componente de red puede tener una o más fuentes de registro que generan diferentes registros. Un ejemplo podría ser la configuración de Sysmon junto con los registros de eventos de Windows para una mejor visibilidad de Windows Endpoint. Podemos dividir nuestras fuentes de registro de red en dos partes lógicas:

**Fuentes de registro centradas en el host**

Estas fuentes de registro capturan eventos ocurridos dentro del host o relacionados con él. Algunas fuentes de registro que generan registros centrados en el host son los registros de eventos de Windows, [^1]Sysmon, Osquery, etc. Algunos ejemplos de registros centrados en el host son:

1. Un usuario que accede a un archivo
2. Un usuario que intenta autenticarse
3. Una actividad de ejecución de un proceso
4. Un proceso que agrega, edita o elimina una clave o valor de registro
5. Ejecución de PowerShell

**Fuentes de registro centradas en la red**

Los registros relacionados con la red se generan cuando los hosts se comunican entre sí o acceden a internet para visitar un sitio web. Algunos protocolos de red son SSH, VPN, HTTP/s, FTP, etc. Ejemplos de estos eventos son:

1. Conexión SSH
2. Acceso a un archivo mediante FTP
3. Tráfico web
4. Un usuario accede a los recursos de la empresa mediante VPN
5. Actividad de intercambio de archivos en red

**Importancia de SIEM**

Ahora que hemos cubierto los distintos tipos de registros, es hora de comprender la importancia de SIEM. Dado que todos estos dispositivos generan cientos de eventos por segundo, examinar los imglogs de cada dispositivo uno por uno en caso de incidente puede ser una tarea tediosa. Esta es una de las ventajas de contar con una solución SIEM. No solo recopila registros de diversas fuentes en tiempo real, sino que también permite correlacionar eventos, buscar en los registros, investigar incidentes y responder con prontitud. Algunas de las características clave de SIEM son:

1. Ingesta de registros en tiempo real
2. Alertas contra actividades anormales
3. Monitoreo y visibilidad 24/7
4. Protección contra las amenazas más recientes mediante detección temprana
5. Visualización e información de datos
6. Capacidad para investigar incidentes pasados.

![[Pasted image 20250827213900.png]]

Answer the questions below

Is Registry-related activity host-centric or network-centric?
respuesta  host-centric

Is VPN related activity host-centric or network-centric?
respuesta  network-centric


---

**==Fuentes de Registros e Ingesta de Registros==**

Todo dispositivo de la red genera algún tipo de registro cada vez que se realiza una actividad en él, como cuando un usuario visita un sitio web, se conecta por SSH, inicia sesión en su estación de trabajo, etc. A continuación, se describen algunos dispositivos comunes que se encuentran en un entorno de red:

**Máquina Windows**

Windows registra todos los eventos que se pueden ver a través de la utilidad Visor de Eventos. Esta asigna un ID único a cada tipo de actividad de registro, lo que facilita al analista su examen y seguimiento. Para ver eventos en un entorno Windows, escriba **Visor de Eventos** en la barra de búsqueda y accederá a la herramienta donde se almacenan y pueden consultarse diferentes registros, como se muestra a continuación. Estos registros de todos los endpoints de Windows se reenvían a la solución SIEM para su supervisión y mejor visibilidad.

![[Pasted image 20250827214044.png]]

**Estación de trabajo Linux**

El sistema operativo Linux almacena todos los registros relacionados, como eventos, errores, advertencias, etc., que luego se incorporan a SIEM para una monitorización continua. Algunas de las ubicaciones comunes donde Linux almacena los registros son:

1. ``/var/log/httpd``: Contiene registros de solicitudes/respuestas HTTP y errores.
2. ``/var/log/cron``: Los eventos relacionados con las tareas cron se almacenan en esta ubicación.
3. ``/var/log/auth.log`` y ``/var/log/secure``: Almacenan los registros relacionados con la autenticación.
4. ``/var/log/kern``: Este archivo almacena los eventos relacionados con el kernel.

A continuación, se muestra un ejemplo de un registro cron:

![[Pasted image 20250827214244.png]]

**Servidor web**

Es importante supervisar todas las solicitudes y respuestas entrantes y salientes del servidor web para detectar cualquier posible intento de ataque web. En Linux, las ubicaciones habituales para escribir todos los registros relacionados con Apache son ``/var/log/apache`` o ``/var/log/httpd``.

A continuación, se muestra un ejemplo de registros de Apache:

![[Pasted image 20250827214332.png]]

**Ingesta de Registros**

Todos estos registros proporcionan una gran cantidad de información y pueden ayudar a identificar problemas de seguridad. Cada solución SIEM tiene su propia forma de ingerir los registros. A continuación, se explican algunos métodos comunes que utilizan:

1) **Agente/Reenviador:** Estas soluciones SIEM proporcionan una herramienta ligera llamada agente (reenviador de Splunk) que se instala en el endpoint. Está configurado para capturar todos los registros importantes y enviarlos al servidor SIEM.

2) **Syslog:** Syslog es un protocolo ampliamente utilizado para recopilar datos de diversos sistemas, como servidores web, bases de datos, etc., y enviarlos en tiempo real a un destino centralizado.

3) **Carga Manual:** Algunas soluciones SIEM, como Splunk, ELK, etc., permiten a los usuarios ingerir datos sin conexión para un análisis rápido. Una vez ingeridos, los datos se normalizan y están disponibles para su análisis.

4) **Reenvío de puertos:** Las soluciones SIEM también pueden configurarse para escuchar en un puerto específico, y luego los endpoints reenvían los datos a la instancia SIEM en dicho puerto.

![[Pasted image 20250827214435.png]]

A continuación, se muestra un ejemplo de cómo Splunk ofrece varios métodos para la ingesta de registros:

![[Pasted image 20250827214447.png]]

Answer the questions below

In which location within a Linux environment are HTTP logs stored?
respuesta  /var/log/httpd


---

**==¿Por qué SIEM?==**

SIEM se utiliza para correlacionar los datos recopilados y detectar amenazas. Una vez detectada una amenaza o superado un umbral determinado, se genera una alerta. Esta alerta permite a los analistas tomar las medidas adecuadas según la investigación. SIEM desempeña un papel importante en el ámbito de la ciberseguridad y ayuda a detectar y protegerse contra las amenazas más recientes de forma oportuna. Proporciona una buena visibilidad de lo que sucede dentro de la infraestructura de red.

**Capacidades de SIEM**

SIEM es un componente fundamental del ecosistema de un Centro de Operaciones de Seguridad (SOC), como se ilustra a continuación. SIEM comienza recopilando registros y examinando si algún evento o flujo ha cumplido la condición establecida en la regla o ha superado un umbral determinado.

Algunas de las capacidades comunes de SIEM son:

1. Correlación entre eventos de diferentes fuentes de registros.
2. Proporciona visibilidad de las actividades centradas tanto en el host como en la red.
3. Permite a los analistas investigar las amenazas más recientes y brindar respuestas oportunas.
4. Busca amenazas que no son detectadas por las reglas establecidas.


![[Pasted image 20250827214701.png]]

**Responsabilidades del Analista de SOC**

Los Analistas de SOC utilizan soluciones SIEM para obtener una mejor visibilidad de lo que sucede dentro de la red. Algunas de sus responsabilidades incluyen:

1. Monitoreo e Investigación.
2. Identificación de Falsos Positivos.
3. Ajuste de las Reglas que Causan Ruido o Falsos Positivos.
4. Informe y Cumplimiento.
5. Identificación de Puntos Ciegos en la Visibilidad de la Red y su Corrección.

Answer the questions below

Read the task above.
No answer needed

---

**==Análisis de Registros y Alertas==**

La herramienta SIEM obtiene todos los registros relacionados con la seguridad mediante agentes, reenvío de puertos, etc. Una vez ingresados ​​los registros, SIEM busca comportamientos no deseados o patrones sospechosos en ellos, basándose en las condiciones establecidas por los analistas en las reglas. Si se cumple la condición, se activa una regla y se investiga el incidente.

**Panel de Control**

Los paneles de control son los componentes más importantes de cualquier SIEM. SIEM presenta los datos para su análisis tras su normalización e ingreso. El resumen de estos análisis se presenta en forma de información práctica mediante múltiples paneles de control. Cada solución SIEM incluye paneles de control predeterminados y ofrece la opción de crear paneles personalizados. Algunos de los datos que se pueden encontrar en un panel de control son:

1. Alertas Destacadas
2. Notificación del Sistema
3. Alerta de Estado
4. Lista de Intentos de Inicio de Sesión Fallidos
5. Conteo de Eventos Ingeridos
6. Reglas Activadas
7. Dominios Principales Visitados

A continuación se muestra un ejemplo de un panel de control predeterminado en Qradar SIEM:

![[Pasted image 20250827214932.png]]

**Reglas de Correlación**

Las reglas de correlación desempeñan un papel importante en la detección oportuna de amenazas, lo que permite a los analistas actuar a tiempo. Son expresiones lógicas configuradas para activarse. Algunos ejemplos son:

1. Si un usuario intenta iniciar sesión 5 veces en 10 segundos, se genera una alerta por múltiples intentos fallidos.
2. Si el inicio de sesión es exitoso después de varios intentos fallidos, se genera una alerta por inicio de sesión exitoso después de varios intentos.
3. Se configura una regla para alertar cada vez que un usuario conecta una memoria USB (útil si la memoria USB está restringida según la política de la empresa).
4. Si el tráfico saliente es superior a 25 MB, se genera una alerta por posible intento de exfiltración de datos (normalmente, depende de la política de la empresa).

**Cómo se crea una regla de correlación**

Para explicar el funcionamiento de la regla, considere los siguientes casos de uso del registro de eventos:

**Caso de uso 1:**

Los adversarios tienden a eliminar los registros durante la fase posterior a la explotación para borrar sus rastros. Se registra un ID de evento único, 104, cada vez que un usuario intenta eliminar o borrar los registros de eventos. Para crear una regla basada en esta actividad, podemos establecer la siguiente condición:

Regla: Si el origen del registro es WinEventLog y el ID de evento es 104 - Activar una alerta "Registro de eventos borrado" ``Event Log Cleared``

**Caso de uso 2:** 

Los adversarios utilizan comandos como ``whoami`` después de la fase de explotación/escalada de privilegios. Será útil incluir los siguientes campos en la regla:

1. Origen del registro: Identificar el origen del registro que captura los registros de eventos.
2. ID de evento: ¿Qué ID de evento está asociado con la actividad de ejecución del proceso? En este caso, el ID de evento 4688 será útil.
3. Nuevo nombre de proceso: ¿Qué nombre de proceso será útil incluir en la regla?

Regla: Si el origen del registro es WinEventLog y el código de evento es 4688, y el nombre del nuevo proceso contiene whoami, se activa una alerta de ejecución del comando WHOAMI ``WHOAMI command Execution DETECTED``

En la tarea anterior, se analizó la importancia de los pares campo-valor. Las reglas de correlación controlan los valores de ciertos campos para su activación. Por eso es importante tener registros normalizados.

Investigación de Alertas

Al monitorear SIEM, los analistas dedican la mayor parte de su tiempo a los paneles, ya que muestran diversos detalles clave sobre la red de forma muy resumida. Una vez que se activa una alerta, se examinan los eventos/flujos asociados a ella y se verifica la regla para determinar qué condiciones se cumplen. Con base en la investigación, el analista determina si se trata de un Verdadero o un Falso Positivo. Algunas de las acciones que se realizan después del análisis son:

1. La alerta es una Falsa Alarma. Puede ser necesario ajustar la regla para evitar que se repitan falsos positivos similares.
2. La alerta es un Verdadero Positivo. Realizar una investigación más exhaustiva.
3. Contactar al propietario del activo para preguntar sobre la actividad.
4. Se confirma la actividad sospechosa. Aísle el host infectado.
5. Bloquee la IP sospechosa.

Pasemos a la siguiente tarea y exploremos cómo funciona SIEM.

Answer the questions below

Which Event ID is generated when event logs are removed?
respuesta 104

What type of alert may require tuning?
respuesta False Alarm


---

**==Lab Work==**

En el laboratorio estático adjunto, se muestran un panel de control y eventos de ejemplo. Cuando se produce una actividad sospechosa, se activa una alerta, lo que significa que algunos eventos coinciden con la condición de alguna regla ya configurada. Complete el laboratorio y responda las siguientes preguntas.

Answer the questions below

Click on Start Suspicious Activity, which process caused the alert?
respuesta cudominer.exe
![[Pasted image 20250828212719.png]]

Find the event that caused the alert, which user was responsible for the process execution?
respuesta chris.fort
![[Pasted image 20250828212700.png]]

What is the hostname of the suspect user?
respuesta HR_02
![[Pasted image 20250828212703.png]]

Examine the rule and the suspicious process; which term matched the rule that caused the alert?
respuesta miner
![[Pasted image 20250828212741.png]]

What is the best option that represents the event? Choose from the following:

- False-Positive  

- True-Positive
respuesta  True-Positive
![[Pasted image 20250828212753.png]]

Selecting the right ACTION will display the FLAG. What is the FLAG?
respuesta THM{000_SIEM_INTRO}
![[Pasted image 20250828212803.png]]

---

**==Conclusión==**

En esta sala, hemos explicado qué es SIEM, sus capacidades y la visibilidad que proporciona. Para comprender a fondo cómo se investigan los incidentes, explore las siguientes salas y desafíos.


---

[^1]: Sysmon se refiere al Monitor del Sistema, un servicio del sistema y controlador de dispositivo de Windows desarrollado por Microsoft, diseñado para supervisar y registrar diversos eventos que ocurren en un sistema Windows.
