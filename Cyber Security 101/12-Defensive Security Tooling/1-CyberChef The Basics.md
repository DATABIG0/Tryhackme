
==**Introducción**==

CyberChef es una aplicación web sencilla e intuitiva, diseñada para facilitar diversas tareas de ciberoperación dentro de su navegador. Es como una navaja suiza para datos: como tener un conjunto de herramientas diseñadas para realizar una tarea específica. Estas tareas abarcan desde codificaciones sencillas como XOR o Base64 hasta operaciones complejas como el cifrado AES o el descifrado RSA. CyberChef opera con recetas, una serie de operaciones que se ejecutan en orden.

![[Pasted image 20250903150610.png]]


---

**==Acceso a la herramienta==**

Hay diferentes maneras de acceder y ejecutar CyberChef. ¡Veamos los dos métodos más prácticos!

**Acceso en línea**

Solo necesitas un navegador web y conexión a internet. Haz clic en este [enlace](https://gchq.github.io/CyberChef) para abrir CyberChef directamente en tu navegador.

**Copia local o sin conexión**

Puedes ejecutarlo sin conexión o localmente en tu equipo descargando la última versión desde este [enlace](https://github.com/gchq/CyberChef/releases). Funciona tanto en Windows como en Linux. Te recomendamos descargar la versión más estable.


---

**==Navegación por la interfaz==**

CyberChef consta de cuatro áreas. Cada una incluye diferentes componentes o funciones.

Estas son las siguientes áreas:

1. Operaciones
2. Receta
3. Entrada
4. Salida

![[Pasted image 20250903150830.png]]

Analicemos cada una de estas áreas a continuación.

**Área de Operaciones**

Este es un repositorio práctico y completo de todas las diversas operaciones que CyberChef puede realizar. Estas operaciones están meticulosamente categorizadas, ofreciendo a los usuarios un acceso conveniente a diversas funciones. Los usuarios pueden utilizar la función de búsqueda para localizar operaciones específicas rápidamente, mejorando su eficiencia y productividad.

A continuación, se presentan algunas operaciones que puede utilizar durante su experiencia en ciberseguridad.

| Operations      | Description                                                                                                                        | Examples                                                                                                                                                                         |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| From Morse Code | Traduce el código Morse a caracteres alfanuméricos (en mayúsculas).                                                                | `- .... .-. . .- - ...` becomes `THREATS` when used with default parameters                                                                                                      |
| URL Encode      | Codifica los caracteres problemáticos en codificación porcentual, un formato compatible con URI/URL.                               | `https://tryhackme.com/r/room/cyberchefbasics` becomes `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics` when used with the parameter “Encode all special chars”      |
| To Base64       | Esta operación codifica los datos sin procesar en una cadena ASCII Base64.                                                         | `This is fun!` becomes `VGhpcyBpcyBmdW4h`                                                                                                                                        |
| To Hex          | Convierte la cadena de entrada a bytes hexadecimales separados por el delimitador especificado.                                    | `This Hex conversion is awesome!` becomes `54 68 69 73 20 48 65 78 20 63 6f 6e 76 65 72 73 69 6f 6e 20 69 73 20 61 77 65 73 6f 6d 65 21`                                         |
| To Decimal      | Convierte los datos de entrada en una matriz de enteros ordinales.                                                                 | `This Decimal conversion is awesome!` becomes `84 104 105 115 32 68 101 99 105 109 97 108 32 99 111 110 118 101 114 115 105 111 110 32 105 115 32 97 119 101 115 111 109 101 33` |
| ROT13           | Un cifrado de sustitución César simple que rota los caracteres alfabéticos en la cantidad especificada (valor predeterminado: 13). | `Digital Forensics and Incident Response` becomes `Qvtvgny Sberafvpf naq Vapvqrag Erfcbafr`                                                                                      |

Como alternativa, puede comprobar directamente cómo funcionan las operaciones pasando el cursor sobre la operación específica. Esto debería ofrecerle un ejemplo o una descripción y un enlace a Wikipedia.

![[Pasted image 20250903150849.png]]

**Área de Recetas**

Esta área se considera el corazón de la herramienta. En ella, puede seleccionar, organizar y ajustar fácilmente las operaciones según sus necesidades. Aquí es donde toma el control, definiendo los argumentos y las opciones de cada operación con precisión y precisión. El área de recetas es un espacio designado para seleccionar y organizar operaciones específicas y luego definir sus respectivos argumentos y opciones para personalizar aún más su comportamiento. En el área de recetas, puede arrastrar las operaciones que desee utilizar y especificar argumentos y opciones.

Las funciones incluyen las siguientes:

- **Guardar receta:** Esta función permite guardar las operaciones seleccionadas.
- **Cargar receta:** Permite cargar recetas previamente guardadas.
- **Borrar receta:** Esta función permite borrar la receta seleccionada durante el uso.

Estas funciones se encuentran en los iconos resaltados a continuación:

![[Pasted image 20250903150910.png]]

La parte inferior de la imagen superior es el botón ¡BAKE!. Este procesa los datos con la receta dada.

Además, puede marcar la casilla de Horneado automático. Esta función permite cocinar automáticamente con la receta seleccionada sin tener que hacer clic manualmente en ¡BAKE! cada vez.

**Área de entrada**

El área de entrada ofrece un espacio intuitivo donde puede introducir fácilmente texto o archivos pegándolos, escribiéndolos o arrastrándolos para realizar operaciones.

![[Pasted image 20250903150926.png]]

Además, cuenta con las siguientes funciones:

- **Añadir una nueva pestaña de entrada:** Aquí se crea una pestaña adicional para que el usuario utilice valores diferentes a los de la pestaña anterior.

![[Pasted image 20250903150943.png]]

- **Abrir carpeta como entrada:** esta función permite a los usuarios cargar una carpeta completa como valor de entrada.

![[Pasted image 20250903150956.png]]

- **Abrir archivo como entrada:** esta función permite al usuario cargar un archivo como su valor de entrada.

![[Pasted image 20250903151014.png]]

- **Borrar entrada y salida:** Esta función permite borrar cualquier valor de entrada insertado y el valor de salida correspondiente.
- **Restablecer el diseño del panel:** Esta función restaura la interfaz de la herramienta a sus tamaños de ventana predeterminados.

**Área de Salida**

El área de salida es un espacio visual que muestra los resultados del procesamiento de datos. Presenta de forma clara los resultados de cualquier manipulación o transformación aplicada a los datos de entrada, lo que permite una visualización clara e intuitiva de la información procesada.

![[Pasted image 20250903151028.png]]

Las características incluyen:

- **Guardar el resultado en archivo:** Esta función permite guardar el resultado en un archivo .dat.
- **Copiar el resultado sin procesar al portapapeles:** Esta función permite copiar el resultado sin procesar directamente al portapapeles, lo que permite copiar rápidamente los resultados para usarlos en otras aplicaciones o documentos.
- **Reemplazar la entrada por la salida:** Esta función permite sobrescribir rápidamente los datos de entrada según los resultados de las operaciones.
- **Maximizar el panel de salida:** Esta función restaura el tamaño de ventana predeterminado de la interfaz de la herramienta.

Answer the questions below

In which area can you find "From Base64"?
respuesta operations

Which area is considered the heart of the tool?
respuesta Recipe

---

**==Antes de nada==**

¡Manténganse alerta!

Antes de empezar, ¡veamos brevemente el proceso de pensamiento al usar CyberChef! Este proceso consta de cuatro pasos diferentes:

![[Pasted image 20250903151050.png]]

Analicemos cada paso con más detalle.

Establecer un objetivo claro es esencial. Este paso implica definir metas específicas y alcanzables. Ayuda a responder a la pregunta "**¿Qué quiero lograr**?". Los objetivos son vitales para proporcionar dirección, propósito y enfoque a tus metas. Un ejemplo sería: "Durante una investigación de seguridad, encontré una cadena de texto sin sentido; quiero saber qué mensaje oculto contiene, si es que lo tiene".

A continuación, introduce tus datos en el área de entrada. En este paso, utilizas tus datos. Aquí es donde pegas o cargas la cadena de texto sin sentido que encontraste.

El tercer paso es seleccionar las **operaciones** que quieres usar. Esto puede ser complicado si aún no estás familiarizado con lo que estás tratando. Siguiendo nuestro ejemplo, todavía estamos determinando qué usar para comprender esta cadena de texto sin sentido. Durante nuestra investigación, encontramos información relevante que indicaba que esta cadena incoherente podría estar usando algún método relacionado con el cifrado. Por lo tanto, decidimos usar cualquier operación de la categoría **Cifrado/Codificación**, incluyendo, entre otras, **ROT13**, **Base64**, **Base85** o **ROT47**. Cabe destacar que podemos usar muchas operaciones en esta categoría.

Por último, comprobamos el resultado para comprobar si es el esperado. Esto nos lleva a preguntarnos: "**¿Hemos logrado nuestro objetivo?**". En nuestro ejemplo, esto significaría: ¿Logramos decodificar la cadena incoherente que encontramos? Si es así, ¡listo! Si no, podríamos tener que repetir los pasos que hemos realizado.

Para mayor claridad visual, consulte la siguiente figura:

![[Pasted image 20250903151105.png]]

Answer the questions below

At which step would you determine, "What do I want to accomplish?
respuesta 1

---

**==Práctica, práctica, práctica==**

Queremos que estés lo más preparado posible. Por lo tanto, exploraremos algunas de las categorías de operaciones más comunes en esta tarea. Reconocer qué categoría utilizar puede mejorar tu capacidad para usar la herramienta de forma más eficiente y eficaz.

**Extractores**

Las operaciones específicas mencionadas en la tabla a continuación se incluyen en la categoría de Extractores.

| Specific                | Description                                                                                                                                                                 |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Extract IP addresses    | Extrae todas las direcciones IPv4 e IPv6.                                                                                                                                   |
| Extract URLs            | Extrae los Localizadores Uniformes de Recursos (URL) de la entrada. Se requiere el protocolo (HTTP, FTP, etc.); de lo contrario, se producirán demasiados falsos positivos. |
| Extract email addresses | Extrae todas las direcciones de correo electrónico de la entrada.                                                                                                           |

La función "Extraer direcciones IP" extrae cualquier dirección IPv4/6 válida de cualquier entrada. Recomendamos consultar nuestra sección "Conceptos de Redes" para un breve resumen de redes.

La función "Extraer direcciones de correo electrónico" extrae cualquier cadena o carácter con el formato "anything@domain[.]com". Algunos ejemplos de dominios son hotmail.com, google.com, tryhackme.com y yahoo.com.

La función "Extraer URL" extrae el Localizador Uniforme de Recursos (URL). Una URL es la dirección utilizada para acceder a recursos en internet. Puede consultar la sección "Fundamentos de Aplicaciones Web" si desea profundizar en el tema de las URL y las aplicaciones web.

**Fecha y Hora**

Las operaciones específicas de la tabla a continuación se clasifican en la categoría "Fecha/Hora".

| Specific            | Description                                                                                   |
| ------------------- | --------------------------------------------------------------------------------------------- |
| From UNIX Timestamp | Convierte una marca de tiempo UNIX en una cadena de fecha y hora.                             |
| To UNIX Timestamp   | Analiza una cadena de fecha y hora en UTC y devuelve la marca de tiempo UNIX correspondiente. |
Una marca de tiempo UNIX es un valor de 32 bits que representa el número de segundos transcurridos desde el 1 de enero de 1970 UTC (la época UNIX). Para convertir "Fri Sep 6 20:30:22 +04 2024" a una marca de tiempo UNIX, utilice la operación "To UNIX Timestamp", donde el resultado sería 1725654622. Si desea convertirlo a un formato más legible, puede utilizar "From UNIX Timestamp".

**Formato de datos**

Las operaciones específicas de la tabla a continuación se incluyen en la categoría de formato de datos.

| Operations  | Description                                                                                                                                                                                                                                                                           | Examples                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| From Base64 | Esta operación decodifica datos de una cadena ASCII Base64 a su formato original.                                                                                                                                                                                                     | `V2VsY29tZSB0byB0cnloYWNrbWUh` becomes `Welcome to tryhackme!`                                |
| URL Decode  | Convierte caracteres URI/URL codificados porcentualmente a sus valores originales.                                                                                                                                                                                                    | `https%3A%2F%2Fgchq%2Egithub%2Eio%2FCyberChef%2F` becomes `https://gchq.github.io/CyberChef/` |
| From Base85 | Notación para codificar datos de bytes arbitrarios. Suele ser más eficiente que Base64. Esta operación decodifica datos de una cadena ASCII (con un alfabeto de su elección, incluidos los preajustes).                                                                               | `BOu!rD]j7BEbo7` becomes `hello world`                                                        |
| From Base58 | Es una notación para codificar datos de bytes arbitrarios. Se diferencia de Base64 al eliminar eficazmente caracteres mal leídos (p. ej., l, 1, 0 y 0) para mejorar la legibilidad.                                                                                                   | `AXLU7qR` becomes`Thm58`                                                                      |
| To Base62   | Es una notación para codificar datos de bytes arbitrarios utilizando un conjunto restringido de símbolos que las personas pueden usar y procesar fácilmente en las computadoras. La alta base numérica da como resultado cadenas más cortas que con el sistema decimal o hexadecimal. | `Thm62` becomes`6NiRkOY`                                                                      |

Operaciones como Base(64, 85, 58, 62) se conocen como codificaciones base. La codificación base toma datos binarios (cadenas de 0 y 1) y los transforma en una representación basada en texto mediante un conjunto específico de caracteres ASCII (Código Estándar Americano para el Intercambio de Información).

Aunque disponemos de una sección dedicada a los fundamentos del hash, veamos brevemente la operación más utilizada: Base64.

Nuestro ejemplo sería codificar las letras "THM". Aquí tenemos una breve tabla ASCII que podemos usar como referencia. Si desea ver la tabla ASCII completa, consulte esta [página](https://en.wikipedia.org/wiki/ASCII).

| Decimal | Binary   | Symbol | -   | Decimal | Binary   | Symbol |
| ------- | -------- | ------ | --- | ------- | -------- | ------ |
| 65      | 01000001 | A      |     | 78      | 01001110 | N      |
| 66      | 01000010 | B      |     | 79      | 01001111 | O      |
| 67      | 01000011 | C      |     | 80      | 01010000 | P      |
| 68      | 01000100 | D      |     | 81      | 01010001 | Q      |
| 69      | 01000101 | E      |     | 82      | 01010010 | R      |
| 70      | 01000110 | F      |     | 83      | 01010011 | S      |
| 71      | 01000111 | G      |     | 84      | 01010100 | T      |
| 72      | 01001000 | H      |     | 85      | 01010101 | U      |
| 73      | 01001001 | I      |     | 86      | 01010110 | V      |
| 74      | 01001010 | J      |     | 87      | 01010111 | W      |
| 75      | 01001011 | K      |     | 88      | 01011000 | X      |
| 76      | 01001100 | L      |     | 89      | 01011001 | Y      |
| 77      | 01001101 | M      |     | 90      | 01011010 | Z      |
**Paso 1: Convertir a binario y fusionar (manualmente)**

Según la tabla anterior, T = 01010100, H = 01001000, M = 01001101. A continuación, concatene estos binarios y asegúrese de que tengan 24 caracteres. Debería obtener 010101000100100001001101

**Paso 2: Dividir y convertir a decimal (manualmente)**

Separe 010101000100100001001101 en 6 caracteres cada uno. Debería obtener 010101 000100 100001 001101. Estos son caracteres de 6 bits; deberíamos tener cuatro instancias de esto ahora. Necesitamos convertir cada instancia a decimal. ¡Convirtamos!

|Binary|Decimal (Base10)|
|---|---|
|010101|21|
|000100|4|
|100001|33|
|001101|13|

**Paso 3: Convertir a Base64 (Manualmente)**

Ahora que tenemos los números del paso anterior, que son 21, 4, 33 y 13, busquemos los caracteres equivalentes en la tabla a continuación. Esta tabla representa una tabla de índices en base64.

| Index | Character | -   | Index | Character | -   | Index | Character |
| ----- | --------- | --- | ----- | --------- | --- | ----- | --------- |
| 0     | **A**     |     | 26    | **a**     |     | 52    | **0**     |
| 1     | **B**     |     | 27    | **b**     |     | 53    | **1**     |
| 2     | **C**     |     | 28    | **c**     |     | 54    | **2**     |
| 3     | **D**     |     | 29    | **d**     |     | 55    | **3**     |
| 4     | **E**     |     | 30    | **e**     |     | 56    | **4**     |
| 5     | **F**     |     | 31    | **f**     |     | 57    | **5**     |
| 6     | **G**     |     | 32    | **g**     |     | 58    | **6**     |
| 7     | **H**     |     | 33    | **h**     |     | 59    | **7**     |
| 8     | **I**     |     | 34    | **i**     |     | 60    | **8**     |
| 9     | **J**     |     | 35    | **j**     |     | 61    | **9**     |
| 10    | **K**     |     | 36    | **k**     |     | 62    | **+**     |
| 11    | **L**     |     | 37    | **l**     |     | 63    | **/**     |
| 12    | **M**     |     | 38    | **m**     |     |       |           |
| 13    | **N**     |     | 39    | **n**     |     |       |           |
| 14    | **O**     |     | 40    | **o**     |     |       |           |
| 15    | **P**     |     | 41    | **p**     |     |       |           |
| 16    | **Q**     |     | 42    | **q**     |     |       |           |
| 17    | **R**     |     | 43    | **r**     |     |       |           |
| 18    | **S**     |     | 44    | **s**     |     |       |           |
| 19    | **T**     |     | 45    | **t**     |     |       |           |
| 20    | **U**     |     | 46    | **u**     |     |       |           |
| 21    | **V**     |     | 47    | **v**     |     |       |           |
| 22    | **W**     |     | 48    | **w**     |     |       |           |
| 23    | **X**     |     | 49    | **x**     |     |       |           |
| 24    | **Y**     |     | 50    | **y**     |     |       |           |
| 25    | **Z**     |     | 51    | **z**     |     |       |           |

Al consultar la tabla, ya deberíamos haber encontrado el carácter correspondiente.

|Index|Characters|
|---|---|
|21|V|
|4|E|
|33|h|
|13|N|

Combina estos caracteres y obtendrás el equivalente a "THM" en formato base64. La respuesta sería VEhN.

¡Increíble! Acabas de convertir manualmente un conjunto de caracteres a base64.

Ahora, analicemos la decodificación de URL. Esta función convierte los caracteres codificados porcentualmente a sus valores originales. Para consultar estos valores, consulta la página [aquí](https://en.wikipedia.org/wiki/Percent-encoding). Ten en cuenta que el conjunto de caracteres predeterminado en HTML5 es UTF-8. Consulta la tabla a continuación para obtener una visión general de lo que normalmente vemos en una URL.

|Characters|From UTF-8|
|---|---|
|:|%3A|
|/|%2F|
|.|%2E|
|=|%3D|
|#|%23|

**Ejercicio práctico**

Haga clic en el botón "Descargar archivos de la tarea" en la parte superior de esta tarea para descargar el archivo que usaremos para responder las preguntas a continuación.

Una vez descargado, puede abrir el archivo, copiar y pegar el contenido en el campo de entrada o usar la función "Abrir archivo como entrada" para subirlo.

Nota: Utilice las operaciones específicas de la categoría "Extractores" para las dos primeras preguntas. Es mejor intentar responder las preguntas primero sin usar las pistas.

Answer the questions below

What is the hidden email address?
respuesta  hidden@hotmail.com
cargamos el archivo en la pagina 

![[Pasted image 20250903173956.png]]

filtramos con extractors para encontrar la primera flag
![[Pasted image 20250903174107.png]]

What is the hidden IP address that ends in .232?
respuesta 102.20.11.232

filtramos con direcciones ip
![[Pasted image 20250903174157.png]]

Which domain address starts with the letter "T"?
respuesta TryHackMe.com 

filtramos por dominios 

![[Pasted image 20250903174243.png]]


What is the binary value of the decimal number 78?
respuesta  01001110

![[Pasted image 20250903174312.png]]

What is the URL encoded value of `https://tryhackme.com/r/careers`?
respuesta  https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Fcareers

utilizamos la opcion de URL Encoder 

![[Pasted image 20250903174756.png]]


---

==**Tu primer cocinero oficial**==

Esta tarea nos permite aplicar lo aprendido en las tareas anteriores. Utilizaremos las áreas de CyberChef y sus funciones para responder a las preguntas.

¡Ahora es el momento de brillar de verdad! ¡Vas a por tu primer cocinero!

![[Pasted image 20250903151144.png]]

¿Listos? ¡A por todas!

Nota: Es mejor intentar responder las preguntas primero sin usar las pistas.

Answer the questions below

Using the file you downloaded in Task 5, which IP starts and ends with "10"?
respuesta 10.10.2.10

filtramos por extractors ip address
![[Pasted image 20250903175050.png]]

What is the base64 encoded value of the string "**Nice Room!**"?
respuesta TmljZSBSb29tIQ==

![[Pasted image 20250903175251.png]]

What is the URL decoded value for `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics`?
respuesta https://tryhackme.com/r/room/cyberchefbasics

![[Pasted image 20250903175340.png]]

What is the datetime string for the Unix timestamp `1725151258`?
respuesta  Sun 1 September 2024 00:40:58 UTC

![[Pasted image 20250903175500.png]]

What is the Base85 decoded string of the value `<+oue+DGm>Ap%u7`?
respuesta This is fun!

![[Pasted image 20250903175550.png]]

---

**==Conclusión==**

En esta sala, analizamos cómo CyberChef es una herramienta potente para gestionar diversas transformaciones de datos y tareas de decodificación. Ya sea que necesite trabajar con Base64, binario o URL, esta herramienta digital ofrece una interfaz visual que facilita la manipulación de datos de forma intuitiva y sencilla. Con una biblioteca de recetas diversa, puede abordar con confianza tareas que van desde la extracción de direcciones de correo electrónico, direcciones IP y dominios. Pudimos navegar por su interfaz y mantener una conversación detallada sobre las diferentes áreas, funciones y parámetros. Sin embargo, tenga en cuenta que, para un procesamiento a gran escala, es fundamental contar con la compatibilidad de otras herramientas.