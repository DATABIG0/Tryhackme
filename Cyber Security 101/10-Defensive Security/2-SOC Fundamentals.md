
**==Introducción al SOC==**

La tecnología ha hecho nuestras vidas más eficientes, pero esta eficiencia conlleva una mayor responsabilidad. Los temores actuales han evolucionado significativamente desde la explotación de activos físicos. Los datos críticos, conocidos como secretos, ya no se almacenan en archivos físicos. Las organizaciones manejan grandes cantidades de datos confidenciales en sus redes y sistemas. Cualquier interrupción, pérdida o modificación no autorizada de estos datos puede causarles graves daños. Los actores de amenazas descubren y explotan nuevas vulnerabilidades en estas redes y sistemas a diario, lo que se convierte en una preocupación importante en ciberseguridad. Las prácticas de seguridad tradicionales pueden no ser suficientes para prevenir muchas de estas amenazas. Es fundamental dedicar un equipo completo a la gestión de la seguridad de su organización.

Un SOC (Centro de Operaciones de Seguridad) es una instalación dedicada operada por un equipo de seguridad especializado. Este equipo tiene como objetivo supervisar continuamente la red y los recursos de una organización e identificar actividades sospechosas para prevenir daños. Este equipo trabaja las 24 horas del día, los siete días de la semana.

En esta sesión se profundizará en algunos conceptos clave del SOC, uno de los campos más importantes de la seguridad defensiva.

Answer the questions below

What does the term SOC stand for?
Security Operations Center 


---

**==Propósito y Componentes==**

El objetivo principal del equipo del SOC es mantener la Detección y la Respuesta intactas. El equipo del SOC cuenta con recursos disponibles en forma de soluciones de seguridad que le ayudan a lograrlo. Estas soluciones integran la red y todos los sistemas de la empresa para supervisarlos desde una ubicación centralizada. Se requiere una monitorización continua para detectar y responder a cualquier incidente de seguridad.

![[Pasted image 20250823162022.png]]


**Detección**

-**Detectar vulnerabilidades:** Una vulnerabilidad es una debilidad que un atacante puede explotar para realizar acciones que exceden su nivel de permiso. Una vulnerabilidad puede descubrirse en el software de cualquier dispositivo (sistema operativo y programas), como un servidor o un ordenador. Por ejemplo, el SOC podría descubrir un conjunto de ordenadores con MS Windows que deben ser parcheados contra una vulnerabilidad publicada específica. En sentido estricto, las vulnerabilidades no son necesariamente responsabilidad del SOC; sin embargo, las vulnerabilidades no corregidas afectan la seguridad de toda la empresa.

-**Detectar actividad no autorizada:** Consideremos el caso en el que un atacante descubrió el nombre de usuario y la contraseña de uno de los empleados y los utilizó para iniciar sesión en el sistema de la empresa. Es crucial detectar este tipo de actividad no autorizada rápidamente antes de que cause daños. Numerosas pistas, como la ubicación geográfica, pueden ayudarnos a detectarlo.

-**Detectar infracciones de políticas:** Una política de seguridad es un conjunto de reglas y procedimientos creados para proteger a una empresa contra amenazas de seguridad y garantizar su cumplimiento. Lo que se considera una infracción varía según la empresa; por ejemplo, la descarga de archivos multimedia pirateados y el envío inseguro de archivos confidenciales de la empresa.

-**Detectar intrusiones**: Las intrusiones se refieren al acceso no autorizado a sistemas y redes. Un escenario podría ser que un atacante explote con éxito nuestra aplicación web. Otro sería que un usuario visite un sitio malicioso e infecte su equipo.

**Respuesta**

-**Apoyo en la respuesta a incidentes:** Una vez detectado un incidente, se toman ciertas medidas para responder. Esta respuesta incluye minimizar su impacto y realizar un análisis de la causa raíz del incidente. El equipo del SOC también ayuda al equipo de respuesta a incidentes a llevar a cabo estas medidas.

