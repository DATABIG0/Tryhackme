
Introduction

![[Pasted image 20251217190646.png]]

TBFC está bajo ataque. Los sistemas presentan un comportamiento extraño y la compañía ahora siente la ausencia de su principal defensor, McSkidy. Sin embargo, McSkidy se aseguró de que el legado perdurara.

El equipo de McSkidy, decidido y bien entrenado, confía plenamente en asegurar todos los sistemas y recuperar el control antes del gran evento, SOCMAS.

Han decidido realizar un análisis forense detallado en uno de los sistemas más críticos de TBFC, dispatch-srv01. Este sistema coordina la entrega de regalos mediante drones durante SOCMAS. Sin embargo, recientemente fue comprometido por los bandidos de conejos del Rey Malhare.

Los defensores de TBFC han decidido dividirse en equipos especializados para descubrir el ataque a este sistema mediante un análisis forense detallado. Mientras otros miembros del equipo investigan registros, volcados de memoria, sistemas de archivos y otros artefactos, usted trabajará para investigar el registro de este sistema comprometido.

![[Pasted image 20251217190710.png]]

Objetivos de aprendizaje

- Comprender qué es el Registro de Windows y qué contiene.
- Profundizar en los subárboles del Registro y las claves raíz.
- Analizar los subárboles del Registro con el Editor del Registro integrado.
- Aprender análisis forense del Registro e investigar con el Explorador del Registro.


Alternatively, you can use the credentials below to connect to the target machine via RDP from your own THM VPN connected machine:

![[Pasted image 20251217190738.png]]

Answer the questions below

I successfully have access to my target machine!

No answer needed


---

# Investigate the Gifts Delivery Malfunctioning

## Registro de Windows

Tu cerebro almacena toda la información que necesitas para funcionar eficazmente. Esto incluye:

- ¿Cómo deberías comportarte?
- ¿Qué harías al despertar?
- ¿Cómo te vestirías?
- ¿Cuáles son tus hábitos?
- ¿Qué te ha pasado últimamente?

Estos son solo algunos datos. Tu cerebro sabe prácticamente todo sobre ti. Es como una base de datos que almacena la configuración humana.

El sistema operativo Windows no es un ser humano, pero también necesita un cerebro que almacene todas sus configuraciones. Este cerebro se conoce como Registro de Windows. El registro contiene toda la información que el sistema operativo Windows necesita para funcionar.

Ahora bien, este cerebro de Windows (Registro) no se almacena en un único lugar, a diferencia del cerebro humano, que se encuentra en un único lugar dentro de la cabeza. Está compuesto por varios archivos separados, cada uno de los cuales almacena información sobre diferentes ajustes de configuración. Estos archivos se conocen como subárboles.

![[Pasted image 20251217190859.png]]

Analicemos todas estas subáreas en la tabla a continuación. La primera columna contiene los nombres de las subáreas, la segunda, el tipo de configuración que almacena cada subáreas y la tercera, su ubicación en el disco.

|Hive Name|Contains|Location|
|---|---|---|
|SYSTEM|- Services<br>- Mounted Devices<br>- Boot Configuration<br>- Drivers<br>- Hardware|`C:\Windows\System32\config\SYSTEM`|
|SECURITY|- Local Security Policies<br>- Audit Policy Settings|`C:\Windows\System32\config\SECURITY`|
|SOFTWARE|- Installed Programs<br>- OS Version and other info<br>- Autostarts<br>- Program Settings|`C:\Windows\System32\config\SOFTWARE`|
|SAM|- Usernames and their Metadata<br>- Password Hashes<br>- Group Memberships<br>- Account Statuses|`C:\Windows\System32\config\SAM`|
|NTUSER.DAT|- Recent Files<br>- User Preferences<br>- User-specific Autostarts|`C:\Users\username\NTUSER.DAT`|
|USRCLASS.DAT|- Shellbags<br>- Jump Lists|`C:\Users\username\AppData\Local\Microsoft\Windows\USRCLASS.DAT`|


Nota: Las opciones de configuración almacenadas en cada subárbol mencionado anteriormente son solo algunos ejemplos. Cada subárbol almacena más que estos.

Ahora que comprende dónde se almacenan estos subárboles del Registro, puede que sienta la tentación de hacer doble clic y abrir estos archivos desde sus respectivas ubicaciones para ver los datos que contienen. Pero aquí está la cuestión: estos subárboles del Registro contienen datos binarios que no se pueden abrir directamente desde el archivo. Por lo tanto, hacer doble clic en ellos solo mostraría información que nunca comprenderá. Entonces, ¿cómo podemos ver los datos del registro?

El sistema operativo Windows tiene una herramienta integrada llamada Editor del Registro, que permite ver todos los datos del registro disponibles en estos subárboles. Puede abrir esta herramienta simplemente escribiendo "Editor del Registro" en la barra de búsqueda.

![[Pasted image 20251218183256.png]]

