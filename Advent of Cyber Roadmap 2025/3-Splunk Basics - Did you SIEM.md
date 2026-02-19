
Introduction

![[Pasted image 20251203155957.png]]

Ya casi es Navidad en Wareville, y el equipo de The Best Festival Company (TBFC) está ocupado preparando la gran celebración. Todo marcha a la perfección hasta que el panel del SOC parpadea en rojo. De repente, aparece un mensaje de rescate:

![[Pasted image 20251203160020.png]]

El mensaje proviene del Rey Malhare, el celoso gobernante de la Isla HopSec, cansado de que se olvide la Pascua. Ha enviado a sus Conejitos Bandidos para atacar los sistemas de TBFC y convertir la Navidad en su nueva festividad, EAST-mas.

Con McSkidy desaparecido y la red bajo ataque, el equipo SOC de TBFC utilizará Splunk para determinar cómo se infiltró el ransomware en el sistema y evitar que el plan del Rey Malhare se vea comprometido antes de Navidad.

Objetivos de aprendizaje

- Ingerir e interpretar datos de registro personalizados en Splunk
- Crear y aplicar extracciones de campos personalizados
- Usar el Lenguaje de Procesamiento de Búsqueda (SPL) para filtrar y refinar los resultados de búsqueda
- Realizar una investigación en Splunk para descubrir información clave

Inicie su máquina virtual haciendo clic en el botón "Iniciar máquina" que aparece a continuación. La máquina tardará entre 2 y 3 minutos en arrancar por completo. Una vez que la máquina esté en funcionamiento, puede conectarse al SIEM de Splunk visitando https://10-66-144-211.reverse-proxy.cell-prod-us-east-1c.vm.tryhackme.com en su navegador.

Nota: Si recibe un error 502 al acceder al enlace, espere un poco más para que la instancia de Splunk arranque por completo.


---

==**Log Analysis with Splunk**==

## Exploración de los registros

En la instancia de Splunk, los datos se han preingresado para que podamos investigar el incidente. En la interfaz de Splunk, haga clic en "Buscar e informes" en el panel izquierdo, como se muestra a continuación:

![[Pasted image 20251203160154.png]]

En la página siguiente, escriba ``index=main`` en la barra de búsqueda para ver todos los registros ingresados. Tenga en cuenta que debe seleccionar ``All Time`` como intervalo de tiempo en el menú desplegable a la derecha de la barra de búsqueda.

![[Pasted image 20251203160213.png]]

Tras ejecutar la consulta, se nos presentarán dos conjuntos de datos independientes preingeridos en Splunk. Podemos comprobarlo haciendo clic en el campo sourcetype en la lista de campos a la izquierda de la página.

![[Pasted image 20251203160234.png]]

Los dos conjuntos de datos son los siguientes:

- **web_traffic:** Esta fuente de datos contiene eventos relacionados con las conexiones web hacia y desde el servidor web.
- **firewall_logs:** Esta fuente de datos contiene los registros del firewall, que muestran el tráfico permitido o bloqueado. La IP local asignada al servidor web es 10.10.1.15.

Analicemos los registros e investiguemos el ataque a nuestros servidores para identificar al responsable.

## Triage inicial

Inicie una búsqueda básica en el índice utilizando su sourcetype personalizado ``web_traffic``, con la siguiente consulta:

**Consulta de búsqueda:** ``index=main sourcetype=web_traffic``

![[Pasted image 20251203160451.png]]

Analicemos nuestro resultado para una mejor comprensión:

