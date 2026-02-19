
**¿Qué es un IDS?**

En la sesión anterior, Introducción a los Firewalls, estudiamos la función de un firewall, una solución de seguridad que suele implementarse en los límites de una red para proteger el tráfico entrante y saliente. El firewall verifica el tráfico cuando se va a establecer una conexión y la deniega si infringe sus reglas. Sin embargo, debe existir algún tipo de seguridad para detectar las actividades de la conexión que lo han atravesado y que ya se han producido. Por lo tanto, si un atacante logra eludir un firewall mediante una conexión aparentemente legítima y luego realiza alguna actividad maliciosa dentro de la red, debe existir un mecanismo para detectarla a tiempo. Para ello, contamos con una solución de seguridad dentro de la red. Esta solución se conoce como Sistema de Detección de Intrusos (IDS).

Pensemos en el ejemplo de la seguridad de un edificio. Un firewall actúa como un portero, controlando a las personas que entran y salen. Siempre existe la posibilidad de que algún malintencionado se cuele dentro y comience a realizar actividades maliciosas. No lo detectaron en la puerta, pero ¿qué pasa si lo detectamos incluso después de entrar? Esto se puede lograr mediante las cámaras de vigilancia presentes en todo el edificio. El IDS actúa como una cámara de vigilancia. Ubicado en una esquina, monitorea el tráfico de la red basándose en sus detecciones de firmas y anomalías, y detecta cualquier tráfico anormal, ya sea entrante o saliente, en la red. Con cada detección, se genera una alerta para los administradores de seguridad. El IDS no actúa sobre estas detecciones; solo notifica a los administradores de seguridad sobre la actividad maliciosa.

![[Pasted image 20250829161828.png]]

Esta sala te brindará un sólido conocimiento de las soluciones IDS. En las próximas tareas, también exploraremos la solución IDS de código abierto más popular.

Answer the questions below

Can an intrusion detection system (IDS) prevent the threat after it detects it? Yea/Nay
respuesta Nay


---

**==Tipos de IDS==**

Los IDS pueden clasificarse de forma diferente según ciertos factores. La principal clasificación de un IDS depende de sus modos de implementación y detección.

**Modos de implementación**

Los IDS pueden implementarse de las siguientes maneras:

+ **Sistema de Detección de Intrusiones en Host (HIDS):** Las soluciones IDS basadas en host se instalan individualmente en los hosts y se encargan de detectar únicamente las posibles amenazas de seguridad asociadas a ese host en particular. Proporcionan una visibilidad detallada de las actividades del host. Sin embargo, la gestión de los sistemas de detección de intrusiones en host puede ser difícil en redes grandes, ya que consumen muchos recursos y requieren administración en cada host.

+ **Sistema de Detección de Intrusiones en Red (NIDS):** Las soluciones IDS basadas en red son cruciales para detectar actividades potencialmente maliciosas en toda la red, independientemente de los hosts específicos. Supervisan el tráfico de red de todos los hosts involucrados para detectar actividades sospechosas. Proporcionan una visión centralizada de todas las detecciones dentro de toda la red.

![[Pasted image 20250829162108.png]]

**Modos de Detección**

+ **IDS Basados ​​en Firmas:** Numerosos ataques ocurren a diario. Cada ataque tiene un patrón único, conocido como firma. Estas firmas son conservadas por los IDS en sus bases de datos para que, si el mismo ataque se repite en el futuro, sea detectado por su firma y notificado a los administradores de seguridad para que tomen medidas. Cuanto más sólida sea la base de datos de firmas del IDS, mayor será la eficiencia con la que detectará las amenazas conocidas. Sin embargo, los IDS basados ​​en firmas no pueden detectar ataques de día cero. Estos ataques no tienen firmas (patrones) previas y no se guardan en las bases de datos del IDS. Por lo tanto, los IDS basados ​​en firmas solo pueden detectar los ataques anteriores, y sus firmas (patrones) se guardan en la base de datos. En las próximas tareas, exploraremos un IDS basado en firmas llamado Snort.