Un SOC se compone de tres pilares. Con todos estos pilares, un equipo del SOC alcanza la madurez necesaria para detectar y responder eficazmente a diferentes incidentes. Estos pilares son las personas, los procesos y la tecnología.

Las personas, los procesos y la tecnología coexisten en un entorno SOC. Un equipo de profesionales que trabaja con herramientas de seguridad de vanguardia y con los procesos adecuados es lo que define un entorno SOC maduro.

En las próximas tareas, analizaremos cada uno de estos pilares individualmente y examinaremos su importancia para el SOC.

Answer the questions below

The SOC team discovers an unauthorized user is trying to log in to an account. Which capability of SOC is this?
Detection

What are the three pillars of a SOC?
People, Process, Technology


---

==**Personas**==

Independientemente de la evolución en la automatización de la mayoría de las tareas de seguridad, las personas en un SOC siempre serán importantes. Una solución de seguridad puede generar numerosas señales de alerta en un entorno SOC, lo que puede causar un gran ruido.

Imagina que formas parte de un equipo de bomberos y cuentas con un software centralizado que integra todas las alarmas de incendios de la ciudad. Supón que recibes muchas notificaciones de incendio a la vez, todas para diferentes lugares. Al llegar a esos lugares, tu equipo descubre que la mayoría se activaron únicamente por el humo excesivo de la cocina. Con el tiempo, todos los esfuerzos serán una pérdida de tiempo y recursos.

En un SOC, con soluciones de seguridad implementadas sin intervención humana, terminarás centrándote en problemas más irrelevantes. Siempre están las personas que ayudan a la solución de seguridad a identificar actividades realmente dañinas y a permitir una respuesta rápida.

Las personas se conocen como el equipo SOC. Este equipo tiene las siguientes funciones y responsabilidades.

![[Pasted image 20250823173934.png]]

**Analista de SOC (Nivel 1):** Cualquier elemento detectado por la solución de seguridad pasaría primero por estos analistas. Son los primeros en responder ante cualquier detección. Los analistas de SOC de Nivel 1 realizan una clasificación básica de alertas para determinar si una detección específica es perjudicial. También informan estas detecciones a través de los canales adecuados.

**Analista de SOC (Nivel 2):** ​​Si bien el Nivel 1 realiza el análisis de primer nivel, algunas detecciones pueden requerir una investigación más profunda. Los analistas de Nivel 2 les ayudan a profundizar en las investigaciones y a correlacionar los datos de múltiples fuentes para realizar un análisis adecuado.

**Analista de SOC (Nivel 3):** Los analistas de Nivel 3 son profesionales con experiencia que buscan proactivamente indicadores de amenaza y brindan apoyo en las actividades de respuesta a incidentes. Las detecciones de gravedad crítica informadas por los analistas de Nivel 1 y Nivel 2 suelen ser incidentes de seguridad que requieren respuestas detalladas, que incluyen contención, erradicación y recuperación. Aquí es donde la experiencia de los analistas de Nivel 3 resulta útil.

**Ingeniero de Seguridad:** Todos los analistas trabajan en soluciones de seguridad. Estas soluciones requieren implementación y configuración. Los ingenieros de seguridad implementan y configuran estas soluciones de seguridad para garantizar su correcto funcionamiento.

**Ingeniero de detección**: Las reglas de seguridad son la lógica que sustenta las soluciones de seguridad para detectar actividades dañinas. Los analistas de nivel 2 y 3 suelen crear estas reglas, mientras que el equipo del SOC a veces también puede utilizar el rol de ingeniero de detección de forma independiente para esta responsabilidad.

**Gerente del SOC**: El gerente del SOC gestiona los procesos que sigue el equipo del SOC y brinda soporte. Además, se mantiene en contacto con el CISO (director de seguridad de la información) de la organización para mantenerlo informado sobre la postura y las iniciativas de seguridad actuales del equipo del SOC.

Nota: Los roles en el equipo del SOC pueden aumentar o disminuir según el tamaño y la criticidad de las organizaciones.

Answer the questions below

Alert triage and reporting is the responsibility of?
SOC Analyst (Level 1)