1. **Consulta de búsqueda (search query):** Esta consulta recupera todos los eventos del índice ``main`` etiquetados con el sourcetype personalizado ``web_traffic``. Esto marca el inicio de la investigación.
2. **Intervalo de tiempo (time range):** El intervalo de tiempo está configurado actualmente como "All Time". En el análisis de seguridad, este intervalo se ajustaría (por ejemplo, a la ventana de pico) después de la carga inicial de datos.
3. **Cronología (timeline):** Este histograma visual muestra la distribución de los 17,172 eventos a lo largo del tiempo. El gráfico indica el volumen de registro diario exitoso, seguido de un pico de tráfico distintivo (un período de alta actividad, probablemente la ventana de ataque).
4. **Campos seleccionados (selected fields):** Estos son los campos seleccionados actualmente para mostrarse en la columna de resumen de la lista de eventos (host, source, sourcetype). Representan metadatos básicos sobre el archivo de registro.
5. **Campos de interés (interesting fields):** Este panel enumera todos los campos que Splunk ha extraído o añadido manualmente automáticamente. Los campos con el prefijo ``#``(por ejemplo, ``#Date_hour``) se generan automáticamente mediante los comandos de tiempo de Splunk. La presencia de ``user_agent``, ``path`` y ``client_ip`` confirma el análisis correcto de la estructura del registro web.
6. **Detalles del evento y extracción de campos:** Esta sección muestra los detalles analizados de un solo evento con campos extraídos como ``user_agent``, ``path``, ``status``, ``client_ip`` y más.

Ahora que comprendemos el diseño de Splunk y cómo leer los registros, continuemos con el análisis de los registros.

## Visualización de la cronología de registros

Grafiquemos el recuento total de eventos a lo largo del tiempo, agrupados por día, para determinar la cantidad de eventos capturados por día. Esto nos ayudará a identificar el día en que recibió una cantidad anormal de registros.

**Consulta de búsqueda:** ``index=main sourcetype=web_traffic | timechart span=1d count``

![[Pasted image 20251203161042.png]]

Los resultados anteriores muestran ahora los registros de eventos capturados por día. Esto podría ser interesante, ya que algunos días se registra un gran volumen de registros. También podemos hacer clic en la pestaña Visualization para examinar el gráfico y obtener una mejor representación, como se muestra a continuación:

![[Pasted image 20251203161117.png]]

Podemos añadir la función ``reverse`` al final para mostrar el resultado en orden descendente, mostrando el día con el mayor número de eventos al principio.

**Consulta de búsqueda:** ``index=main sourcetype=web_traffic | timechart span=1d count | sort by count | reverse``

![[Pasted image 20251203161200.png]]


Hay un período claro de intensa actividad durante el cual el Rey Malhare lanzó su fase principal de ataque.

## Detección de Anomalías

Ahora que hemos examinado los días con registros anormales, usando la tabla y el gráfico, usemos la misma consulta de búsqueda para examinar varios campos y buscar valores sospechosos. Necesitamos regresar a la pestaña Eventos para continuar.

**User_Agent**

Hagamos clic en el campo ``user_agent`` en el panel izquierdo, como se muestra a continuación. Nos mostrará los detalles sobre los agentes de usuario capturados hasta el momento.

![[Pasted image 20251203161302.png]]

Tras un análisis más detallado, queda claro que, además de los agentes de usuario legítimos, como las variantes de Mozilla, recibimos una gran cantidad de agentes sospechosos, que debemos investigar más a fondo.

**client_ip**

El segundo campo que examinaremos es ``client_ip``, que contiene las direcciones IP de los clientes que acceden al servidor web. Inmediatamente, destaca una dirección IP en particular, que investigaremos más a fondo.

![[Pasted image 20251203161349.png]]

**path**

El tercer campo que examinaremos es la ruta, que contiene la URI solicitada y a la que acceden las IP del cliente. Los resultados que se muestran a continuación indican claramente algunos ataques que merecen la pena investigar.

![[Pasted image 20251203161420.png]]

## Filtrando valores benignos

Sabemos que los conejos del Rey Malhare usan scripts y herramientas, no navegadores estándar. Filtraremos todo el tráfico estándar.

Excluiremos los agentes de usuario legítimos comunes. La siguiente consulta eliminará los agentes de usuario legítimos de los resultados y solo mostrará los sospechosos, que investigaremos más a fondo.

**Consulta de búsqueda:** ``index=main sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox*``

![[Pasted image 20251203161503.png]]

