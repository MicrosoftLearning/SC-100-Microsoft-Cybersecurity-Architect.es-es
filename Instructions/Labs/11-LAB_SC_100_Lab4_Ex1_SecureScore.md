# Administración de la posición de seguridad

El equipo de seguridad de Contoso quiere mejorar su posición de seguridad mediante la Puntuación de seguridad de Microsoft, una herramienta que proporciona recomendaciones e instrucciones sobre cómo reducir la superficie expuesta a ataques y proteger contra amenazas.

El equipo de seguridad revisa y delega las acciones recomendadas de puntuación de seguridad a sus miembros extendidos del equipo (embajadores de seguridad) que administran el estado y el plan de acción asociados a las acciones de mejora. El equipo de seguridad también quiere controlar el acceso a la información de posición de seguridad y a los orígenes de datos que la alimentan. Joni Shermann es uno de los embajadores de seguridad y necesita acceso a la administración de exposición.

Recientemente, se han recibido informes de que asociados no invitados se admitían automáticamente en llamadas de Teams a las que no fueron invitados directamente.  Debido a la naturaleza sensible y confidencial de las llamadas, el equipo de seguridad quiere controlar esto.

## Parte 1: Diseñar una solución (necesaria)

### Enfoque de diseño

En la pestaña de acciones recomendadas de Puntuación de seguridad de Microsoft se enumeran las recomendaciones de seguridad que abordan las posibles superficies de ataque. Esas acciones se pueden compartir o delegar.

Los equipos de seguridad necesitan controlar el acceso a la información de posición de seguridad de la organización y a los orígenes de datos específicos que la alimentan. El modelo de control de acceso basado en rol (RBAC) unificado de Microsoft Defender XDR proporciona una única experiencia de administración de permisos que proporciona una ubicación central para que los administradores controlen los permisos de usuario en diferentes soluciones de seguridad.

Para asegurarte de que los embajadores de seguridad tienen los permisos de rol necesarios, debes crear un rol personalizado. Para que el portal de seguridad de Microsoft Defender XDR empiece a aplicar los permisos y las asignaciones configurados en los nuevos roles personalizados o los roles importados, debes activar el modelo de RBAC unificado de Microsoft Defender XDR para algunas o todas las cargas de trabajo.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Joni Shermann administrará las acciones y el estado asociados a las recomendaciones de puntuación de seguridad. |Administración de exposición: puntuación de seguridad y RBAC unificado de Defender XDR | Crea un rol para administrar la posición de seguridad y conceder acceso a Joni Shermann. |
|Controla el acceso a la información de posición de seguridad y a los orígenes de datos que la alimentan. | RBAC unificado de Microsoft Defender XDR | Activa RBAC unificado de Microsoft Defender XDR para el rol personalizado. |
|Compartir acción recomendada de puntuación de seguridad |Puntuación segura | Comparte la acción recomendada. |

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Crear un rol personalizado para administrar la posición de seguridad para la administración de exposición

En esta tarea, configurarás un rol personalizado centrado en la posición de seguridad y, más específicamente, en la administración de la exposición. Como parte del rol personalizado, concederás a Joni Shermann acceso al origen de datos para administración de exposiciones.