Which role in the SOC team allows you to work dedicatedly on establishing rules for alerting security solutions?
Detection Engineer


---

==**Procesos**==

Analizamos los roles y responsabilidades de las diferentes personas que trabajan en el equipo SOC. Cada rol tiene sus propios procesos, al igual que vimos el rol de los Analistas SOC de Nivel 1 como los primeros en responder para realizar el triage de alertas y determinar si son perjudiciales. Analicemos algunos procesos importantes involucrados en un SOC.

Triage de Alertas

El triage de alertas es la base del equipo SOC. La primera respuesta ante cualquier alerta es realizar el triage. El triage se centra en analizar la alerta específica. Esto determina la gravedad de la alerta y nos ayuda a priorizarla. El triage de alertas se basa en responder a las 5 preguntas clave. ¿Cuáles son estas 5 preguntas clave?

![[Pasted image 20250823181055.png]]

A continuación, se presentan algunas preguntas que deben responderse durante el triage de una alerta.

Alerta: Malware detectado en el host: PC GEORGE

| 5 Ws   | Answers                                                                                                                                                                                            |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| What?  | Se detectó un archivo malicioso en uno de los hosts de la red de la organización.                                                                                                                  |
| When?  | El archivo se detectó a las 13:20 del 5 de junio de 2024.                                                                                                                                          |
| Where? | El archivo se detectó en el directorio del host: "GEORGE PC".                                                                                                                                      |
| Who?   | El archivo se detectó para el usuario George.                                                                                                                                                      |
| Why?   | Tras la investigación, se descubrió que el archivo se descargó de un sitio web de venta de software pirata. La investigación con el usuario reveló que lo descargó para usar un software gratuito. |
Informes

Las alertas dañinas detectadas deben escalarse a analistas de alto nivel para una respuesta y resolución oportunas. Estas alertas se escalan como tickets y se asignan a las personas pertinentes. El informe debe abordar las 5 W junto con un análisis exhaustivo, y se deben utilizar capturas de pantalla como evidencia de la actividad.

Respuesta a Incidentes y Análisis Forense

En ocasiones, las detecciones reportadas apuntan a actividades altamente maliciosas que son críticas. En estos escenarios, los equipos de alto nivel inician una respuesta a incidentes. El proceso de respuesta a incidentes se analiza en detalle en la sala de Respuesta a Incidentes. En ocasiones, también se requiere una actividad forense detallada. Esta actividad forense tiene como objetivo determinar la causa raíz del incidente mediante el análisis de los artefactos de un sistema o red.

Answer the questions below

At the end of the investigation, the SOC team found that John had attempted to steal the system's data. Which 'W' from the 5 Ws does this answer?
respuesta  WHO

The SOC team detected a large amount of data exfiltration. Which 'W' from the 5 Ws does this answer?
respuesta WHAT

---


**==Tecnología==**

Contar con el personal y los procesos adecuados nunca sería suficiente sin soluciones de seguridad para la detección y respuesta. La sección de Tecnología en los pilares del SOC se refiere a las soluciones de seguridad. Estas soluciones minimizan eficientemente el esfuerzo manual del equipo del SOC para detectar y responder a las amenazas.

La red de una organización consta de numerosos dispositivos y aplicaciones. Como equipo de seguridad, detectar y responder individualmente a las amenazas en cada dispositivo o aplicación requeriría un esfuerzo y recursos considerables. Las soluciones de seguridad centralizan toda la información de los dispositivos o aplicaciones presentes en la red y automatizan las capacidades de detección y respuesta.

Veamos brevemente algunas de estas soluciones de seguridad:

-**SIEM**: La Gestión de Información y Eventos de Seguridad (SIEM) es una herramienta popular utilizada en casi todos los entornos SOC. Esta herramienta recopila registros de varios dispositivos de red, denominados fuentes de registro. Las reglas de detección se configuran en la solución SIEM, que contiene la lógica para identificar actividad sospechosa. La solución SIEM nos proporciona las detecciones tras correlacionarlas con múltiples fuentes de registro y nos alerta en caso de coincidencia con alguna de las reglas. Las soluciones SIEM modernas superan este análisis de detección basado en reglas, brindándonos análisis del comportamiento del usuario e inteligencia de amenazas. Los algoritmos de aprendizaje automático respaldan esto para mejorar las capacidades de detección.

