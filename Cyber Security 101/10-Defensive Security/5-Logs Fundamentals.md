
**==Introducción a los Registros==**

Los atacantes son astutos. Evitan dejar el máximo rastro posible de la víctima para evitar ser detectados. Sin embargo, el equipo de seguridad determina con éxito cómo se ejecutó el ataque e incluso, en ocasiones, logra encontrar al responsable.

Supongamos que unos policías investigan la desaparición de un preciado relicario en una cabaña en la selva nevada. Observan que la puerta de madera de la cabaña está brutalmente dañada y el techo se derrumba. Hay huellas en el camino nevado que lleva a la cabaña. Finalmente, descubren imágenes de las cámaras de seguridad de una residencia vecina. Al reunir todos estos rastros, la policía determinó con éxito quién estaba detrás del ataque. En muchos casos de este tipo se encuentran diversos rastros; al reunirlos, se acerca al delincuente.

![[Pasted image 20250826174456.png]]

Parece que estos rastros desempeñan un papel importante en las investigaciones.

¿Qué sucedería si algo ocurriera dentro de un dispositivo digital? ¿Dónde encontramos todos estos rastros para investigar más a fondo?

Existen varios lugares dentro de un sistema donde se pueden obtener los rastros de un ataque. Los registros contienen la mayoría de estos rastros. Los registros son las huellas digitales que deja cualquier actividad, ya sea normal o maliciosa. Rastrear la actividad y a la persona responsable de su ejecución se facilita mediante los registros.

![[Pasted image 20250826174511.png]]

**Casos de uso de registros**

A continuación, se presentan algunas áreas clave en las que los registros desempeñan un papel fundamental.

| Use Case                             | Description                                                                                                                                                                                                                         |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security Events Monitoring           | Los registros nos ayudan a detectar comportamientos anómalos cuando se utiliza la monitorización en tiempo real.                                                                                                                    |
| Incident Investigation and Forensics | Los registros son el registro de todo tipo de actividad. Ofrecen información detallada sobre lo ocurrido durante el incidente. El equipo de seguridad utiliza los registros para realizar análisis de causa raíz de los incidentes. |
| Troubleshooting                      | Como los registros también registran los errores en los sistemas o aplicaciones, pueden utilizarse para diagnosticar problemas y facilitar su solución.                                                                             |
| Performance Monitoring               | Los registros también pueden proporcionar información valiosa sobre el rendimiento de las aplicaciones.                                                                                                                             |
| Auditing and Compliance              | Los registros desempeñan un papel fundamental en la auditoría y el cumplimiento normativo, ya que facilitan el registro de diferentes tipos de actividades.                                                                         |

En esta sala, comprenderá los distintos tipos de registros que se mantienen en diferentes sistemas. También investigaremos de forma práctica los registros como rastros de diferentes ataques.

Answer the questions below

Where can we find the majority of attack traces in a digital system?
respuesta Logs

---

Tipos de registros

En la tarea anterior, vimos varios casos de uso de los registros. Sin embargo, existe un desafío. Imagine que necesita investigar un problema en un sistema a través de los registros; abre el archivo de registro de ese sistema y, tras ver numerosos eventos de diferentes categorías, se siente perdido.

La solución es la siguiente: los registros se dividen en varias categorías según el tipo de información que proporcionan. Ahora solo necesita consultar el archivo de registro específico al que se refiere el problema.

Por ejemplo, si necesita investigar los inicios de sesión exitosos de ayer en un período de tiempo específico en el sistema operativo Windows, en lugar de consultar todos los registros, solo necesita consultar los **registros de seguridad** del sistema para encontrar la información de inicio de sesión. También existen otros tipos de registros útiles para investigar diferentes incidentes. Analicémoslos.

![[Pasted image 20250827150812.png]]

