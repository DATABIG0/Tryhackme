
**==Introducción==**

La seguridad se ha convertido en un término de moda; todas las empresas quieren afirmar que sus productos o servicios son seguros. ¿Pero lo son?

Antes de analizar los diferentes principios de seguridad, es fundamental conocer al adversario contra el que protegemos nuestros activos. ¿Intenta impedir que un niño pequeño acceda a su portátil? ¿O intenta proteger un portátil que contiene diseños técnicos que valen millones de dólares? Utilizar los mismos mecanismos de protección contra niños pequeños y agentes de espionaje industrial sería absurdo. Por lo tanto, conocer a nuestro adversario es fundamental para poder comprender sus ataques y comenzar a implementar los controles de seguridad adecuados.
![[Pasted image 20250909160209.png]]

Es imposible lograr una seguridad perfecta; ninguna solución es 100 % segura. Por lo tanto, intentamos mejorar nuestra estrategia de seguridad para dificultar el acceso de nuestros adversarios.

---

**==CIA==**

![[Pasted image 20250909160306.png]]

Antes de poder describir algo como seguro, debemos considerar mejor qué constituye la seguridad. Al evaluar la seguridad de un sistema, es necesario considerar la tríada de seguridad: confidencialidad, integridad y disponibilidad (CIA).

- **La confidencialidad** garantiza que solo las personas o destinatarios previstos puedan acceder a los datos.
- **La integridad** busca garantizar que los datos no se puedan alterar; además, podemos detectar cualquier alteración si se produce.
- **La disponibilidad** busca garantizar que el sistema o servicio esté disponible cuando se necesite.

![[Pasted image 20250909160358.png]]

Consideremos la tríada de seguridad de la CIA al realizar un pedido en línea:

- **Confidencialidad**: Al comprar en línea, espera que su número de tarjeta de crédito se revele únicamente a la entidad que procesa el pago. Si duda de que la información de su tarjeta de crédito se divulgue a alguien no confiable, lo más probable es que no continúe con la transacción. Además, si una filtración de datos resulta en la divulgación de información personal identificable, incluyendo tarjetas de crédito, la empresa sufrirá enormes pérdidas a múltiples niveles.
- **Integridad**: Después de completar su pedido, si un intruso logra alterar la dirección de envío que proporcionó, el paquete se enviará a otra persona. Sin integridad de datos, podría ser muy reacio a realizar su pedido a este vendedor.
- **Disponibilidad**: Para realizar su pedido en línea, deberá navegar por el sitio web de la tienda o usar su aplicación oficial. Si el servicio no está disponible, no podrá explorar los productos ni realizar un pedido. Si continúa teniendo problemas técnicos, podría finalmente darse por vencido y comenzar a buscar otra tienda en línea. 

Consideremos la CIA en relación con los historiales médicos de los pacientes y los sistemas relacionados:

- **Confidencialidad**: Según diversas leyes en los países modernos, los profesionales sanitarios deben garantizar y mantener la confidencialidad de los historiales médicos. En consecuencia, pueden ser considerados legalmente responsables si divulgan ilegalmente los historiales médicos de sus pacientes.
- **Integridad**: Si el historial de un paciente se altera accidental o maliciosamente, puede dar lugar a la administración de un tratamiento incorrecto, lo que, a su vez, puede poner en peligro la vida. Por lo tanto, el sistema sería inútil y potencialmente perjudicial si no se garantiza la integridad de los historiales médicos.
- **Disponibilidad**: Cuando un paciente acude a una clínica para realizar un seguimiento de su estado de salud, el sistema debe estar disponible. Un sistema no disponible significaría que el médico no puede acceder al historial del paciente y, en consecuencia, no sabrá si algún síntoma actual está relacionado con su historial médico. Esta situación puede dificultar el diagnóstico médico y hacerlo más propenso a errores.

El énfasis no tiene por qué ser el mismo en las tres funciones de seguridad. Un ejemplo sería un anuncio universitario. Aunque no suele ser confidencial, la integridad del documento es crucial.

**Más allá de la CIA**

![[Pasted image 20250909160530.png]]

Yendo un paso más allá de la tríada de seguridad de la CIA, podemos pensar en:

