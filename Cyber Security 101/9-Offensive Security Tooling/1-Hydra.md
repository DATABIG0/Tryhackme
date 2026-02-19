repositrio oficial 
https://github.com/vanhauser-thc/thc-hydra

herramienta kali hydra
https://en.kali.tools/?p=220

## Hydra Commands

Las opciones que pasamos a Hydra dependen del servicio (protocolo) que estemos atacando. Por ejemplo, si quisiéramos realizar un ataque de fuerza bruta a un FTP con el nombre de usuario `user` y la lista de contraseñ
as `passlist.txt`, usaríamos el siguiente comando:

hydra -l user -P passlist.txt ftp://10.201.83.70

### SSH

`hydra -l <username> -P <full path to pass> 10.201.83.70 -t 4 ssh`

|Option|Description|
|---|---|
|`-l`|specifies the (SSH) username for login|
|`-P`|indicates a list of passwords|
|`-t`|sets the number of threads to spawn|
Por ejemplo, hydra -l root -P passwords.txt 10.201.83.70 -t 4 ssh se ejecutará con los siguientes argumentos:

-Hydra usará root como nombre de usuario para ssh.
-Probará las contraseñas del archivo passwords.txt.
-Habrá cuatro hilos ejecutándose en paralelo, como indica -t 4.

### Post Web Form

También podemos usar Hydra para forzar formularios web. Debes saber qué tipo de solicitud realiza; los métodos GET o POST son comunes. Puedes usar la pestaña de red de tu navegador (en las herramientas de desarrollo) para ver los tipos de solicitud o el código fuente.

También podemos usar Hydra para forzar formularios web. Debes saber qué tipo de solicitud realiza; los métodos GET o POST son comunes. Puedes usar la pestaña de red de tu navegador (en las herramientas de desarrollo) para ver los tipos de solicitud o el código fuente.

`sudo hydra <username> <wordlist> 10.201.83.70 http-post-form "<path>:<login_credentials>:<invalid_response>"`

| Option                | Description                                                                              |
| --------------------- | ---------------------------------------------------------------------------------------- |
| `-l`                  | the username for (web form) login                                                        |
| `-P`                  | the password list to use                                                                 |
| `http-post-form`      | the type of the form is POST                                                             |
| `<path>`              | the login page URL, for example, `login.php`                                             |
| `<login_credentials>` | the username and password used to log in, for example, `username=^USER^&password=^PASS^` |
| `<invalid_response>`  | part of the response when the login fails                                                |
| `-V`                  | verbose output for every attempt                                                         |
A continuación, se muestra un ejemplo más concreto de un comando de Hydra para forzar un formulario de inicio de sesión POST:

`hydra -l <username> -P <wordlist> 10.201.83.70 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

-La página de inicio de sesión es solo /, es decir, la dirección IP principal.
-El nombre de usuario es el campo del formulario donde se introduce el nombre de usuario.
-El nombre de usuario especificado reemplazará a ^USER^.
-La contraseña es el campo del formulario donde se introduce la contraseña.
-Las contraseñas proporcionadas reemplazarán a ^PASS^.
-Finalmente, F=incorrecto es una cadena que aparece en la respuesta del servidor cuando falla el inicio de sesión.


Answer the questions below

Use Hydra to bruteforce molly's web password. What is flag 1?

![[Pasted image 20250817184938.png]]


![[Pasted image 20250817184857.png]]
![[Pasted image 20250817184919.png]]

iniciamos sesión con las credenciales obtenidas

![[Pasted image 20250817185246.png]]



Use Hydra to bruteforce molly's SSH password. What is flag 2?

![[Pasted image 20250817182727.png]]

![[Pasted image 20250817183152.png]]

![[Pasted image 20250817183212.png]]