+ **IDS Basados ​​en Anomalías:** Este tipo de IDS primero aprende el comportamiento normal (línea base) de la red o sistema y realiza detecciones si se produce alguna desviación de dicho comportamiento. Los sistemas de detección de intrusos (IDS) basados ​​en anomalías también pueden detectar ataques de día cero, ya que no se basan en las firmas disponibles, sino que detectan anomalías dentro de la red o el sistema comparando el estado actual con el comportamiento normal (línea base). Sin embargo, este tipo de IDS puede generar muchos falsos positivos (marcando actividades benignas como maliciosas) debido a que la naturaleza de la mayoría de los programas legítimos coincide con la de los maliciosos. Los IDS basados ​​en anomalías los marcarían como maliciosos y considerarían que cualquier comportamiento inusual es malicioso. También podemos reducir los falsos positivos generados por los IDS basados ​​en anomalías mediante su ajuste (definiendo manualmente el comportamiento normal en el IDS).

+ **IDS híbrido:** Un IDS híbrido combina los métodos de detección de los IDS basados ​​en firmas y los basados ​​en anomalías para aprovechar las ventajas de cada enfoque. Algunas amenazas conocidas pueden ya tener firmas en la base de datos del IDS; en este caso, el IDS híbrido utilizaría la técnica de detección del IDS basado en firmas. Si detecta una nueva amenaza, puede aprovechar el método de detección del IDS basado en anomalías. 


Los sistemas de detección de intrusos (IDS) basados ​​en firmas pueden detectar amenazas rápidamente, mientras que otros sistemas de detección de intrusos (IDS) pueden tener una alta sobrecarga de procesamiento. Sin embargo, también es fundamental considerar los IDS en función de diversos factores. Los IDS basados ​​en firmas pueden ser una buena opción para cubrir una pequeña superficie de amenaza. Los IDS basados ​​en anomalías y los IDS híbridos pueden ayudar a detectar los ataques de día cero modernos, que aumentan a diario y pueden causar daños masivos a las organizaciones.

Answer the questions below

Which type of IDS is deployed to detect threats throughout the network?
respuesta  Network Intrusion Detection System

Which IDS leverages both signature-based and anomaly-based detection techniques?
respuesta  Hybrid IDS


---

==**Ejemplo de IDS: Snort**==

Snort es una de las soluciones IDS de código abierto más utilizadas, desarrollada en 1998. Utiliza detecciones basadas en firmas y anomalías para identificar amenazas conocidas. Estas se definen en los archivos de reglas de la herramienta Snort. Varios archivos de reglas integrados vienen preinstalados en el paquete de esta herramienta. Estos archivos contienen diversos patrones de ataque conocidos. Las reglas integradas de Snort pueden detectar una gran cantidad de tráfico malicioso. Sin embargo, puede configurar Snort para que detecte tipos específicos de tráfico de red que no están cubiertos por los archivos de reglas predeterminados. Puede crear reglas personalizadas según sus necesidades para detectar tráfico específico. También puede deshabilitar las reglas de detección integradas si no apuntan a tráfico dañino para su sistema o red y definir reglas personalizadas en su lugar. En la próxima tarea, exploraremos las reglas integradas y crearemos reglas personalizadas para detectar tráfico específico.

**Modos de Snort**

![[Pasted image 20250829162706.png]]

| Mode                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Use Case                                                                                                                                                                                                                                                                  |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Packet sniffer mode                     | Este modo lee y muestra los paquetes de red sin analizarlos. El modo de rastreo de paquetes de Snort no está directamente relacionado con las funciones de IDS, pero puede ser útil para la monitorización y la resolución de problemas de red. En algunos casos, los administradores de sistemas podrían necesitar leer el flujo de tráfico sin realizar ninguna detección para diagnosticar problemas específicos. En este caso, pueden utilizar el modo de rastreo de paquetes de Snort. Este modo permite mostrar el tráfico de red en la consola o incluso exportarlo en un archivo.                                     | El equipo de red observa algunos problemas de rendimiento de la red. Para diagnosticarlos, necesitan información detallada del tráfico de la red. Para ello, pueden utilizar el modo de rastreo de paquetes de Snort.                                                     |
| Packet logging mode                     | Snort detecta el tráfico de red en tiempo real y muestra las detecciones como alertas en la consola para que los administradores de seguridad puedan tomar medidas. Sin embargo, en algunos casos, es necesario registrar el tráfico de red para su posterior análisis. El modo de registro de paquetes de Snort permite registrar el tráfico de red como un archivo PCAP (formato estándar de captura de paquetes). Esto incluye todo el tráfico de red y cualquier detección derivada de él. Los investigadores forenses pueden usar estos archivos de registro de Snort para analizar la causa raíz de ataques anteriores. | El equipo de seguridad necesita iniciar una investigación forense de un ataque de red. Necesitarán los registros de tráfico para realizar el análisis de la causa raíz. El tráfico de red registrado mediante el modo de registro de paquetes de Snort puede serles útil. |
| Network Intrusion Detection System mode | El modo NIDS de Snort es el modo principal que monitorea el tráfico de red en tiempo real y aplica sus archivos de reglas para identificar cualquier coincidencia con los patrones de ataque conocidos almacenados como firmas. Si existe una coincidencia, se genera una alerta. Este modo proporciona la funcionalidad principal de una solución IDS.                                                                                                                                                                                                                                                                       | El equipo de seguridad debe supervisar proactivamente su red o sistemas para detectar posibles amenazas. Para ello, pueden aprovechar el modo NIDS de Snort.                                                                                                              |

