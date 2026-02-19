
**==Introducción a la Respuesta a Incidentes==**

Imagina vivir en una calle con mucha inseguridad y con muchos objetos de valor en casa. Seguramente estás pensando en contratar un guardia de seguridad y varias cámaras de CCTV. Esconder los objetos de valor en una habitación subterránea secreta es una buena idea por si algún intruso consigue entrar. Estas son las medidas que debes planificar para la seguridad de tu hogar, incluso antes de que se produzca cualquier ataque.

Además de estas medidas proactivas, ¿alguna vez has considerado cómo funcionaría la situación si alguien burlara tus mecanismos de seguridad externos y accediera a tu casa? También debes tomar otras medidas después de un ataque.

Abordemos lo anterior en el ámbito digital. Quizás hayas oído hablar de algún ciberataque a alguna organización que les haya causado pérdidas de miles de dólares. Diariamente se reportan varios casos de este tipo en internet. Estos se conocen como incidentes de ciberseguridad. Al igual que en el caso anterior, donde planificaste la seguridad de tu hogar, los incidentes de ciberseguridad también requieren planificación y recursos para evitar grandes pérdidas.

La Respuesta a Incidentes gestiona un incidente de principio a fin. Desde la implementación de seguridad en varias áreas para prevenir incidentes hasta combatirlos y minimizar su impacto, la respuesta a incidentes es una guía exhaustiva.

Esta sala le ayudará a comprender los conceptos críticos de la respuesta a incidentes y le dará la oportunidad de resolver su primer incidente de manera práctica.


---

**==¿Qué son los incidentes?==**

En tus dispositivos informáticos, como portátiles, teléfonos móviles, etc., se ejecutan diversos procesos. Algunos son interactivos, lo que significa que tú realizas las acciones, como jugar un videojuego o ver un vídeo. También hay procesos no interactivos ejecutándose en segundo plano que pueden no requerir tu interacción. Son simplemente necesarios para tu dispositivo. Ambos tipos de procesos generan varios eventos. Cualquiera que sea su acción, se registra un evento.

Los eventos se generan en grandes cantidades con regularidad. Esto se debe a que muchos procesos se ejecutan en un dispositivo, cada uno realizando diferentes tareas rutinarias, lo que genera numerosos eventos. Estos eventos, en ocasiones, pueden indicar que algo está sucediendo en tu dispositivo. ¿Cómo podemos comprobar esta gran cantidad de eventos y ver si indican alguna actividad destructiva? Existen soluciones de seguridad para resolver este problema. Estos eventos se incorporan a las soluciones de seguridad como registros, y estas pueden detectar actividades dañinas en ellos. ¡Esto nos facilitó mucho el trabajo! Pero espera un momento; el verdadero reto surge después de que la solución de seguridad detecta estas actividades.

![[Pasted image 20250826162956.png]]


Por lo tanto, cuando una solución de seguridad detecta un evento o un grupo de eventos asociados con una posible actividad dañina, activa una alerta. El equipo de seguridad analiza estas alertas. Algunas pueden ser falsos positivos, mientras que otras pueden ser verdaderos positivos. Las alertas que indican algo peligroso, pero no son dañinas, se denominan falsos positivos. En cambio, las alertas que indican algo dañino y realmente son peligrosas se denominan verdaderos positivos. El siguiente ejemplo lo ilustra mejor:

**Falso positivo:** Una solución de seguridad emitió una alerta sobre la transferencia de una gran cantidad de datos desde un sistema a una dirección IP externa. Al analizar esta alerta, el equipo de seguridad descubrió que el sistema en cuestión estaba realizando una copia de seguridad en un servicio de almacenamiento en la nube, lo que provocó el incidente. Esto se conoce como falso positivo.

**Verdadero positivo:** Una solución de seguridad emitió una alerta sobre un intento de phishing contra uno de los usuarios de la organización. Al analizar esta alerta, el equipo de seguridad descubrió que el correo electrónico era de phishing, enviado a este usuario para comprometer el sistema. Esto se conoce como verdadero positivo.

Estas alertas positivas reales a veces se denominan **incidentes**. Suponiendo que la alerta ya se categoriza como incidente, el siguiente paso es asignarle un nivel de gravedad. Imagine que forma parte del equipo de seguridad y recibe varios incidentes simultáneamente. ¿A qué incidente respondería primero? Aquí es donde el concepto de gravedad del incidente resulta útil. Los incidentes se pueden clasificar como bajos, medios, altos o críticos según su impacto. Los incidentes de gravedad crítica siempre tienen la mayor prioridad, seguidos de los de gravedad alta, y así sucesivamente.

