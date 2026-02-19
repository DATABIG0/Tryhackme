

**==Introducción==**

FlareVM, o "Análisis Forense, Lógico e Ingeniería Inversa", destaca por ser una colección completa y cuidadosamente seleccionada de herramientas especializadas, diseñadas exclusivamente para satisfacer las necesidades específicas de ingenieros inversos, analistas de malware, personal de respuesta a incidentes, investigadores forenses y expertos en pruebas de penetración. Este kit de herramientas, desarrollado por el equipo FLARE de FireEye, es una herramienta poderosa para desentrañar misterios digitales, comprender mejor el comportamiento del malware y profundizar en los complejos detalles de los ejecutables.

![[Pasted image 20250912130016.png]]

Casi todos los archivos que utilizaremos en esta sala se encuentran en la carpeta C:\Users\Administrator\Desktop\Sample.

Aviso legal: La máquina FlareVM conectada a esta sala contiene archivos de muestra maliciosos como parte de los ejercicios prácticos y no tiene acceso a internet. Estos archivos no deben descargarse, ejecutarse (fuera de la máquina FlareVM) ni distribuirse bajo ninguna circunstancia. Hacerlo podría dañar su sistema o red. Manipule siempre estos archivos únicamente en entornos aislados, controlados y seguros.


---

**==Arsenal de Herramientas==**

En esta tarea, le presentaremos las herramientas de FlareVM. Cuenta con numerosas herramientas especializadas de análisis forense, respuesta a incidentes e investigación de malware.

A continuación, se muestran las herramientas agrupadas por categoría.

**Ingeniería Inversa y Depuración**

La ingeniería inversa es como resolver un rompecabezas al revés: se desmonta un producto terminado para comprender su funcionamiento. La depuración consiste en identificar errores, comprender por qué ocurren y corregir el código para evitarlos.

- **Ghidra:** Suite de ingeniería inversa de código abierto desarrollada por la NSA.
- **x64dbg**: Depurador de código abierto para binarios en formatos x64 y x32.
- **OllyDbg**: Depurador para ingeniería inversa a nivel de ensamblador.
- **Radare2**: Una sofisticada plataforma de código abierto para ingeniería inversa.
- **Binary Ninja:** Una herramienta para desensamblar y descompilar binarios.
- **PEiD**: Herramienta de detección de empaquetadores, criptografía y compiladores. 

**Desensambladores y Descompiladores**

Los desensambladores y descompiladores son herramientas cruciales en el análisis de malware. Ayudan a los analistas a comprender el comportamiento, la lógica y el flujo de control del software malicioso, descomponiéndolo en un formato más comprensible. Las herramientas mencionadas a continuación se utilizan comúnmente en esta categoría.

- **CFF Explorer**: un editor de archivos ejecutables portátiles (PE).
- **Hopper Disassembler**: un depurador, desensamblador y descompilador.
- **RetDec**: un descompilador de código abierto para código máquina.

**Análisis estático y dinámico**

El análisis estático y dinámico son dos métodos cruciales en ciberseguridad para examinar malware. El análisis estático implica inspeccionar el código sin ejecutarlo, mientras que el análisis dinámico implica observar su comportamiento mientras se ejecuta. Las herramientas mencionadas a continuación se utilizan comúnmente en esta categoría.

- **Process Hacker**: un sofisticado editor de memoria y observador de procesos.
- **PEview**: un visor de archivos ejecutables portátiles (PE) para análisis. 
- **Dependency Walker**: Herramienta para visualizar las dependencias de DLL de un ejecutable.
- **DIE (Detect It Easy)**: Herramienta de detección de empaquetadores, compiladores y criptogramas.

**Informática forense y respuesta a incidentes**

La informática forense digital implica la recopilación, el análisis y la preservación de evidencia digital de diversas fuentes, como computadoras, redes y dispositivos de almacenamiento. Asimismo, la respuesta a incidentes se centra en la detección, contención, erradicación y recuperación de ciberataques. Las herramientas mencionadas a continuación se utilizan comúnmente en esta categoría.

- **Volatility**: Marco de análisis de volcado de RAM para análisis forense de memoria.
- **Rekall**: Marco para análisis forense de memoria en respuesta a incidentes.
- **FTK Imager**: Herramientas de adquisición y análisis de imágenes de disco para uso forense.

**Análisis de red**

