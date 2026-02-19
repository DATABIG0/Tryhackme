**==¿Cuál es el propósito de un firewall?==**

Hemos visto guardias de seguridad en centros comerciales, bancos, restaurantes y casas. Estos guardias se ubican en las entradas de estas áreas para controlar a las personas que entran y salen. El propósito de este control es asegurar que nadie entre sin permiso. Este guardia actúa como un muro entre su área y los visitantes.

Diariamente fluye mucho tráfico entrante y saliente entre nuestros dispositivos digitales y la Internet a la que están conectados. ¿Qué pasaría si alguien se colara entre este tráfico masivo sin ser detectado? También necesitaríamos un guardia de seguridad para nuestros dispositivos digitales, que pudiera verificar los datos que entran y salen de ellos. Este guardia de seguridad es lo que llamamos **firewall**. Un firewall está diseñado para inspeccionar el tráfico entrante y saliente de una red o dispositivo digital. El objetivo es el mismo que el del guardia de seguridad que se encuentra afuera de un edificio: no permitir que ningún visitante no autorizado entre en un sistema o red. Se le dan instrucciones al firewall estableciendo reglas para que verifique todo el tráfico. Todo lo que entra o sale de su dispositivo o red se enfrenta primero al firewall. El firewall permite o deniega ese tráfico según sus reglas. La mayoría de los firewalls actuales van más allá del filtrado basado en reglas y ofrecen funciones adicionales para proteger su dispositivo o red del exterior. Analizaremos todos estos firewalls y realizaremos demostraciones prácticas de laboratorio con algunos de ellos.

![[Pasted image 20250828213025.png]]

Answer the questions below

Which security solution inspects the incoming and outgoing traffic of a device or a network?
respuesta Firewall


---

**==Tipos de firewalls==**

La implementación de firewalls se popularizó en las redes después de que las organizaciones descubrieran su capacidad para filtrar el tráfico dañino de sus sistemas y redes. Posteriormente, se introdujeron diversos tipos de firewalls, cada uno con una función específica. También es importante tener en cuenta que los distintos tipos de firewalls funcionan en distintas capas del modelo OSI. Los firewalls se clasifican en varios tipos.

Examinemos algunos de los tipos de firewalls más comunes y sus funciones en el modelo OSI.

![[Pasted image 20250828213130.png]]

**Cortafuegos sin estado**

Este tipo de cortafuegos opera en las capas 3 y 4 del modelo OSI y funciona únicamente filtrando los datos según reglas predeterminadas, sin tener en cuenta el estado de las conexiones anteriores. Esto significa que cada paquete cumple las reglas, independientemente de si forma parte de una conexión legítima. No conserva información sobre el estado de las conexiones anteriores para tomar decisiones sobre paquetes futuros. Por ello, estos cortafuegos pueden procesar los paquetes rápidamente. Sin embargo, no pueden aplicar políticas complejas a los datos basándose en su relación con las conexiones anteriores. Supongamos que el cortafuegos rechaza algunos paquetes de una única fuente basándose en sus reglas. Idealmente, debería descartar todos los paquetes futuros de esta fuente, ya que los paquetes anteriores no pudieron cumplir con las reglas del cortafuegos. Sin embargo, el cortafuegos sigue olvidándolo, y los paquetes futuros de esta fuente se tratarán como nuevos y volverán a coincidir con sus reglas.

**Cortafuegos con estado**

A diferencia de los cortafuegos sin estado, este tipo de cortafuegos va más allá del filtrado de paquetes mediante reglas predeterminadas. También registra las conexiones anteriores y las almacena en una tabla de estado. Esto añade una capa adicional de seguridad al inspeccionar los paquetes según su historial de conexiones. Los firewalls con estado operan en las capas 3 y 4 del modelo OSI. Supongamos que el firewall acepta algunos paquetes de una dirección de origen según sus reglas. En ese caso, registrará esta conexión en su tabla de estado y permitirá que todos los paquetes futuros de esta conexión se permitan automáticamente sin inspeccionarlos todos. De igual forma, los firewalls con estado registran las conexiones para las que rechazan algunos paquetes y, basándose en esta información, rechazan todos los paquetes posteriores provenientes del mismo origen.

**Cortafuegos proxy**