El uso más relevante de Snort como IDS proviene de su modo NIDS. Sin embargo, Snort puede utilizarse en cualquiera de los modos mencionados, según las necesidades.

Answer the questions below

Which mode of Snort helps us to log the network traffic in a PCAP file?
respuesta Packet Logging Mode

What is the primary mode of Snort called?
respuesta Network Intrusion Detection System Mode


---

**==Uso de Snort==**

Durante la instalación de Snort, debe proporcionar su interfaz y rango de red. Puede ejecutar Snort normalmente, capturando únicamente el tráfico destinado a su host. Sin embargo, si desea usar Snort para capturar y detectar intrusiones en toda su red, debe activar el modo promiscuo de la interfaz de red de su host.

Snort cuenta con archivos de reglas integrados, un archivo de configuración y otros archivos. Estos se almacenan en el directorio ``/etc/snort``. El archivo clave de Snort es su archivo de configuración ``snort.conf``, donde se pueden especificar los archivos de reglas que se habilitarán, el rango de red que se monitoreará y habilitar otras configuraciones. Los archivos de reglas se almacenan en la carpeta ``rules``. Usemos el comando ``ls`` para listar todos los archivos y carpetas presentes en el directorio principal de Snort:

![[Pasted image 20250829163038.png]]

**Formato de la regla**

Ahora, analicemos cómo se crean las reglas en Snort. Existe una forma específica de escribirlas. A continuación, se muestra un ejemplo de regla que detectaría paquetes ICMP (generalmente utilizados al hacer ping a un host) provenientes de cualquier dirección IP y puerto, y que llegan a la red doméstica (el rango de red se define en el archivo de configuración de Snort) a cualquier puerto. Una vez detectado dicho tráfico, se generan alertas de "Ping detectado".

![[Pasted image 20250829163109.png]]

Los detalles de los componentes involucrados en esta regla se detallan a continuación:

+ **Acción:** Especifica la acción a tomar cuando se activa la regla. En este caso, la acción es "alertar" cuando el tráfico coincide con esta regla.

+ **Protocolo:** Se refiere al protocolo que coincide con esta regla. En este caso, usamos el protocolo "ICMP", que se utiliza al hacer ping a un host.

+ **IP de origen:** Determina la IP desde la que se origina el tráfico. Dado que queremos detectar tráfico desde cualquier IP de origen, la configuramos como "cualquiera".

+ **Puerto de origen:** Determina el puerto desde el que se origina el tráfico. Dado que queremos detectar tráfico desde cualquier puerto de origen, la configuramos como "cualquiera".

+ **IP de destino:** Especifica la IP de destino de la que proviene el tráfico coincidente; genera la alerta. En este caso, usamos "$HOME_NET". Esta es una variable, y su valor se define como el rango completo de nuestra red en el archivo de configuración de Snort.

+ **Puerto de destino:** Especifica el puerto al que llegará el tráfico. Como queremos detectar el tráfico que llega a cualquier puerto, lo configuramos como "cualquiera".