1. Inicia sesión en la máquina virtual cliente Windows **LON-SC1** con la cuenta de **Administrador** local. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **`https://security.microsoft.com`** e inicia sesión en **Microsoft Defender** como Administrador MOD **admin@WWLxZZZZZZ.onmicrosoft.com** (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.
1. En el cuadro de diálogo **¿Mantener la sesión iniciada?**, activa la casilla **No volver a mostrar esto** y, a continuación, selecciona **No**.
1. Cierra el cuadro de diálogo Guardar la contraseña de la parte inferior. Para ello, selecciona **Nunca** para no guardar las credenciales predeterminadas de administradores globales en el navegador.
1. Si ves un cuadro de información en la parte superior derecha de la pantalla que indica **Administrar autenticación multifactor**, selecciona la **X** para cerrarlo.
1. En el panel de navegación izquierdo, expande **Sistema** y, a continuación, selecciona **Permisos**.
1. Si es la primera vez que accedes a la configuración de Microsoft Defender, tendrás que esperar unos minutos mientras Defender prepara nuevos espacios para tus datos y los conecta.  Una vez que finalices, actualiza la página de permisos hasta que veas una lista que incluya Microsoft Defender XDR, Microsoft Entra ID, roles y grupos de puntos de conexión, roles de correo electrónico y colaboración y Cloud Apps. Estas pueden tardar algún tiempo en aparecer.
1. En **Microsoft Defender XDR(1)**, selecciona **Roles**.
1. Selecciona **Crear rol personalizado**.
1. En el campo Nombre de rol, escribe **`SecureScore Manager`** y luego selecciona **Siguiente**.
1. Seleccione **Posición de seguridad**.
1. En la ventana Posición de seguridad:
    - Selecciona **Seleccionar permisos personalizados**
    - En Administración de posturas, selecciona **Seleccionar permisos personalizados**
    - Elige **Administración de exposición (administrar)**
    - Seleccione **Aplicar**.
    - Seleccione **Siguiente**.
1. En la página **Asignar usuarios y orígenes de datos**, selecciona **Agregar asignación** y rellena los campos como se indica a continuación:
    - Nombre de asignación: **`ExposureManagement`**
    - Asignar usuarios y grupos: escribe **`Joni Sherman`** y selecciónalo.
    - En **Orígenes de datos**, selecciona el menú desplegable para ver una lista de los orígenes de datos disponibles. Selecciona solo **Administración de exposición de seguridad de Microsoft**.  Si se muestran otros orígenes de datos, anula su selección.
    - Selecciona **Agregar**.
    - Selecciona **Siguiente**.
1. En la página Revisar y finalizar, selecciona **Enviar** y, después, selecciona **Listo**.
1. Debes estar en la página **Permisos y roles** y ver el rol personalizado que acabas de crear. Deja esta pestaña abierta, porque volverás a ella en la siguiente tarea.

Has configurado correctamente un rol personalizado para la posición de seguridad que concede a Joni Shermann acceso al origen de datos de Administración de exposición.

### Tarea 2: Activar RBAC unificado de Defender XDR para cargas de trabajo específicas

Para que el portal de seguridad de Microsoft Defender XDR empiece a aplicar los permisos y las asignaciones configurados en tus nuevos roles personalizados, debes activar el modelo de RBAC unificado de Microsoft Defender XDR para las cargas de trabajo.

Al activar algunas o todas las cargas de trabajo para usar el nuevo modelo de permisos, los roles y permisos de estas cargas de trabajo se controlan completamente mediante el modelo de RBAC unificado de Microsoft Defender XDR en el portal de Microsoft Defender.

En esta tarea explorarás la página donde se activan las cargas de trabajo.

1. Todavía deberías tener iniciada la sesión en el portal de Microsoft Defender y estar en la página **Permisos y roles**. Deberías ver el control personalizado que creaste.
1. Ten en cuenta la información del banner gris, algunos de los roles aún no son aplicables, ya que no has activado todas las cargas de trabajo. Selecciona **Activar cargas de trabajo**.
1. Anota la descripción en **Activar el control de acceso basado en rol unificado**.  Al activar algunas o todas las cargas de trabajo para usar el nuevo modelo de permisos, los roles y permisos de estas cargas de trabajo se controlan completamente mediante el modelo de RBAC unificado de Microsoft Defender XDR en el portal de Microsoft Defender.
1. Para este ejercicio, el origen de datos de Administración de exposición está habilitado de forma predeterminada, por lo que no hay ninguna configuración para habilitar esa carga de trabajo. Si has creado un rol personalizado que incluía permisos para otras cargas de trabajo, como Office 365 o Administración de dispositivos y vulnerabilidades, como ejemplos, tendrías que activar esas cargas de trabajo específicas para activar el rol personalizado, como parte de RBAC unificado.

Has aprendido a activar el modelo de RBAC unificado de Microsoft Defender XDR para algunas o todas las cargas de trabajo.

### Tarea 3: Compartir una acción recomendada

Comparte una acción recomendada de puntuación de seguridad de Microsoft. En esta tarea, publicarás la acción en un canal de Teams. Al publicarla en Teams, los usuarios del canal verán un aviso, pero no tendrán acceso al origen de datos para editar el estado o administrar la acción. Solo Joni Shermann, que es miembro del canal de Teams y tiene permisos de rol, puede acceder a la acción recomendada.

1. Deberías seguir con la sesión iniciada en el portal de Microsoft Defender XDR.
1. En el panel de navegación izquierdo, expande **Administración de exposición** y, después, selecciona **Puntuación de seguridad**.
1. Selecciona la pestaña **Acciones recomendadas**.
1. Busque **`Only invited users should be automatically admitted to Teams meetings`** y selecciónelo.
1. Selecciona **Compartir** y, en el menú desplegable, selecciona **Microsoft Teams**.
1. En el campo **Equipo**, selecciona **Mark 8 Project Team** y, en el campo **Canal**, selecciona **Investigación y desarrollo del canal**.
1. Selecciona **Publicar mensaje en Teams**.

Joni Sherman y su Mark 8 Project Team recibirán una notificación sobre la acción recomendada en el canal de Teams.

### Tarea 4: Administrar recomendaciones

Como Joni Sherman, recibiste la notificación de Teams de que se recomienda una acción específica para aumentar la posición de seguridad de la organización.  Como miembro extendido del equipo de seguridad, tienes los permisos de rol para administrar la acción recomendada y documentar la solución.

En esta tarea, administrarás la acción recomendada y documentarás las soluciones.

1. Abre una ventana InPrivate de Microsoft Edge, ve a **`https://office.com`** e inicia sesión como **JoniS@WWLxZZZZZZ.onmicrosoft.com**.
1. Si la página de aterrizaje aparece borrosa, actualiza la página.
1. Selecciona el icono del iniciador de aplicaciones, situado a la izquierda del banner superior que dice Contoso Electronics y selecciona **Teams**.
1. En la ventana de Bienvenida a Teams, selecciona **Comenzar**. Teams puede tardar un minuto o dos en configurarse. Si aparece una pantalla de código QR para Teams para dispositivos móviles, ciérrala.
1. Abra Teams. En **Mark 8 Project Team**, selecciona **Ver todos los canales** y, a continuación, selecciona **Investigación y desarrollo**.
1. Revisa el mensaje publicado en la tarea anterior.
1. En el mensaje publicado, selecciona el vínculo **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.  Dado que a ti, Joni Shermann, se te ha concedido permiso a través del rol personalizado, puedes acceder a la puntuación de seguridad.  Otros miembros del equipo del proyecto Mark 8 pueden ver la publicación, pero no tienen acceso a la puntuación de seguridad.
1. Seleccione **Editar estado y plan de acción**.
1. Marca **Resuelto a través de tercero**.
1. Agrega una nota **Protegida actualmente** en el campo **Plan de acción**.
1. Selecciona **Guardar y cerrar**.
1. Cierra las pestañas del explorador InPrivate.

Como Joni Shermann, editaste correctamente el estado de la acción recomendada.

### Tarea 5 (opcional): Adele Vance accede a la publicación de Teams

En esta tarea, Adele Vance accede al canal Mark 8 Project Team y selecciona el vínculo en el mensaje publicado.

1. Abre una ventana InPrivate de Microsoft Edge, ve a **`https://office.com`** e inicia sesión como Adele Vance, **AdeleV@WWLxZZZZZZ.onmicrosoft.com**.
1. Si la página de aterrizaje aparece borrosa, actualiza la página.
1. Selecciona el icono del iniciador de aplicaciones, situado a la izquierda del banner superior que dice Contoso Electronics y selecciona **Teams**.
1. En la ventana de Bienvenida a Teams, selecciona **Comenzar**.
1. Abra Teams. En **Mark 8 Project Team**, selecciona **Ver todos los canales** y, a continuación, selecciona **Investigación y desarrollo**.
1. Revisa el mensaje publicado en la tarea anterior.
1. Selecciona el vínculo en el mensaje publicado **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.
1. Se te lleva directamente a la puntuación de seguridad de Microsoft, pero no tienes permiso para acceder a estos datos, ya que Adele Vance no se agregó como miembro al rol personalizado que creaste.
1. Cierra las pestañas del explorador InPrivate.

En esta tarea, has confirmado que los miembros del proyecto Mark 8 pueden ver el mensaje publicado para la acción recomendada para ayudar a mejorar la posición de seguridad de la organización, pero solo los asociados que se han agregado al rol personalizado pueden acceder a la información de puntuación de seguridad.
