# Laboratorio 4- Ejercicio 2: Acceso global seguro

Después de configurar el servidor de supervisión, debes establecer redes seguras en el servidor de archivos mediante el Acceso global seguro (GSA). Quieres asegurarte de que el acceso a estas máquinas esté protegido hasta que estos servidores de archivos se puedan migrar al almacenamiento en la nube seguro, especialmente si Tailwind Traders está incorporando servidores locales a la infraestructura de TI de tu empresa. Has decidido volver a trabajar con la infraestructura VPN de Tailwind Traders para permitir que los empleados accedan a los servidores. 

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
<!--BITE AUSFÜLLEN-->
|Requisito|Solución|Plan de acción|
|----|----|----|
|Habilitar acceso remoto seguro para servidores locales| Acceso global seguro de EntraID | Habilitación del Acceso global seguro  |
|Integrar con la infraestructura existente | Application Proxy | Implementar proxy de aplicación en el servidor de archivos de Contoso |

## Parte 2: Implementar la solución (opcional)

## Tarea 1: Activar el acceso global seguro

El primer paso es activar el acceso global seguro en el inquilino. Esto te permitirá usar un proxy de App de Azure para proporcionar acceso seguro a los recursos de OnPremises.

1. Inicia sesión en la **máquina virtual cliente 1** (LON-SC1) como cuenta **lon-sc1\admin**. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **https://entra.microsoft.com** e inicia sesión en Entra Portal como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
3. Se te pedirá que configures la autenticación multifactor; sigue las instrucciones.
4. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla No volver a mostrar esto y, a continuación, selecciona **No**.
5. Cierra el cuadro de diálogo guardar contraseña de la parte inferior. Para ello, selecciona Nunca, para no guardar las credenciales predeterminadas de administradores globales en el explorador.
6. En el panel de navegación izquierdo, expande **Acceso global seguro** y selecciona **Panel**.
7. En **Activar acceso global seguro en el inquilino**, selecciona **Activar**.

Has activado correctamente el acceso global seguro.

## Tarea 2: Implementar Application Proxy

El acceso global seguro se basa en el proxy de aplicación que te permitirá crear un punto de conexión de nube seguro para los recursos locales. En este caso, permitirás el servidor de prueba que hayas configurado antes para comunicarse a través de la infraestructura de proxy.

1. Inicia sesión en la **máquina virtual del servidor 1** (LON-SC2) como cuenta **lon-sc1\admin** . El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **https://entra.microsoft.com** e inicia sesión en Entra Portal como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
3. En **Acceso global seguro** en el panel de navegación izquierdo, expande **Conectar** y selecciona **Conectores**.
4. Seleccione **Descargar servicio de conector**.
5.  Selecciona **Aceptar las condiciones y descargar**.
6.  Instalación del **conector de Application Proxy de Microsoft Azure Active Directory **.
7.  Durante el proceso de instalación, debes iniciar sesión con el nombre de usuario y la contraseña proporcionados por el laboratorio.
8.  Abre el **CMD** y ejecuta el comando **ipconfig** y anota la dirección IP.
9.  Vuelve al portal Entra y actualiza la página Conectores.

Deberías ver la máquina virtual incorporada y la dirección IP asociada. Esto significa que te has conectado correctamente al conector.

## Tarea 3: Crear recurso compartido en el servidor de archivos

En esta tarea, crearás un recurso compartido de SMB en el servidor de archivos local al que tendrás acceso a través de GSA.

1. Todavía debes iniciar sesión en LON-SC2.
2. Abre el **Explorador**, ve a la unidad C: y crea una carpeta denominada **Compartir**.
3. Selecciona la carpeta Compartir y abre las **propiedades**.
4. Selecciona **Uso compartido**.
5. Selecciona **Compartir...**.
6. Selecciona **Todos** en la lista desplegable y selecciona **Agregar**.
7. Seleccione **Compartir**.
8. Selecciona **No, conviertas la red a la que estoy conectado/a en una red privada**.

## Tarea 4: Configuración del Acceso rápido y asignación de usuarios

Para que los usuarios accedan al servidor de archivos a través del cliente GSA, debes habilitar el acceso rápido y asignarlo a los usuarios de prueba. Sin esta configuración, el usuario de prueba no podrá conectarse al servidor de archivos.

1. En el panel de navegación izquierdo, expande **Aplicaciones** y selecciona **Acceso rápido**. Escriba la siguiente información:
    - Nombre: **SMB a ContosoFS**
    - Grupo de conectores: **Predeterminado**
1. Selecciona **Agregar segmento de aplicación de acceso rápido** y rellena la siguiente información:
    - Tipo de destino: Dirección IP
    - Dirección IP: "**LA DIRECCIÓN IP DE LA MÁQUINA VIRTUAL**"
    - Puertos: 445
1. Seleccione **Aplicar**.
1. Selecciona **Guardar** y vuelve a cargar el menú Acceso rápido.
1. En el lado izquierdo, selecciona **Usuario y grupos**.
1. Selecciona **Agregar usuario o grupo**.
1. Selecciona **Ninguno seleccionado**.
1. Agrega **Administrador MOD**.
1. Haz clic en **Seleccionar** > **Asignar**.

Has habilitado correctamente el acceso rápido para el usuario de prueba, en este caso tu cuenta de administrador.

## Tarea 5: El diapositivo se vincula a Entra ID

Para usar el acceso global seguro, debes vincular el punto de conexión de cliente a Entra ID. En caso contrario, el cliente GSA no funcionará.

1. Conéctate a LON-SC1, abre el menú Inicio y selecciona **Configuración**.
2. Selecciona **Cuentas** > **Obtener acceso a trabajo o escuela**.
3. Para agregar una cuenta profesional o educativa, selecciona **Conectar**.
4. Haz clic en **Vincular dispositivo a Entra ID**.
5. Inicia sesión con las credenciales de **administrador de MOD** que proporciona el proveedor de laboratorio.

Una vez el punto de conexión esté vinculado a Entra ID, podrás usar el cliente de GSA para conectarte a los recursos que proteges con el Acceso global seguro.

## Tarea 6: Activación del perfil y validación de la conexión

El Acceso global seguro se divide en dos partes. La parte en la que trabajas se denomina Acceso privado y protege los recursos locales y privados, como servidores de archivos o aplicaciones en el entorno local. Para habilitar el acceso al servidor de archivos, tienes que habilitar el perfil de acceso privado que permite a los usuarios acceder a los recursos asignados a ellos a través del Acceso rápido.

1. En el menú Acceso global seguro del panel de navegación izquierdo del Centro de administración de Microsoft Entra, expande **Conectar** y elige **Reenvío de tráfico**.
2. Activa **Perfil de acceso privado**.
3. Seleccione **Aceptar**.
4. En el panel de navegación izquierdo, en **Conectar**, elige **Descarga de cliente**.
5. En Windows 10/11, selecciona **Descargar cliente**.
6. Instala el **Cliente de acceso global seguro**.
7. Durante el proceso de instalación, debes iniciar sesión con tu Administrador MOD.
8. Abre el **Explorador** en Windows y ve a la barra de menús **Este equipo**, selecciona los puntos suspensivos (...) y selecciona **Conectar a unidad de red**.
9. Carpeta: `\\IP-ADDRESS\Share` Usa la dirección IP que anotaste anteriormente.
10. Seleccione **Finalizar**.
11. Escribe el nombre de usuario y la contraseña locales para asignar la unidad de red.


Se ha conectado correctamente al servidor de archivos mediante acceso global seguro.