El problema con los firewalls anteriores era su incapacidad para inspeccionar el contenido de un paquete. Los firewalls proxy, o puertas de enlace a nivel de aplicación, actúan como intermediarios entre la red privada e Internet y operan en la capa 7 del modelo OSI. También inspeccionan el contenido de todos los paquetes. Las solicitudes de los usuarios en una red son reenviadas por este proxy tras inspeccionarlas y enmascararlas con su propia dirección IP para proporcionar anonimato a las direcciones IP internas. Se pueden aplicar políticas de filtrado de contenido a estos firewalls para permitir o denegar el tráfico entrante y saliente en función de su contenido.

**Firewall de Nueva Generación (NGFW)**

Este es el tipo de firewall más avanzado, que opera desde la capa 3 hasta la capa 7 del modelo OSI, ofreciendo inspección profunda de paquetes y otras funcionalidades que mejoran la seguridad del tráfico de red entrante y saliente. Cuenta con un sistema de prevención de intrusiones que bloquea actividades maliciosas en tiempo real. Ofrece análisis heurístico analizando los patrones de ataques y bloqueándolos instantáneamente antes de que lleguen a la red. Los NGFW cuentan con capacidades de descifrado SSL/TLS, que inspeccionan los paquetes tras descifrarlos y correlacionan los datos con la información de inteligencia de amenazas para tomar decisiones eficientes.

La siguiente tabla enumera las características de cada firewall, lo que le ayudará a elegir el más adecuado para cada caso de uso.

| Firewalls                 | Characteristics                                                                                                                                                                                                     |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stateless firewalls       | - Filtrado básico<br>- Sin registro de conexiones anteriores<br>- Eficiente para redes de alta velocidad                                                                                                            |
| Stateful firewalls        | - Reconocer el tráfico por patrones<br>- Se pueden aplicar reglas complejas<br>- Monitorear las conexiones de red                                                                                                   |
| Proxy firewalls           | - Inspecciona también los datos dentro de los paquetes<br>- Ofrece opciones de filtrado de contenido<br>- Proporciona control de aplicaciones<br>- Descifra e inspecciona paquetes de datos SSL/TLS                 |
| Next-generation firewalls | - Proporciona protección avanzada contra amenazas<br>- Incluye un sistema de prevención de intrusiones<br>- Identifica anomalías mediante análisis heurístico<br>- Descifra e inspecciona paquetes de datos SSL/TLS |

Answer the questions below

Which type of firewall maintains the state of connections?
respuesta stateful firewall

Which type of firewall offers heuristic analysis for the traffic?
respuesta next-generation firewall

Which type of firewall inspects the traffic coming to an application?
respuesta proxy firewall

---

**==Reglas en los Firewalls==**

Un firewall le permite controlar el tráfico de su red. Aunque filtra el tráfico según sus reglas integradas, se pueden definir reglas personalizadas para diversas redes. Por ejemplo, puede que algunas redes deseen denegar todo el tráfico SSH que entra en su red. Sin embargo, su red podría tener el requisito de permitir el tráfico SSH desde algunas direcciones IP específicas. Las reglas le permiten configurar estos ajustes personalizados para el tráfico entrante y saliente de su red.

A continuación se describen los componentes básicos de una regla de firewall:

+ **Dirección de origen:** La dirección IP del equipo que origina el tráfico.
+ **Dirección de destino:** La dirección IP del equipo que recibe los datos.
+ **Puerto:** El número de puerto para el tráfico.
+ **Protocolo:** El protocolo que se utilizará durante la comunicación.
+ **Acción:** Define la acción que se tomará al identificar cualquier tráfico de esta naturaleza.
+ **Dirección:** Este campo define la aplicabilidad de la regla al tráfico entrante o saliente. 

**Tipos de acciones**

El componente "Acción" de una regla indica los pasos a seguir después de que un paquete de datos se encuentre dentro de la categoría de la regla definida. A continuación, se explican tres acciones principales que se pueden aplicar a una regla.

**Permitir**

La acción "Permitir" de una regla indica que se permitirá el tráfico específico definido en ella.

Por ejemplo, creemos una regla con una acción para permitir todo el tráfico saliente de nuestra red hacia el puerto 80 (utilizado para el tráfico HTTP a Internet).