- **Autenticidad**: Auténtico significa no ser fraudulento ni falsificado. La autenticidad consiste en garantizar que el documento, archivo o dato proviene de la fuente declarada.
- **No repudio**: Repudiar significa negarse a reconocer la validez de algo. El no repudio garantiza que la fuente original no pueda negar ser la fuente de un documento, archivo o dato en particular. Esta característica es indispensable en diversos ámbitos, como las compras, el diagnóstico de pacientes y la banca.

Estos dos requisitos están estrechamente relacionados. La necesidad de distinguir los archivos o pedidos auténticos de los falsos es indispensable. Además, garantizar que la otra parte no pueda negar ser la fuente es vital para la operatividad de muchos sistemas.

En las compras en línea, dependiendo de su negocio, podría tolerar intentar entregar una camiseta con pago contra reembolso y luego descubrir que el destinatario nunca realizó dicho pedido. Sin embargo, ninguna empresa puede tolerar enviar 1000 coches para descubrir que el pedido es falso. En el ejemplo de un pedido de compra, se desea confirmar que el cliente efectivamente realizó el pedido; esto se conoce como autenticidad. Además, se desea garantizar que no pueda negar la realización del pedido; esto se conoce como no repudio.

Como empresa, si recibe un pedido de 1000 automóviles, debe garantizar la autenticidad del pedido; además, la fuente no debe poder negar la realización del mismo. Sin autenticidad ni no repudio, la empresa no puede operar.

**Héxada Parkeriana**

En 1998, Donn Parker propuso la Hexada Parkeriana, un conjunto de seis elementos de seguridad. Estos son:

1. Disponibilidad
2. Utilidad
3. Integridad
4. Autenticidad
5. Confidencialidad
6. Posesión


Ya hemos abordado cuatro de los seis elementos anteriores. Analicemos los dos restantes:

- **Utilidad**: La utilidad se centra en la utilidad de la información. Por ejemplo, un usuario podría haber perdido la clave de descifrado para acceder a un portátil con almacenamiento cifrado. Aunque el usuario aún conserva la computadora portátil con sus discos intactos, no puede acceder a ellos. En otras palabras, aunque aún está disponible, la información se encuentra en un formato inservible, es decir, sin utilidad.
- **Posesión**: Este elemento de seguridad exige que protejamos la información de la apropiación, copia o control no autorizados. Por ejemplo, un adversario podría robar una unidad de respaldo, lo que significa que perderíamos la posesión de la información mientras la tenga. Por otro lado, el adversario podría cifrar nuestros datos mediante ransomware; esto también conlleva la pérdida de la posesión de los datos.

**Answer the questions below**

Click on "View Site" and answer the five questions. What is the flag that you obtained at the end?
respuesta  THM{CIA_TRIAD}

---

**==DAD==**

![[Pasted image 20250922173941.png]]

La seguridad de un sistema se ve atacada por varios medios. Puede ser mediante la divulgación, alteración o destrucción de datos secretos.

- Divulgación es lo opuesto a confidencialidad. En otras palabras, la divulgación de datos confidenciales constituiría un ataque a la confidencialidad.
- Alteración es lo opuesto a Integridad. Por ejemplo, la integridad de un cheque es indispensable.
- Destrucción/Denegación es lo opuesto a Disponibilidad.

Lo opuesto a la tríada CIA sería la tríada DAD: Divulgación, Alteración y Destrucción.

Considere el ejemplo anterior de los historiales médicos y los sistemas relacionados:

- **Divulgación**: Como en la mayoría de los países modernos, los profesionales sanitarios deben mantener la confidencialidad de los historiales médicos. Por lo tanto, si un atacante logra robar algunos de estos historiales médicos y publicarlos en línea para su consulta pública, el profesional sanitario sufrirá pérdidas debido a este ataque de divulgación de datos.
- **Alteración**: Considere la gravedad de la situación si el atacante logra modificar los historiales médicos del paciente. Este ataque de alteración podría provocar la administración de un tratamiento incorrecto y, en consecuencia, podría poner en peligro la vida.
- **Destrucción/Denegación**: Consideremos el caso de un centro médico que ha dejado de usar papel por completo. Si un atacante logra que los sistemas de bases de datos no estén disponibles, el centro no podrá funcionar correctamente. Podrían volver al papel temporalmente; sin embargo, los historiales clínicos de los pacientes no estarían disponibles. Este ataque de denegación paralizaría todo el centro.

Protegerse contra la divulgación, la alteración y la destrucción/denegación es fundamental. Esta protección equivale a trabajar para mantener la confidencialidad, la integridad y la disponibilidad.