![[Pasted image 20250826162157.png]]

Answer the questions below

What is triggered after an event or group of events point at a harmful activity?
respuesta alert

If a security solution correctly identifies a harmful activity from a set of events, what type of alert is it?
respuesta true positive

If a fire alarm is triggered by smoke after cooking, is it a true positive or a false positive?
respuesta false positive

---

**==Tipos de incidentes==**

Se suele etiquetar cualquier actividad dañina asociada al mundo digital como un intento de hackeo. Esto puede ser correcto, pero es un término muy genérico en términos de ciberseguridad. Los incidentes de seguridad pueden ser de diferentes tipos. En las tareas anteriores, vimos un ejemplo de una alerta positiva real, que se convirtió en incidente tras el análisis del equipo de seguridad. Este incidente estaba relacionado con el correo electrónico de phishing, que probablemente incluía un archivo adjunto malicioso. Si se descarga en el sistema, este archivo adjunto puede tener consecuencias perjudiciales. Este es un tipo de incidente. Existen otros tipos de incidentes, que pueden ocurrir de forma independiente o en conjunto con la misma víctima.

**Infecciones de malware:** El malware es un programa malicioso que puede dañar un sistema, una red o una aplicación. La mayoría de los incidentes están asociados con infecciones de malware. Existen diferentes tipos de malware, cada uno con un potencial único de causar daños. Las infecciones de malware se deben principalmente a archivos que pueden ser texto, documentos, ejecutables, etc.

![[Pasted image 20250826164753.png]]

**Brechas de seguridad:** Las brechas de seguridad surgen cuando una persona no autorizada accede a datos confidenciales (algo que no queremos que vean ni tengan). Las brechas de seguridad son de suma importancia, ya que muchas empresas dependen de sus datos confidenciales, a los que solo el personal autorizado debe acceder.

![[Pasted image 20250826164835.png]]

**Fugas de datos:** Las fugas de datos son incidentes en los que la información confidencial de una persona u organización se expone a entidades no autorizadas. Muchos atacantes utilizan las fugas de datos para dañar la reputación de sus víctimas o utilizan esta técnica para amenazarlas y obtener lo que necesitan de ellas. A diferencia de las brechas de seguridad, las fugas de datos también pueden ser causadas involuntariamente por errores humanos o configuraciones incorrectas.

![[Pasted image 20250826164854.png]]

**Ataques internos:** Los incidentes internos de una organización se conocen como ataques internos. Imagine a un empleado descontento que infecta toda la red a través de una memoria USB en su último día. Este es un ejemplo de un ataque interno. Alguien dentro de su organización que inicia un ataque intencionalmente entra en esta categoría. Estos ataques pueden ser peligrosos, ya que un atacante interno siempre tiene mayor acceso a los recursos que un atacante externo.

![[Pasted image 20250826164906.png]]

**Ataques de Denegación de Servicio:** La disponibilidad es uno de los tres pilares de la ciberseguridad. Las soluciones de seguridad defensivas y las personas buscan constantemente maneras de proteger la información; garantizan que los datos estén disponibles para todos simultáneamente. Esto se debe a que no tiene sentido proteger algo que no está disponible para nosotros. Los ataques de Denegación de Servicio, o ataques DoS, son incidentes en los que el atacante satura un sistema, red o aplicación con solicitudes falsas, dejándolo inaccesible para los usuarios legítimos. Esto ocurre debido al agotamiento de los recursos disponibles para atender las solicitudes.

![[Pasted image 20250826164923.png]]

Todos estos incidentes tienen un potencial único para afectar negativamente a la víctima. La gravedad del impacto que generan es inconmensurable. Esto se debe a que un incidente en particular puede ser desastroso para una organización, mientras que puede causar daños menores a otra. Por ejemplo, XYZ Corp. podría no verse gravemente afectada por una fuga de datos, ya que la información que almacena puede ser inútil para cualquier otra persona. Sin embargo, podría sufrir pérdidas masivas en caso de un ataque de denegación de servicio (DoS) en su sitio web principal, ya que sus servicios dependen de él.


Answer the questions below

A user's system got compromised after downloading a file attachment from an email. What type of incident is this?
respuesta malware infection

What type of incident aims to disrupt the availability of an application?
respuesta Denial of service 


---


**==Proceso de Respuesta a Incidentes==**

