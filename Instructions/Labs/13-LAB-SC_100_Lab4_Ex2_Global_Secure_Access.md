# Acceso global seguro

Después de configurar un servidor de supervisión, debes establecer redes seguras en el servidor de archivos mediante Acceso seguro global (GSA). Quieres asegurarte de que el acceso a estas máquinas esté protegido hasta que estos servidores de archivos se puedan migrar al almacenamiento en la nube seguro, especialmente si Tailwind Traders está incorporando servidores locales a la infraestructura de TI de tu empresa. Has decidido volver a trabajar con la infraestructura VPN de Tailwind Traders para permitir que los empleados accedan a los servidores. 

Para establecer redes seguras, empezarás con la creación de un proxy de App de Azure y la inscripción del cliente en Entra ID, antes de crear un conector. Después, configurarás una directiva de acceso e instalarás el cliente GSA. Por último, probarás la conexión de GSA para asegurarte de que todo funciona correctamente.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, protegerás el acceso remoto al entorno local.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Habilitar acceso remoto seguro para servidores locales
- Integrar con la infraestructura existente
- No usar la infraestructura en desuso de Tailwind Traders

Acceso global seguro se integra con la infraestructura en la nube existente de Contoso Ltd. y permite a los empleados acceder remotamente de forma segura a servidores locales dentro de la infraestructura local de Tailwind Traders. Revisa GSA y ten en cuenta las diferencias con otras estrategias para el acceso remoto a los servicios.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Habilitar acceso remoto seguro para servidores locales| Acceso global seguro de EntraID | Habilitación del Acceso global seguro  |
|Integrar con la infraestructura existente | Application Proxy | Implementar proxy de aplicación en el servidor de archivos de Contoso |

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Activar el acceso global seguro

El primer paso es activar el acceso global seguro en el inquilino.

1. Inicia sesión en la máquina virtual **LON-SC1** (el punto de conexión de cliente) como **Administrador** local. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **https://entra.microsoft.com** e inicia sesión en Entra Portal como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
1. En el cuadro de diálogo **¿Mantener la sesión iniciada?**, activa la casilla **No volver a mostrar esto** y, a continuación, selecciona **No**.
1. En el cuadro de diálogo **Guardar contraseña**, selecciona **No ahora**.
1. Si aparece el cuadro de diálogo **Iniciar sesión en Microsoft Edge**, selecciona el botón **No, gracias**.
1. Si ves un cuadro de información en la parte superior derecha de la pantalla que indica **Administrar autenticación multifactor**, selecciona la **X** para cerrarlo.
1. En el panel de navegación izquierdo, expande **Acceso global seguro** y selecciona **Panel**.
1. En **Activar acceso global seguro en el inquilino**, selecciona **Activar**.

Has activado correctamente el acceso global seguro.

### Tarea 2: Habilitar TLS e instalar el conector de red privada

El conector de red privada es un agente ligero que se instala en Windows Server, en el entorno local, que tiene acceso a los recursos y las aplicaciones de back-end, y se usa para facilitar la conexión al servicio de Acceso global seguro.  El Windows Server donde se va a instalar el conector debe tener TLS 1.2 habilitado antes de instalar el conector de red privada.