El análisis de red incluye diferentes métodos y técnicas para estudiar y analizar redes con el fin de descubrir patrones, optimizar el rendimiento y comprender la estructura y el comportamiento subyacentes de la red.

- **Wireshark**: Analizador de protocolos de red para el registro y análisis de tráfico. 
- **Nmap**: herramienta de detección de vulnerabilidades y mapeo de red.
- **Netcat**: herramienta útil para leer y escribir datos en conexiones de red.

**Análisis de archivos**

El análisis de archivos es una técnica que se utiliza para examinar archivos en busca de posibles amenazas de seguridad y garantizar los permisos adecuados.

- **FileInsight**: programa para examinar y editar archivos binarios.
- **Hex Fiend**: editor hexadecimal ligero y rápido.
- **HxD**: visualización y edición de archivos binarios con un editor hexadecimal.

**Scripting y automatización**

El scripting y la automatización implican el uso de scripts como PowerShell y Python para automatizar tareas y procesos repetitivos, haciéndolos más eficientes y menos propensos a errores humanos.

- **Python**: centrado principalmente en la automatización con módulos y herramientas de Python.
- **PowerShell Empire**: marco para la postexplotación de PowerShell.

**Sysinternals Suite**

Sysinternals Suite es un conjunto de utilidades avanzadas del sistema diseñadas para ayudar a los profesionales de TI y desarrolladores a administrar, solucionar problemas y diagnosticar sistemas Windows.

- **Autoruns**: muestra qué ejecutables están configurados para ejecutarse durante el arranque del sistema. 
- **Explorador de Procesos**: Proporciona información sobre los procesos en ejecución.
- **Monitor de Procesos**: Monitorea y registra la actividad de procesos/hilos en tiempo real.

¿Has revisado todas las categorías? Hay muchísimas, ¿verdad? No te preocupes, no abordaremos todas esas herramientas ahora mismo; ¡podríamos tardar meses en terminar! Queremos presentarte el concepto de tener un único conjunto de herramientas para diferentes propósitos, lo que te dará una idea de lo que podría funcionar mejor para la tarea específica.

En la siguiente tarea, analizaremos las herramientas estándar utilizadas para la investigación.

**Answer the questions below**

Which tool is an Open-source debugger for binaries in x64 and x32 formats?
respuesta x64dbg

What tool is designed to analyze and edit Portable Executable (PE) files?
respuesta CFF Explorer

Which tool is considered a sophisticated memory editor and process watcher?
respuesta  Process Hacker

Which tool is used for Disc image acquisition and analysis for forensic use?
respuesta FTK Imager

What tool can be used to view and edit a binary file?
respuesta  HxD


---

**==Herramientas de uso común para la investigación: Resumen==**

Examinemos las herramientas que abordaremos en esta sala. Estas herramientas son las básicas para las investigaciones iniciales. Consulte la lista a continuación.

| **Tool**         | **Investigative Value**                                                                                                                                                          |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Procmon          | Una herramienta útil para rastrear la actividad del sistema, especialmente en lo que respecta a la investigación de malware, resolución de problemas e investigaciones forenses. |
| Process Explorer | Permite ver el proceso de la relación padre-hijo, las DLL cargadas y su ruta.                                                                                                    |
| HxD              | Los archivos maliciosos pueden examinarse o modificarse mediante edición hexadecimal.                                                                                            |
| Wireshark        | Observar e investigar el tráfico de la red para buscar actividad inusual.                                                                                                        |
| CFF Explorer     | Puede generar hashes de archivos para verificar la integridad, autenticar la fuente de los archivos del sistema y validar su validez.                                            |
| PEStudio         | Análisis estático o estudio de las propiedades de archivos ejecutables sin ejecutar los archivos.                                                                                |
| FLOSS            | Extrae y desofusca todas las cadenas de programas de malware mediante técnicas avanzadas de análisis estático.                                                                   |

Puede seguir las instrucciones y abrir las herramientas y archivos en FlareVM mientras analizamos la descripción general de algunas de estas herramientas.

**Monitor de Procesos (Procmon)**

Una potente herramienta de Windows diseñada para ayudarle a registrar problemas con las aplicaciones de su sistema. Le permite **ver, registrar y realizar un seguimiento de la actividad del sistema y de los archivos de Windows en tiempo real**. El Monitor de Procesos es útil para supervisar la actividad del sistema, especialmente en lo que respecta a la **investigación de malware, la resolución de problemas y las investigaciones forenses**. Monitorea en tiempo real la actividad del sistema de archivos, el registro y los subprocesos/procesos.