Proteger la confidencialidad y la integridad al extremo puede restringir la disponibilidad, y aumentar la disponibilidad al extremo puede resultar en la pérdida de confidencialidad e integridad. Una buena implementación de los principios de seguridad requiere un equilibrio entre estos tres factores.

**Answer the questions below**

The attacker managed to gain access to customer records and dumped them online. What is this attack?
respuesta  **Disclosure**

A group of attackers were able to locate both the main and the backup power supply systems and switch them off. As a result, the whole network was shut down. What is this attack?
respuesta **Destruction/Denial**


---

**Conceptos Fundamentales de los Modelos de Seguridad**

Hemos aprendido que la tríada de seguridad está representada por Confidencialidad, Integridad y Disponibilidad (CIA). Cabe preguntarse: ¿cómo podemos crear un sistema que garantice una o más funciones de seguridad? La respuesta estaría en el uso de modelos de seguridad. En esta tarea, presentaremos tres modelos de seguridad fundamentales:

- Modelo Bell-LaPadula
- Modelo de Integridad de Biba
- Modelo de Clark-Wilson

**Modelo Bell-LaPadula**

El Modelo Bell-LaPadula busca lograr la confidencialidad mediante la especificación de tres reglas:

- **Propiedad de Seguridad Simple**: Esta propiedad, denominada "no lectura ascendente", establece que un sujeto con un nivel de seguridad inferior no puede leer un objeto con un nivel de seguridad superior. Esta regla impide el acceso a información sensible por encima del nivel autorizado.
- **Propiedad de Seguridad Estrella**: Esta propiedad, denominada "no escritura descendente", establece que un sujeto con un nivel de seguridad superior no puede escribir en un objeto con un nivel de seguridad inferior. Esta regla impide la divulgación de información sensible a un sujeto con un nivel de seguridad inferior.
- **Propiedad de Seguridad Discrecional**: Esta propiedad utiliza una matriz de acceso para permitir operaciones de lectura y escritura.

En la tabla a continuación se muestra un ejemplo de matriz de acceso, que se utiliza junto con las dos primeras propiedades.

| Subjects  | Object A   | Object B  |
| --------- | ---------- | --------- |
| Subject 1 | Write      | No access |
| Subject 2 | Read/Write | Read      |

Las dos primeras propiedades se pueden resumir como "escribir, leer". Se puede compartir información confidencial con personas con mayor habilitación de seguridad (escribir) y recibir información confidencial de personas con menor habilitación de seguridad (leer).

El modelo Bell-LaPadula tiene ciertas limitaciones. Por ejemplo, no fue diseñado para gestionar el intercambio de archivos.

**Modelo Biba**

El modelo Biba busca lograr la integridad mediante la especificación de dos reglas principales:

- **Propiedad de integridad simple**: Esta propiedad se conoce como "no leer"; un sujeto con mayor integridad no debe leer de un objeto con menor integridad.
- **Propiedad de integridad estrella**: Esta propiedad se conoce como "no escribir"; un sujeto con menor integridad no debe escribir en un objeto con mayor integridad.

Estas dos propiedades se pueden resumir como "leer, escribir". Esta regla contrasta con el modelo Bell-LaPadula, lo cual no debería sorprender, ya que uno se centra en la confidencialidad mientras que el otro en la integridad.

El modelo Biba presenta varias limitaciones. Un ejemplo es que no gestiona amenazas internas (amenazas internas).

**Modelo Clark-Wilson**

El modelo Clark-Wilson también busca lograr la integridad mediante los siguientes conceptos:

- **Elemento de datos restringido (CDI)**: Se refiere al tipo de datos cuya integridad se desea preservar.
- **Elemento de datos no restringido (UDI)**: Se refiere a todos los tipos de datos más allá del CDI, como la entrada del usuario y del sistema.
- **Procedimientos de transformación (TP)**: Estos procedimientos son operaciones programadas, como lectura y escritura, y deben mantener la integridad de los CDI.
- **Procedimientos de verificación de integridad (IVP)**: Estos procedimientos verifican y garantizan la validez de los CDI.

Solo hemos cubierto tres modelos de seguridad. El lector puede explorar muchos otros modelos de seguridad. Algunos ejemplos incluyen:

- Modelo de Brewer y Nash
- Modelo de Goguen-Meseguer
- Modelo de Sutherland
- Modelo de Graham-Denning
- Modelo de Harrison-Ruzzo-Ullman