Nota: La solución SIEM solo ofrece capacidades de detección en un entorno SOC.

-**EDR**: Endpoint Detection and Response (EDR) proporciona al equipo del SOC visibilidad detallada, tanto en tiempo real como histórica, de las actividades de los dispositivos. Opera a nivel de endpoint y puede ejecutar respuestas automatizadas. EDR cuenta con amplias capacidades de detección para endpoints, lo que permite investigarlos en detalle y responder con solo unos clics.

-**Firewall**: Un firewall funciona exclusivamente para la seguridad de la red y actúa como una barrera entre las redes internas y externas (como Internet). Supervisa el tráfico de red entrante y saliente y filtra el tráfico no autorizado. El firewall también implementa reglas de detección que nos ayudan a identificar y bloquear el tráfico sospechoso antes de que llegue a la red interna.

Otras soluciones de seguridad desempeñan funciones únicas en un entorno SOC, como antivirus, [^1]EPP, [^2]IDS/IPS, XDR, [^4]SOAR, entre otras. La decisión sobre qué tecnología implementar en el SOC se produce después de una cuidadosa consideración de la superficie de amenaza y los recursos disponibles en la organización.

Answer the questions below

Which security solution monitors the incoming and outgoing traffic of the network?
respuesta firewall

Do SIEM solutions primarily focus on detecting and alerting about security incidents? (yea/nay)
respuesta yea

---


**==Ejercicio práctico de SOC==**

Este ejercicio práctico utiliza personas, procesos y tecnología y ofrece una guía práctica del rol de un analista de nivel 1 en el equipo SOC.

Escenario

Usted es el analista de nivel 1 del equipo SOC de su organización. Recibe una alerta indicando que se ha observado un escaneo de puertos en uno de los hosts de la red. Tiene acceso a la solución SIEM, donde puede consultar todos los registros asociados a esta alerta. Debe revisar los registros individualmente y responder a las 5 preguntas que se indican a continuación.

**Nota**: El equipo de evaluación de vulnerabilidades notificó al equipo SOC que estaban ejecutando un escaneo de puertos dentro de la red desde el host `10.0.0.8`

Answer the questions below

What: Activity that triggered the alert?
respuesta Port Scan

When: Time of the activity?
repuesta June 12, 2024 17:24

Where: Destination host IP?
respuesta 10.0.0.3

Who: Source host name?
respuesta Nessus

Why: Reason for the activity? Intended/Malicious
respuesta Intended

Additional Investigation Notes: Has any response been sent back to the port scanner IP? (yea/nay)
respuesta yea

What is the flag found after closing the alert?
respuesta THM{000_INTRO_TO_SOC}

---


**==Conclusión==**

Esta sala nos ayudó a aprender datos interesantes sobre el equipo del SOC. Vimos sus responsabilidades y los pilares (Personas, Procesos y Tecnología) que fortalecen cualquier entorno SOC. Esta sala se centró en comprender cómo las Personas, los Procesos y la Tecnología desempeñan su papel en los casos de uso diario del SOC. Finalmente, participamos en un laboratorio práctico y resolvimos una alerta real del SOC como analistas de nivel 1.

[^1]: An endpoint protection platform (EPP) is a solution deployed on endpoint devices to prevent file-based malware attacks, detect malicious activity, and provide the investigation and remediation capabilities needed to respond to dynamic security incidents and alerts.

[^2]: Intrusion Prevention System (IPS) is a device or application that detects and stops intrusions attempts proactively. They are usually deployed in front of the protected asset and block any potential threat from reaching their target.


[^4]: SOAR stands for Security Orchestration, Automation, and Response. It is a solution that helps organisations to streamline and automate their security operations, including incident management, threat intelligence, and vulnerability response.