A continuación, le mostramos cómo utilizarlo eficazmente para la investigación.

![[Pasted image 20250912130038.png]]

Según esta entrada de registro, el proceso lsass.exe, relacionado con el Servicio del Subsistema de Autoridad de Seguridad Local (LSASS), ha leído correctamente un archivo. LSASS gestiona la autenticación y se comunica frecuentemente con archivos cruciales del sistema, como lsasrv.dll (Servicio del Servidor de Autoridad de Seguridad Local).

Aunque se trata de un proceso estándar del sistema, LSASS puede ser objeto de ataques de volcado de credenciales si examina los registros en busca de indicios de actividad maliciosa. Mimikatz y otras herramientas intentan acceder a la memoria de LSASS con frecuencia. En estas situaciones, debe estar atento a cualquier actividad sospechosa adicional relacionada con LSASS, como patrones de acceso inusuales o procesos que leen o escriben en lsass.exe.

No se preocupe, ¡el ejemplo anterior no muestra indicios de malware!

**Explorador de Procesos (Procexp)**

El Explorador de Procesos ofrece información detallada sobre los procesos activos que se ejecutan en su equipo. Le permite profundizar en el funcionamiento interno de su sistema, proporcionando una lista completa de los procesos en ejecución y sus cuentas de usuario vinculadas. Si alguna vez tuvo curiosidad sobre qué programa está accediendo a un archivo o carpeta específicos, Process Explorer puede proporcionarnos esa información.

![[Pasted image 20250912130152.png]]

Como puede ver en la imagen superior, la aplicación CFF Explorer está abierta. Usando Process Explorer (procexp), ubicado en el escritorio, identificamos el proceso y su proceso principal. Esto suele ser bastante útil cuando queremos monitorear qué otros procesos se están generando, como desde un documento de Word, un archivo LNK o incluso un archivo ISO, ya que los atacantes suelen abusar de ellos.

**HxD**

HxD es un editor hexadecimal rápido y flexible para editar archivos, memoria y unidades de cualquier capacidad. Se puede aplicar a la investigación forense, la recuperación de datos, la depuración y la manipulación precisa de datos binarios. Entre sus funciones importantes se incluyen la visualización del contenido de archivos y memoria, la edición, la búsqueda y la comparación de datos hexadecimales. Veamos cómo funciona la herramienta.

![[Pasted image 20250912130227.png]]

Esta instantánea del editor hexadecimal de HxD muestra el archivo binario possible_medusa.txt. Los datos hexadecimales a la izquierda indican el contenido del archivo en hexadecimal, y la interpretación ASCII aparece a la derecha. Curiosamente, el archivo comienza con **4D 5A (Little Endian)**, lo que indica que es ejecutable.
El Inspector de Datos a la derecha permite examinar bytes individuales mostrando sus valores en diversos tipos de datos (p. ej., entero, flotante), lo que facilita una evaluación de datos más sencilla.

Al permitir un examen exhaustivo de los datos hexadecimales sin procesar de un archivo, HxD facilita la consulta identificando tipos de archivos, estructuras y posibles daños. Su función Inspector de Datos ayuda a ofrecer información sobre valores de bytes específicos.

**CFF Explorer**

Con la completa información de archivos de CFF Explorer, los investigadores pueden generar hashes de archivos para verificar la integridad, autenticar el origen de los archivos del sistema y validar su validez (p. ej., buscando alteraciones inusuales). Es importante saber esto cuando se analiza malware, ya que puede haber código peligroso oculto en archivos de sistema alterados.

![[Pasted image 20250912130338.png]]

Los detalles del archivo cryptominer.bin se muestran en el ejemplo. El 23 de septiembre de 2024, se generó un archivo ejecutable portátil de 64 bits. La información del archivo se puede verificar mediante sus hashes (SHA-1 y MD5). Durante las investigaciones, esta herramienta ayuda a confirmar la búsqueda de información del archivo y a localizar posibles problemas.

**Wireshark**

En cuanto al análisis del tráfico de red, Wireshark es una potente herramienta que los investigadores pueden utilizar para localizar conexiones sospechosas, examinar protocolos y detectar posibles ataques o exfiltración de datos. En este caso, TLSv1.2 sugiere una conexión segura y cifrada que puede enmascarar actividades dañinas o proteger el tráfico legítimo.

![[Pasted image 20250912130413.png]]