| Log Type         | Usage                                                                                                                                                                                                                                                               | Example                                                                                                                                                                                       |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| System Logs      | Los registros del sistema pueden ser útiles para solucionar problemas de ejecución del sistema operativo. Estos registros proporcionan información sobre diversas actividades del sistema operativo.                                                                | - Eventos de inicio y apagado del sistema<br>- Eventos de carga del controlador<br>- Eventos de error del sistema<br>- Eventos de hardware                                                    |
| Security Logs    | Los registros de seguridad ayudan a detectar e investigar incidentes. Estos registros proporcionan información sobre las actividades relacionadas con la seguridad en el sistema.                                                                                   | - Eventos de autenticación<br>- Eventos de autorización<br>- Eventos de cambios en la política de seguridad<br>- Eventos de cambios en la cuenta de usuario    - Eventos de actividad anormal |
| Application Logs | Los registros de la aplicación contienen eventos específicos relacionados con la aplicación. Cualquier actividad interactiva o no interactiva que ocurra dentro de la aplicación se registrará aquí.                                                                | - Eventos de interacción del usuario<br>- Eventos de cambios en la aplicación<br>- Eventos de actualización de la aplicación<br>- Eventos de error de la aplicación                           |
| Audit Logs       | Los registros de auditoría proporcionan información detallada sobre los cambios del sistema y los eventos del usuario. Estos registros son útiles para los requisitos de cumplimiento y también pueden desempeñar un papel vital en la supervisión de la seguridad. | - Eventos de acceso a datos<br>- Eventos de cambio del sistema<br>- Eventos de actividad del usuario<br>- Eventos de aplicación de políticas                                                  |
| Network Logs     | Los registros de red proporcionan información sobre el tráfico entrante y saliente de la red. Desempeñan un papel crucial en la resolución de problemas de red y también pueden ser útiles durante la investigación de incidentes.                                  | - Eventos de tráfico de red entrante<br>- Eventos de tráfico de red saliente<br>- Registros de conexión de red       - Registros del firewall de red                                          |
| Access Logs      | Los registros de acceso proporcionan información detallada sobre el acceso a diferentes recursos. Estos recursos pueden ser de diferentes tipos, lo que nos proporciona información sobre su acceso.                                                                | - Registros de acceso al servidor web<br>- Registros de acceso a la base de datos           - Registros de acceso a la aplicación<br>- Registros de acceso a la API                           |
|                  |                                                                                                                                                                                                                                                                     |                                                                                                                                                                                               |

Nota: Puede haber otros tipos de registros según las distintas aplicaciones y los servicios que prestan.

Ahora que comprendemos qué son estos registros y cómo pueden ser útiles en diferentes escenarios, veamos cómo analizarlos y extraer información valiosa de ellos. El análisis de registros es una técnica para extraer datos valiosos de los registros. Implica la búsqueda de cualquier indicio de actividad anormal o inusual. Buscar una actividad específica o anomalías en los registros a simple vista es imposible. Por esta razón, disponemos de varias técnicas manuales y automatizadas para el análisis de registros. En las próximas tareas, realizaremos un análisis manual de los registros de acceso de Windows y del servidor web.

Answer the questions below

Which type of logs contain information regarding the incoming and outgoing traffic in the network?
respuesta Network Logs

Which type of logs contain the authentication and authorization events?
respuesta Security Logs


---

**==Análisis de los registros de eventos de Windows==**

Al igual que otros sistemas operativos, Windows también registra muchas de las actividades que se llevan a cabo. Estas se almacenan en archivos de registro separados, cada uno con una categoría específica. Algunos de los tipos de registros cruciales que se almacenan en un sistema operativo Windows son:

1. **Aplicación:** Existen numerosas aplicaciones ejecutándose en el sistema operativo. Toda la información relacionada con dichas aplicaciones se registra en este archivo. Esta información incluye errores, advertencias, problemas de compatibilidad, etc.

2. **Sistema:** El sistema operativo tiene diferentes operaciones en ejecución. Toda la información relacionada con estas operaciones se registra en el archivo de registro del sistema. Esta información incluye problemas con los controladores, problemas de hardware, información de inicio y apagado del sistema, información de servicios, etc.

3. **Seguridad:** Este es el archivo de registro más importante del sistema operativo Windows en términos de seguridad. Registra todas las actividades relacionadas con la seguridad, incluyendo la autenticación de usuarios, los cambios en las cuentas de usuario, los cambios en las políticas de seguridad, etc.

Además, existen otros archivos de registro en Windows diseñados para registrar actividades relacionadas con acciones y aplicaciones específicas.

A diferencia de otros archivos de registro estudiados en tareas anteriores, que no contaban con una aplicación integrada para visualizarlos, el sistema operativo Windows cuenta con una utilidad llamada Visor de Eventos, que ofrece una interfaz gráfica de usuario intuitiva para ver y buscar cualquier dato en estos registros.

Para abrir el Visor de Eventos, haga clic en el botón Inicio de Windows y escriba "Visor de Eventos". Se abrirá automáticamente, como se muestra a continuación. El área resaltada en la captura de pantalla muestra los diferentes registros disponibles.

