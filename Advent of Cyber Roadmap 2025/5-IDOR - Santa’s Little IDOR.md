
Introduction

![[Pasted image 20251205113809.png]]

Los elfos de Wareville están en alerta máxima desde la desaparición de McSkidy. Recientemente, el equipo de soporte ha recibido numerosas llamadas de padres que no pueden activar cupones en el sitio web TryPresentMe. También mencionaron que están recibiendo numerosos correos electrónicos de phishing dirigidos con información no pública. El equipo de soporte se mantiene alerta y ha solicitado la ayuda del personal de TBFC. Al investigar este peculiar caso, descubrieron una cuenta con un nombre sospechoso, Sir Carrotbane, que tiene muchos cupones asignados. Por ahora, han eliminado la cuenta y recuperado los cupones. Pero algo está sucediendo. ¿Puedes ayudar al personal de TBFC a investigar el sitio web TryPresentMe y corregir las vulnerabilidades?

**Objetivos de aprendizaje**

- Comprender el concepto de autenticación y autorización
- Aprender a detectar posibles oportunidades para Referencias Directas a Objetos Inseguras (IDOR)
- Explotar IDOR para realizar una escalada horizontal de privilegios
- Aprender a convertir IDOR en SDOR (Referencia Directa a Objetos Segura)


---

# ==IDOR on the Shelf==

## Es peligrosamente obvio, de verdad.

¿Alguna vez has visto un enlace como este: https://awesome.website.thm/TrackPackage?packageID=1001?

Al ver un enlace como este, ¿te has preguntado qué pasaría si simplemente cambiaras el ID del paquete a 11 o 12? En su forma más simple, este podría ser un caso potencial de IDOR.

IDOR significa Referencia Directa a Objetos Insegura y es un tipo de vulnerabilidad de control de acceso. Las aplicaciones web suelen usar referencias para determinar qué datos devolver al realizar una solicitud. Sin embargo, si el servidor web no realiza comprobaciones para garantizar que se le permita ver esos datos antes de enviarlos, puede provocar una grave divulgación de información confidencial. Una buena pregunta es:

¿Por qué sucede esto tan a menudo?

Necesitamos comprender mejor las referencias y el desarrollo web para responder a esta pregunta. Veamos cómo se vería una tabla que almacenara los números de paquete de nuestro ejemplo de enlace:

|packageID|person|address|status|
|---|---|---|---|
|1001|Alice Smith|123 Main St, Springfield|Delivered|
|1002|Bob Johnson|42 Elm Ave, Shelbyville|In Transit|
|1003|Carol White|9 Oak Rd, Capital City|Out for Delivery|
|1004|Daniel Brown|77 Pine St, Ogdenville|Pending|
|1005|Eve Martinez|5 Maple Ln, North Haverbrook|Returned|
Si el usuario desea conocer el estado de su paquete y realiza una solicitud web, el método más sencillo es permitirle proporcionar su ID de paquete. Recuperamos los datos de la base de datos mediante la consulta SQL más simple:

``SELECT person, address, status FROM Packages WHERE packageID = value;``

Sin embargo, dado que packageID es un número secuencial, resulta bastante obvio adivinar los packageID de otros clientes. Además, dado que la aplicación web no verifica que la persona que realiza la solicitud sea la misma que la propietaria del paquete, surge una vulnerabilidad IDOR, que permite a los atacantes recuperar los detalles de los paquetes que pertenecen a otros usuarios. Peor aún es cuando una función como esta no requiere la autenticación del usuario, ya que no habría forma de saber quién realiza la solicitud. Para profundizar un poco más, necesitamos comprender la autenticación, la autorización y la escalada de privilegios.

### Una nota de uno de los coautores de esta tarea: 
No me convence el nombre de la vulnerabilidad IDOR. Prefiero el nombre "Omisión de autorización". Si quieres entender mi razonamiento, amplía la información aquí, ¡pero no te aburras con los detalles! 
#### Obviamente no está relacionado

El término completo, Referencia Directa a Objetos Insegura, suena sofisticado, pero no describe realmente qué está fallando. La parte "Referencia Directa a Objetos" simplemente significa que un sistema usa un ID (como /user/1) para apuntar a algo. Ese no es el problema. El verdadero problema es que el sistema no comprueba si la persona que realiza la solicitud tiene permiso para acceder a él.

Mucha gente intenta "arreglar" los IDOR ocultándolos o codificándolos. Por ejemplo, cambiando /user/1 por /user/ea21f09b2. Eso podría hacer que parezca más difícil de adivinar, pero si el servidor sigue sin comprobar los permisos, es igual de inseguro. La vulnerabilidad no radica en cómo se referencia el objeto, sino en la omisión de las comprobaciones de autorización.