Esto muestra los paquetes capturados con detalles sobre el protocolo, el origen, el destino y otra información. La mayoría de los paquetes muestran que se utilizan TLSv1.2 y TCP para la transmisión cifrada. Los datos sin procesar del paquete se muestran en formato ASCII y hexadecimal, con una parte significativa cifrada mediante TLSv1.2.

**PEStudio**

El análisis estático, o el estudio de las propiedades de los archivos ejecutables sin ejecutarlos, se realiza con PEstudio. Esta función es beneficiosa en diversas situaciones. PEstudio ofrece información diversa sobre un archivo sin poner a los usuarios en peligro de ejecución, lo que ayuda a identificar ejecutables sospechosos o dañinos.

¿Cómo funciona? Veamos la imagen a continuación.

![[Pasted image 20250912130458.png]]

Este ejemplo muestra el análisis de un archivo ejecutable, PSexec.exe (no en la máquina virtual; este es solo un ejemplo), con PEstudio 9.22, una herramienta de análisis de malware estático. El archivo tiene un doble propósito: es legítimo para los administradores de sistemas, pero potencialmente explotado por hackers para acceso remoto.

El valor de entropía del archivo, de 6,596, indica una remota posibilidad de empaquetado o cifrado, algo típico de software peligroso. La versión 2.34 de esta aplicación de consola de 32 bits le permite ejecutar programas de forma remota, una función que se utiliza frecuentemente para migrar lateralmente durante los ataques. El archivo se ensambla con Visual C++ 8.

La naturaleza de doble uso de PsExec, generalmente legítimo pero sospechoso en entornos comprometidos, junto con indicadores bajos a medios y una entropía moderadamente alta, hace que su presencia en un sistema sea preocupante, especialmente si no se prevé la ejecución remota de código. Su uso en fases posteriores a la explotación justifica una mayor investigación para determinar si se está utilizando de forma maliciosa.

**FLOSS**

Mediante técnicas avanzadas de análisis estático, el solucionador de cadenas ofuscadas de FLARE (FLOSS, anteriormente FireEye Labs Obfuscated String Solver) extrae y desofusca automáticamente todas las cadenas de programas maliciosos. Al igual que strings.exe, puede mejorar el análisis estático básico de binarios desconocidos. FLOSS también incluye más scripts de Python en su directorio, que pueden usarse para cargar la salida del script en otros programas como IDA Pro o Binary Ninja.

![[Pasted image 20250912130733.png]]
![[Pasted image 20250912130804.png]]
![[Pasted image 20250912130822.png]]

En el ejemplo anterior, FLOSS extrajo 189 cadenas estáticas del binario, que podrían contener información codificada, como rutas de archivos, URL (probablemente para servidores de comando y control), direcciones IP, llamadas a la API, mensajes de error, registro, claves de cifrado y datos de configuración. Sin embargo, no se identificaron cadenas decodificadas, lo que sugiere que FLOSS no detectó ni decodificó cadenas generadas dinámicamente u ofuscadas durante este análisis. El malware suele utilizar cadenas ofuscadas para ocultar su comportamiento malicioso.

**Answer the questions below**

Which tool was formerly known as FireEye Labs Obfuscated String Solver?
respuesta  FLOSS

Which tool offers in-depth insights into the active processes running on your computer?
respuesta  Process Explorer

By using the Process Explorer (procexp) tool, under what process can we find smss.exe?
respuesta  system
![[Pasted image 20250919173600.png]]

Which powerful Windows tool is designed to help you record issues with your system's apps?
respuesta  Procmon

Which tool can be used for Static analysis or studying executable file properties without running the files?
respuesta  PEStudio

Using the tool PEStudio to open the file **cryptominer.bin** in the Desktop\Sample folder, what is the sha256 value of the file?
respuesta  E9627EBAAC562067759681DCEBA8DDE8D83B1D813AF8181948C549E342F67C0E

![[Pasted image 20250919173950.png]]

Using the tool PEStudio to open the file **cryptominer.bin** in the Desktop\Sample folder, how many functions does it have?
respuesta  102
![[Pasted image 20250919174312.png]]

What tool can generate file hashes for integrity verification, authenticate the source of system files, and validate their validity?
respuesta  CFF Explorer

Using the tool CFF Explorer to open the file **possible_medusa.txt** in the Desktop\Sample folder, what is the MD5 of the file?
respuesta
646698572AFBBF24F50EC5681FEB2DB7
![[Pasted image 20250919174458.png]]