![[Pasted image 20250827172502.png]]

Puede hacer clic en "Registros de Windows" en la sección resaltada para ver los diferentes tipos de registros que mencionamos al principio de esta tarea. La primera sección resaltada muestra los diferentes archivos de registro. Al hacer clic en uno de estos archivos, veremos los diferentes registros, como se puede ver en la segunda sección resaltada. Por último, en la tercera sección resaltada, tenemos diferentes opciones para analizar los registros.

![[Pasted image 20250827172533.png]]

Haga doble clic en uno de estos registros para ver su contenido.

![[Pasted image 20250827172556.png]]

Así es como se ve un registro de eventos de Windows. Tiene diferentes campos. Los principales se describen a continuación:

1. **Descripción:** Este campo contiene información detallada de la actividad.
2. **Nombre del registro:** El nombre del registro indica el nombre del archivo de registro.
3. **Registrado:** Este campo indica la hora de la actividad.
4. **ID de evento:** Los ID de evento son identificadores únicos para una actividad específica.

Existen numerosos ID de evento disponibles en los registros de eventos de Windows. Podemos usarlos para buscar cualquier actividad específica. Por ejemplo, el ID de evento 4624 identifica de forma única la actividad de un inicio de sesión exitoso, por lo que solo necesita buscar este ID de evento 4624 al investigar inicios de sesión exitosos.

A continuación, se muestra una tabla con algunos ID de evento importantes en el sistema operativo Windows.

| Event ID | Description                                         |
| -------- | --------------------------------------------------- |
| 4624     | Se ha iniciado sesión correctamente.                |
| 4625     | Se ha producido un error al iniciar sesión.         |
| 4634     | Se ha cerrado sesión correctamente.                 |
| 4720     | Se ha creado una cuenta de usuario.                 |
| 4724     | Se intentó restablecer la contraseña de una cuenta. |
| 4722     | Se habilitó una cuenta de usuario.                  |
| 4725     | Se desactivó una cuenta de usuario.                 |
| 4726     | Se eliminó una cuenta de usuario.                   |
Hay muchos más ID de evento. No es necesario recordarlos todos, pero conviene recordar los más importantes.

El Visor de Eventos nos permite buscar registros relacionados con un ID de evento específico mediante la función "Filtrar Registro Actual". Podemos hacer clic en esta función para aplicar cualquier filtro.

![[Pasted image 20250827172720.png]]

Al hacer clic en la opción "Filtrar registro actual", se nos pedirá que introduzcamos los ID de evento que queremos filtrar. En la captura de pantalla a continuación, filtré el ID de evento 4624.

![[Pasted image 20250827172743.png]]

Una vez que presiono el botón "Aceptar", puedo ver todos los registros con el ID de evento: 4624. Ahora puedo ver cualquiera de estos registros haciendo doble clic en ellos.

![[Pasted image 20250827172804.png]]

Ejercicio

El viernes, una organización crítica reportó haber sido víctima de un ciberataque. Tras la investigación, se extrajeron datos críticos de un servidor de archivos de la red de la organización. El equipo de seguridad logró determinar el nombre de usuario y la dirección IP del sistema comprometido en la red, que tenía acceso al servidor de archivos en el momento del ataque.

Su tarea es descubrir las actividades del atacante en este sistema comprometido antes de que accediera al servidor de archivos.

Answer the questions below

What is the name of the last user account created on this system?
respuesta hacked

abrimos el visor de eventos , seleccionamos windoes logs y security, y filtramos por el evento 4720 que es el de creacion de ususarios y revisamos la ultima cuenta creada

![[Pasted image 20250827181704.png]]

Which user account created the above account?
respuesta Administrator

![[Pasted image 20250827181733.png]]

On what date was this user account enabled? Format: M/D/YYYY
respuesta  6/7/2024

![[Pasted image 20250827181753.png]]

Did this account undergo a password reset as well? Format: Yes/No
respuesta yes

filtramos por el código de proceso 4724 que es el de cambios de contraseña

![[Pasted image 20250827182202.png]]


---

**==Análisis de registros de acceso al servidor web==**

Interactuamos con muchos sitios web a diario. A veces, simplemente queremos ver el sitio web, y otras, iniciar sesión o cargar un archivo en cualquier campo de entrada disponible. Estos son simplemente diferentes tipos de solicitudes que realizamos a un sitio web. Todas estas solicitudes son registradas por el sitio web y almacenadas en un archivo de registro en el servidor web que lo ejecuta.