Por eso prefiero llamarlo "Omisión de Autorización". Explica exactamente lo que sucede: alguien está eludiendo las reglas que deciden quién puede ver o modificar algo. Ya sea que el ID sea un número, un hash o una cadena aleatoria, el riesgo es el mismo si el servidor no verifica el acceso. Puedes leer más [aquí](https://www.mwrcybersec.com/whats-the-deal-with-idor) si quieres.

## La identidad define nuestro alcance

Para comprender la causa raíz de IDOR, es importante comprender los principios básicos de autenticación y autorización:

- **Autenticación:** El proceso mediante el cual usted verifica su identidad. Por ejemplo, al proporcionar su nombre de usuario y contraseña.
- **Autorización:** El proceso mediante el cual la aplicación web verifica sus permisos. Por ejemplo, ¿puede visitar la página de administración de una aplicación web o realizar un pago con una cuenta específica?

Puede pensar que la autenticación solo se realiza una vez al proporcionar su nombre de usuario y contraseña, ¡pero no es así! Después de proporcionar sus credenciales, recibe una cookie o token, denominado información de sesión. Cada solicitud posterior que realiza a la aplicación incluye esta información de sesión, que es verificada por la aplicación. Este proceso de verificación inicial sigue siendo autenticación y se realiza para cada solicitud. Por eso, los sitios web a menudo le redirigen a la página de inicio de sesión. Esto significa que su información de sesión ha expirado y, por lo tanto, debe volver a autenticarse con sus credenciales para recibir nueva información de sesión.

La autorización no puede realizarse antes de la autenticación. Si la aplicación no sabe quién eres, no podrá verificar los permisos de tu usuario. Es muy importante recordar esto. Si tu IDOR no requiere autenticación (iniciar sesión o proporcionar información de sesión), como en nuestro ejemplo de seguimiento de paquetes, primero tendremos que solucionar el problema de autenticación antes de poder solucionar el de autorización, que consiste en garantizar que los usuarios solo puedan obtener información sobre los paquetes que poseen.

El último aspecto teórico que abordaremos son los tipos de escalada de privilegios:

- **Escalada de privilegios vertical:** Se refiere a la escalada de privilegios donde obtienes acceso a más funciones. Por ejemplo, puedes ser un usuario normal de la aplicación, pero puedes realizar acciones que deberían estar restringidas para un administrador.
- **Escalada de privilegios horizontal:** Se refiere a la escalada de privilegios donde usas una función para la que estás autorizado, pero obtienes acceso a datos a los que no tienes acceso. Por ejemplo, solo deberías poder ver tus cuentas, no las de otros.

IDOR suele ser una forma de escalada de privilegios horizontal. Puedes usar la función de seguimiento de paquetes, pero deberías estar restringido a realizar esa acción de seguimiento solo para los paquetes que posees. Ahora que entendemos la teoría, ¡veamos cómo aprovechar IDOR en la práctica!

## Iterar dígitos, observar respuestas

Comencemos con el ejemplo más simple de IDOR. En la aplicación web, autentiquemos la aplicación usando los siguientes datos.

![[Pasted image 20251205114545.png]]

Una vez autenticado, deberías ver un panel como este:

![[Pasted image 20251205114605.png]]

Comencemos usando las **Herramientas de Desarrollo** de nuestro navegador para comprender mejor qué sucede en segundo plano. Haga clic derecho en la página y seleccione Inspeccionar. Luego, haga clic en la pestaña **Network**, como se muestra a continuación:

![[Pasted image 20251205114638.png]]

Ahora, actualicemos la página para ver qué solicitudes se están realizando. Debería verse así:

![[Pasted image 20251205114805.png]]

Analicemos con más detalle la solicitud ``view_accountinfo``. Al hacer clic en ella, verá lo siguiente:

![[Pasted image 20251205114839.png]]

En la imagen de arriba, podemos ver que el ``user_id`` con el valor 10 se utilizó para la solicitud. Si hacemos clic y expandimos la pestaña "Respuesta", podemos ver que este ``user_id`` corresponde a nuestro usuario:

![[Pasted image 20251205114913.png]]

Esto nos indica que la aplicación usa nuestro ``user_id`` como referencia para obtener detalles. Veamos qué sucede al cambiar esto. En Herramientas para desarrolladores, dirígete a la pestaña **Storage**, expande el menú desplegable **local storage** a la izquierda y haz clic en la URL:

![[Pasted image 20251205114951.png]]

Cambiemos el ``user_id`` a 11 y veamos qué sucede. Haz doble clic en el campo Value de la entrada de datos ``auth_user``, actualiza el ``user_id`` a 11 y guárdalo pulsando Intro. Ahora, actualiza la página. ¡De repente, parece que eres un usuario completamente diferente!

Esta es la forma más simple de IDOR. Simplemente cambiando el ``user_id`` a otro valor, podremos ver los datos de otros usuarios. Algunos IDOR pueden estar un poco más ocultos. ¡Que no veas un número directo no significa que no exista! Profundicemos. Para continuar con los siguientes desafíos de la tarea, cambia el id de nuevo a 10 siguiendo los mismos pasos que seguiste anteriormente. También puedes cerrar sesión en la aplicación y volver a iniciarla con el nombre de usuario y la contraseña.

## In Disguise: Referencias obvias

A veces, el IDOR puede no ser tan simple como un simple número. En ciertos casos, es posible que se haya utilizado codificación. En el perfil cargado, haz clic en el icono del ojo junto al primer hijo, como se muestra en la imagen de abajo.

![[Pasted image 20251205115107.png]]

Ahora vuelve a la pestaña Red y observa las solicitudes que se están realizando; deberías ver una solicitud como esta:

![[Pasted image 20251205115138.png]]

En pocas palabras, ``Mg==`` es simplemente la versión codificada en base64 del número 2. Se podría realizar IDOR usando esta solicitud, pero primero habría que codificar el número en base64.

## En los resúmenes, los objetos permanecen

La codificación no es lo único que se puede usar para ocultar posibles vulnerabilidades de IDOR. A veces, los valores pueden parecerse a un hash, como MD5 o SHA1. Si quieres ver cómo se vería, observa la solicitud que se realiza al hacer clic en el icono de edición junto a un elemento secundario.

![[Pasted image 20251205115220.png]]

Aunque la cadena pueda parecer aleatoria, tras una investigación más profunda, se puede observar que se trata de un tipo de hash. Si comprendemos qué valor se utilizó para generar el hash, podemos realizar un ataque IDOR simplemente replicando la función hash. Usar algo como un [hash identifier ](https://hashes.com/en/tools/hash_identifier)puede ayudar a comprender rápidamente qué algoritmo de hash se está utilizando y, a menudo, puede indicar qué datos se han codificado.

## Es determinista, obviamente reproducible.

A veces es necesario investigar a fondo para encontrar el IDOR. A veces, el IDOR no es tan claro. En otras ocasiones, el IDOR se deriva del algoritmo real utilizado. En este último caso, analicemos nuestros comprobantes. Aunque los valores puedan parecer aleatorios, debemos investigar qué algoritmo se utilizó para generarlos. Su formato se parece a un UUID, así que usemos un sitio web como [UUID Decoder](https://www.uuidtools.com/decode) para intentar comprender qué formato de UUID se utilizó. Copie uno de los comprobantes en el sitio web para decodificarlo y debería ver algo como esto:

![[Pasted image 20251205115802.png]]

Aunque estos parecen completamente aleatorios, podemos ver que se usó la versión 1 del UUID. El problema con el UUID 1 es que si conocemos la fecha exacta en que se generó el código, podemos recuperarlo. Por ejemplo, supongamos que supiéramos que los elfos siempre generaban cupones entre las 20:00 y las 21:00. En ese caso, podemos crear UUID para todo ese período (3600 UUID, ya que tenemos 60 minutos y 60 segundos en un minuto), que podríamos usar en un ataque de fuerza bruta para intentar recuperar un cupón válido y obtener más regalos.

Ahora que hemos visto los distintos IDOR que se pueden encontrar, ¡veamos cómo solucionarlos y evitarlos!

## Mejorar el diseño, eliminar el riesgo

Ahora que sabemos qué es el IDOR, veamos cómo solucionarlo. La mejor manera de detener el IDOR es asegurarse de que el servidor verifique quién solicita los datos cada vez. No basta con ocultar o cambiar el número de ID; El sistema debe confirmar que el usuario conectado está autorizado a ver o modificar dicha información.

No confíe en trucos como Base64 o el hash de los ID; estos aún pueden adivinarse o decodificarse. En su lugar, mantenga todas las comprobaciones de permisos reales en el servidor. Cada vez que llegue una solicitud, verifique: "¿Este usuario posee o tiene permiso para ver este elemento?".

Use IDs aleatorios o difíciles de adivinar para los enlaces públicos, pero recuerde que los IDs aleatorios por sí solos no garantizan la seguridad de su aplicación. Pruebe siempre su aplicación intentando abrir los datos de otro usuario y asegurándose de que estén bloqueados. Finalmente, registre y monitoree los intentos de acceso fallidos; pueden ser señales tempranas de que alguien intenta explotar un IDOR.


**Answer the questions below**

What does IDOR stand for?

Respuesta: Insecure Direct Object Reference

What type of privilege escalation are most IDOR cases?

Respuesta: Horizontal

Exploiting the IDOR found in the `view_accounts` parameter, what is the `user_id` of the parent that has 10 children?

Respuesta: 15
![[Pasted image 20251205191259.png]]

**Bonus Task:** If you want to dive even deeper, use either the base64 or md5 child endpoint and try to find the `id_number` of the child born on 2019-04-17? To make the iteration faster, consider using something like Burp's Intruder. If you want to check your answer, click the hint on the question.

Check

**Bonus Task:** Want to go even further? Using the `/parents/vouchers/claim` endpoint, find the voucher that is valid on 20 November 2025. Insider information tells you that the voucher was generated exactly on the minute somewhere between 20:00 - 24:00 UTC that day. What is the voucher code? If you want to check your answer, click the hint on the question.

Check

If you enjoyed today's room, check out our complete [IDOR](https://tryhackme.com/room/idor) room!


![[Pasted image 20251205121839.png]]
![[Pasted image 20251205121856.png]]
![[Pasted image 20251205121914.png]]
![[Pasted image 20251205122038.png]]
![[Pasted image 20251205122324.png]]
![[Pasted image 20251205122518.png]]
![[Pasted image 20251205122602.png]]
![[Pasted image 20251205185919.png]]
![[Pasted image 20251205190153.png]]