1. Inicia sesión en la máquina virtual del servidor, **LON-SC2**, con la cuenta de **Administrador** local. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Al iniciar sesión en la máquina virtual, se abrirá Administrador del servidor.  Puedes minimizar esta ventana.
1. Antes de instalar el conector de red privada en el servidor, debes habilitar TLS 1.2.  Hay varias maneras de hacerlo. En este ejercicio, copiarás los comandos para establecer las claves del Registro en un archivo y, a continuación, ejecutarás ese archivo.

    1. Abre **Microsoft Edge**.
    1. En una pestaña del explorador, escribe la dirección URL:**`https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors`** presiona la tecla ENTRAR en el teclado para abrir la documentación del producto.
    1. Desplázate hacia abajo hasta la sección **Requisitos de seguridad de la capa de transporte (TLS)** y en el cuadro de código que aparece en **Establecer claves del Registro**, selecciona **Copiar**.
    1. Desde la máquina virtual, abrirás el Bloc de notas. En el campo de búsqueda de la barra de tareas, escribe **`Notepad`** y selecciona **Bloc de notas** para abrir la aplicación.
    1. Usa **Ctrl+V** para pegar el código en el Bloc de notas.  No cambies nada en el código pegado. Se requiere la primera línea de código.
    1. En el Bloc de notas, selecciona **Archivo** y haz clic en **Guardar como**. 
    1. En el campo **Guardar como tipo**, selecciona **Todos los archivos** en la lista desplegable y, en el campo **Nombre de archivo**, escribe **`EnableTLS.reg`** y, a continuación, selecciona **Guardar.**  Es importante guardar el archivo con la extensión .reg. Anote dónde se guarda el documento y cierra el Bloc de notas.
    1. En la barra de tareas, abre **Explorador de archivos y ve a la carpeta donde guardaste el archivo (el valor predeterminado es This PC >** Documents).
    1. Haz doble clic en el nombre de archivo, **Enable-TLS** para ejecutarlo.  Dado que vas a cambiar el archivo del Registro, se te preguntará, **¿Estás seguro de que deseas continuar?**  Haz clic en **Sí** y luego en **Aceptar**.  
    1. Puesto que has actualizado el registro, deberás reiniciar el servidor. En la barra de tareas de la máquina virtual de servidor, selecciona el **icono de Windows**, selecciona **Power**, **Reiniciar** y, después **, Continuar**.
    1. Después del reinicio, vuelve a iniciar sesión en la máquina virtual del servidor, como administrador** local**.
    1. Minimiza o cierra la aplicación Administrador del servidor.
1. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **`https://entra.microsoft.com`** e inicia sesión en Entra Portal como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
1. Descarta los cuadros de diálogo, tal como hiciste en la tarea anterior.
1. En el panel de navegación izquierdo, expande **Acceso global seguro**, expande **Conectar** y selecciona **Conectores**.
1. En la parte superior de la página Conectores de red privada, selecciona **Descargar servicio de conector**.
1. Revisa la información y selecciona **Aceptar términos y descargar**.
1. En la ventana de descargas de la esquina superior derecha de la página, cuando se complete la descarga, selecciona **Abrir archivo**.  Si la ventana de descargas se cerró antes de poder seleccionar Abrir archivo, selecciona **Explorador de archivos** en la barra de tareas, ve a la carpeta **Descargas** y, a continuación, ejecuta el archivo **MicrosoftEntraPrivateNetworkConnectorInstaller**.
1. Activa la casilla situada junto a **Acepto los términos y las condiciones de la licencia** y después selecciona **Instalar**.
1. Durante el proceso de instalación, debes iniciar sesión con el nombre de usuario y la contraseña del administrador de MOD. La instalación tardará algunos minutos.
1. Una vez completada la instalación, **cierra** la ventana de instalación y actualiza la página del explorador.  Deberías ver que el conector aparece y está activo.
1. En la barra de búsqueda de Windows, en la barra de tareas, escribe **`cmd`** y selecciona **Símbolo del sistema**. 
1. En la ventana Administrador: símbolo del sistema, ejecuta el comando **`ipconfig`**, anota la dirección IP privada del servidor y cierra la ventana del símbolo del sistema.

Has instalado correctamente el conector de red privada en el servidor local.

### Tarea 3: Crear una carpeta en el servidor de archivos

En esta tarea, crearás un recurso compartido de SMB en el servidor de archivos local al que se tendrá acceso mediante GSA.

1. Todavía debes iniciar sesión en LON-SC2.
1. En la barra de tareas, abre **Explorador de archivos**, ve la unidad C: y crea una carpeta denominada **Compartir**.
1. Con la tecla del mouse derecho, selecciona la carpeta **Compartir** y selecciona **Propiedades**.
1. En la ventana Compartir propiedades, selecciona la pestaña **Uso compartido**.
1. Selecciona **Compartir...**.
1. En la lista desplegable, selecciona **Todos** y selecciona **Agregar**.
1. Selecciona **Compartir**.
1. Selecciona **No, conviertas la red a la que estoy conectado/a en una red privada**.
1. Selecciona **Listo** y, después, **Cerrar**.
1. Minimiza o cierra el Explorador de archivos.

Has creado una carpeta compartida en el servidor. Es a esta carpeta y a su contenido al que accederás a través de GSA.

