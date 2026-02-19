
Introduction

![[Pasted image 20251219165521.png]]

McSkidy está encarcelado en Quantum Warren del rey Malhare. Sir BreachBlocker III fue encargado de asegurar la fortaleza e implementó varios controles de acceso para evitar cualquier escape. Sus defensas son dignas de su nombre.

Sin embargo, McSkidy logró enviar pistas vitales a su equipo utilizando imágenes inofensivas de conejitos. Un mensaje reveló que era necesario desactivar cinco cerraduras para asegurar una ruta de escape. Las cerraduras se pueden romper examinando su lógica y aprovechando el chat integrado del sistema para los guardias. Se les puede eludir revelando detalles vitales o incluso contraseñas. Sin embargo, necesitarás hablar su idioma.

Objetivos de aprendizaje
Introducción a la codificación/decodificación
Aprende a utilizar CyberChef
Identificar información útil en aplicaciones web a través de encabezados HTTP.

**Answer the questions below**

Let us siege the fortress!

No answer needed


---
# ==Important Concepts==

## Codificación y decodificación

La codificación es un método para transformar datos para garantizar la compatibilidad entre diferentes sistemas. Se diferencia del cifrado en su propósito y proceso.

![[Pasted image 20251219170024.png]]

La decodificación es el proceso de convertir datos codificados a su forma original, legible y utilizable.

## Descripción general de CyberChef