El resultado revela resultados interesantes. Al hacer clic en el campo ``client_ip``, podemos ver que una única dirección IP es responsable de todos los agentes de usuario sospechosos. Anotemos esto para una investigación más profunda y completemos las secciones ``<REDACTED>`` de las próximas consultas con esa IP.

## Delimitando las IP sospechosas

En situaciones reales, a menudo nos encontramos con varias direcciones IP que intentan atacar constantemente nuestros servidores. Para delimitar las direcciones IP que no envían solicitudes desde navegadores comunes de escritorio o móviles, podemos usar la siguiente consulta:

**Consulta de búsqueda:** ``sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox* | stats count by client_ip | sort -count | head 5``

![[Pasted image 20251203162057.png]]

El resultado confirma la IP principal utilizada por los Bandit Bunnies. En la consulta de búsqueda, el "-" en la parte "sort -count" ordenará el resultado por conteo en orden inverso; es lo mismo que usar la función "reverse". Seleccionemos esta dirección IP y filtrémosla para ver las huellas de las actividades capturadas.

## Rastreando la cadena de ataque

Ahora nos centraremos en la IP del atacante seleccionado para rastrear sus pasos cronológicamente, confirmando el uso de múltiples herramientas y cargas útiles. No olvide reemplazar ``<REDACTED>`` con la IP que anotamos anteriormente.

**Reconocimiento (Footprinting)**

Comenzaremos la búsqueda del sondeo inicial de los archivos de configuración expuestos utilizando la siguiente consulta:

**Consulta de búsqueda:** ``sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("/.env", "/*phpinfo*", "/.git*") | table _time, path, user_agent, status``

![[Pasted image 20251203162252.png]]

El resultado confirma que el atacante utilizó herramientas de bajo nivel (curl, wget) y se encontró con códigos de estado 404/403/401.

**Enumeración (Prueba de vulnerabilidades)**

Búsqueda de vulnerabilidades comunes de cruce de rutas y redireccionamiento abierto.

**Consulta de búsqueda:** ``sourcetype=web_traffic client_ip="<REDACTED>" AND path="*..*" OR path="*redirect*"``

![[Pasted image 20251203162337.png]]

El resultado muestra los recursos a los que el atacante intenta acceder. Actualicemos la consulta de búsqueda para obtener el recuento de recursos solicitados por el atacante. Esta consulta filtra las rutas que contienen ``../../`` o el término "redirect", como se muestra a continuación. Esto se hace para buscar rastros de intentos de atravesar la ruta (``../../``). Para ello, debemos actualizar la consulta de búsqueda para escapar caracteres como ``..\/..\/.``

**Consulta de búsqueda:** ``sourcetype=web_traffic client_ip="<REDACTED>" AND path="*..\/..\/*" OR path="*redirect*" | stats count by path``

![[Pasted image 20251203162440.png]]