**Answer the questions below**

Click on "View Site" and answer the four questions. What is the flag that you obtained at the end?
respuesta  THM{SECURITY_MODELS}

---

**==Defensa en profundidad==**

![[Pasted image 20250922174732.png]]

**Defensa en Profundidad** se refiere a crear un sistema de seguridad de múltiples niveles; por eso también se le llama Seguridad Multinivel.

Considere la siguiente analogía: tiene un cajón cerrado con llave donde guarda sus documentos importantes y objetos de valor. El cajón está cerrado con llave; sin embargo, ¿quiere que esta cerradura sea lo único que se interponga entre un ladrón y sus objetos de valor? Si pensamos en la seguridad multinivel, preferiríamos que el cajón estuviera cerrado con llave, la habitación correspondiente, la puerta principal del apartamento, la verja del edificio, e incluso podría incluir algunas cámaras de seguridad. Aunque estos múltiples niveles de seguridad no pueden detener a todos los ladrones, bloquearían a la mayoría y ralentizarían a los demás.


---

**==ISO/IEC 19249==**

La Organización Internacional de Normalización (ISO) y la Comisión Electrotécnica Internacional (IEC) han creado la norma ISO/IEC 19249. En esta tarea, repasaremos brevemente la norma ISO/IEC 19249:2017 Tecnologías de la información - Técnicas de seguridad - Catálogo de principios de arquitectura y diseño para productos, sistemas y aplicaciones seguros. El objetivo es comprender mejor lo que las organizaciones internacionales enseñarían sobre los principios de seguridad.

La norma ISO/IEC 19249 enumera cinco principios de arquitectura:

1. **Separación de dominios**: Cada conjunto de componentes relacionados se agrupa como una sola entidad; los componentes pueden ser aplicaciones, datos u otros recursos. Cada entidad tendrá su propio dominio y se le asignará un conjunto común de atributos de seguridad. Por ejemplo, considere los niveles de privilegio del procesador x86: el núcleo del sistema operativo puede ejecutarse en el anillo 0 (el nivel más privilegiado). En cambio, las aplicaciones en modo usuario pueden ejecutarse en el anillo 3 (el nivel menos privilegiado). La separación de dominios está incluida en el Modelo de Goguen-Meseguer. 
2. **Capas**: Cuando un sistema se estructura en muchos niveles abstractos, es posible imponer políticas de seguridad a diferentes niveles; además, sería factible validar su funcionamiento. Consideremos el modelo OSI (Interconexión de Sistemas Abiertos) con sus siete capas en redes. Cada capa del modelo OSI proporciona servicios específicos a la capa superior. Esta estratificación permite imponer políticas de seguridad y validar fácilmente que el sistema funciona según lo previsto. Otro ejemplo en el mundo de la programación son las operaciones de disco; un programador suele utilizar las funciones de lectura y escritura de disco proporcionadas por el lenguaje de programación de alto nivel elegido. El lenguaje de programación oculta las llamadas al sistema de bajo nivel y las presenta como métodos más intuitivos. La estratificación se relaciona con la defensa en profundidad.
3. **Encapsulación**: En la programación orientada a objetos (POO), ocultamos las implementaciones de bajo nivel y evitamos la manipulación directa de los datos de un objeto proporcionando métodos específicos para tal fin. Por ejemplo, si se tiene un objeto de reloj, se proporcionaría un método increment() en lugar de dar al usuario acceso directo a la variable de segundos. El objetivo es evitar valores no válidos para las variables. De manera similar, en sistemas más grandes, se usaría (o incluso diseñaría) una interfaz de programación de aplicaciones (API) adecuada que la aplicación utilizaría para acceder a la base de datos.
4. **Redundancia**: Este principio garantiza la disponibilidad y la integridad. Existen numerosos ejemplos relacionados con la redundancia. Consideremos el caso de un servidor de hardware con dos fuentes de alimentación integradas: si una falla, el sistema continúa funcionando. Consideremos una configuración RAID 5 con tres unidades: si una falla, los datos permanecen disponibles en las dos restantes. Además, si se modifican incorrectamente los datos en uno de los discos, se detectaría mediante la paridad, lo que garantiza la integridad de los datos.
5. **Virtualización**: Con la llegada de los servicios en la nube, la virtualización se ha vuelto más común y popular. El concepto de virtualización consiste en compartir un único conjunto de hardware entre varios sistemas operativos. La virtualización proporciona capacidades de sandboxing que mejoran los límites de seguridad, la detonación segura y la vigilancia de programas maliciosos.

