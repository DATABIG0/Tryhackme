
Introduction

![[Pasted image 20251218172025.png]]

WareVille no se siente bien desde que apareció el agujero de gusano. Todos en TBFC están en alerta máxima: los sistemas se están volviendo locos, los paneles están aumentando y las alertas de SOC se han disparado sin parar. En medio del caos, McSkidy mantiene su atención en una alerta particular que llamó su atención: un correo electrónico que se hace pasar por northpole-hr. Está lleno de emojis de zanahorias, pero lo extraño es esto: no existe un departamento de recursos humanos en el Polo Norte. El HR de TBFC está en el Polo Sur.

Profundizando más, encontró que se descargó un pequeño archivo PowerShell de ese correo electrónico. Entre el código hay cadenas aleatorias de caracteres, todo un galimatías, nada legible de un vistazo.

McSkidy sabe que los actores maliciosos a menudo ocultan códigos y datos mediante una técnica llamada ofuscación. ¿Pero qué es realmente? ¿Y cómo podemos descifrarlo?

Objetivos de aprendizaje

Aprenda sobre la ofuscación, por qué y dónde se utiliza.
Conozca la diferencia entre codificación, cifrado y ofuscación.
Aprenda sobre la ofuscación y las técnicas comunes.
Utilice CyberChef para recuperar texto sin formato de forma segura.

Alternatively, you can use the credentials below to connect to the target machine via RDP from your own THM VPN connected machine:

![[Pasted image 20251218172115.png]]

Answer the questions below

Start the target machine and continue with the next task.
No answer needed


---

# Obfuscation & Deobfuscation

## Entendiendo el galimatías

La ofuscación es la práctica de dificultar la lectura y el análisis de los datos. Los atacantes lo utilizan para evadir la detección básica y retrasar las investigaciones.

Digamos que una herramienta de seguridad bloqueará automáticamente cualquier archivo que contenga la palabra "the bandit yeti". Para evadir esto, los atacantes pueden utilizar una técnica de cifrado simple llamada "ROT1" para ocultar la cadena.

ROT1 es una técnica de cifrado que avanza cada letra 1 en el alfabeto. La letra "a" se convierte en "b"," b" se convierte en "c", y así sucesivamente. Usando este cifrado, "carrot coins go brr"  se convierten en "dbsspu dpjot hp css".

![[Pasted image 20251218172414.png]]

Esto puede complicarse aún más si se utiliza ROT13, que hace avanzar a los personajes 13 espacios.

## Ofuscación en el mundo real

Hasta ahora, lo hemos mantenido simple. En el mundo real, encontrarás una gama más amplia de técnicas.

Una técnica un poco más complicada sería utilizar XOR. Cada carácter se representa como un byte y cada byte se combina con una clave mediante la operación matemática XOR. No es necesario entrar en detalles sobre cómo funciona. Lo único que debes saber es que esta operación cambia los bytes en bytes diferentes, lo que en ocasiones hace que el texto resultante acabe con símbolos poco comunes o caracteres no legibles.

Ofuscar con XOR no es algo que se pueda hacer fácilmente de forma manual. Pero, afortunadamente, existen herramientas disponibles que pueden ayudarnos con esto. Una de esas herramientas ampliamente utilizadas se llama CyberChef.

Intentemos ofuscar una cadena usando XOR siguiendo los pasos a continuación:

1. Abra CyberChef visitando este [enlace](https://gchq.github.io/CyberChef/) en su navegador.
2. En la parte superior derecha, verá un cuadro de Entrada. Aquí es donde pegas el texto que deseas cambiar/ofuscar. En nuestro caso, utilice "carrot supremacy".
3. En el panel izquierdo, debajo de Operaciones, busque "XOR" y arrástrelo hacia el centro, debajo de Receta. Esto le indica a CyberChef que aplique esa técnica a su texto de entrada.
4. Cada operación tiene configuraciones que puede ajustar. En nuestro caso, configuramos la clave en "a". Asegúrese de que el menú desplegable junto a Clave esté configurado en HEX.
5. El resultado ofuscado debería aparecer automáticamente en la sección Salida. Si no es así, haga clic en ¡HORNEAR! en la parte inferior de la pantalla.

Como puedes ver arriba, carrot supremacy en hilo ahora se convierte en ``ikxxe~*y zxogkis``.

## Detección de patrones

Lo bueno de las técnicas de ofuscación conocidas es que es fácil revertirlas una vez que descubres la técnica utilizada.

Puede utilizar estas pistas visuales rápidas para adivinar la técnica de ofuscación utilizada:

- ROT1: las palabras comunes parecen “a una letra de distancia”, los espacios permanecen iguales. Bastante fácil de detectar.
- ROT13 - Busca palabras de tres letras. Los más comunes como "the" convertido en "gur". Y "and" se convierte en "naq". Los espacios siguen siendo los mismos.
- Base64: cadenas largas que contienen principalmente caracteres alfanuméricos (es decir, A-Z, a-z, 0–9), a veces con + o /, y a menudo terminan en ``=`` o ``==``.
- XOR: un poco más complicado. Parecen símbolos aleatorios pero mantienen la misma longitud que el original. Si se reutilizó un breve secreto, es posible que observe una pequeña repetición cada pocos caracteres.

Una vez que sepa qué cifrado se utilizó, puede volver a CyberChef, pero esta vez utilice una operación que produce el efecto inverso. Por ejemplo, para desofuscar Base64 se utiliza "From Base64" en lugar de `To Base64`.

![[Pasted image 20251218172758.png]]

## Patrones desconocidos

¿No estás seguro de lo que estás mirando? Está bien. Incluso si no tiene idea de qué cifrado se utilizó, es bastante fácil seguir probando diferentes operaciones sólo para ver si el texto se vuelve legible.

CyberChef también incluye una operación llamada Magic que automáticamente adivina y prueba decodificadores comunes por usted. Para usarlo, simplemente agregue la operación Magic y observe los resultados. Mostrará múltiples resultados y depende de usted comprobar cuál termina teniendo sentido. Incluso puedes marcar "Modo intensivo" para asegurarte de que pruebe más posibilidades antes de rendirte.

![[Pasted image 20251218172827.png]]

¡Por supuesto, esto no captará todo (especialmente claves XOR personalizadas o capas inusuales)! Por lo tanto, utilícelo como una pista que le ayudará a descubrirlo. Por ejemplo, una de las siguientes preguntas no se puede resolver completamente solo con la operación Magic.

## Ofuscación en capas

Para dificultar la desofuscación, los actores de amenazas a menudo combinan múltiples técnicas, casi como un enfoque en capas.

Por ejemplo, un script que los actores de amenazas quieren ocultar se puede comprimir con gzip, aplicar XOR con una tecla x y, finalmente, codificar en Base64 producirá esta cadena ofuscada: ``H4sIADKZ42gA/32PT2sqQRDE7/MpitGDgrPEJJcXyOGha1xwVaLwyLvI6rbuhP3HTHswm/3uzmggIQfrUD3VzI/u7iDXljepNkFth6KDmYsWnBF2R2OoZOyrPCUDXSKB1UWdEzjZ5hQI8c9oJrU4cn1kyPXbMgRW0X/nF8WLcTSJwvFX9Jr/jUP5i1NOgPeLfjxvtKQQL8RqlOk8jZgKfGJSmTDZZWqxfacdoxFAl0814Rl6j153EyxXkR1VJSe6JNNHAzmOXiHRgnJLPk+iWeiyR63+uIm6Hb5B92NG5YGzK5sm7FnfTSxfzl3rgoJ1tWKjy0NPnpxUHKs0xXT6VBSy7zjZ3A3UY4tmOPjTAs29t4dWQu2vpwyua7niJ7iyCeZJQaIVZ/xwdy/JAQAA``

Para revertir este tipo de ofuscación en capas, aplique las operaciones en el orden opuesto: decodificar Base64, XOR con x, luego descomprima gzip. La siguiente captura de pantalla muestra cómo encadenar estas operaciones para recuperar el contenido original.

![[Pasted image 20251218172932.png]]

## Desenvolver el huevo de Pascua

Afortunadamente, McSkidy detectó algo fraudulento en el correo electrónico que recibimos. Extrajo un script de PowerShell del PDF y lo colocó en una máquina virtual aislada para descubrir qué está haciendo. Hay cierta confusión en este guión, ¿puedes ayudarla a entender de qué se trata?

Abra SantaStealer.ps1, ubicado en el escritorio de la máquina virtual en Visual Studio, haciendo doble clic en él (tarda un momento en abrirse) y navegue hasta la sección "Comenzar aquí" del script. Siga las instrucciones en los comentarios del código y guárdelo, luego ejecute el script desde una terminal PowerShell para obtener su primer indicador. Para abrir PowerShell, haga clic en Inicio (o presione la tecla de Windows), escriba "PowerShell" y presione Entrar. En la terminal de PowerShell, ejecute los dos comandos que se muestran en los comentarios del script.

![[Pasted image 20251218172959.png]]

Hay un segundo desafío esperándote. Esta vez, debes ofuscar la clave API del actor malicioso usando XOR. Siga las instrucciones de la Parte 2 en los comentarios del código y luego ejecute el script nuevamente para obtener su última bandera.

**Answer the questions below**

What is the first flag you get after deobfuscating the C2 URL and running the script?

Respuesta: THM{C2_De0bfuscation_29838}
![[Pasted image 20251218180946.png]]
![[Pasted image 20251218181220.png]]
![[Pasted image 20251218181841.png]]
![[Pasted image 20251218181906.png]]

What is the second flag you get after obfuscating the API key and running the script again?

Respuesta: THM{API_Obfusc4tion_ftw_0283}
![[Pasted image 20251218182011.png]]
![[Pasted image 20251218182154.png]]
![[Pasted image 20251218182326.png]]
![[Pasted image 20251218182609.png]]
![[Pasted image 20251218182803.png]]


If you want to learn more about Obfuscation, check out our [Obfuscation Principles](https://tryhackme.com/room/obfuscationprinciples) room!

no necesita respuesta