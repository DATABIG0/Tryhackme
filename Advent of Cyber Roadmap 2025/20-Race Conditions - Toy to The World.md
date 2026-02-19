
Introduction

![[Pasted image 20251220163432.png]]

La Mejor Compañía de Festivales (TBFC) lanzó su SleighToy de edición limitada, con solo diez piezas disponibles a medianoche. En cuestión de segundos, miles de personas se apresuraron a comprar uno, pero algo extraño ocurrió. Más de diez afortunados clientes recibieron correos electrónicos de confirmación indicando que sus pedidos se habían realizado correctamente. La confusión se extendió rápidamente. ¿Cómo pudo todo el mundo comprar el "último" juguete? Se llamó a McSkidy para que investigara.

Rápidamente se dio cuenta de que varios compradores compraban al mismo tiempo, burlando la falla de sincronización del sistema. Los traviesos Bandit Bunnies de Sir Carrotbane habían encontrado la manera de explotar este caos, inundando la caja con clics rápidos. Por la mañana, TBFC se enfrentó a compradores enfadados, falta de existencias y un misterio que reveló lo peligrosos que podían ser unos pocos milisegundos durante el ajetreo navideño.

Objetivos de aprendizaje

Comprender qué son las condiciones de carrera y cómo pueden afectar a las aplicaciones web.
Aprender a identificar y explotar las condiciones de carrera en las solicitudes web.
Cómo las solicitudes concurrentes pueden manipular los valores de las existencias o las transacciones. Explore técnicas de mitigación simples para prevenir vulnerabilidades en condiciones de carrera.

Answer the questions below

I can successfully connect to the machine.

No answer needed


---

# ==Race Condition==

Una condición de carrera ocurre cuando dos o más acciones ocurren simultáneamente, y el resultado del sistema depende del orden en que terminan. En aplicaciones web, esto suele ocurrir cuando varios usuarios o solicitudes automatizadas acceden o modifican simultáneamente recursos compartidos, como el inventario o los saldos de las cuentas. Si no se realiza una sincronización adecuada, esto puede generar resultados inesperados, como transacciones duplicadas, artículos sobrevendidos o cambios de datos no autorizados.

![[Pasted image 20251220163633.png]]

## Tipos de Condiciones de Carrera

Generalmente, los ataques de condición de carrera se pueden dividir en tres categorías:

- **Tiempo de Verificación a Tiempo de Uso (TOCTOU):** Una condición de carrera TOCTOU ocurre cuando un programa verifica algo primero y lo usa después, pero los datos cambian entretanto. Esto significa que lo que era cierto en el momento de la verificación podría dejar de serlo cuando se realiza la acción. Es como comprobar si un juguete está en stock y, para cuando haces clic en "Comprar", alguien más ya lo ha comprado. Por ejemplo, dos usuarios compran el mismo "último artículo" al mismo tiempo porque se verificó el stock antes de actualizarlo.
- **Recurso compartido:** Esto ocurre cuando varios usuarios o sistemas intentan modificar los mismos datos simultáneamente sin el control adecuado. Dado que ambas actualizaciones se realizan simultáneamente, el resultado final depende de cuál finalice último, lo que genera confusión. Imaginemos a dos cajeros actualizando la misma hoja de cálculo de inventario a la vez, y uno sobrescribe el trabajo del otro.
- **Violación de atomicidad:** Una operación atómica debería realizarse de una sola vez, ya sea completamente completa o no completada. Cuando partes de un proceso se ejecutan por separado, otra solicitud puede interferir y generar resultados inconsistentes. Es como pagar un artículo, pero antes de que el sistema lo confirme, alguien más cambia el precio. Por ejemplo, se registra un pago, pero la confirmación del pedido falla porque otra solicitud interrumpe el proceso.

## Momento de actuar

Ahora que comprendemos los conceptos básicos, tomemos el ejemplo de la aplicación de carrito de compras TBFC y explotemos la condición de carrera.

## Configuración del entorno

Primero, configuraremos Firefox para enrutar el tráfico a través de Burp Suite. En AttackBox, abra Firefox, haga clic en el icono de FoxyProxy (1) y seleccione el perfil Burp (2) para que todas las solicitudes del navegador se envíen a Burp, como se muestra a continuación:

![[Pasted image 20251220163747.png]]

A continuación, haga clic en el icono de Burp Suite en el escritorio para iniciar la aplicación.

![[Pasted image 20251220163808.png]]

Verá una pantalla de introducción; seleccione Proyecto temporal en memoria y haga clic en Siguiente.

![[Pasted image 20251220163829.png]]

En la pantalla de configuración, haga clic en Iniciar Burp para iniciar la aplicación.

![[Pasted image 20251220163852.png]]

Una vez iniciada la aplicación verás la siguiente pantalla, donde utilizaremos la opción Proxy y Repetidor para explotar la condición de carrera.

![[Pasted image 20251220163920.png]]

Antes de continuar, asegúrese de desactivar la función "Interceptar" en Burp Suite. Abra la pestaña "Proxy" y revise la subpestaña "Interceptar". Si el botón indica "Interceptar activado", haga clic en él para que cambie a "Interceptar desactivado". Este paso garantiza que Burp Suite ya no retenga las solicitudes de su navegador y las permita procesarse con normalidad.