Use the CFF Explorer tool to open the file **possible_medusa.txt** in the Desktop\Sample folder. Then, go to the **DOS Header Section.** What is the e_magic value of the file?
respuesta  5A4D

![[Pasted image 20250919174544.png]]

---

**==Análisis de archivos maliciosos==**


En esta tarea, nos pondremos manos a la obra. ¡Comencemos!

Usando las herramientas de nuestra máquina virtual Flare, analizaremos diferentes ejecutables, los ejecutaremos y veremos qué hacen en una máquina específica.

Un usuario descargó un archivo **windows.exe** sospechoso el 24/09/2024 a las 3:43. Esta descarga se marcó como una amenaza potencial. El equipo de monitorización le ha enviado un correo electrónico solicitando un análisis. Le han enviado el archivo, que ahora se encuentra en la carpeta **C:\Users\Administrator\Desktop\Sample**.

![[Pasted image 20250920085038.png]]

Nuestro enfoque inicial para esta investigación consiste en realizar un análisis estático para obtener información inicial del binario.

**Análisis con PEStudio**

Comencemos con PEStudio. Abramos el archivo con esta herramienta. ¿Qué información podemos usar?

![[Pasted image 20250920085118.png]]

Para los hashes **MD5 9FDD4767DE5AEC8E577C1916ECC3E1D6** y **SHA-1 A1BC55A7931BFCD24651357829C460FD3DC4828F** calculados, se recomienda compararlos con bases de datos consolidadas como VirusTotal. Si no se detectan detecciones, es más probable que se trate de una campaña de malware reciente o aún no descubierta.

Aunque el archivo afirma estar conectado al Editor del Registro de Windows (REGEDIT), como se puede ver en la **descripción**, es probable que se trate de un intento de engañar a los usuarios para evitar ser detectados.

Las herramientas legítimas de REGEDIT suelen encontrarse en el directorio **C:\Windows\System32**, en lugar de en la ubicación de descarga del usuario.

¿Qué más?

![[Pasted image 20250920085139.png]]

Редактор реестра" - "Registry Editor", "Операционная система. La presencia de Microsoft® Windows® en los metadatos del archivo resulta sospechosa, especialmente si el usuario o la organización no operan en un entorno de habla rusa. Esto podría tener graves consecuencias para nuestra organización.

La ausencia de un **encabezado completo** indica que el archivo podría estar comprimido u ofuscado para evitar su detección mediante herramientas de análisis estático. Este es un comportamiento típico del malware sofisticado que intenta evadir la detección alterando secciones críticas de su archivo PE.

Las pestañas de **funciones** enumeran las **llamadas a la API** que el archivo ha importado. Esto también se conoce como IAT (Tabla de Direcciones de Importación). Al hacer clic en la pestaña de la lista negra, PeStudio ordenará la API moviendo todas las funciones incluidas en la lista negra a la parte superior. Esto es útil porque nos permite comprender cómo podría comportarse el malware una vez que compromete un host. La imagen a continuación muestra qué API se ha importado.

![[Pasted image 20250920085202.png]]

Estas son las funciones importantes que observamos.

**set_UseShellExecute**: Esta función permite que el proceso utilice el shell del sistema operativo para ejecutar otros procesos. Esto se observa a menudo en malware que genera procesos adicionales para realizar acciones maliciosas.

**CryptoStream, RijndaelManaged, CipherMode, CreateDecryptor**: Estas API indican que el ejecutable utiliza funciones criptográficas, específicamente Rijndael (cifrado AES). El malware puede usar criptografía para cifrar comunicaciones y archivos, o incluso implementar funciones de ransomware.

**Análisis con FLOSS**

Abra PowerShell y vaya al directorio donde se encuentra nuestro archivo, que es **C:\Users\Administrator\Desktop\Sample**. Tenga en cuenta que puede tardar un tiempo en aparecer el mensaje de PowerShell. Ejecute el comando ``FLOSS.exe .\windows.exe > windows.txt``. Esto ejecutará la herramienta **floss.exe** y la guardará en un archivo llamado windows.txt en el mismo directorio.

![[Pasted image 20250920085221.png]]

Abra el archivo y vaya a la parte inferior del resultado.

![[Pasted image 20250920085251.png]]

¿No te suenan? ¡Estas son las funciones que vimos antes con la herramienta PEStudio!

**Analizar con Process Explorer y Process Monitor**

