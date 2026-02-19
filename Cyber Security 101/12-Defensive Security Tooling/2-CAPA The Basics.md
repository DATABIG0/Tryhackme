
**==Introducción==**

Uno de los desafíos al analizar software potencialmente malicioso es el riesgo de que nuestra máquina o entorno se vea comprometido al ejecutarlo, a menos que dispongamos de un entorno de pruebas o un entorno completamente aislado donde podamos realizar todas las pruebas que queramos. En general, existen dos tipos de análisis: dinámico y estático. Esta sesión se centrará en la realización de análisis estáticos con una herramienta llamada CAPA.

![[Pasted image 20250904190429.png]]

CAPA (Plataforma de Análisis Común para Artefactos) es una herramienta desarrollada por el equipo de FireEye Mandiant. Está diseñada para identificar las capacidades presentes en archivos ejecutables como ejecutables portátiles (PE), binarios ELF, módulos .NET, shellcode e incluso informes de entornos de pruebas. Para ello, analiza el archivo y aplica un conjunto de reglas que describen comportamientos comunes, lo que le permite determinar las capacidades del programa, como la comunicación de red, la manipulación de archivos, la inyección de procesos y muchas más.

La ventaja de CAPA es que encapsula años de conocimiento en ingeniería inversa en una herramienta automatizada, haciéndola accesible incluso para quienes no son expertos en ingeniería inversa. Esto puede ser increíblemente útil para analistas y profesionales de seguridad, ya que les permite comprender rápidamente la funcionalidad de software potencialmente malicioso sin aplicar ingeniería inversa al código manualmente.

Esta herramienta es especialmente útil en el análisis de malware y la búsqueda de amenazas, donde comprender las capacidades de un binario es crucial para la respuesta a incidentes y la adopción de medidas defensivas.


---

**==Descripción general de la herramienta: Cómo funciona CAPA==**

En esta tarea, veremos cómo usar CAPA. Ejecutar la herramienta es facilísimo. Primero, abra PowerShell; tenga en cuenta que la solicitud puede tardar un poco. A continuación, asegúrese de estar en el directorio correcto (C:\Users\Administrator\Desktop\capa); luego, ejecute capa o capa.exe, seleccione el binario y ¡listo!

En este ejemplo, usaremos cryptbot.bin; tenga en cuenta que los resultados de este archivo se analizarán en la siguiente tarea.

Después de ejecutar el comando, espere el resultado, que puede tardar varios minutos. Esto no es para finalizar, sino para que se familiarice con la herramienta, por lo que le sugerimos que continúe la tarea mientras CAPA se ejecuta o que detenga el procesamiento. Existen alternativas para analizar los resultados. Consulte el comando a continuación.

![[Pasted image 20250905173655.png]]

Además del comando -h, que nos proporciona más información sobre los parámetros disponibles con la herramienta, utilizaremos dos (2) parámetros muy utilizados, ``-v`` y -``vv``, que nos proporcionarán un resultado más detallado. Sin embargo, esto aumentará el tiempo de procesamiento. Analizaremos los resultados de estas opciones en las próximas tareas.

| Option                | Description                                         | Sample Syntax                 |
| --------------------- | --------------------------------------------------- | ----------------------------- |
| `-h` or `--help`      | Mostrar este mensaje de ayuda y salir.              | `capa -h`                     |
| `-v` or `--verbose`   | Habilitar documento de resultados detallado.        | `capa.exe .\cryptbot.bin -v`  |
| `-vv` or `--vverbose` | Habilitar un documento de resultados muy detallado. | `capa.exe .\cryptbot.bin -vv` |

Este debería ser el resultado del comando. *Tenga en cuenta que los resultados pueden variar. Si ejecutó CAPA en algunos archivos, podría mostrar o no la misma información que la que se muestra a continuación.

![[Pasted image 20250905173842.png]]
![[Pasted image 20250905173855.png]]
![[Pasted image 20250905173912.png]]
![[Pasted image 20250905173925.png]]

Como sabemos que el tiempo de procesamiento es de varios minutos, lo hemos preprocesado en un archivo llamado cryptbot.txt, ubicado en C:\Users\Administrator\Desktop\capa. Al mismo tiempo, lo hemos adjuntado a esta tarea; simplemente haga clic en el botón en la esquina superior derecha de esta tarea. Abra otra terminal de PowerShell y use el comando ``Get-Content cryptbot.txt``.

![[Pasted image 20250905174021.png]]

Al cargar el contenido en PowerShell, se obtendrá el mismo resultado desde la terminal anterior.

¡Listo! ¡Hemos terminado!

Un momento, ¿cuáles son esos resultados? ¿Cómo podemos interpretarlos?

Answer the questions below

What command-line option would you use if you need to check what other parameters you can use with the tool? Use the shortest format.
respuesta -h

What command-line options are used to find detailed information on the malware's capabilities? Use the shortest format.
respuesta -v

What command-line options do you use to find very verbose information about the malware's capabilities? Use the shortest format.
respuesta -vv

What PowerShell command will you use to read the content of a file?
respuesta Get-Content


---

**==Análisis de los resultados de CAPA - Parte 1: Información general, MITRE y MAEC==**

Como se mencionó en la tarea anterior, los resultados de la ejecución de CAPA contra cryptbot.bin se analizarán en la siguiente tarea. Por lo tanto, analizaremos los resultados por bloque y tema.

El primer bloque contiene información básica sobre el archivo. Esto incluye lo siguiente:

- Los algoritmos criptográficos, como md5 y sha1/256.
- El campo de análisis indica cómo CAPA realizó el análisis del archivo.
- El campo "os" revela el contexto del sistema operativo (SO) al que se aplican las capacidades identificadas.
- El campo "arch" permite determinar si se trata de un binario relacionado con la arquitectura x86.
- La ruta donde se encuentra el archivo analizado.

![[Pasted image 20250905174048.png]]

**MITRE ATT&CK**

El marco MITRE ATT&CK (Tácticas, Técnicas y Conocimiento Común Adversario) es un repositorio global de conocimiento completo que documenta meticulosamente las tácticas y técnicas empleadas por los actores de amenazas en cada etapa de un ciberataque. Funciona como un manual estratégico que proporciona información detallada sobre los métodos de los atacantes, desde obtener acceso inicial hasta mantener una presencia, escalar privilegios, evadir defensas, moverse lateralmente dentro de una red y mucho más.