[CyberChef](https://cyberchef.io/) también se conoce como la navaja cibernética suiza. ¿Listo para cocinar algunas recetas?

|Area|Description|
|---|---|
|Operations|Repository of diverse CyberChef capabilities|
|Recipe|Fine-tune and chain the operations area|
|Input|Here you provide the input for your recipe|
|Output|Here is the output of your recipe|

## Ejemplo sencillo

Prueba tu primera receta:

- Abra la versión CyberChef en línea en su navegador habitual o use la versión CyberChef sin conexión disponible en la sección de marcadores de AttackBox. Arrastre y suelte la operación To Base64 desde el área Operaciones en el lado izquierdo al área Receta en el centro y agregue IamRoot en el área Entrada.
- Agregue otra operación, From Base64, para mostrar la entrada inicial nuevamente, mostrando las operaciones en cadena.

Nota: Puede habilitar/deshabilitar una operación en la receta alternando el botón central a la derecha de la operación.

![[Pasted image 20251219170745.png]]

¡Felicidades! Diste los primeros pasos para convertirte en un maestro chef.

## Inspeccionar páginas web

Además del contenido renderizado de una página web, su navegador normalmente recibe y puede mostrar información adicional.

Para este desafío, tendrá la oportunidad de analizar más profundamente esa información y darle un buen uso.

Para ello, dependiendo de su navegador, puede acceder a la funcionalidad como se muestra a continuación:

|Browser|Menu path|
|---|---|
|Chrome|`More tools` > `Developer tools`|
|Firefox|`Menu` (☰) > `More tools` > `Web Developer Tools`|
|Microsoft Edge|`Settings and more (...)` > `More tools` > `Developer tools`|
|Opera|`Developer` > `Developer tools`|
|Safari|`Develop` > `Show Web Inspector` (Requires enabling the "Develop" menu in `Preferences` > `Advanced`)|

Nota: Para una mejor experiencia, puedes reubicar la consola en el lado derecho del navegador. Busque los tres puntos en el lado derecho de la consola.

![[Pasted image 20251219171700.png]]

  
Answer the questions below

Locked and loaded.

No answer needed


---
# ==First Lock - Outer Gate==

## Información clave

Si aún no lo ha hecho, inicie la máquina de destino, espere unos minutos para que se inicie y luego, desde AttackBox, podrá acceder a la aplicación web en http://MACHINE_IP:8080.

McSkidy reveló algunas pistas vitales en su mensaje. Tendrás que aprovechar cualquier información útil para romper las cerraduras.

A continuación se detallan los puntos clave a tener en cuenta:

**El chat está codificado en Base64**. Intente decodificar esto en CyberChef. Esto se aprovechará para extraer información útil de los guardias. Tenga en cuenta que a partir del Bloqueo 3 en adelante, los guardias tardarán más en responder.

![[Pasted image 20251219171820.png]]

**Nombre del guardia**. Esta lógica persistirá a lo largo de los niveles. Asegúrate de anotar el nombre del guardia para cada nivel.

![[Pasted image 20251219171844.png]]

**Encabezados**. Nuevamente, inspeccionando la página pero esta vez cambiando a la pestaña "Red". Asegúrese de actualizar la página una vez después de cambiar a esta pestaña y seleccione la primera respuesta.

![[Pasted image 20251219171943.png]]

**Lógica de inicio de sesión**. Inspeccionará la página y cambiará a la pestaña "Depurador". Haga coincidir la cerradura con la lógica respectiva. También puedes encontrar comentarios útiles que explican lo que necesitas para cocinar en CyberChef.

![[Pasted image 20251219172006.png]]

## Primera cerradura: puerta exterior

![[Pasted image 20251219174450.png]]

Ok, es hora de asediar la fortaleza. ¿Listo? 

1. Primero, identifique el nombre del guardia y codifíquelo en Base64. Utilizará esto como entrada de nombre de usuario. 

2. A continuación, utilizando la información de los encabezados de la página, identifique la pregunta mágica y codifíquela también en Base64.

![[Pasted image 20251219172045.png]]

3. Utilice la pregunta mágica de codificación en el chat. El guardia responderá con la contraseña de nivel codificada. 

4. Ahora, cambie a la pestaña "Depurador" e identifique la lógica de inicio de sesión. En este caso, la contraseña está codificada en Base 64.

![[Pasted image 20251219172113.png]]

5. Al decodificar la respuesta del guardia, tendrá la contraseña en texto plano. 

6. Utilice el nombre de usuario codificado y la contraseña en texto plano para iniciar sesión.

¡Excelente trabajo! Un candado está caído y sólo quedan cuatro por romper.

**Answer the questions below**

What is the password for the first lock?

Respuesta: Iamsofluffy


![[Pasted image 20251219174524.png]]
![[Pasted image 20251219174846.png]]
![[Pasted image 20251219182551.png]]
![[Pasted image 20251219175219.png]]
![[Pasted image 20251219175210.png]]
![[Pasted image 20251219175314.png]]
![[Pasted image 20251219175333.png]]
![[Pasted image 20251219182829.png]]
![[Pasted image 20251219182846.png]]
![[Pasted image 20251219183002.png]]



---
# ==Second Lock - Outer Wall==

![[Pasted image 20251219183056.png]]
## Segunda cerradura: pared exterior

Excelente trabajo rompiendo ese primer nivel.

Este nivel aumenta un poco la dificultad, pero no te preocupes, lo resolverás. ¡Vamos! 

1. Nuevamente, identifique el nombre del guardia y guarde la salida codificada para más adelante. 

2. Luego, extraiga y codifique la pregunta mágica y recupere la contraseña codificada del guardia.

![[Pasted image 20251219172259.png]]

3. Volviendo a observar la lógica de inicio de sesión, verá que esta vez la codificación se aplica dos veces. Eso significa que tienes que decodificar desde Base64 dos veces. 

4. Continúe e inicie sesión con la nueva contraseña y el nombre de usuario guardado.

![[Pasted image 20251219172323.png]]

Estás cada vez más cerca de conseguir una ruta de escape; sólo quedan tres cerraduras. Sigan con el buen trabajo.

**Answer the questions below**

What is the password for the second lock?

Check

![[Pasted image 20251219183124.png]]
![[Pasted image 20251219183157.png]]
![[Pasted image 20251219183632.png]]
![[Pasted image 20251219183257.png]]
![[Pasted image 20251219183317.png]]
![[Pasted image 20251219183336.png]]
![[Pasted image 20251219183434.png]]
![[Pasted image 20251219183419.png]]
![[Pasted image 20251219183453.png]]
![[Pasted image 20251219183509.png]]
![[Pasted image 20251219183655.png]]
![[Pasted image 20251219183704.png]]


---
# ==Third Lock - Guard House==

![[Pasted image 20251219183752.png]]
## Tercera esclusa: caseta de vigilancia

Hasta ahora, todo bien. Como vio en el nivel anterior, la lógica de inicio de sesión comienza a utilizar operaciones encadenadas.

Esta será la tendencia para este y los siguientes niveles.

1. Como siempre, recopile toda la información necesaria (nombre de usuario codificado, contraseña codificada del guardia, clave XOR).

![[Pasted image 20251219172419.png]]

Nota: A partir de este bloqueo, no hay una pregunta mágica, pero a veces puedes pedirle amablemente al guardia que te dé la contraseña. Aún será necesario decodificarlo según la lógica de inicio de sesión. Tenga en cuenta que el guardia a veces puede quedarse dormido o tardar mucho en responder (~2-3 minutos), por lo que mantener el mensaje breve ayudará a obtener la respuesta. Incluso un simple "Contraseña, por favor". recorrerá un largo camino. 

2. Si observa la lógica de inicio de sesión, hay un ligero giro. La contraseña primero se aplica XOR con una clave y luego se codifica en Base64.

## Tiempo de teoría

XOR es una operación popular que, además de los datos de entrada, también utiliza una clave. El proceso implica un OR exclusivo bit a bit entre los datos y la clave.

![[Pasted image 20251219172458.png]]

Quizás te preguntes: "Está bien, pero ¿cómo puedo revertir esto?". Bueno, saltándonos la larga explicación matemática, XOR tiene una propiedad mágica: cuando vuelves a realizar XOR el resultado con la clave, el nuevo resultado serán los datos iniciales. Adelante, prueba esto en CyberChef. Coloque dos operaciones XOR una tras otra, use la misma clave para ambas y el resultado debería ser idéntico.

![[Pasted image 20251219172529.png]]

3. Con este nuevo conocimiento, cree la receta necesaria para encontrar la contraseña en texto plano.

![[Pasted image 20251219172553.png]]

![[Pasted image 20251219172604.png]]

4. Utilice las credenciales y desbloquee el siguiente nivel.

**Answer the questions below**

What is the password for the third lock?

Respuesta: BugsBunny

![[Pasted image 20251219190650.png]]
![[Pasted image 20251219184645.png]]
![[Pasted image 20251219190717.png]]
![[Pasted image 20251219190755.png]]
![[Pasted image 20251219191323.png]]
![[Pasted image 20251219191334.png]]
![[Pasted image 20251219191358.png]]
![[Pasted image 20251219191719.png]]
![[Pasted image 20251219191809.png]]
![[Pasted image 20251219191821.png]]


---
# ==Fourth Lock - Inner Castle==

## Cuarta cerradura - Castillo interior

Ya casi llegamos. En este nivel, Sir BreachBlocker III te lanza una bola curva. Veamos cómo abordar esto. 

1. Pero primero, siga adelante y observe la lógica de inicio de sesión como antes. No necesitaremos información de encabezado para este.

![[Pasted image 20251219172719.png]]

2. Después de pedirle la contraseña al guardia y mirar su respuesta, parece un poco extraño. Al mismo tiempo, la lógica de inicio de sesión muestra el uso de un hash MD5.

![[Pasted image 20251219172743.png]]

## Tiempo de teoría

MD5, o algoritmo de resumen de mensajes 5, es un algoritmo criptográfico que produce un valor hash de tamaño fijo. Si bien se supone que esta es una función unidireccional, lo que significa que no se puede revertirla, se pueden aprovechar los hashes precalculados para identificar la entrada. 

3. Al juntar los dos, la contraseña en texto plano se pasa a través de MD5 y usted tiene el hash. Esto parece un trabajo para CrackStation. 

4. Continúe, abra el sitio y pegue el hash para recuperar la contraseña.

![[Pasted image 20251219172810.png]]

5. Utilice las credenciales y avance al nivel final.

Fantástico. Una cerradura más y se asegurará de que McSkidy tenga un paso seguro y escape.

**Answer the questions below**

What is the password for the fourth lock?

Respuesta: 

![[Pasted image 20251219191923.png]]
![[Pasted image 20251219192113.png]]
![[Pasted image 20251219192105.png]]
![[Pasted image 20251219192157.png]]
![[Pasted image 20251219192225.png]]
![[Pasted image 20251219192638.png]]
![[Pasted image 20251219192652.png]]
![[Pasted image 20251219192720.png]]
![[Pasted image 20251219192842.png]]
![[Pasted image 20251219192905.png]]
![[Pasted image 20251219192913.png]]


---
# Fifth Lock - Prison Tower

![[Pasted image 20251219193017.png]]

## Quinta cerradura - Torre de la prisión

¿Listo para el último obstáculo?

A medida que las defensas se debilitan, recibes otro mensaje oculto de McSkidy:

"Puedo ver que estás listo para romper el último candado. Tenga en cuenta que Sir BreachBlocker III implementó diferentes mecanismos para el último candado, que cambian ocasionalmente. Asegúrese de utilizar el enfoque correcto al decodificar la contraseña".

Suena complicado, pero no te desesperes. Encontrarás una manera. 

1. Empecemos. Extraiga la información como antes, anotando el nombre del guardia codificado.

![[Pasted image 20251219172904.png]]

2. Además, anote el ID de la receta en el encabezado y haga coincidir la lógica de inicio de sesión correspondiente. A continuación se muestra una hoja de referencia rápida para decodificar cada receta.

|Recipe ID|Reverse Logic|
|---|---|
|1|From Base64 ⇒ Reverse ⇒ ROT13|
|2|From Base64 ⇒ From Hex ⇒ Reverse|
|3|ROT13 ⇒ From Base64 ⇒ XOR(extracted key)|
|4|ROT13 ⇒ From Base64 ⇒ ROT47|

3. Cree la receta inversa con CyberChef y extraiga la contraseña final.

Finalmente, se rompió el último candado y usted proporcionó un camino seguro para que McSkidy escapara.

**Answer the questions below**

What is the password for the fifth lock?

Respuesta: 51rBr34chBl0ck3r

What is the retrieved flag?

Respuesta: THM{M3D13V4L_D3C0D3R_4D3P7}

![[Pasted image 20251219192946.png]]
![[Pasted image 20251219193247.png]]
![[Pasted image 20251219193210.png]]
![[Pasted image 20251219193230.png]]

![[Pasted image 20251219193330.png]]
![[Pasted image 20251219193355.png]]
![[Pasted image 20251219193443.png]]
![[Pasted image 20251219193518.png]]
![[Pasted image 20251219193954.png]]
![[Pasted image 20251219194037.png]]
![[Pasted image 20251219194100.png]]
![[Pasted image 20251219194114.png]]
![[Pasted image 20251219194122.png]]



---
# Epilogue

![[Pasted image 20251219173001.png]]

Cuando McSkidy pasó por el Castillo Interior, escuchó una voz atronadora: “¿Por qué la Navidad debería ser toda la diversión?”

McSkidy logró regresar a Wareville justo a tiempo cuando TBFC estaba a punto de sufrir otro desastre.

Answer the questions below

If you found decoding secrets interesting, you can also check out the [Introduction to Cryptography](https://tryhackme.com/room/cryptographyintro), which dives into the world of cryptography.

No answer needed


> Looking for the key to **Side Quest 3**? Hopper has left us this [cyberchef link](https://gchq.github.io/CyberChef/#recipe=To_Base64\('A-Za-z0-9%2B/%3D'\)Label\('encoder1'\)ROT13\(true,true,false,7\)Split\('H0','H0%5C%5Cn'\)Jump\('encoder1',8\)Fork\('%5C%5Cn','%5C%5Cn',false\)Zlib_Deflate\('Dynamic%20Huffman%20Coding'\)XOR\(%7B'option':'UTF8','string':'h0pp3r'%7D,'Standard',false\)To_Base32\('A-Z2-7%3D'\)Merge\(true\)Generate_Image\('Greyscale',1,512\)&input=SG9wcGVyIG1hbmFnZWQgdG8gdXNlIEN5YmVyQ2hlZiB0byBzY3JhbWJsZSB0aGUgZWFzdGVyIGVnZyBrZXkgaW1hZ2UuIEhlIHVzZWQgdGhpcyB2ZXJ5IHJlY2lwZSB0byBkbyBpdC4gVGhlIHNjcmFtYmxlZCB2ZXJzaW9uIG9mIHRoZSBlZ2cgY2FuIGJlIGRvd25sb2FkZWQgZnJvbTogCgpodHRwczovL3RyeWhhY2ttZS1pbWFnZXMuczMuYW1hem9uYXdzLmNvbS91c2VyLXVwbG9hZHMvNWVkNTk2MWM2Mjc2ZGY1Njg4OTFjM2VhL3Jvb20tY29udGVudC81ZWQ1OTYxYzYyNzZkZjU2ODg5MWMzZWEtMTc2NTk1NTA3NTkyMC5wbmcKClJldmVyc2UgdGhlIGFsZ29yaXRobSB0byBnZXQgaXQgYmFjayE) as a lead. See if you can recover the key and access the corresponding challenge in our [Side Quest Hub](https://tryhackme.com/adventofcyber25/sidequest)!

No answer needed