|Action|Source|Destination|Protocol|Port|Direction|
|---|---|---|---|---|---|
|Allow|192.168.1.0/24|Any|TCP|80|Outbound|

**Denegar**

La acción "Denegar" de una regla implica que el tráfico definido en ella se bloqueará y no se permitirá. Estas reglas son fundamentales para que el equipo de seguridad deniegue tráfico específico procedente de direcciones IP maliciosas y cree más reglas para reducir la superficie de amenaza de la red.

Por ejemplo, creemos una regla con una acción para denegar todo el tráfico entrante en el puerto 22 (utilizado para la conexión remota a una máquina mediante SSH) de nuestro servidor crítico.

|Action|Source|Destination|Protocol|Port|Direction|
|---|---|---|---|---|---|
|Deny|Any|192.168.1.0/24|TCP|22|Inbound|

**Reenviar**

La acción "Reenviar" redirige el tráfico a un segmento de red diferente mediante las reglas de reenvío creadas en los firewalls. Esto aplica a los firewalls que proporcionan funcionalidad de enrutamiento y actúan como puertas de enlace entre diferentes segmentos de red.

Por ejemplo, creemos una regla con una acción para reenviar todo el tráfico entrante en el puerto 80 (usado para el tráfico HTTP) al servidor web 192.168.1.8.

|Action|Source|Destination|Protocol|Port|Direction|
|---|---|---|---|---|---|
|Forward|Any|192.168.1.8|TCP|80|Inbound|

**Direccionalidad de las reglas**

Los firewalls tienen diferentes categorías de reglas, cada una clasificada según la direccionalidad del tráfico en el que se crean. Examinemos cada una de estas direccionalidades.

![[Pasted image 20250828214803.png]]

**Reglas de entrada**

Las reglas se clasifican como reglas de entrada cuando están diseñadas para aplicarse únicamente al tráfico entrante. Por ejemplo, podría permitir el tráfico HTTP entrante (puerto 80) en su servidor web.

**Reglas de salida**

Estas reglas están diseñadas únicamente para el tráfico saliente. Por ejemplo, bloquear todo el tráfico SMTP saliente (puerto 25) de todos los dispositivos excepto el servidor de correo.

**Reglas de reenvío**

Las reglas de reenvío se crean para reenviar tráfico específico dentro de la red. Por ejemplo, se puede crear una regla de reenvío para reenviar el tráfico HTTP entrante (puerto 80) al servidor web ubicado en su red.

Answer the questions below

Which type of action should be defined in a rule to permit any traffic?
respuesta allow

What is the direction of the rule that is created for the traffic leaving our network?
respuesta outbound


---

**==Firewall de Windows Defender==**

**Firewall de Windows Defender**

Windows Defender es un firewall integrado, introducido por Microsoft en el sistema operativo Windows. Este firewall contiene todas las funciones básicas para crear, permitir o denegar programas específicos, o crear reglas personalizadas. Esta tarea está diseñada para cubrir algunos de los componentes esenciales del Firewall de Windows Defender, que puede utilizar para restringir el tráfico de red entrante y saliente de su sistema. Para abrir este firewall, abra la búsqueda de Windows y escriba "Firewall de Windows Defender".

La página de inicio del Firewall de Windows Defender muestra los "Perfiles de red" y las opciones disponibles. Este es el panel principal con todas las opciones del firewall.

![[Pasted image 20250828215004.png]]

**Perfiles de red**

Hay dos perfiles de red disponibles. El firewall de Windows determina tu red actual según el Reconocimiento de ubicación de red (NLA) y aplica la configuración de firewall de ese perfil. Cada perfil tiene una configuración de firewall diferente.

1. **Redes privadas:** Esto incluye las configuraciones de firewall que se aplican al conectarse a nuestra red doméstica.

2. **Redes públicas o de invitados:** Esto incluye las configuraciones de firewall que se aplican al conectarse a una red pública o no confiable, como cafeterías, restaurantes, etc. Por ejemplo, al conectarse a redes públicas, puedes configurar el firewall para bloquear todas las conexiones de red entrantes y permitir solo las salientes esenciales. Esta configuración se aplicará al perfil de red pública y no se implementará cuando estés en tu red doméstica privada.