### Tarea 4: Configuración del Acceso rápido y asignación de usuarios

El acceso privado proporciona dos maneras de configurar los recursos privados que desea tunelizar a través del servicio. Aplicaciones Acceso rápido o Acceso global seguro. En este ejercicio, utilizarás el Acceso rápido.

El Acceso rápido es el grupo principal de FQDN y direcciones IP que desea proteger. Al configurar el Acceso rápido, vas a crear una nueva aplicación empresarial que actúa como contenedor para los recursos privados que deseas proteger.

Para que los usuarios accedan a los recursos, el servidor de archivos a través del cliente GSA debe habilitar el Acceso rápido y asignarlo a los usuarios de prueba.

1. Puedes permanecer en LON-SC2 para este paso.
1. En el panel de navegación izquierdo, expande **Acceso global seguro**, expande **Aplicaciones** y, a continuación, selecciona **Acceso rápido**. Escriba la siguiente información:
    - Nombre: **`SMB to ContosoFS`**
    - Grupo de conectores: **Predeterminado**
1. Selecciona **Agregar segmento de aplicación de acceso rápido** y rellena la siguiente información:
    - Tipo de destino: **Dirección IP**
    - Dirección IP: la dirección IP privada del servidor que anotaste en el paso anterior, **`192.168.2.100`**.
    - Puertos: **`445`**
1. Selecciona **Aplicar**.
1. Seleccione **Guardar**. Una vez que veas el campo de estado del segmento de aplicación, actualiza la página del explorador. Al actualizar la página, se te redirigirá a la página **Acceso rápido | Propiedades de acceso a la red**.
1. En el lado izquierdo, selecciona **Usuario y grupos**.
1. Selecciona **Agregar usuario o grupo**.
1. Selecciona **Ninguno seleccionado**.
1. En el campo de búsqueda, escribe **`MOD Administrator`**, y luego selecciónalo en los resultados de búsqueda.
1. En la parte inferior de la página, presiona **Seleccionar** y, a continuación, selecciona **Asignar**.

Has habilitado correctamente el acceso rápido para el usuario de prueba.

### Tarea 5: El diapositivo se vincula a Entra ID

Para usar el acceso global seguro, debes unir el punto de conexión de cliente, la máquina virtual LON-SC1 a Microsoft Entra ID. En caso contrario, el cliente GSA no funcionará.

1. Vuelve a la máquina virtual **LON-SC1** (esta es la máquina virtual del punto de conexión de cliente)
1. Con el botón derecho del ratón, selecciona el icono de Windows en la barra de tareas y selecciona **Configuración**.
1. En el panel de navegación izquierdo, selecciona **Cuentas**.
1. En la página Cuentas, selecciona **Obtener acceso a trabajo o escuela**.
1. Para agregar una cuenta profesional o educativa, selecciona **Conectar**.
1. En la parte inferior de la ventana, selecciona **Unir dispositivo a Microsoft Entra ID**.
1. Inicia sesión con las credenciales de **administrador de MOD** que proporciona el proveedor de laboratorio.
1. En la ventana **Asegurarse de que se trata de tu organización** , revisa la información y, a continuación, selecciona **Unirse**.
1. Revisa la información de la ventana **Todo listo** y selecciona **Listo**.
1. Ahora que el dispositivo está unido a Entra ID con la cuenta de administrador MOD, debes iniciar sesión con esa cuenta.
    1. En la barra de tareas, selecciona el icono de **Windows**, haz clic en **Administrador** y, a continuación, selecciona **Cambiar usuario**.
    1. En la parte inferior izquierda de la ventana, selecciona **Otro usuario** e inicia sesión con la cuenta de administrador MOD.
    1. La configuración de la cuenta tardará unos minutos y aparecerá la ventana **Más información necesaria** . Esto iniciará el proceso para configurar la autenticación multifactor.  Sigue las instrucciones para configurar la autenticación multifactor.

Una vez que el punto de conexión se haya unido a Entra ID, podrás configurar el cliente GSA que se usa para conectarse a los recursos que se protegen mediante el acceso global seguro.

### Tarea 6: Activación del perfil de reenvío de tráfico y descarga del cliente de escritorio de GSA