En este ejemplo, analizaremos la conectividad de red del archivo **cobaltstrike.exe**, ubicado en **C:\Users\Administrator\Desktop\Sample**.

Intentaremos averiguar si el archivo tiene alguna conexión de red con algún posible servidor C2. ¡Comencemos! Ejecuta el archivo **cobaltstrike.exe** y abre **Process Explorer** en el escritorio o desde la barra de tareas. También puedes buscarlo en la barra de búsqueda de Windows. Si haces clic manualmente en el binario, **Explorer.exe** sería el proceso principal y cobaltstrike.exe sería el proceso secundario. Veamos si es así.

![[Pasted image 20250920085325.png]]

¡Así es, como puede ver en la captura de pantalla anterior! Recuerde que esta información es crucial, pero centrémonos en nuestro objetivo: determinar si este proceso se conecta a la red y a qué destino. **El ID del proceso es 4756**. Tenga en cuenta que el ID del proceso puede ser diferente al de su equipo. Haga clic derecho en el proceso, seleccione **Propiedades** y vaya a la pestaña **TCP/IP**. Deberíamos poder determinar el destino al que se conecta y el estado que envía.

![[Pasted image 20250920085344.png]]

¡Listo! Por otra parte, al realizar un análisis, este debe ser verificado y preciso. Por lo tanto, no dependeremos de una sola herramienta. Usaremos otra para determinar si la información es correcta. Detenga el proceso y vuelva a ejecutarlo. Esta vez, usaremos **Procmon** o **Proces Monitor**. Este también se encuentra en el escritorio o en la barra de tareas.

Al abrir Procmon, buscar el binario es complicado, ya que mostrará todos los procesos activos. Lo que haremos es filtrarlo. La imagen de abajo muestra el icono del filtro. También puede presionar **Ctrl + L**.

![[Pasted image 20250920085404.png]]

Usar este filtro implica varios pasos. Esto incluye:
1. Seleccionar el nombre del proceso.
2. Seleccionar "Contiene".
3. Escribir cualquier valor que contenga una palabra relacionada con el proceso. En este caso, "cobalt".
4. Hacer clic en "Incluir".
5. Luego, en "Agregar" y en "Aplicar".
6. Debería poder ver las condiciones agregadas.

![[Pasted image 20250920085422.png]]

Esto debería darnos un resultado más detallado.

![[Pasted image 20250920085436.png]]

Esto confirma que el binario efectivamente estaba realizando una conexión a una dirección IP desconocida que es 47.120.46.210.

**Answer the questions below**

Using PEStudio, open the file windows.exe. What is the **entropy value** of the file windows.exe? 
respuesta 7.999
![[Pasted image 20250922152532.png]]

Using PEStudio, open the file windows.exe, then go to manifest (administrator section)**.** What is the value under **requestedExecutionLevel**?
respuesta requireAdministrator
![[Pasted image 20250922152651.png]]

Which function allows the process to use the operating system's shell to execute other processes?
respuesta  set_UseShellExecute
![[Pasted image 20250922152808.png]]

Which API starts with R and indicates that the executable uses cryptographic functions?
respuesta RijndaelManaged
![[Pasted image 20250922153542.png]]

What is the Imphash of cobaltstrike.exe?
respuesta 92EEF189FB188C541CBD83AC8BA4ACF5
![[Pasted image 20250922153631.png]]

What is the defanged IP address to which the process cobaltstrike.exe is connecting?
respuesta 47[.]120[.]46[.]210
![[Pasted image 20250922173352.png]]

What is the destination port number used by cobaltstrike.exe when connecting to its C2 IP Address?
respuesta 81
![[Pasted image 20250922161608.png]]

During our analysis, we found a process called cobaltstrike.exe. What is the **parent process** of cobaltstrike.exe?
respuesta explorer.exe
![[Pasted image 20250922173321.png]]

---

**==Conclusión==**

En esta sala, presentamos FlareVM (Análisis Forense, Análisis Lógico e Ingeniería Inversa), un entorno completo y personalizado diseñado para la respuesta a incidentes, la ingeniería inversa de malware y el análisis forense. Revisamos las herramientas instaladas y las clasificamos según su propósito. A continuación, analizamos algunas herramientas estándar de uso generalizado durante una investigación, como PEStudio, CFF Explorer, Process Monitor y Process Explorer. Finalmente, adquirimos experiencia práctica en el análisis de programas o archivos maliciosos con estas herramientas.