Para permitir o deshabilitar cualquier aplicación en cualquiera de tus perfiles de red, haz clic en la opción (resaltada con un 1 en la captura de pantalla). Esto te llevará a la página con todas las aplicaciones y funciones instaladas en tu sistema. Puedes marcar las que quieras permitir en cualquiera de tus perfiles de red o desmarcarlas si no las necesitas. El Firewall de Windows Defender está activado por defecto. Sin embargo, si desea activarlo o desactivarlo, puede hacer clic en la opción (resaltada con el número 2 en la captura de pantalla). Esto le llevará a la configuración de ambos perfiles de red. En lugar de desactivarlo por completo, algo que Microsoft no recomienda, también puede bloquear todas las conexiones entrantes. También puede hacer clic en "Restaurar valores predeterminados" (resaltado con el número 3 en la captura de pantalla) desde el panel principal en cualquier momento para restaurar la configuración predeterminada del firewall.

![[Pasted image 20250828215114.png]]

**Reglas personalizadas**

El Firewall de Windows Defender también permite crear reglas personalizadas para la red, permitiendo o denegando tráfico específico según sea necesario. Creemos una regla personalizada para bloquear todo el tráfico saliente en HTTP (puerto 80) o HTTPS (puerto 443). Tras crear esta regla, no podremos navegar por ningún sitio web, ya que estos sitios web operan en el puerto 80 o 443, que bloquearemos.

Antes de crear esta regla, probemos si podemos acceder a un sitio web. Para probar, visitemos http://10.10.10.10/. Como se muestra en la siguiente captura de pantalla, podemos acceder a este sitio web.

![[Pasted image 20250828215148.png]]

Para crear una regla personalizada, seleccione "Configuración avanzada" entre las opciones disponibles en el panel principal. Se abrirá una nueva pestaña donde podrá crear sus propias reglas.

Nota: La regla creada a continuación ya está disponible en la máquina virtual conectada. Si desea probarla, puede crearla en su equipo host Windows o en cualquier otro equipo.

![[Pasted image 20250828215218.png]]

Puede ver las opciones disponibles para crear reglas de entrada y salida.

![[Pasted image 20250828215241.png]]

Creemos una regla de salida para bloquear todo el tráfico HTTP y HTTPS saliente. Para ello, haga clic en la opción "Reglas de salida" a la izquierda y, a continuación, en "Nueva regla" a la derecha. Se abrirá el asistente de reglas. En el primer paso, seleccione la opción "Personalizada" y pulse "Siguiente".

![[Pasted image 20250828215303.png]]

En el segundo paso, seleccione "Todos los programas" en la siguiente opción y pulse "Siguiente". En el tercer paso, se le pedirá que seleccione el tipo de protocolo. Seleccione "TCP" como tipo de protocolo, deje el puerto local como está y cambie el puerto remoto a "Puertos específicos" en el menú desplegable. Escriba los números de puerto en el campo de abajo (en nuestro caso, 80,443). Ahora, pulse "Siguiente".

Nota: Separe los números de puerto con comas y no deje espacios entre ellos.

![[Pasted image 20250828215330.png]]


En la pestaña Ámbito, mantenga las direcciones IP locales y remotas como están y pulse el botón Siguiente. En la pestaña Acción, active la opción Bloquear la conexión y pulse Siguiente.

![[Pasted image 20250828215350.png]]

En la pestaña Perfil, mantenemos todos los perfiles de red marcados. Finalmente, el último paso es asignar un nombre a la regla y una descripción opcional, y pulsar el botón "Finalizar".

Podemos ver que nuestra regla está entre las reglas de salida disponibles.

![[Pasted image 20250828215411.png]]

Ahora, probemos nuestra regla navegando a http://10.10.10.10/. Recibimos un mensaje de error que indica que no podemos acceder a esta página, lo que significa que la regla funciona.

![[Pasted image 20250828215454.png]]

**Ejercicio**

El equipo de seguridad detectó tráfico entrante y saliente sospechoso en su sistema Windows crítico. Crearon reglas en su firewall de Windows Defender para bloquear parte del tráfico de red específico. Debe responder algunas preguntas al final de esta tarea examinando las reglas creadas.

Answer the questions below

What is the name of the rule that was created to block all incoming traffic on the SSH port?
respuesta Core Op