Este archivo de registro contiene todas las solicitudes realizadas al sitio web, junto con información sobre el período de tiempo, la IP solicitada, el tipo de solicitud y la URL. A continuación, se muestran los campos de un registro de ejemplo de un archivo de registro de acceso al servidor web Apache, que se encuentra en el directorio: ``/var/log/apache2/access.log``

1. Dirección IP: “172.16.0.1” - La dirección IP del usuario que realizó la solicitud.

2. Marca de tiempo: “[06/Jun/2024:13:58:44]” - La hora en que se realizó la solicitud al sitio web.

3. Solicitud: Detalles de la solicitud.
	Método HTTP: “GET” - Indica al sitio web la acción que debe realizar en la solicitud.
	URL: “/” - El recurso solicitado.

4. Código de estado: “200” - La respuesta del servidor. Diferentes números indican diferentes resultados.

5. Agente de usuario: “Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/58.0.3029.110 Safari/537.36” - Información sobre el sistema operativo, navegador, etc. del usuario al realizar la solicitud.

Podemos realizar un análisis manual de registros mediante algunas utilidades de línea de comandos en el sistema operativo Linux. Los siguientes comandos pueden ser útiles durante el análisis manual de registros.

`cat` es una utilidad popular para mostrar el contenido de un archivo de texto. Podemos usar el comando ``cat`` para mostrar el contenido de un archivo de registro, ya que normalmente está en formato de texto.

![[Pasted image 20250827182539.png]]

La mayoría de los sistemas rotan los registros regularmente. Esta rotación les permite crear archivos de registro individuales para periodos específicos y no almacenarlos todos en un solo archivo. Sin embargo, a veces, es necesario combinar dos archivos de registro. La utilidad de línea de comandos ``cat`` también puede ser útil en este caso. Podemos combinar los resultados de varios archivos en uno solo, como se muestra a continuación.

![[Pasted image 20250827182602.png]]

``grep`` es una utilidad de línea de comandos muy útil que permite buscar cadenas y patrones dentro de un archivo de registro. Por ejemplo, podría necesitar verificar si una dirección IP específica está presente en su archivo de registro. Puede hacerlo con el siguiente comando: El siguiente comando buscará la cadena "192.168.1.1" en el archivo access.log y mostrará todas las líneas que la contengan.

![[Pasted image 20250827182709.png]]

El comando ``less`` es útil para gestionar varios archivos de registro. Es posible que necesite analizar fragmentos específicos uno por uno. Para ello, puede usar la utilidad de línea de comandos ``less``, que le permite ver una página a la vez.

![[Pasted image 20250827182732.png]]

Usa la ``barra espaciadora`` para ir a la página siguiente y la tecla ``b`` para ir a la página anterior.

Después de ejecutar este comando, los registros se mostrarán en páginas, una por una, lo que facilita el análisis manual. Si deseas buscar algo en los registros, puedes escribir ``/`` seguido del patrón que buscas y pulsar Intro.

Usa la tecla ``n`` para ir a la siguiente ocurrencia de tu búsqueda y la tecla ``N`` para ir a la anterior.

Answer the questions below

What is the IP which made the last GET request to URL: “/contact”?
respuesta 10.0.0.1
ejecutamos el siguiente comando para filtar la busqueda 
``grep "GET /contact" access.log``

![[Pasted image 20250827211210.png]]

When was the last POST request made by IP: “172.16.0.1”?
respuesta 06/Jun/2024:13:55:44
ejecutamos el siguiente comando filtrando por la direccion IP dada 
``grep "172.16.0.1" access.log``

![[Pasted image 20250827212039.png]]

Based on the answer from question number 2, to which URL was the POST request made?
respuesta /contact
revisamos la salida de la terminal 
![[Pasted image 20250827212402.png]]

---

**==Conclusión==**

En esta sala, aprendimos cómo los registros son una fuente importante de información durante una investigación. Estudiamos los diferentes tipos de registros y sus casos de uso, y aprendimos a analizarlos de forma manual y automática.

Los ejercicios prácticos de Análisis del Registro de Eventos de Windows y Análisis del Registro de Acceso al Servidor Web de las tareas anteriores les brindaron la oportunidad de trabajar con los archivos de registro de diferentes escenarios de incidentes.