Para habilitar el acceso a recursos o aplicaciones privados en el entorno local, debes habilitar el perfil de reenvío de tráfico para acceso privado y asignar usuarios.

También debes descargar e instalar el cliente de escritorio del Acceso seguro global.  

El tráfico de Acceso privado se puede reenviar al servicio mediante la conexión a través del cliente de escritorio de Acceso global seguro.

1. Todavía debes estar en **LON-SC1**, en el cual has iniciado sesión con la cuenta de administrador MOD.
1. Abre **Microsoft Edge**. Se te pedirá que configures Microsoft Edge.
1. En Microsoft Edge, ve a **`https://entra.microsoft.com`**.
1. En el panel de navegación izquierdo, expande **Acceso global seguro**, expande **Conectar** y elige **Reenvío de tráfico**.  Es posible que tengas que expandir el panel de navegación izquierdo. Para ello, selecciona **>>** para ver las opciones.
1. Selecciona el botón deslizante situado junto a **Perfil de acceso privado** y, a continuación, selecciona **Aceptar**.
1. Ahora que has habilitado el perfil de acceso privado, deberás asignar usuarios.
    1. En la tarjeta de perfil de acceso privado, en **Asignaciones de usuarios y grupos**, selecciona **Ver**.
    1. Selecciona donde dice **0 usuarios, 0 grupos asignados**
    1. Selecciona **Agregar usuario o grupo**.
    1. Selecciona **Ninguno seleccionado**.
    1. En la barra de búsqueda, escribe **`MOD Administrator`**, selecciona **Administrador MOD**, presiona **Seleccionar** y luego selecciona **Asignar**.
1. En el panel de navegación izquierdo, en **Conectar**, elige **Descarga de cliente**.
1. En Windows 10/11, selecciona **Descargar cliente**.
1. En la ventana Descargas, selecciona **Abrir archivo**. Si la ventana de descargas se cerró antes de poder seleccionar Abrir archivo, selecciona **Explorador de archivos** en la barra de tareas, ve a la carpeta **Descargas** y, a continuación, ejecuta el archivo **GlobalSecureAccessClient**.
1. Selecciona **Acepto los términos y condiciones de la licencia** y, a continuación, selecciona **Instalar**. En la ventana Control de cuentas de usuario que aparece, selecciona **Sí**.
1. Una vez completada correctamente la instalación, **cierra** la ventana.
1. En la barra de tareas, selecciona la flecha arriba para mostrar los iconos ocultos.  Aquí verás el icono de cliente de acceso global seguro. Si no tiene una marca de verificación verde, haz clic con el botón derecho en el icono y selecciona **Habilitar**. Puede tardar varios minutos en mostrarse con una marca de verificación verde para indicar que está conectado.
1. En la barra de tareas, selecciona **Explorador de archivos** y ve a **Este PC**. Selecciona los puntos suspensivos (**...**) y selecciona **Asignar unidad de red**.
1. En el campo Carpeta, escribe `\\192.168.2.100\Share`. Usa la dirección IP que anotaste anteriormente Y selecciona **Conectar con distintas credenciales**.
1. Seleccione **Finalizar**.
1. Para asignar la unidad de red, usa las credenciales de la cuenta de administrador local en LON-SC2.  
    1. Campo Correo electrónico: **`Administrator`** (esto puede variar según el proveedor de servicios de hosting del laboratorio).
    1. Campo Contraseña: **`Pa55w.rd`** (esto puede variar según el proveedor de servicios de hosting del laboratorio).
    
    >[!NOTE] Se reconoce que el uso de la cuenta de administrador local no es un escenario típico. Se usa en este ejercicio debido al entorno local simplificado. En un escenario más realista, con un entorno local más implicado, el usuario accedería a los recursos privados con su cuenta de Entra ID.

1. Antes de pasar al siguiente laboratorio, se recomienda cambiar de usuario para un tamaño de pantalla óptimo.
    1. En la barra de tareas, selecciona el icono de **Windows**, selecciona **Administrador MOD** y, a continuación, selecciona **Cambiar usuario**.
    1. En la parte inferior izquierda de la ventana, selecciona **Administrador** y, a continuación, inicia sesión con la cuenta de administrador local.

Se ha conectado correctamente al servidor de archivos mediante acceso global seguro.
