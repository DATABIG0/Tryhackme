Instalar FoxyProxy: Descarga e instala la extensión FoxyProxy Basic.

Acceder a las opciones de FoxyProxy: Una vez instalado, aparecerá un botón en la esquina superior derecha del navegador Firefox. Haz clic en el botón FoxyProxy para acceder a las opciones.

![[Pasted image 20250817144801.png]]

Crear configuración de proxy Burp: En la ventana emergente de opciones de FoxyProxy, haga clic en el botón Opciones. Se abrirá una nueva pestaña del navegador con las configuraciones de FoxyProxy. Haga clic en el botón Agregar para crear una nueva configuración de proxy.

![[Pasted image 20250817144949.png]]

Agregar detalles de proxy: En la página "Agregar proxy", complete los siguientes valores:

- Title: `Burp` (or any preferred name)
- Proxy IP: `127.0.0.1`
- Port: `8080`
![[Pasted image 20250817145132.png]]

Guardar configuración: Haga clic en Guardar para guardar la configuración del proxy Burp.

Activar la configuración del proxy: Haga clic en el icono de FoxyProxy en la esquina superior derecha del navegador Firefox y seleccione la configuración de Burp. Esto redirigirá el tráfico de su navegador a través de 127.0.0.1:8080. Tenga en cuenta que Burp Suite debe estar ejecutándose para que su navegador pueda realizar solicitudes cuando esta configuración esté activada.

![[Pasted image 20250817145146.png]]

Habilitar Proxy Intercept en Burp Suite: cambie a Burp Suite y asegúrese de que Intercept esté activado en la pestaña Proxy.

![[Pasted image 20250817145112.png]]