Como puede ver en la captura de pantalla anterior del Editor del Registro, hay algunas carpetas llamadas ``HKEY_LOCAL_MACHINE``,`` HKEY_CURRENT_USER`` y más. ¿Pero no esperábamos que se viera SYSTEM, SECURITY, SOFTWARE, etc., para que podamos ver sus datos? No se preocupe, Windows organiza todos los subárboles del registro en estas claves raíz estructuradas. En lugar de ver las colmenas del registro, siempre obtendrá estas claves raíz del registro cada vez que abra el registro. Ahora bien, ¿qué clave de registro contiene los datos de qué subárbol de registro? Para responder a esta pregunta, tenemos una tabla a continuación que asigna las claves de registro con sus respectivas colmenas de registro.

|Hive on Disk|Where You See It in Registry Editor|
|---|---|
|SYSTEM|`HKEY_LOCAL_MACHINE\SYSTEM`|
|SECURITY|`HKEY_LOCAL_MACHINE\SECURITY`|
|SOFTWARE|`HKEY_LOCAL_MACHINE\SOFTWARE`|
|SAM|`HKEY_LOCAL_MACHINE\SAM`|
|NTUSER.DAT|`HKEY_USERS\<SID> and HKEY_CURRENT_USER`|
|USRCLASS.DAT|`HKEY_USERS\<SID>\Software\Classes`|
En la tabla anterior, puede ver que la mayoría de las secciones del registro se encuentran bajo la clave ``HKEY_LOCAL_MACHINE (HKLM)``. Podemos verificar esto haciendo clic en la pequeña flecha de alternancia en el lado izquierdo de la clave HKLM en el Editor del Registro, como se muestra en la siguiente captura de pantalla:

![[Pasted image 20251218184405.png]]

Como puede ver, las colmenas SYSTEM, SOFTWARE, SECURITY y SAM están bajo la clave HKLM. NTUSER.DAT y USRCLASS.DAT se encuentran en HKEY_USERS (HKU) y HKEY_CURRENT_USER (HKCU).

Nota: Las otras dos claves (HKEY_CLASSES_ROOT (HKCR) y HKEY_CURRENT_CONFIG (HKCC)) no forman parte de ningún archivo de colmena independiente. Se completan dinámicamente cuando Windows se está ejecutando.

Hasta ahora, hemos aprendido qué es el registro, dónde se encuentra (en subárboles de registro separados) y cómo ver el registro a través del Editor del registro, que muestra las claves de registro respaldadas por estos subárboles de registro.

Ahora, veamos cómo podemos extraer información del registro. Piense en ello como navegar a diferentes archivos en el explorador de archivos. Si conoce la ruta donde está almacenado el archivo, puede ir directamente a esa ubicación para buscar el archivo. Echemos un vistazo a algunos ejemplos:

## Ejemplo 1: Ver dispositivos USB conectados

Nota: El contenido de la clave de registro explicado en este ejemplo no está disponible en la máquina virtual adjunta.

El registro almacena información sobre los dispositivos USB que se han conectado al sistema. Esta información está presente en la colmena SYSTEM. Para verlo:

1. Abra el Editor del Registro.
2. Navegue hasta la siguiente ruta: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR.
3. Aquí verá la información de los dispositivos USB (marca, modelo e ID del dispositivo).
4. Cada dispositivo tendrá lo siguiente:
5. Una subclave principal que es la identificación del tipo y fabricante del dispositivo USB.
6. Una subclave debajo de lo anterior (por ejemplo) que representa los dispositivos únicos bajo este modelo.

![[Pasted image 20251218190136.png]]

## Ejemplo 2: Ver programas ejecutados por el usuario

El registro almacena información sobre los programas que el usuario ejecutó usando el cuadro de diálogo Ejecutar Win + R. Esta información está presente en la colmena NTUSER.DAT. Para verlo:

1. Abra el Editor del Registro.
2. Navegue hasta la siguiente ruta: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU.
3. Aquí verá la lista de comandos escritos por el usuario en el cuadro de diálogo Ejecutar para ejecutar aplicaciones.

![[Pasted image 20251218190725.png]]

## Registro forense

Dado que el registro contiene una amplia gama de datos sobre el sistema Windows, desempeña un papel crucial en las investigaciones forenses. La ciencia forense del registro es el proceso de extracción y análisis de evidencia del registro. En las investigaciones forenses digitales de Windows, los investigadores analizan el registro, los registros de eventos, los datos del sistema de archivos, los datos de la memoria y otros datos relevantes para construir la línea de tiempo completa del incidente.

La siguiente tabla enumera algunas claves de registro que son particularmente útiles durante las investigaciones forenses.

|Registry Key|Importance|
|---|---|
|`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`|It stores information on recently accessed applications launched via the GUI.|
|`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`|It stores all the paths and locations typed by the user inside the Explorer address bar.|
|`HKLM\Software\Microsoft\Windows\CurrentVersion\App Paths`|It stores the path of the applications.|
|`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`|It stores all the search terms typed by the user in the Explorer search bar.|
|`HKLM\Software\Microsoft\Windows\CurrentVersion\Run`|It stores information on the programs that are set to automatically start (startup programs) when the users logs in.|
|`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`|It stores information on the files that the user has recently accessed.|
|`HKLM\SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`|It stores the computer's name (hostname).|
|`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`|It stores information on the installed programs.|