La norma ISO/IEC 19249 enseña cinco principios de diseño:

1. **Privilegio mínimo**: También se puede definir informalmente como "según la necesidad" o "según la necesidad de saber", al responder a la pregunta "¿quién puede acceder a qué?". El principio del privilegio mínimo enseña que se debe proporcionar la menor cantidad de permisos posible para que cada persona realice su tarea, y nada más. Por ejemplo, si un usuario necesita ver un documento, se le deben otorgar permisos de lectura sin derechos de escritura.
2. **Minimización de la superficie de ataque**: Todo sistema tiene vulnerabilidades que un atacante podría utilizar para comprometerlo. Algunas vulnerabilidades son conocidas, mientras que otras aún no se han descubierto. Estas vulnerabilidades representan riesgos que debemos intentar minimizar. Por ejemplo, en uno de los pasos para reforzar un sistema Linux, deshabilitaríamos cualquier servicio que no necesitemos.
3. **Validación centralizada de parámetros**: Muchas amenazas se deben a que el sistema recibe información, especialmente de los usuarios. Las entradas no válidas pueden utilizarse para explotar vulnerabilidades del sistema, como la denegación de servicio y la ejecución remota de código. Por lo tanto, la validación de parámetros es un paso necesario para garantizar el estado correcto del sistema. Considerando la cantidad de parámetros que maneja un sistema, su validación debe centralizarse en una biblioteca o sistema.
4. **Servicios de seguridad general centralizados**: Como principio de seguridad, debemos centralizar todos los servicios de seguridad. Por ejemplo, crearíamos un servidor centralizado para la autenticación. Por supuesto, se podrían tomar las medidas adecuadas para garantizar la disponibilidad y evitar la creación de un punto único de fallo.
5. **Preparación para la gestión de errores y excepciones**: Al crear un sistema, debemos tener en cuenta que los errores y las excepciones ocurren y ocurrirán. Por ejemplo, en una aplicación de compras, un cliente podría intentar realizar un pedido de un artículo agotado. Una base de datos podría sobrecargarse y dejar de responder a una aplicación web. Este principio enseña que los sistemas deben diseñarse a prueba de fallos; por ejemplo, si un firewall falla, debería bloquear todo el tráfico en lugar de permitirlo. Además, debemos tener cuidado de que los mensajes de error no filtren información que consideramos confidencial, como el volcado de contenido de memoria que contiene información relacionada con otros clientes.

En las siguientes preguntas, consulte los cinco principios de diseño de la norma ISO/IEC 19249 mencionados anteriormente. Responda con un número entre 1 y 5, según el número del principio de diseño.

**Answer the questions below**

Which principle are you applying when you turn off an insecure server that is not critical to the business?
respuesta 2 capas

Your company hired a new sales representative. Which principle are they applying when they tell you to give them access only to the company products and prices?
respuesta 1 privilegio minimo

While reading the code of an ATM, you noticed a huge chunk of code to handle unexpected situations such as network disconnection and power failure. Which principle are they applying?
respuesta 5 preparacion para la gestion de errores 


---

**==Confianza Cero versus Confianza pero Verificación==**

La confianza es un tema muy complejo; en realidad, no podemos funcionar sin confianza. Si uno pensara que el fabricante del portátil ha instalado spyware en él, lo más probable es que terminara reconstruyendo el sistema. Si desconfiara del fabricante del hardware, dejaría de usarlo por completo. Si consideramos la confianza a nivel empresarial, la situación se vuelve aún más sofisticada; sin embargo, necesitamos algunos principios rectores de seguridad. Dos principios de seguridad que nos interesan en relación con la confianza son:

- Confianza pero Verificación
- Confianza Cero

**Confianza pero Verificación**: Este principio enseña que siempre debemos verificar, incluso cuando confiamos en una entidad y su comportamiento. Una entidad puede ser un usuario o un sistema. Verificar generalmente requiere establecer mecanismos de registro adecuados; verificar significa revisar los registros para garantizar que todo funcione correctamente. En realidad, no es posible verificarlo todo; basta con pensar en el trabajo que supone revisar todas las acciones realizadas por una sola entidad, como las páginas de internet visitadas por un solo usuario. Esto requiere mecanismos de seguridad automatizados, como proxy, detección de intrusiones y sistemas de prevención de intrusiones.