Resultados bastante interesantes. Revela intentos de lectura de archivos del sistema (``../../*``), lo que demuestra que el atacante pasó del simple escaneo a realizar pruebas de vulnerabilidad activas.

**Ataque de inyección SQL**

Encuentre la herramienta de ataque automatizada y su carga útil mediante la siguiente consulta:

**Consulta de búsqueda:** ``sourcetype=web_traffic client_ip="<REDACTED>" AND user_agent IN ("*sqlmap*", "*Havij*") | table _time, path, status``

![[Pasted image 20251203162545.png]]

Los resultados anteriores confirman el uso de inyecciones SQL conocidas y cadenas de ataque específicas como SLEEP(5). Un código de estado 504 suele confirmar un ataque de inyección SQL basado en tiempo exitoso.

## Intentos de exfiltración

Buscar intentos de descarga de archivos grandes y sensibles (copias de seguridad, registros). Podemos usar la siguiente consulta:

**Consulta de búsqueda:** ``sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("*backup.zip*", "*logs.tar.gz*") | table _time path, user_agent``

![[Pasted image 20251203162638.png]]

Los resultados indican que el atacante estaba exfiltrando grandes fragmentos de archivos de registro comprimidos mediante herramientas como curl, zgrab, entre otras. Podemos confirmar los detalles de estas conexiones en los registros del firewall.

## Ransomware Staging y RCE

Las solicitudes de archivos confidenciales como ``/logs.tar.gz`` y ``/config`` indican que el atacante está recopilando datos para una doble extorsión. En los registros, identificamos algunas solicitudes relacionadas con bunnylock y shell.php. Utilicemos la siguiente consulta para ver de qué se tratan estas consultas de búsqueda.

**Consulta de búsqueda:** ``sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("*bunnylock.bin*", "*shell.php?cmd=*") | table _time, path, user_agent, status``

![[Pasted image 20251203162734.png]]

Los resultados anteriores confirman claramente un webshell exitoso. El atacante ha obtenido control total del servidor web y también puede ejecutar comandos. Este tipo de ataque se denomina Ejecución Remota de Código (RCE). La ejecución de ``/shell.php?cmd=./bunnylock.bin`` indica que se está ejecutando un programa similar a un ransomware en el servidor.

## Correlación de la Comunicación C2 Saliente

Dirigimos la búsqueda a los ``firewall_logs`` utilizando la IP del Servidor Comprometido (10.10.1.5) como origen y la IP del atacante como destino.

**Consulta de búsqueda:** ``sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="<REDACTED>" AND action="ALLOWED" | table _time, action, protocol, src_ip, dest_ip, dest_port, reason``

![[Pasted image 20251203162852.png]]

Esta consulta demuestra que el servidor estableció inmediatamente una conexión saliente con la IP C2 del atacante en el puerto ``DEST_PORT`` sospechoso. Los campos ``ACTION=ALLOWED`` y ``REASON=C2_CONTACT`` confirman que el canal de comunicación del malware estaba activo.

## Volumen de datos exfiltrados

También podemos usar la función suma para calcular la suma de los bytes transferidos, utilizando el campo bytes_transferred, como se muestra a continuación:

**Consulta de búsqueda:** ``sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="<REDACTED>" AND action="ALLOWED" | stats sum(bytes_transferred) by src_ip``

![[Pasted image 20251203163000.png]]

Los resultados muestran un gran volumen de datos transferidos desde el servidor web comprometido al servidor C2.

## Conclusión

- I**dentidad encontrada:** El atacante se identificó mediante el mayor volumen de tráfico web malicioso procedente de la IP externa.
- **Vector de intrusión:** El ataque siguió una clara progresión en los registros web ``sourcetype=web_traffic``.
- **Reconocimiento:** Se iniciaron sondeos mediante cURL/Wget, buscando archivos de configuración (``/.env``) y probando vulnerabilidades de cruce de rutas.
- **Explotación:** El uso de agentes de usuario SQLmap y cargas útiles específicas (SLEEP(5)) confirmó la fase de explotación exitosa.
- **Entrega de la carga útil:** La acción sobre el objetivo se estableció mediante la ejecución exitosa final del comando ``cmd=./bunnylock.bin`` a través del shell web.
- **Confirmación C2:** La consulta a los registros del firewall (``sourcetype=firewall_logs``) demostró la actividad posterior a la explotación. El servidor interno comprometido (SRC_IP: 10.10.1.5) estableció una conexión C2 saliente a la IP del atacante.

**Answer the questions below**

What is the attacker IP found attacking and compromising the web server?

Respuesta:  198.51.100.55
![[Pasted image 20251203171141.png]]

Which day was the peak traffic in the logs? (Format: YYYY-MM-DD)

Respuesta:  2025-10-12
![[Pasted image 20251203170805.png]]

What is the count of Havij user_agent events found in the logs?

Respuesta: 993
![[Pasted image 20251203185735.png]]

How many path traversal attempts to access sensitive files on the server were observed?

Respuesta: 658
![[Pasted image 20251203170953.png]]

Examine the firewall logs. How many bytes were transferred to the C2 server IP from the compromised web server?

Respuesta: 126167
![[Pasted image 20251203185303.png]]

If you enjoyed today's room, check out the [Incident Handling With Splunk](https://tryhackme.com/room/splunk201) room to learn more about analyzing logs with Splunk.

No requiere respuesta