![[Pasted image 20250829160600.png]]

A rule was created to allow SSH from one single IP address. What is the rule name?
respuesta Infra team

![[Pasted image 20250829160615.png]]

Which IP address is allowed under this rule?
respuesta 192.168.13.7

![[Pasted image 20250829160617.png]]

---

==**Firewall iptables de Linux**==

En la tarea anterior, analizamos el firewall integrado disponible en el sistema operativo Windows. ¿Qué ocurre si eres usuario de Linux? Sigues necesitando controlar el tráfico de tu red. Linux también ofrece la funcionalidad de un firewall integrado. Disponemos de varias opciones de firewall. Repasemos brevemente la mayoría y exploremos una en detalle.

**Netfilter**

Netfilter es el framework dentro del sistema operativo Linux con las principales funcionalidades de firewall, incluyendo filtrado de paquetes, NAT y seguimiento de conexiones. Este framework sirve de base para diversas utilidades de firewall disponibles en Linux para controlar el tráfico de red. A continuación, se enumeran algunas utilidades de firewall comunes que utilizan este framework:

+ **iptables**: Esta es la utilidad más utilizada en muchas distribuciones de Linux. Utiliza el framework Netfilter, que proporciona diversas funcionalidades para controlar el tráfico de red.
+ **nftables:** Es el sucesor de la utilidad "iptables", con funciones mejoradas de filtrado de paquetes y NAT. También se basa en el framework Netfilter. 
+ **firewalld:** Esta utilidad también opera en el framework Netfilter y cuenta con conjuntos de reglas predefinidos. Funciona de forma diferente a las demás e incluye diferentes configuraciones de zona de red predefinidas.

**ufw**

ufw (Uncomplicated Firewall), como su nombre indica, elimina las complicaciones de crear reglas con una sintaxis compleja en "iptables" (o su sucesor) al ofrecer una interfaz más sencilla. Es más intuitiva para principiantes. Básicamente, cualquier regla que necesite en "iptables" puede definirse con comandos sencillos a través de ufw, lo que a su vez configuraría las reglas deseadas en "iptables". Veamos algunos comandos básicos de ufw a continuación.

Para comprobar el estado del firewall, puede usar el siguiente comando:

![[Pasted image 20250828215736.png]]

Si aparece inactivo, puedes habilitarlo usando el siguiente comando:

![[Pasted image 20250828215800.png]]

Para desactivar el firewall, escriba ``disable`` en lugar de ``enable`` en el comando anterior.

A continuación se muestra una regla creada para permitir todas las conexiones salientes desde una máquina Linux. El valor predeterminado del comando significa que se define esta política como predeterminada y permite todo el tráfico saliente, a menos que se defina una restricción de tráfico saliente para una aplicación específica en una regla independiente. También puede crear una regla para permitir o denegar el tráfico entrante en su máquina reemplazando "outgoing" por "incoming" en el siguiente comando:

![[Pasted image 20250828215830.png]]

Puede denegar el tráfico entrante en cualquier puerto de su sistema. Supongamos que queremos bloquear el tráfico SSH entrante. Podemos lograrlo con el comando ``ufw deny 22/tcp``. Como puede ver, primero especificamos la acción, en este caso "deny"; además, especificamos el puerto y el protocolo de transporte, que es el puerto TCP 22, o simplemente 22/tcp.

![[Pasted image 20250828215856.png]]

Para enumerar todas las reglas activas en un orden numerado, puede utilizar el siguiente comando:

![[Pasted image 20250828215916.png]]

Para eliminar cualquier regla, ejecute el siguiente comando con el número de regla a eliminar:

![[Pasted image 20250828215939.png]]

Estas diferentes utilidades se pueden usar para administrar Netfilter. Elegir la utilidad adecuada para Linux depende de varios factores, como la familiaridad con el sistema operativo y sus requisitos. Puede comprobar sus conocimientos sobre firewalls Linux creando algunas reglas definidas en esta tarea y probándolas para asegurarse de que funcionan correctamente.

Answer the questions below

Which Linux firewall utility is considered to be the successor of "iptables"?
respuesta nftables

What rule would you issue with ufw to deny all outgoing traffic from your machine as a default policy? (answer without sudo)
respuesta ufw default deny outgoing