**Confianza Cero**: Este principio considera la confianza como una vulnerabilidad y, en consecuencia, protege contra amenazas internas. Tras considerar la confianza como una vulnerabilidad, la confianza cero intenta eliminarla. Implica indirectamente la enseñanza de "nunca confíes, siempre verifica". En otras palabras, toda entidad se considera adversaria hasta que se demuestre lo contrario. La confianza cero no otorga confianza a un dispositivo en función de su ubicación o propiedad. Este enfoque contrasta con los modelos anteriores que confiaban en redes internas o dispositivos empresariales. Se requiere autenticación y autorización antes de acceder a cualquier recurso. Por lo tanto, si se produce una vulneración, el daño estaría más contenido si se hubiera implementado una arquitectura de confianza cero.

La microsegmentación es una de las implementaciones utilizadas para la confianza cero. Se refiere al diseño donde un segmento de red puede ser tan pequeño como un solo host. Además, la comunicación entre segmentos requiere autenticación, comprobaciones de listas de control de acceso y otros requisitos de seguridad.

Existe un límite en cuanto a la aplicación de la confianza cero sin afectar negativamente a una empresa; Sin embargo, esto no significa que no debamos aplicarlo siempre que sea posible.


---

**==Amenaza versus Riesgo==**

![[Pasted image 20251016182248.png]]

Hay tres términos que debemos tener en cuenta para evitar confusiones.

- **Vulnerabilidad**: Vulnerable significa susceptible a ataques o daños. En seguridad de la información, una vulnerabilidad es una debilidad.
- **Amenaza**: Una amenaza es un peligro potencial asociado a esta debilidad o vulnerabilidad.
- **Riesgo**: El riesgo se refiere a la probabilidad de que un agente amenazante explote una vulnerabilidad y el consiguiente impacto en el negocio.

Más allá de los sistemas de información, una sala de exposición con puertas y ventanas de vidrio estándar presenta una debilidad o vulnerabilidad debido a la naturaleza del vidrio. Por consiguiente, existe la amenaza de que las puertas y ventanas de vidrio se rompan. Los propietarios de la sala de exposición deben considerar el riesgo, es decir, la probabilidad de que una puerta o ventana de vidrio se rompa y el consiguiente impacto en el negocio.

Considere otro ejemplo directamente relacionado con los sistemas de información. Usted trabaja en un hospital que utiliza un sistema de base de datos específico para almacenar todos los historiales médicos. Un día, mientras sigues las últimas noticias de seguridad, descubres que el sistema de base de datos utilizado no solo es vulnerable, sino que además se ha publicado un código de explotación de prueba de concepto funcional. Este código indica que la amenaza es real. Con esta información, debes considerar el riesgo resultante y decidir los siguientes pasos.

Abordaremos las amenazas y los riesgos en detalle en una sala aparte.


---

**==Conclusión==**

En esta sala se abordaron diversos principios y conceptos relacionados con la seguridad. A estas alturas, ya debería estar familiarizado con CIA y DAD, así como con otros términos como autenticidad, repudio, vulnerabilidad, amenaza y riesgo. Analizamos tres modelos de seguridad y la norma ISO/IEC 19249. Hemos abordado diferentes principios de seguridad, como defensa en profundidad, confiar pero verificar y confianza cero.

Finalmente, cabe mencionar el Modelo de Responsabilidad Compartida, especialmente dada la creciente dependencia de los servicios en la nube. Se requieren diversos aspectos para garantizar una seguridad adecuada, como el hardware, la infraestructura de red, los sistemas operativos, las aplicaciones, etc. Sin embargo, los clientes que utilizan servicios en la nube tienen diferentes niveles de acceso según el servicio que utilicen. Por ejemplo, un usuario de Infraestructura como Servicio (IaaS) tiene control (y responsabilidad) total sobre el sistema operativo.

Por otro lado, un usuario de Software como Servicio (SaaS) no tiene acceso directo al sistema operativo subyacente. Por lo tanto, lograr la seguridad en un entorno de nube requiere que tanto el proveedor de servicios en la nube como el usuario cumplan con su parte. El Modelo de Responsabilidad Compartida es un marco de seguridad en la nube que garantiza que cada parte sea consciente de su responsabilidad.

Tras finalizar la clase de Principios de Seguridad, puede pasar a la clase de Introducción a la Criptografía.