Se pueden utilizar muchas otras claves de registro para extraer pruebas importantes de un sistema Windows durante la investigación de un incidente. La investigación de estas claves de registro durante el análisis forense no se puede realizar a través de la herramienta incorporada del Editor del Registro. Debido a que el análisis del Registro no se puede realizar en el sistema bajo investigación (debido a la posibilidad de modificación), recopilamos los Colmenas del Registro y los abrimos sin conexión en nuestra estación de trabajo forense. Sin embargo, el Editor del Registro no permite abrir colmenas sin conexión. El editor de registro también muestra algunos de los valores clave en binario que no son legibles.

Para resolver este problema, existen algunas herramientas creadas para análisis forense del registro. En esta tarea utilizará la herramienta [Registry Explorer](https://ericzimmerman.github.io/), que es una herramienta forense del registro. Es de código abierto y puede analizar los datos binarios del registro, y podemos analizarlos sin temor a modificarlos.

## Práctico

En este ejemplo práctico, utilizaremos la herramienta Registry Explorer para analizar los Colmenas del Registro del sistema comprometido, despacho-srv01. Los Colmenas del Registro se han recopilado y están disponibles en la carpeta C:\Users\Administrator\Desktop\Registry Hives en la máquina adjunta a esta tarea.

Paso 1: Inicie el Explorador del Registro

Haga clic en el icono de Registry Explorer fijado en la barra de tareas de la máquina de destino para iniciarlo.

![[Pasted image 20251218192632.png]]

Paso 2: cargue las colmenas del registro

Una vez que se abra el Explorador del Registro con una interfaz vacía, siga estos pasos para cargar las colmenas:

1. Haga clic en la opción Archivo del menú superior
2. Seleccione Cargar colmena en el menú desplegable

![[Pasted image 20251218192707.png]]

Paso 3: Manejo de la urticaria sucia

Mientras se cargan los Colmenas del Registro, es importante saber que estos Colmenas del Registro a veces pueden estar "sucios" cuando se recopilan de sistemas activos, lo que significa que pueden tener transacciones incompletas. Para garantizar una carga limpia:

1. En la ventana emergente Cargar subárboles, navegue hasta C:\Users\Administrator\Desktop\Registry Hives.
2. Seleccione el archivo de colmena deseado (por ejemplo, SYSTEM)
3. Mantenga presionada la tecla **SHIFT** y luego presione Abrir para cargar los archivos de registro de transacciones asociados. Esto garantiza que obtendrá un estado de colmena limpio y consistente para el análisis.

![[Pasted image 20251218192741.png]]

4. Aparecerá un mensaje que indica la reproducción exitosa de los registros de transacciones.
5. Repita el mismo proceso para todas las demás colmenas que desee cargar.

![[Pasted image 20251218192802.png]]

Paso 4: investigar las claves de registro

Después de cargar la sección SISTEMA, puede navegar a claves de registro específicas para su investigación. Practiquemos encontrando el nombre de la computadora:

- Vaya a: ROOT\ControlSet001\Control\ComputerName\ComputerName. O también puedes simplemente escribir "ComputerName" en la barra de búsqueda para localizar rápidamente la clave, como se muestra a continuación.

![[Pasted image 20251218192832.png]]

- Alternativamente, puede hacer clic en la pestaña Marcadores disponibles y navegar hasta la clave ComputerName desde allí.
- Examine los valores para identificar el nombre de host del sistema. Debajo del valor de Datos, encontrará DISPATCH-SRV01.

![[Pasted image 20251218192929.png]]

Ahora que comprende cómo cargar colmenas y navegar en el Explorador del Registro, está listo para comenzar su investigación forense y descubrir evidencia de la intrusión TBFC en el servidor de Dispatch.

Nota: La actividad anormal en despacho-srv01 comenzó el 21 de octubre de 2025.

Consejo: La tabla que figura en la explicación de Registry Forensics será tu amiga.

**Answer the questions below**

What application was installed on the `dispatch-srv01` before the abnormal activity started?

Respuesta: DroneManager Updater
navegamos a la siguiente ruta: HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
listamos por el timestamp para las fechas y encontramos 
![[Pasted image 20251219161539.png]]


What is the full path where the user launched the application (found in question 1) from?

Respuesta: C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe
navegamos a la siguiente ruta: 
HKCU\NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist
![[Pasted image 20251219163726.png]]

Which value was added by the application to maintain persistence on startup?

Respuesta:  "C:\Program Files\DroneManager\dronehelper.exe" --background
navegamos a la siguiente ruta: 
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
![[Pasted image 20251219165309.png]]

If you enjoyed today's room, feel free to check out the [Expediting Registry Analysis](https://tryhackme.com/room/expregistryforensics) room.

Check
No answer needed