En la tarea anterior, vimos diferentes tipos de incidentes. A veces, gestionar diversos incidentes en un entorno puede resultar difícil. Debido a la naturaleza específica de los incidentes en las organizaciones, es necesario contar con un proceso estructurado de respuesta. Los Marcos de Respuesta a Incidentes nos ayudan en este sentido. Estos son los enfoques genéricos que se deben seguir en cualquier incidente para lograr una respuesta eficaz. Analizaremos los dos marcos de respuesta a incidentes más utilizados: SANS y NIST.

SANS y NIST son organizaciones reconocidas que contribuyen a la ciberseguridad. SANS ha ofrecido diversos cursos y certificaciones en ciberseguridad, y NIST ha participado en el desarrollo de estándares y directrices para la ciberseguridad. Tanto SANS como NIST tienen marcos de respuesta a incidentes bastante similares.

El marco de respuesta a incidentes de SANS consta de seis fases, que se pueden denominar «PICERL» para facilitar su memorización.

| Phase           | Explanation                                                                                                                                                                                                                                                                                                                                             | Example                                                                                                                                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Preparation     | Esta es la primera fase. La fase de preparación incluye la creación de los recursos necesarios para gestionar un incidente. Estos recursos incluyen el desarrollo de equipos de respuesta a incidentes, la implementación de un plan de respuesta a incidentes adecuado y la implementación de las soluciones de seguridad necesarias para combatirlos. | Capacitación para empleados sobre correos electrónicos de phishing. Los correos electrónicos de phishing son correos fraudulentos enviados por atacantes maliciosos que pueden engañarle para que realice acciones que podrían provocar un incidente.          |
| Identification  | La fase de identificación se refiere a la búsqueda de cualquier comportamiento anormal que pueda indicar un incidente. Esto implica el uso de diversas soluciones y técnicas de seguridad para monitorear eventos anormales.                                                                                                                            | El equipo de seguridad detecta una gran cantidad de datos que se envían desde uno de los hosts. Tras el análisis, se descubrió que estaba comprometido tras la descarga de un archivo malicioso desde un archivo adjunto de un correo electrónico de phishing. |
| Containment     | Una vez identificado un incidente, el siguiente paso debe ser contenerlo. Esto implica minimizar el impacto del ataque. Esto suele lograrse aislando el equipo afectado, desactivando las cuentas de usuario comprometidas, etc.                                                                                                                        | El equipo de seguridad aísla el host de la red para minimizar el impacto e impedir que el atacante acceda a otros sistemas, aprovechando el host comprometido.                                                                                                 |
| Eradication     | Esta fase, como su nombre indica, consiste en eliminar la amenaza del entorno atacado. La amenaza puede ser de cualquier tipo. La fase de erradicación garantizará que el entorno afectado esté limpio, y ahora podemos pasar a la fase de recuperación.                                                                                                | Se realizó un análisis exhaustivo de malware en el sistema para eliminar el software malicioso del host.                                                                                                                                                       |
| Recovery        | La fase de recuperación es fundamental en esta cadena. Implica recuperar los sistemas afectados a partir de la copia de seguridad o reconstruirlos. Los sistemas recuperados se prueban y están listos para su uso.                                                                                                                                     | El host comprometido se reconfiguró y los datos extraídos se restauraron a partir de la copia de seguridad.                                                                                                                                                    |
| Lessons Learned | Esta es también una parte importante del ciclo de respuesta a incidentes. Se identifican y documentan las deficiencias en la detección y el análisis del incidente, lo que ayuda a mejorar el proceso general en futuros incidentes.                                                                                                                    | Se lleva a cabo una reunión de revisión posterior al incidente para analizar su causa raíz y mejorar la seguridad para prevenir futuros ataques.                                                                                                               |

![[Pasted image 20250826170453.png]]

El Marco de Respuesta a Incidentes del NIST es similar al marco SANS que estudiamos anteriormente. El número de fases de este marco se reduce a 4.

![[Pasted image 20250826170517.png]]

A continuación se muestra la comparación de ambos:

![[Pasted image 20250826170541.png]]

Las organizaciones pueden derivar sus procesos de respuesta a incidentes siguiendo estos marcos. Cada proceso cuenta con un documento formal que enumera todos los procedimientos organizacionales relevantes. El documento formal de respuesta a incidentes se denomina **Plan de Respuesta a Incidentes**. Este documento estructurado describe el enfoque durante cualquier incidente. Está aprobado formalmente por la alta dirección y contiene los procedimientos a seguir antes, durante y después de que se complete un incidente.

Los componentes clave de este plan incluyen (entre otros):