CAPA utiliza este formato para los resultados. Tenga en cuenta que algunos resultados pueden contener o no el identificador de técnica y subtécnica.

| Format                                                                                                                     | Sample                                                                                   | Explanation                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **ATT&CK Tactic**::**ATT&CK Technique**::**Technique Identifier**                                                          | Defense Evasion::Obfuscated Files or Information::T1027                                  | **DEFENSE EVASION =** ATT&CK Tactic  <br>**Obfuscated Files or Information =** ATT&CK Technique  <br>**T1027 =** Technique Identifier                                                                                                      |
| **ATT&CK Tactic**::**ATT&CK Technique**::**ATT&CK Sub-Technique**::**Technique Identifier**[.]Sub-technique **Identifier** | Defense Evasion::Obfuscated Files or Information::Indicator Removal from Tools T1027.005 | **DEFENSE EVASION** = ATT&CK Tactic  <br>**Obfuscated Files or Information** = ATT&CK Technique  <br>**Indicator Removal from Tools** = ATT&CK Sub-Technique  <br>**T1027 =** Technique Identifier  <br>**005** = Sub-Technique Identifier |
![[Pasted image 20250905174108.png]]

En el resultado final de CAPA, se hizo referencia al marco MITRE. Este marco ayuda a los analistas y defensores a mapear el comportamiento del archivo con la estrategia del adversario, lo que puede ayudar a delimitar el alcance de la investigación durante un incidente. Para profundizar en este tema, le recomendamos consultar nuestra sección sobre el marco [MITRE ATT&CK](https://tryhackme.com/r/room/mitre).

**MAEC**

La Enumeración y Caracterización de Atributos de Malware es un lenguaje especializado diseñado para codificar y comunicar detalles complejos sobre el malware. Contiene una amplia gama de atributos, incluyendo comportamientos, artefactos e interconexiones entre diversas instancias de malware. Este lenguaje funciona como un sistema estandarizado para rastrear y analizar las complejas complejidades del malware.

![[Pasted image 20250905174134.png]]

Revisemos la siguiente tabla para ver los valores MAEC más utilizados por CAPA: Descargador y Lanzador.

| **MAEC Value** | Description                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Launcher       | Presenta comportamientos que desencadenan acciones específicas similares a las del malware.                                      |
| Downloader     | Presenta comportamientos que incluyen la descarga y ejecución de otros archivos, generalmente presentes en malware más complejo. |

Cuando CAPA etiqueta un archivo con un valor MAEC de "lanzador", indica que el archivo muestra un comportamiento similar, entre otros:

- Descarga de cargas útiles adicionales
- Activación de mecanismos de persistencia
- Conexión a servidores de comando y control (C2)
- Ejecución de funciones específicas

¡Esto es interesante! Algunos de estos comportamientos también están presentes en el Catálogo de Comportamiento de Malware (MBC) y el bloque de Capacidad, que analizaremos en la siguiente tarea.

Además, cuando CAPA etiqueta un archivo con un valor MAEC de "Descargador", indica que el archivo muestra un comportamiento similar, entre otros:

- Obtención de cargas útiles o recursos adicionales de internet
- Incorporación de actualizaciones
- Ejecución de etapas secundarias
- Recuperación de archivos de configuración

Answer the questions below

What is the sha256 of cryptbot.bin?
respuesta ae7bc6b6f6ecb206a7b957e4bb86e0d11845c5b2d9f7a00a482bef63b567ce4c

What is the **Technique** Identifier of **Obfuscated Files or Information**?
respuesta T1027

What is the **Sub-Technique** Identifier of **Obfuscated Files or Information::Indicator Removal from Tools**?
respuesta T1027.005

When CAPA tags a file with this MAEC value, it indicates that it demonstrates behaviour similar to, but not limited to, **Activating persistence mechanisms**?
respuesta launcher

When CAPA tags a file with this MAEC value, it indicates that the file demonstrates behaviour similar to, but not limited to, **Fetching additional payloads or resources from the internet**?
respuesta Downloader


---

**==Análisis de los resultados de CAPA - Parte 2: Catálogo de comportamientos de malware==**

En esta tarea, abordaremos los siguientes temas:

- MBC
- Objetivo (Objective)
- Microobjetivo (Micro-Objective)
- Comportamientos de MBC (MBC Behaviors)
- Microcomportamiento (Micro-Behavior)
- Métodos (Methods)

Pasemos al siguiente bloque. Esta terminal también se puede ver en la Tarea 2, donde ejecutamos la herramienta CAPA. Haga clic en la terminal de vista a continuación.

![[Pasted image 20250905183755.png]]

Abordaremos el Catálogo de comportamientos de malware para comprender mejor el bloque anterior.

**Catálogo de comportamientos de malware (MBC)**

El MBC está diseñado para respaldar diversos aspectos del análisis de malware, como el etiquetado, el análisis de similitud y la generación de informes estandarizados. En esencia, funciona como un catálogo de objetivos y comportamientos de malware. El MBC también puede vincularse a los métodos ATT&CK y registrar todos los comportamientos y características del código descubiertos durante el análisis de malware. Es importante tener en cuenta que los nombres de los comportamientos de MBC pueden coincidir o no con las técnicas ATT&CK correspondientes. La información de las páginas de comportamiento complementa el contenido de las páginas ATT&CK. En otras palabras, al registrar comportamientos de malware, los usuarios de MBC harán referencia a ATT&CK, pero MBC no duplica la información de ATT&CK.

El contenido de MBC a continuación se puede representar en dos formatos.

|Format|Sample|Explanation|
|---|---|---|
|**OBJECTIVE**::**Behavior**::**Method**[**Identifier**]|ANTI-STATIC ANALYSIS::Executable Code Obfuscation::Argument Obfuscation [B0032.020]|**Anti-static Analysis** = OBJECTIVE  <br>**Executable Code Obfuscation** = BEHAVIOR  <br>**Argument Obfuscation** = METHOD  <br>**BOO32.020** = IDENTIFIER|
|**OBJECTIVE**::**Behavior**::[**Identifier**]|COMMUNICATION::HTTP Communication:: [C0002]|**COMMUNICATION** = OBJECTIVE  <br>**HTTP Communication** = BEHAVIOR  <br>**C0002** = IDENTIFIER|

La diferencia entre ambos formatos radica en que el primero contiene detalles adicionales denominados MÉTODO, que también puede considerarse una subtécnica.

Para comprender mejor esta parte, es necesario analizar también el Objetivo, el Comportamiento y los Métodos.

**Objetivo**

El Objetivo se basa en las tácticas de ATT&CK en el contexto del comportamiento del malware, aunque no todas están incluidas. Además, MBC incluye Análisis Anticonductual y Antiestático. Estos objetivos están diseñados para el análisis de malware, con el objetivo de caracterizarlo. Consulte la tabla a continuación para obtener una explicación de cada uno.

| **Objective**                | **Explanation**                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Anti-Behavioral Analysis** | El malware intenta evitar su detección obstaculizando el análisis del comportamiento mediante herramientas como entornos sandbox o depuradores.                                                                                                                                                                                                          |
| **Anti-Static Analysis**     | El malware intenta obstruir o agregar complejidad al análisis estático, lo que hace que sea más difícil para los profesionales de seguridad identificar y comprender sus comportamientos e intenciones maliciosas.                                                                                                                                       |
| **Collection**               | El malware se centra en identificar y recopilar información de la máquina o red de destino.                                                                                                                                                                                                                                                              |
| **Command and Control**      | El malware suele establecer comunicación con los sistemas comprometidos mediante diversos métodos, como servidores de comando y control, redes peer-to-peer u otros. Esta comunicación permite al malware controlar los sistemas comprometidos, lo que permite a los atacantes ejecutar comandos, extraer datos o realizar otras actividades maliciosas. |
| **Credential Access**        | El objetivo principal del malware es robar credenciales de cuentas, como nombres de usuario y contraseñas.                                                                                                                                                                                                                                               |
| **Defense Evasion**          | El malware tiene como objetivo eludir y eludir los diversos mecanismos de detección y seguridad presentes en el sistema para evitar ser detectado o mitigado.                                                                                                                                                                                            |

|                          |                                                                                                                                                                                                                                                                                                                                 |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Discovery**            | El Malware busca recopilar información detallada sobre la configuración y la instalación del sistema o del entorno de red, incluido el hardware, el software y la infraestructura de red.                                                                                                                                       |
| **Execution**            | El malware está diseñado para ejecutar comandos o código no autorizado en un sistema informático específico sin el consentimiento del usuario. Esto puede incluir una amplia gama de actividades dañinas, como robar información personal, dañar archivos o acceder al sistema sin autorización.                                |
| **Exfiltration**         | El malware está diseñado para infiltrarse en sistemas o redes informáticas y robar y extraer datos confidenciales. Esto puede incluir información personal, datos financieros y cualquier otro dato valioso almacenado en el sistema o red objetivo.                                                                            |
| **Impact**               | El malware tiene como objetivo manipular, interrumpir o dañar los sistemas y datos informáticos. Puede acceder a los ordenadores a través de correos electrónicos infectados, sitios web comprometidos y otros medios engañosos, lo que provoca pérdidas financieras, violaciones de la privacidad e inestabilidad del sistema. |
| **Lateral Movement**     | El malware busca propagarse a través de la red, ya sea de forma activa mediante el acceso a la máquina o de forma pasiva, como por ejemplo a través de correos electrónicos maliciosos.                                                                                                                                         |
| **Persistence**          | El malware se desarrolla intencionalmente con la capacidad de permanecer sin ser detectado y operativo en un sistema informático durante un período prolongado.                                                                                                                                                                 |
| **Privilege Escalation** | El malware busca infiltrarse en un sistema informático o red para obtener permisos o control elevados. Una vez dentro del entorno objetivo, el malware puede intentar aumentar sus privilegios, acceder a información confidencial o tomar el control de los recursos del sistema con fines maliciosos.                         |

**Microobjetivo**

Los microobjetivos se asocian con microcomportamientos, que se refieren a una o varias acciones de software potencialmente malicioso que no son necesariamente maliciosas y que pueden tener diversos objetivos. Algunos ejemplos son los binarios de las aplicaciones de mensajería. Sin embargo, es importante tener en cuenta que estos comportamientos suelen ser objeto de abuso. Por eso, CAPA podría haber detectado este comportamiento.

| **Micro-Objective** | **Description**                                                                                                                                             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **PROCESS**         | exhibir comportamientos relacionados con procesos tales como, entre otros, crear proceso, establecer contexto de hilo, finalizar proceso y verificar mutex. |
| **MEMORY**          | exhibiendo comportamientos tales como, pero no limitados a, asignar memoria, cambiar la protección de la memoria y liberar memoria.                         |
| **COMMUNICATION**   | exhibiendo comportamientos tales como (sin limitarse a) tráfico de red (DNS, FTP, HTTP, ICMP, SMTP).                                                        |
| **DATA**            | exhibiendo comportamientos tales como, entre otros, verificar cadenas, comprimir, decodificar y codificar datos                                             |

El resultado final de CAPA, Objetivo y Microobjetivo se muestra únicamente en la columna Objetivo.

**Comportamientos de MBC**

La columna Comportamientos de MBC contiene comportamientos y microcomportamientos con o sin sus métodos e identificadores. Consulte el enlace Resumen de [MBC](https://github.com/MBCProject/mbc-markdown/blob/main/mbc_summary.md) para obtener una lista completa del contenido de MBC.

A continuación se muestra una versión compilada de Comportamientos/Microcomportamientos y su identificador.

| **Objective**                         | **Behavior**                          | Identifiers | Explanation                                                                                                                                                                                                                                                                                                             |
| ------------------------------------- | ------------------------------------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ANTI-BEHAVIORAL ANALYSIS              | **Virtual Machine Detection**         | **B0009**   | El malware verifica si se ejecuta en un entorno virtual. Durante el reconocimiento del sistema, examina diversos artefactos del usuario y del sistema.                                                                                                                                                                  |
| ANTI-STATIC ANALYSIS                  | **Executable Code Obfuscation**       | **B0032**   | El código ejecutable se ha ocultado intencionalmente para evitar el análisis de código estático. Este comportamiento se relaciona específicamente con el código ejecutable de una muestra de malware, incluidas sus secciones de datos y texto.                                                                         |
| EXECUTION                             | **Command and Scripting Interpreter** | **E1059**   | El malware puede explotar intérpretes de comandos y scripts para ejecutar comandos, scripts o binarios maliciosos. Se dirige a intérpretes integrados como cmd.exe o PowerShell en Windows o Bash en sistemas tipo Unix. Los atacantes también pueden usar otros lenguajes de scripting como Python, Perl o JavaScript. |
| DISCOVERY                             | **File and Directory Discovery**      | **E1083**   | El malware tiene la capacidad de buscar archivos específicos en ubicaciones particulares enumerando archivos y directorios.                                                                                                                                                                                             |
| ANTI-STATIC ANALYSIS, DEFENSE EVASION | **Obfuscated Files or Information**   | **E1027**   | El malware puede ofuscar archivos o información mediante codificación, cifrado o cualquier otro método, lo que dificulta su análisis. También puede codificar o cifrar muestras de malware.                                                                                                                             |

**Microcomportamiento**

El término "comportamientos de bajo nivel" en el análisis de malware se refiere a acciones que el malware exhibe y que no son necesariamente maliciosas y que pueden tener diversos objetivos. Estos comportamientos suelen documentarse como "microcomportamientos" en el análisis de Características de Comportamiento de Malware (MBC). Ejemplos de estos comportamientos de bajo nivel incluyen la creación de sockets TCP y la evaluación de condiciones específicas dentro de cadenas. Es importante tener en cuenta que el hecho de que un comportamiento se clasifique como de bajo nivel no significa que sea inofensivo, ya que podría formar parte de un plan malicioso más amplio.

| **Micro-Objective** | **Micro-Behaviors**    | Identifiers | Explanation                                                                                                                                                          |
| ------------------- | ---------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MEMORY              | **Allocate Memory**    | **C0007**   | El malware utiliza con frecuencia la asignación de memoria como parte de su estrategia para descomprimirse y ejecutar sus actividades maliciosas.                    |
| PROCESS             | **Create Process**     | **C0017**   | El malware crea un proceso mediante WMI o shellcode. También puede crear un proceso suspendido.                                                                      |
| COMMUNICATION       | **HTTP Communication** | **C0002**   | El malware es capaz de iniciar comunicaciones HTTP.                                                                                                                  |
| DATA                | **Check String**       | **C0019**   | El malware puede inspeccionar una cadena para identificar características específicas, como contenido ASCII, números de tarjetas de crédito y longitud de la cadena. |

|             |                      |           |                                                                           |
| ----------- | -------------------- | --------- | ------------------------------------------------------------------------- |
| DATA        | **Encode Data**      | **C0026** | El malware tiene la capacidad de codificar datos utilizando base64 y XOR. |
| FILE SYSTEM | **Create Directory** | **C0046** | El malware puede crear un directorio.                                     |
| FILE SYSTEM | **Delete File**      | **C0047** | El malware tiene la capacidad de eliminar un archivo.                     |
| FILE SYSTEM | **Read File**        | **C0051** | El malware puede leer un archivo.                                         |
| FILE SYSTEM | **Writes File**      | **C0052** | El malware tiene la capacidad de escribir en un archivo.                  |

Tenga en cuenta que en el resultado final de CAPA, el comportamiento y el microcomportamiento se muestran solo en la columna Comportamiento.

**Métodos**

Por último, revisemos los MÉTODOS. A continuación, se presentan algunos métodos incluidos en los resultados del ejemplo anterior. Los métodos están vinculados a los comportamientos; por lo tanto, para verlos todos, consulte cada comportamiento/microcomportamiento específico de interés.

| Behavior                        | Methods or sub-technique        | Identifier | Explanation                                                                                                                          |
| ------------------------------- | ------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Executable Code Obfuscation     | **Argument Obfuscation**        | B0032.020  | Los argumentos numéricos o de cadena simples para las llamadas API se calculan en tiempo de ejecución, lo que dificulta el análisis. |
| Executable Code Obfuscation     | **Stack Strings**               | B0032.017  | Construye y descifra cadenas en la pila en cada uso, luego deséchalas para evitar referencias obvias.                                |
| HTTP Communication              | **Read Header**                 | C0002.014  | Encabezado de lectura HTTP.                                                                                                          |
| Encode Data                     | **Base64**                      | C0026.001  | El malware puede codificar datos utilizando Base64.                                                                                  |
| Encode Data                     | **XOR**                         | C0026.002  | El malware puede utilizar XOR para codificar datos.                                                                                  |
| Obfuscated Files or Information | **Encoding-Standard Algorithm** | E1027.m02  | La codificación de muestras de malware, archivos u otra información utiliza un algoritmo estándar (por ejemplo, base64).             |

Ahora que tenemos una buena visión general y comprendemos el contenido del MBC, deberíamos poder explicar el resultado de la muestra anterior. Por lo tanto, hagamos un breve resumen usando uno de los resultados. ¿Les parece?

![[Pasted image 20250905175724.png]]

Aquí está la explicación del resultado anterior. Consulte la tabla a continuación.

| Label         | Value           | Explanation                                                                                                              |
| ------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------ |
| MBC Objective | **DATA**        | exhibiendo comportamientos tales como, pero no limitados a, verificar cadenas, comprimir, decodificar y codificar datos. |
| MBC Behavior  | **Encode Data** | El malware tiene la capacidad de codificar datos utilizando base64 y XOR.                                                |
| Method        | **Base64**      | El malware puede codificar datos utilizando Base64.                                                                      |
| Identifier    | **C0026.001**   | El identificador transmite información sobre un comportamiento. También funciona como etiqueta.                          |

Conociendo esta información, ¡podemos simplemente decir que este archivo puede usar el esquema de codificación base64!

Answer the questions below

What serves as a catalogue of malware objectives and behaviours?
respuesta Malware Behavior Catalogue

Which field is based on ATT&CK tactics in the context of malware behaviour?
respuesta  Objective

What is the Identifier of **"Create Process**" micro-behavior?
respuesta C0017

What is the behaviour with an Identifier of **B0009**?
respuesta Virtual Machine Detection

Malware can be used to obfuscate data using base64 and XOR. What is the related **micro-behavior** for this?
respuesta Encode Data

Which micro-behavior refers to "**Malware is capable of initiating HTTP communications**"?
respuesta HTTP Communication


---

**==Análisis de los resultados de CAPA, parte 3: Espacios de nombres==**

Dividiremos la discusión en dos temas principales: Capacidad y Espacio de nombres. En esta tarea, nos centraremos en el análisis del Espacio de nombres.

A continuación, encontrará la salida de ``capa.exe``. Tenga en cuenta que también puede verla en la Tarea 2. Haga clic en Ver terminal a continuación.

![[Pasted image 20250909162017.png]]

El contenido de este bloque se representa en el siguiente formato.

|Format|Sample|Explanation|
|---|---|---|
|**Capability(Rule Name)**::**TLN(Top-Level Namespace)**/**Namespace**|reference anti-VM strings::Anti-Analysis/anti-vm/vm-detection|**Reference anti-VM strings** = Capability(Rule Name)  <br>**Anti-Analysis** = TLN or Top-Level Namespace  <br>**anti-vm/vm-detection** = Namespace|

**Espacios de nombres**

CAPA utiliza espacios de nombres para agrupar elementos con el mismo propósito.

| Top-Level Namespace (TLN) | Explanation                                                                                                                                                                                                                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| anti-analysis             | Contiene un conjunto de reglas diseñadas específicamente para detectar comportamientos del malware que evaden el análisis. Estos comportamientos incluyen técnicas de ofuscación, empaquetado y antidepuración.                                                                                                          |
| collection                | Contiene un conjunto de reglas relacionadas con los datos que el malware puede enumerar y recopilar para exfiltración u otros fines. Considérelo como el aspecto de "recopilación de datos" del comportamiento del malware.                                                                                              |
| communication             | Contiene un conjunto de reglas que rigen los diferentes comportamientos de comunicación del malware. Esto abarca cómo interactúa con las redes, incluyendo la transmisión y recepción de datos, las comunicaciones de comando y control, y otros comportamientos relacionados con la red.                                |
| compiler                  | Contiene un conjunto de reglas y configuraciones para reconocer entornos de compilación o compiladores específicos empleados en la generación de ejecutables. Estos espacios de nombres sirven esencialmente como la "firma" única que identifica el proceso de compilación de un programa.                              |
| data-manipulation         | Contiene un conjunto de reglas que rigen los comportamientos involucrados en la alteración de datos dentro de archivos ejecutables. Este aspecto puede considerarse el componente de "transformación de datos" del comportamiento del malware, abarcando acciones como el cifrado de cadenas y la codificación de datos. |

|                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| executable       | Contiene un conjunto de reglas relativas a los atributos de los archivos ejecutables. Estos atributos incluyen secciones PE o información de depuración asociada al ejecutable.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| host-interaction | Contiene un conjunto de reglas relacionadas con los comportamientos que implican interacciones con el sistema host. Esto abarca cómo el malware interactúa con su entorno. Específicamente, las reglas de este espacio de nombres pueden capturar comportamientos relacionados con la lectura, escritura o modificación de archivos en el disco, incluyendo la creación, eliminación o modificación de archivos y directorios.                                                                                                                                                                                                                                                                                                                                                                  |
| impact           | Contiene un conjunto de reglas relacionadas con las posibles consecuencias o efectos del comportamiento de un programa. Considérelo como el aspecto que se centra en el posible daño que este malware puede causar. Puede incluir comportamientos relacionados con el acceso remoto, la exfiltración, la destrucción o la modificación de datos.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| internal         | Las reglas del sistema no están diseñadas para el uso directo de los analistas ni para la generación de informes. Su propósito es el desarrollo y la ejecución de reglas internas de la herramienta CAPA.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| lib              | bloques de construcción para crear otras reglas                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| linking          | Contiene reglas para identificar comportamientos que implican la vinculación o la carga dinámica de código o bibliotecas externas durante la ejecución del programa. Esta es su función principal y es crucial para la seguridad del programa. Comprender el comportamiento de la vinculación es esencial por varias razones. El malware a menudo depende de bibliotecas o componentes externos (como OpenSSL, Zlib u otras bibliotecas de terceros) para realizar tareas específicas. Detectar estas dependencias ayuda a los analistas a comprender las capacidades del malware. Las bibliotecas externas también introducen una superficie de ataque adicional. Si existe una vulnerabilidad en una biblioteca vinculada, el malware o los defensores pueden explotarla durante el análisis. |
| load-code        | Contiene un conjunto de reglas y regulaciones relacionadas con los comportamientos asociados con la carga o ejecución dinámica de código durante la ejecución de un programa. Este concepto puede compararse con el aspecto de "inyección de código en tiempo de ejecución" del comportamiento del malware, que implica la introducción de código no autorizado durante la ejecución de un programa.                                                                                                                                                                                                                                                                                                                                                                                            |
| malware-family   | Contiene un conjunto de reglas relacionadas con comportamientos vinculados a familias o grupos de malware específicos. Sirve para identificar las características distintivas o "firmas" asociadas a familias de malware conocidas, lo que permite una detección y clasificación más precisa de amenazas potenciales.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| nursery          | Este es un escenario que contiene reglas para aquellos que no están del todo pulidos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| persistence      | Contiene reglas relacionadas con los comportamientos asociados con el mantenimiento del acceso o la persistencia en un sistema comprometido. Este espacio de nombres se centra principalmente en comprender cómo el malware puede establecerse y mantenerse presente en un entorno comprometido, lo que le permite persistir y realizar actividades maliciosas durante un período prolongado.                                                                                                                                                                                                                                                                                                                                                                                                   |
| runtime          | Contiene un conjunto de reglas que buscan identificar el lenguaje o la plataforma en la que se ejecuta el programa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| targeting        | Contiene un conjunto de reglas relacionadas con los comportamientos exhibidos por los programas que interactúan con los cajeros automáticos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

Veamos cómo funciona esto consultando la siguiente tabla.

| Top-Level Namespace (TLN) | Namespaces           | Rule YAML File                                                                                                  | Explanation                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Anti-Analysis**         | anti-vm/vm-detection | reference-anti-vm-strings-targeting-virtualbox.yml  <br>  <br>reference-anti-vm-strings-targeting-virtualpc.yml | El espacio de nombres "anti-vm/vm-detection" contiene reglas para detectar entornos de máquinas virtuales (VM). Estas reglas se centran en identificar cadenas o patrones específicos que el malware suele usar para detectar máquinas virtuales en ejecución. Con estas reglas, CAPA puede identificar si el malware busca claves de registro específicas de VMware, la presencia de herramientas de VMware u otros elementos relacionados con las VM. |
|                           | obfuscation          | obfuscated-with-dotfuscator.yml  <br>  <br>obfuscated-with-smartassembly.yml                                    | El malware suele emplear técnicas de ofuscación para dificultar el análisis. Estas incluyen métodos como el cifrado de cadenas, la ofuscación de código, el empaquetado y trucos antidepuración. El espacio de nombres de ofuscación aborda estas técnicas, que ocultan u ocultan el verdadero propósito del código.                                                                                                                                    |

Para esto, solo usamos Anti-Analysis como TLN o espacio de nombres de nivel superior. Bajo este TLN, agrupamos espacios de nombres, como anti-vm/vm-detection y ofuscación. Cada espacio de nombres contiene un conjunto de reglas que también están agrupadas. Para anti-vm/vm-detection, tenemos reglas y su archivo de configuración, como:

- reference-anti-vm-strings-targeting-virtualbox.yml
- reference-anti-vm-strings-targeting-virtualpc.yml

Lo mismo ocurre con el espacio de nombres de ofuscación. Tenemos reglas agrupadas, como:

- obfuscated-with-dotfuscator.yml
- obfuscated-with-smartassembly.yml

De nuevo, tenga en cuenta que esto todavía está bajo el TLN Anti-Analysis.

Consulte también la ilustración a continuación.

![[Pasted image 20250909162313.png]]

Además de lo mencionado en la tabla anterior, existen algunos espacios de nombres adicionales en Anti-Analysis con sus reglas correspondientes. Si desea obtener más información, consulte este [enlace](https://github.com/MBCProject/capa-rules-1/tree/master/anti-analysis).

Utilice este [enlace ](https://github.com/MBCProject/capa-rules-1?tab=readme-ov-file#namespace-organization)si le interesan otros espacios de nombres de nivel superior (TLN), como colección, compilador, persistencia, enlace e impacto.

Answer the questions below

Which top-level Namespace contains a set of rules specifically designed to detect behaviours, including obfuscation, packing, and anti-debugging techniques **exhibited by malware to evade analysis**?
respuesta anti-analysis

Which namespace contains rules to **detect virtual machine (VM) environments**? Note that this is not the TLN or Top-Level Namespace.
respuesta anti-vm/vm-detection

Which Top-Level Namespace contains rules related to **behaviours associated with maintaining access or persistence within a compromised system**? This namespace is focused on understanding how malware can establish and maintain a presence within a compromised environment, allowing it to persist and carry out malicious activities over an extended period.
respuesta  persistence

Which namespace addresses techniques such as **String Encryption, Code Obfuscation, Packing, and Anti-Debugging Tricks**, which conceal or obscure the true purpose of the code?
respuesta obfuscation

Which Top-Level Namespace Is a **staging ground** for rules that are not quite polished?
respuesta Nursery


---

**==Análisis de los resultados de CAPA, parte 4: Capacidad==**

En esta tarea, continuaremos la discusión de la tarea anterior.

**Capacidad**

A continuación, se muestra una tabla con la capacidad y su TLN, espacio de nombres y las reglas asociadas al archivo YAML. Por favor, léala con atención.

| Capability                                     | Top-Level Namespace (TLN)                                                                         | Namespaces            | Rule YAML file                                                            | Notes                                                                                                                                             |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------- | --------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| reference anti-VM strings                      | [**Anti-Analysis**](https://github.com/MBCProject/capa-rules-1/tree/master/anti-analysis)         | anti-vm/vm-detection  | reference-anti-vm-strings.yml                                             | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/anti-analysis/anti-vm/vm-detection)  |
| reference anti-VM strings targeting VMWare     | **Anti-Analysis**                                                                                 | anti-vm/vm-detection  | reference-anti-vm-strings-targeting-vmware.yml                            | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/anti-analysis/anti-forensic)         |
| reference anti-VM strings targeting VirtualBox | **Anti-Analysis**                                                                                 | anti-vm/vm-detection  | reference-anti-vm-strings-targeting-virtualbox.yml                        | You may check the TLN(Top-Level Namespace).                                                                                                       |
| reference HTTP User-Agent string               | [**Communication**](https://github.com/MBCProject/capa-rules-1/tree/master/communication)         | http/client           | reference-http-user-agent-string.yml                                      | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/communication/http/client))          |
| check HTTP status code                         | **Communication**                                                                                 | http                  | check-http-status-code.yml                                                | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/communication/http)                  |
|                                                |                                                                                                   |                       |                                                                           |                                                                                                                                                   |
| reference Base64 string                        | [**Data Manipulation**](https://github.com/MBCProject/capa-rules-1/tree/master/data-manipulation) | encoding/base64       | reference-base64-string.yml                                               | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/data-manipulation/encoding/base64)   |
| encode data using XOR                          | **Data Manipulation**                                                                             | encoding/XOR          | encode-data-using-xor.yml                                                 | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/data-manipulation/encoding/xor)      |
| contain a thread local storage (.tls) section  | [**Executable**](https://github.com/MBCProject/capa-rules-1/tree/master/executable)               | pe/section/tls        | contain-a-thread-local-storage-tls-section.yml                            | You may check the TLN(Top-Level Namespace) for more rules.                                                                                        |
| get common file path                           | [**Host-Interaction**](https://github.com/MBCProject/capa-rules-1/tree/master/host-interaction)   | file-system           | get-common-file-path.yml                                                  | You may check the TLN(Top-Level Namespace) for more rules.                                                                                        |
| create directory                               | **Host-Interaction**                                                                              | file-system/create    | create-directory.yml                                                      | You may check the TLN(Top-Level Namespace) for more rules.                                                                                        |
| delete file                                    | **Host-Interaction**                                                                              | file-system/delete    | delete-file.yml                                                           | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/host-interaction/file-system/delete) |
| read file on Windows                           | **Host-Interaction**                                                                              | file-system/read      | read-file-on-windows.yml                                                  | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/host-interaction/file-system/read)   |
| write file on Windows                          | **Host-Interaction**                                                                              | file-system/write     | write-file-on-windows.yml                                                 | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/host-interaction/file-system/write)  |
| get thread local storage value                 | **Host-Interaction**                                                                              | process               | get-thread-local-storage-value.yml                                        | This rule is found under **TLN [Nursery](https://github.com/mandiant/capa-rules/tree/master/nursery),** a staging ground for unpolished rules.    |
| allocate or change RWX memory                  | **Host-Interaction**                                                                              | process/inject        | allocate-or-change-rwx-memory.yml                                         | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/host-interaction/process/inject)     |
| create process on Windows                      | **Host-Interaction**                                                                              | process create        | create-process-on-windows.yml                                             | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/host-interaction/process/create)     |
| reference cryptocurrency strings               | [**Impact**](https://github.com/MBCProject/capa-rules-1/tree/master/impact)                       | impact/cryptocurrency | reference-cryptocurrency-strings.yml                                      | This rule is found under **TLN [Nursery](https://github.com/mandiant/capa-rules/tree/master/nursery),** a staging ground for unpolished rules.    |
| link function at runtime on Windows            | [**Linking**](https://github.com/MBCProject/capa-rules-1/tree/master/linking)                     | runtime-linking       | link-function-at-runtime-on-windows.yml                                   | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/linking/runtime-linking)             |
| parse PE header                                | [**load-code**](https://github.com/MBCProject/capa-rules-1/tree/master/load-code)                 | load-code/pe          | parse-pe-header.yml  <br>  <br>resolve-function-by-parsing-pe-exports.yml | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/load-code/pe)                        |
| resolve function by parsing PE exports         | [**load-code**](https://github.com/MBCProject/capa-rules-1/tree/master/load-code)                 | load-code/pe          | resolve-function-by-parsing-pe-exports.yml                                | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/load-code/pe)                        |
| run PowerShell expression                      | [**load-code**](https://github.com/MBCProject/capa-rules-1/tree/master/load-code/powershell)      | load-code/PowerShell  | run-powershell-expression.yml                                             | To check all rules under this namespace, click [here](https://github.com/MBCProject/capa-rules-1/tree/master/linking/runtime-linking)             |
| schedule task via at                           | [**persistence**](https://github.com/MBCProject/capa-rules-1/tree/master/persistence)             | scheduled-tasks       | schedule-task-via-at.yml                                                  | You may check the TLN(Top-Level Namespace) for more rules.                                                                                        |
| schedule task via schtasks                     | [**persistence**](https://github.com/MBCProject/capa-rules-1/tree/master/persistence)             | scheduled-tasks       | schedule-task-via-schtasks.yml                                            | You may check the TLN(Top-Level Namespace) for more rules.                                                                                        |

Para explicar esto con más detalle, revisemos la primera capacidad de la tabla: "referenciar cadenas anti-VM".

- Observamos que las reglas relacionadas en formato YML son reference-anti-vm-strings.yml. 
- Esta se encuentra en el espacio de nombres anti-vm/vm-detection 
- que también se encuentra en el espacio de nombres de nivel superior Anti-Analysis.

Esto indica que CAPA pudo identificar que el software potencialmente malicioso busca claves de registro específicas de VMware, la presencia de herramientas de VMware u otros elementos relacionados con la máquina virtual mediante el archivo YAML de la regla reference-anti-vm-strings.yml. El malware suele realizar este comportamiento para evitar la detección. Por eso CAPA lo marcó.

Veamos otro ejemplo: "programar tarea mediante schtasks".

- Observamos que las reglas relacionadas en formato YML son schedule-task-via-schtasks.yml*. 
- Esto se encuentra en el espacio de nombres «programmed-tasks»
- que también se encuentra en el espacio de nombres de nivel superior «persistente». 

Esto nos indica que CAPA podría identificar comportamientos relacionados con las tareas programadas dentro del sistema operativo Windows. Podría haber reconocido patrones que indican que el ejecutable se registra como una tarea programada para mantener la persistencia mediante la regla definida en «schedule-task-via-schtasks.yml».

¡Un momento! ¿Has notado algo?

¡Correcto! El elemento «Capability» tiene el mismo nombre que los archivos YML de «Reglas», con un guion (-) añadido entre los espacios. Es sencillo, ya que «Capability» es el nombre de la regla.

Ahora bien, queremos mencionar algunas excepciones. Si la «Capability» o las reglas no se encuentran en su espacio de nombres, tomemos las cadenas de criptomonedas de referencia de «Capability» de la tabla anterior; esto debería estar en el espacio de nombres de nivel superior «Impact», ¿verdad? Sin embargo, si revisa las carpetas, no encontrará las reglas correspondientes. Se encontrarán en el TLN de Nursery. Este es el marcador de posición para las reglas que aún no están completamente pulidas.

Ahora que tenemos una buena visión general y comprendemos el contenido de Capacidad y Espacio de nombres, deberíamos poder explicar el resultado de ejemplo de las tareas anteriores. Por lo tanto, hagamos un breve resumen usando uno de los resultados. ¿De acuerdo?

![[Pasted image 20250909170556.png]]

Aquí está la explicación del resultado anterior. Consulte la tabla a continuación.

| Label                   | Value                           | Explanation                                                                                                                                                                                                                                                                                                              |
| ----------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Capability              | **reference base64 string**     | El malware tiene la capacidad de codificar datos utilizando un esquema base64.                                                                                                                                                                                                                                           |
| Top-Level Namespace     | **data-manipulation**           | Contiene un conjunto de reglas que rigen los comportamientos involucrados en la alteración de datos dentro de archivos ejecutables. Este aspecto puede considerarse el componente de "transformación de datos" del comportamiento del malware, abarcando acciones como el cifrado de cadenas y la codificación de datos. |
| Namespace               | **encoding/base64**             | Este espacio de nombres consta de reglas para codificar y decodificar datos utilizando Base64 y XOR                                                                                                                                                                                                                      |
| Rule YAML File Matched? | **reference-base64-string.yml** | Recuerde que el nombre de la capacidad es también el nombre de la regla con un guion adicional (-) entre los espacios.                                                                                                                                                                                                   |

Con esta información, ¡podría decirse que este archivo puede usar el esquema de codificación base64!

¡Ya hemos terminado de analizar los resultados de la muestra de la tarea anterior!

Answer the questions below

What **rule yaml file** was matched if the Capability or rule name is **check HTTP status code**?
respuesta check-http-status-code.yml

What is the **name of the Capability** if the rule YAML file is `reference-anti-vm-strings.yml`?
respuesta reference anti-VM strings

Which **TLN** or Top-Level Namespace includes the Capability or rule name **run PowerShell expression**?
respuesta load-code

Check the conditions inside the `check-for-windows-sandbox-via-registry.yml` rule file from this [link](https://github.com/MBCProject/capa-rules-1/blob/master/anti-analysis/anti-vm/vm-detection/check-for-windows-sandbox-via-registry.yml). What is the **value of the API** that ends in `Ex` is it looking for?
respuesta RegOpenKeyEx

---

**==¡Más información, más diversión!==**

¿No te interesa saber qué coincidió exactamente dentro de la regla? ¡Pues a mí sí!

En esta tarea, intentaremos determinar el motivo de la activación de las reglas y las condiciones implicadas. Para ello, usaremos el parámetro -vv o **muy verboso**.

|Option|Description|Sample Syntax|
|---|---|---|
|`-v` or `--verbose`|enable verbose result document|`capa.exe -v .\cryptbot.bin`|
|`-vv` or `--vverbose`|enable very verbose result document)|`capa.exe -vv .\cryptbot.bin`|
¡Vamos a ejecutarlo!

![[Pasted image 20250909173435.png]]

Esto nos dará resultados más detallados; sin embargo, tomará bastante tiempo. Ya procesamos esto y le asignamos el nombre cryptbot_vv.txt al archivo en "C:\Users\Administrator\Desktop\capa". Recuerda que no es necesario esperar a que la herramienta termine de ejecutarse; lo hicimos para que puedas familiarizarte con su funcionamiento y experimentar con sus parámetros.

Abre otra terminal de PowerShell y examina el archivo con el comando Get-Content cryptbot_vv.txt.

![[Pasted image 20250909173456.png]]

¿Has abierto el archivo? ¿Tienes más de tres mil líneas similares a esta?

Acceder a esta enorme cantidad de información mediante una terminal o un editor de texto será un desafío.

Para analizar este resultado fácilmente, necesitamos hacer dos cosas. Primero, usaremos los parámetros -j y -vv, y dirigiremos el resultado a un archivo .json. El comando sería capa.bin -j -vv .\cryptbot.bin > cryptbot_vv.json

![[Pasted image 20250909173517.png]]

Nuevamente, esto llevará bastante tiempo, similar a los comandos anteriores que ejecutamos. Lo procesamos y creamos un archivo llamado cryptbot_vv.json ubicado en "C:\Users\Administrator\Desktop\capa". Además, adjuntamos el archivo a esta tarea. Recuerda que no es necesario esperar a que la herramienta termine de ejecutarse; lo hicimos para que puedas familiarizarte con su funcionamiento y experimentar con sus parámetros.

Podemos comenzar con el siguiente paso.


**CAPA Web Explorer**

El segundo paso es subir el archivo a CAPA Explorer Web. Podemos usar la versión en [línea](https://mandiant.github.io/capa/explorer/#/) o la versión sin conexión que ya está en la máquina virtual. Hay un navegador Google Chrome en el escritorio llamado capa_web_explorer_offline.html. También puedes acceder a él usando un marcador de Chrome. Ten en cuenta que la página local puede tardar hasta un minuto en cargarse en Chrome en la máquina de destino.

![[Pasted image 20250909173616.png]]

¡Ahora deberíamos tener acceso a la página de inicio!

![[Pasted image 20250909173703.png]]

Busca el botón "Subir desde local" en la parte inferior izquierda de la página y selecciona el archivo cryptbot_vv.json en C:\Users\Administrator\Desktop\capa. Una vez subido, deberías obtener un resultado similar.

![[Pasted image 20250909173730.png]]

¿No se ve genial y más fácil de usar? ¡Seguro que sí!

Ahora es el momento de explorar esta excelente adición a la herramienta. Revisaremos algunas funciones y comprobaremos qué coincidió exactamente dentro de la regla. Esto nos dará una mejor idea de cómo funciona la regla.

Repasemos nuestro primer ejemplo a continuación. Sabemos que la función era hacer referencia a cadenas anti-VM dirigidas a VMWare, y el archivo de configuración de la regla o archivo YAML correspondiente es anti-VM-Strings-targeting-VMWare.yml. Observe el recuadro en la imagen.

![[Pasted image 20250909173802.png]]

A continuación, le mostraremos una descripción general del contenido de la regla. Concéntrese en las características, ya que CAPA utiliza las siguientes cadenas para comprobar si se encuentran dentro del archivo analizado.

![[Pasted image 20250909173838.png]]
![[Pasted image 20250909173920.png]]

¿Lo viste? ¡Correcto! En las características, CAPA Web Explorer hace referencia a la cadena "/VMWare/i". En resumen, CAPA indica que, en este espacio de nombres, podríamos identificar cadenas con el valor VMWare mediante las condiciones de la regla y expresiones regulares.

Veamos otro ejemplo. Sabemos que la capacidad era hacer referencia a la tarea programada mediante schtasks, y la regla correspondiente era programar la tarea mediante schtasks.yml. Observa el recuadro en la imagen.

![[Pasted image 20250909173945.png]]

Lo mismo aplica a nuestro primer ejemplo; le mostraremos el resumen del contenido de la regla. Concéntrese en las características, ya que CAPA utiliza las siguientes cadenas para comprobar si hay cadenas en el archivo analizado.

![[Pasted image 20250909174007.png]]

Con esta función, CAPA Web Explorer hace referencia a la cadena "/schtasks/i y /\/create /i". En resumen, CAPA indica que, bajo este espacio de nombres, y mediante las condiciones de la regla y expresiones regulares, podemos identificar cadenas con el valor schtasks y create.

**Cuadro de búsqueda global**

Otra característica interesante de esta herramienta son sus opciones de filtro y el cuadro de búsqueda global, que son muy útiles.

![[Pasted image 20250909174051.png]]

Podríamos examinar rápidamente esta abrumadora información usando CAPA Web Explorer en comparación con cualquier editor de texto.

¡No dudes en explorar más!

Answer the questions below

Which parameter allows you to output the result of CAPA into a **.json file**?
respuesta  -j

What tool allows you to interactively explore CAPA results in your web browser?
respuesta  CAPA Web Explorer

Which feature of this CAPA Web Explorer allows you to filter options or results?
respuesta  Global Search Box

---

**==Conclusión==**

En esta sala, analizamos cómo CAPA se aprovecha y desempeña un papel crucial en la ciberseguridad, analizando software potencialmente malicioso o peligroso y buscando proactivamente amenazas potenciales mediante análisis estático. Esto se logra automatizando el proceso de detección de funcionalidades complejas dentro de archivos ejecutables y presentando los hallazgos en un formato fácil de entender para los expertos en seguridad. Esta simplificación de conceptos complejos de ingeniería inversa facilita la comprensión rápida del software potencialmente dañino, lo que en última instancia fortalece la respuesta a incidentes y las estrategias defensivas.