+ **Metadatos de la regla:** Cada regla tiene metadatos. Estos se definen al final de la regla entre paréntesis. Sus componentes son los siguientes:

	+ **Mensaje (msg):** Describe el mensaje que se mostrará cuando se active la regla en cuestión. El mensaje debe indicar el tipo de actividad detectada. En este caso, usamos "Ping detectado".

	+ **ID de firma (sid):** Cada regla tiene un identificador único que la diferencia de las demás. Este identificador se denomina ID de firma (sid). En este caso, configuramos el sid como "10001".

	+ **Revisión de la regla (rev):** Establece el número de revisión de la regla. Cada vez que se modifica la regla, su número de revisión se incrementa. Esto facilita el seguimiento de los cambios en cualquier regla.

**Creación de reglas**

Peguemos la regla de ejemplo explicada anteriormente en el archivo "local.rules" personalizado, en el directorio de reglas de Snort.

Primero, abra el archivo "local.rules" en un editor de texto:

![[Pasted image 20250829163305.png]]

Ahora, agregue la siguiente regla al archivo después de las reglas ya existentes:

``alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)``

Nota: Necesitaremos las demás reglas ya existentes en la siguiente tarea, así que no las elimine.

Una vez editado el archivo correctamente, presione "Ctrl+x" y se le pedirá que presione "y" para guardar los cambios. Presione "y" para guardar los cambios.

**Prueba de reglas**

Primero, iniciemos la herramienta Snort para detectar cualquier intrusión definida en el archivo de reglas. Para ello, ejecutemos el siguiente comando con privilegios de sudo en nuestra consola:

![[Pasted image 20250829163347.png]]

Nota: Si su interfaz de bucle invertido no se llama "lo", sustitúyala por el nombre correcto.

Como esta regla está diseñada para alertarnos sobre cualquier paquete ICMP dirigido a nuestra dirección de bucle invertido, intentemos hacer ping a nuestra dirección de bucle invertido para comprobar si la regla funciona:

![[Pasted image 20250829163408.png]]

La siguiente captura de pantalla muestra la alerta "Ping de bucle invertido detectado" generada por Snort al hacer ping a la IP de bucle invertido de nuestro host. Esto significa que nuestra regla funciona correctamente.

![[Pasted image 20250829163426.png]]

**Ejecución de Snort en archivos PCAP**

Vimos cómo Snort puede utilizarse para la detección de intrusiones en el tráfico en tiempo real. Sin embargo, en ocasiones, puede encontrarse con un caso en el que el tráfico de red histórico se registra en un archivo y es necesario realizar una investigación forense para determinar cualquier indicio de intrusión en dicho tráfico. Este tráfico suele registrarse en el formato estándar de captura de paquetes "PCAP". Snort también puede realizar detecciones en estos archivos PCAP que contienen el tráfico de red histórico.

![[Pasted image 20250829163455.png]]

Se puede utilizar el siguiente comando con privilegio sudo para realizar esta acción:

![[Pasted image 20250829163515.png]]

Nota: Reemplace "Task.pcap" con la ruta a su archivo PCAP para su análisis.

Answer the questions below

Where is the main directory of Snort that stores its files?
respuesta /etc/snort

Which field in the Snort rule indicates the revision number of the rule?
respuesta rev

Which protocol is defined in the sample rule created in the task?
respuesta icmp

What is the file name that contains custom rules for Snort?
respuesta local.rules


---

**==Práctica de laboratorio==**

Ejercicio

Escenario: Eres un investigador forense externo. Una empresa te contacta para investigar un ataque reciente a su red. Le entregaron un archivo PCAP llamado "Intro_to_IDS.pcap", que contenía el tráfico de red capturado durante el ataque. Tu tarea consiste en ejecutar Snort en este archivo PCAP y responder a las preguntas de esta tarea.

Nota: El archivo PCAP Intro_to_IDS.pcap se encuentra en el directorio /etc/snort/. Debes cambiar el directorio a /etc/snort y ejecutar el comando de análisis PCAP en ese nuevo archivo PCAP, tal como hicimos en la tarea 4.

Answer the questions below

What is the IP address of the machine that tried to connect to the subject machine using SSH?
respuesta 10.11.90.211

nos movemos al directorio /etc/snort para que el comando funcione correctamente
![[Pasted image 20250901203854.png]]

se abre el archivo .pcap
![[Pasted image 20250901204016.png]]


What other rule message besides the SSH message is detected in the PCAP file?
respuesta Ping Detected

![[Pasted image 20250901204146.png]]

What is the sid of the rule that detects SSH?
respuesta 1000002

![[Pasted image 20250901204329.png]]