![[Pasted image 20251220163948.png]]

## Realizar una solicitud legítima

Ahora que el entorno está configurado, realice una solicitud normal. Abra Firefox, visite la aplicación web en http://MACHINE_IP y verá la siguiente página de inicio de sesión:

![[Pasted image 20251220164020.png]]

En el panel de inicio de sesión del sitio, introduce tus credenciales: usuario: attacker y contraseña: attacker@123. Tras iniciar sesión, accederás al panel principal, donde se muestra el SleighToy de edición limitada, con solo 10 unidades disponibles.

![[Pasted image 20251220164108.png]]

Para realizar una compra legítima, haga clic en Agregar al carrito para el SleighToy y luego haga clic en Pagar para ir a la página de pago.

![[Pasted image 20251220164146.png]]

En la página de pago, haz clic en Confirmar y pagar para completar la compra. Verás un mensaje de confirmación de compra, como se muestra a continuación:

![[Pasted image 20251220164206.png]]

## Aprovechamiento de la condición de carrera

Ahora que hemos realizado una solicitud legítima, regrese a Burp Suite y haga clic en Proxy > Historial HTTP. Busque la solicitud POST al punto final /process_checkout creada por nuestra solicitud de pago legítima. Haga clic derecho en esa entrada y seleccione "Enviar a repetidor". Esto copiará la solicitud HTTP exacta (encabezados, cookies, cuerpo) en la herramienta Repetidor de Burp, como se muestra a continuación:

![[Pasted image 20251220164233.png]]

A continuación, cambie a la pestaña Repetidor y confirme que la solicitud aparece allí, haga clic derecho en la primera pestaña, seleccione Agregar pestaña al grupo y haga clic en Crear grupo de pestañas.

![[Pasted image 20251220164258.png]]

Ingrese un nombre para el grupo de pestañas, como carrito, y haga clic en Crear, lo que creará un grupo de pestañas llamado carrito.

![[Pasted image 20251220164318.png]]

Luego, haz clic derecho en la pestaña de solicitud y selecciona Duplicar pestaña. Cuando se te solicite, introduce el número de copias que deseas (por ejemplo, 15). Ahora tendrás esa misma cantidad de pestañas de solicitud idénticas dentro del grupo del carrito.

![[Pasted image 20251220164337.png]]

A continuación, utilice el menú desplegable Enviar de la barra de herramientas Repetidor y seleccione Enviar grupo en paralelo (sincronización de último byte), que lanza todas las copias a la vez y espera el byte final de cada respuesta, maximizando la superposición de tiempo para activar las condiciones de carrera.

![[Pasted image 20251220164357.png]]

Una vez hecho esto, haga clic en "Enviar grupo (en paralelo)". Esto enviará las 15 solicitudes al servidor simultáneamente. El servidor intentará procesarlas simultáneamente, lo que provocará el error de sincronización (debido al procesamiento de varias solicitudes a la vez).

![[Pasted image 20251220164423.png]]

Por último, visita la aplicación web y verás varios pedidos confirmados y el stock de SleighToy reducido (posiblemente se vuelva negativo).

![[Pasted image 20251220164443.png]]

## Mitigación

El atacante inició sesión y realizó una compra normal del SleighToy de edición limitada. Con Burp Suite, capturó la solicitud de pago y la envió varias veces en paralelo. Debido a que la aplicación no gestionaba correctamente los pagos simultáneos, cada solicitud se completó correctamente antes de que se actualizara el stock. Esto le permitió comprar más juguetes de los disponibles, lo que provocó una condición de carrera y elevó el stock a valores negativos. A continuación, se presentan algunas medidas de mitigación para evitar la vulnerabilidad:

- Utilice transacciones atómicas de la base de datos para que la deducción de stock y la creación de pedidos se ejecuten como una sola operación consistente.
- Realice una validación final del stock justo antes de confirmar la transacción para evitar la sobreventa.
- Implemente claves de idempotencia para las solicitudes de pago a fin de garantizar que los duplicados no se procesen varias veces.
- Aplique controles de limitación de velocidad o concurrencia para bloquear intentos de pago rápidos y repetidos del mismo usuario o sesión.

**Answer the questions below**

What is the flag value once the stocks are negative for **SleighToy Limited Edition**?

Respuesta: THM{WINNER_OF_R@CE007} 

![[Pasted image 20251220172239.png]]

Repeat the same steps as were done for ordering the SleighToy Limited Edition. What is the flag value once the stocks are negative for **Bunny Plush (Blue)**?

Respuesta: THM{WINNER_OF_Bunny_R@ce}

![[Pasted image 20251220172617.png]]
![[Pasted image 20251220172636.png]]
![[Pasted image 20251220172719.png]]
![[Pasted image 20251220172744.png]]
![[Pasted image 20251220172821.png]]
![[Pasted image 20251220172834.png]]
![[Pasted image 20251220172847.png]]
![[Pasted image 20251220172858.png]]
![[Pasted image 20251220172916.png]]
![[Pasted image 20251220172956.png]]
![[Pasted image 20251220173014.png]]
![[Pasted image 20251220173027.png]]


Feel free to check out the [Race Conditions](https://tryhackme.com/r/room/raceconditionsattacks) room if you enjoyed this task.

Check