-Roles y responsabilidades
-Metodología de respuesta a incidentes
-Plan de comunicación con las partes interesadas, incluidas las fuerzas del orden
-Ruta de escalamiento a seguir

Answer the questions below

The Security team disables a machine's internet connection after an incident. Which phase of the SANS IR lifecycle is followed here?
respuesta containment

Which phase of NIST corresponds with the lessons learned phase of the SANS IR lifecycle?
respuesta post incident activity


---

**==Técnicas de Respuesta a Incidentes==**

Recuerde que estudiamos la segunda fase del ciclo de vida de la respuesta a incidentes: "Identificación" en SANS y "Detección y Análisis" en NIST. Es muy difícil detectar comportamientos anormales e identificar incidentes manualmente. Existen múltiples soluciones de seguridad que cumplen funciones específicas para detectar incidentes. Algunas incluso pueden responder a los incidentes y ejecutar las demás fases del ciclo de vida, como la contención, la erradicación, etc. A continuación, se ofrece una breve explicación de algunas de estas soluciones:

**-SIEM:** La Solución de Gestión de Información y Eventos de Seguridad (SIEM) recopila todos los registros importantes en una ubicación centralizada y los correlaciona para identificar incidentes.
**-AV:** El antivirus (AV) detecta programas maliciosos conocidos en un sistema y los analiza periódicamente.
**-EDR:** La Detección y Respuesta de Endpoints (EDR) se implementa en todos los sistemas, protegiéndolos contra algunas amenazas avanzadas. Esta solución también puede contener y erradicar la amenaza.

![[Pasted image 20250826172225.png]]

Tras identificar los incidentes, se deben seguir ciertos procedimientos, como investigar el alcance del ataque, tomar las medidas necesarias para prevenir daños mayores y eliminarlo de raíz. Estos pasos pueden variar según el tipo de incidente. En este caso, contar con instrucciones paso a paso para abordar cada tipo de incidente ayuda a ahorrar mucho tiempo. Este tipo de instrucciones se conocen como **Manuales de Estrategia**.

Los Manuales de Estrategia son las directrices para una respuesta integral a incidentes.

A continuación, se muestra un ejemplo de Manual de Estrategia para un incidente: Correo electrónico de phishing.

1. Notificar a todas las partes interesadas sobre el incidente de correo electrónico de phishing.
2. Determinar si el correo electrónico era malicioso mediante un análisis del encabezado y el cuerpo del correo.
3. Buscar archivos adjuntos en el correo electrónico y analizarlos.
4. Determinar si alguien abrió los archivos adjuntos.
5. Aislar los sistemas infectados de la red.
6. Bloquear al remitente del correo electrónico.

Por otro lado, los **Manuales de Operaciones** son la ejecución detallada, paso a paso, de pasos específicos durante diferentes incidentes. Estos pasos pueden variar según los recursos disponibles para la investigación.

Answer the questions below

Step-by-step comprehensive guidelines for incident response are known as?
respuesta Playbooks


---

**==Respuesta a Incidentes de Laboratorio==**

Escenario: En esta tarea, iniciará un incidente descargando un archivo adjunto de un correo electrónico de phishing. El archivo adjunto es malware. Una vez descargado el archivo, se iniciará un incidente. Ahora comenzará a investigarlo. La primera fase consiste en determinar cuántos hosts están infectados con este mismo archivo, ya que es muy probable que una sola campaña de phishing se dirija a varios empleados de la misma organización. Verá algunos hosts en los que este archivo se ejecutó después de descargarse y otros en los que solo se descargó. Realizará las acciones necesarias en todos estos hosts y verá una cronología detallada de los eventos en el host infectado.

Realizará una respuesta completa a incidentes después de que un correo electrónico de phishing afecte a varios hosts de una red. Debe seguir los pasos indicados en el sitio y responder a las preguntas a continuación:

Answer the questions below

What was the name of the malicious email sender?
respuesta Jeff Johnson

What was the threat vector?
respuesta Email Attachment

How many devices downloaded the email attachment?
respuesta 3

How many devices executed the file?
respuesta 1

What is the flag found at the end of the exercise?
respuesta THM{My_First_Incident_Response}


---

**==Conclusión==**

En esta sala, aprendimos sobre los diferentes conceptos de respuesta a incidentes. Estudiamos cómo y cuándo se clasifica un evento como incidente y las prioridades asignadas a cada uno. También analizamos los tipos de incidentes y los marcos de respuesta a incidentes: SANS y NIST, que nos guían en la gestión de incidentes. Por último, vimos algunas herramientas para la respuesta a incidentes y realizamos un laboratorio práctico realista.