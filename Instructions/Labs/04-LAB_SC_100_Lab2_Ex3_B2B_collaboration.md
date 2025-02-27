# Sincronización entre inquilinos

Contoso adquirió recientemente Tailwind Traders y ha sido difícil determinar qué invitados son clientes o asociados, y cuáles son empleados de la empresa adquirida. Tu tarea es proporcionar una lista de direcciones común inicial de Tailwind Traders a Contoso. Además, tu inquilino solo debe permitir que se agreguen nombres de dominio conocidos como usuarios invitados a Entra ID. Quieres limitar quién puede invitar a los invitados a la organización solo a usuarios internos. Restringirás el acceso externo solo a un dominio. También crearás una colaboración B2B y una sincronización entre inquilinos de Tailwind Traders a Contoso.

Como arquitecto de ciberseguridad, debes asegurarte de que se cumplen todos los requisitos e implementar los cambios necesarios en Entra ID para aplicar principios de Confianza cero. En este ejercicio, crearás un equipo con un asociado de laboratorio para crear una sincronización entre inquilinos.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los requisitos a los que se enfrentan Contoso Ltd. y Tailwind Traders.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Sincronizar usuarios de ambas empresas
- Hacer que los usuarios externos sean identificables como externos
- Restringir los derechos de invitación solo a los empleados internos 
- Restringir el acceso externo a dominios de confianza de la empresa

En el segundo paso, examina el entorno existente de Contoso Ltd. Microsoft Entra ID ofrece soluciones para habilitar la colaboración externa. Investiga qué controles existen y qué directivas ya están en vigor. Usa el portal de Entra ID para revisar las configuraciones y directivas actuales y determinar qué ajustes se deben implementar para cumplir los requisitos para la implantación.

La tercera fase implica la elaboración del concepto de la solución. Tras la investigación, es evidente que la sincronización entre inquilinos es la mejor manera de habilitar la colaboración que cumpla todos los requisitos.  

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Restringir los derechos de invitación solo a los empleados internos|Configuración de colaboración externa|Limitar los derechos de invitación a los miembros del inquilino y roles de invitación de administrador específicos|
|Bloquear invitaciones de todos, excepto la lista de dominios de confianza|Configuración de colaboración externa|Crear una lista de permitidos de invitación, incluidos solo dominios de confianza|
|Sincronizar usuarios de ambas empresas|Sincronización entre inquilinos de Entra ID|Establecer la confianza de acceso entre los inquilinos de Entra ID y crear una configuración que sincronice a los usuarios con el otro inquilino|
|Hacer que los usuarios externos sean identificables como externos|Asignación de atributos entre inquilinos|Editar el atributo displayName de cada usuario sincronizado mediante la creación de una expresión personalizada mediante la función de asignación de atributos de la configuración de sincronización entre inquilinos|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Formar equipos y preparativos

En esta tarea, comprobarás los requisitos previos de una sincronización entre inquilinos y formarás equipo con un asociado de laboratorio.

1. Inicia sesión en la máquina virtual cliente 1 (LON-Sc1) como cuenta **lon-sc1\admin** . El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **`https://entra.microsoft.com`** e inicia sesión en el portal de Entra ID como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.
1. Si se te pide que configures la autenticación multifactor, sigue las instrucciones.
1. En el cuadro de diálogo **¿Mantener la sesión iniciada?**, activa la casilla **No volver a mostrar esto** y, a continuación, selecciona **No**.
1. Cierra el cuadro de diálogo Guardar contraseña. Para ello, selecciona **No ahora** para no guardar las credenciales predeterminadas del administrador global en el explorador.
1. En el panel de navegación izquierdo, ve a **Identificar** > **Información general**.
1. Anota el **Id. de inquilino** y el **Dominio principal** que se presentan en la pestaña **Información general**.
1. Intercambia el **Id. de inquilino** y el **Dominio principal** con tu asociado de laboratorio.

Debes tener un plan de qué topología deseas usar, qué usuarios estarán en el ámbito de la primera prueba de sincronización y cómo quieres asignarlos al inquilino de Entra ID de Contoso.

### Tarea 2: Configurar acceso entre inquilinos

Puesto que ahora has preparado la información que necesitas para la implementación de la sincronización entre inquilinos, ahora realizarás los pasos necesarios para que el inquilino acceda al inquilino de los asociados y viceversa.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com**.
1. En la barra de navegación izquierda, ve a **Identidad** > **Identidades externas** > **Configuración de acceso entre inquilinos**.
1. Selecciona la pestaña **Configuración de la organización** y selecciona **Agregar organización**.
1. Rellena el campo **Id. de inquilino o nombre de dominio** con el identificador de inquilino proporcionado por el asociado de laboratorio y selecciona **Agregar**.
1. En **Acceso entrante** para Contoso, selecciona **Heredar de forma predeterminada** para acceder a la configuración de sincronización entre inquilinos para ese inquilino específico.
1. En la **Configuración de confianza**, habilita **Canjear automáticamente invitaciones con el inquilino Contoso**.
1. Seleccione **Guardar**.
1. En **Sincronización entre inquilinos**, habilita **Permitir que los usuarios se sincronicen en este inquilino**.
1. Selecciona **Guardar** y cierra el cuadro de diálogo con la **X** de la esquina superior derecha.
1. En **Acceso saliente** para Contoso, selecciona **Heredar de forma predeterminada** para acceder a la configuración de sincronización entre inquilinos para ese inquilino específico.
1. En **Configuración de confianza**, habilita **Canjear automáticamente invitaciones con el inquilino Contoso**.
1. Selecciona **Guardar** y cierra el cuadro de diálogo con la **X** de la esquina superior derecha.

Has habilitado a tu inquilino para sincronizarse de ambas maneras con el inquilino del asociado sin necesidad de que los usuarios canjeen sus invitaciones manualmente. 

### Tarea 3: Restringir acceso externo

En esta tarea, restringirás la capacidad de invitar a nuevos usuarios invitados a tu organización mediante el control del ámbito de los usuarios con permiso para enviar invitaciones. Limitarás el ámbito de los dominios que se pueden invitar como invitados al dominio de inquilino del asociado.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com**.
1. En el panel de navegación izquierdo, ve a **Identidad** > **Identidades externas** > **Configuración de colaboración externa**.
1. En **Configuración de invitación de invitados**, selecciona **Los usuarios miembros y los asignados a roles específicos de administrador pueden invitar a usuarios invitados, incluyendo invitados con permisos de miembro**.
1. En **Restricciones de colaboración**, selecciona **Permitir invitaciones solo a los dominios especificados**.
1. Agrega el dominio de tu asociado de laboratorio **WWLxZZZZZZ.onmicrosoft.com** (donde ZZZZZZ es el identificador de inquilino único de tu asociado de laboratorio proporcionado por el proveedor de hospedaje del laboratorio).
1. Seleccione **Guardar**.

Ahora tienes restringido quién puede invitar y quién puede ser invitado a tu inquilino.

### Tarea 4: Crear una configuración

En esta tarea, crearás una configuración básica y probarás la conexión con el otro inquilino.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com**.
1. En el panel de navegación izquierdo, ve a **Identidad** > **Identidades externas** > **Sincronización entre inquilinos** > **Configuraciones**.
1. Crea una **Nueva configuración**.
1. Escribe el nombre **Sincronización entre inquilinos de Contoso** y selecciona **Crear**.
1. En la página **Aprovisionamiento**, cambia el **Modo de aprovisionamiento** a **Automático**.
1. En el cuadro **Id. de inquilino**, escribe el identificador de inquilino del asociado que anotaste en la Tarea 1.
1. Seleccione **Test Connection** (Probar conexión).
1. Seleccione **Guardar**.

Si has configurado las opciones de acceso correctamente, deberías ver un mensaje que indica que las credenciales proporcionadas están autorizadas para habilitar el aprovisionamiento. Si se produce un error en la conexión de prueba, comprueba si el asociado ha escrito el dominio correcto en la Tarea 3 y ha configurado la sincronización entre inquilinos, tal como se describe en la Tarea 2.

### Tarea 5: Definir ámbito de usuario

En esta Tarea, definirás quién está en el ámbito de la primera sincronización.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com** en la configuración de aprovisionamiento de la configuración recién creada. Si no, sigue estos 3 pasos para volver:
   1. En el panel de navegación izquierdo, ve a **Identidad** > **Identidades externas** > **Sincronización entre inquilinos** > **Configuraciones**.
   1. Selecciona **Sincronización entre inquilinos de Contoso**
   1. Ve a **Aprovisionamiento**.
1. Expande la sección **Configuración**.
1. Comprueba que la lista desplegable Ámbito está establecida en **Sincronizar solo usuarios y grupos asignados**.
1. Si tuviste que cambiar esta configuración, selecciona **Guardar**.
1. En el panel de navegación, selecciona **Usuarios y grupos**.
1. Selecciona **Agregar usuario o grupo**.
1. En la página **Agregar asignación**, selecciona **Ninguna seleccionada**.
1. Busca **Legal** y resalta el **Equipo legal** con la casilla y elige **Seleccionar**.
1. Selecciona **Asignar** para agregar el equipo que consta de dos usuarios al ámbito de sincronización.

Ahora has definido tu primer ámbito de usuarios para la sincronización con el inquilino del asociado.

### Tarea 6: Revisar asignaciones de atributos

En esta tarea, revisarás las asignaciones de atributos y te asegurarás de que los usuarios sincronizados se mostrarán en la lista global de direcciones de Contoso.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com** en la configuración **Usuarios y grupos** de la configuración de sincronización entre inquilinos. Si no, sigue estos 2 pasos para volver a la página de configuración:
   1. En el panel de navegación izquierdo, ve a **Identidad** > **Identidades externas** > **Sincronización entre inquilinos** > **Configuraciones**.
   1. Selecciona **Sincronización entre inquilinos de Contoso**.
1. Ve a **Aprovisionamiento** y expande la sección **Asignaciones**.
1. Seleccione **Aprovisionar usuarios de Microsoft Entra ID**.
1. En el atributo **showInAddressList**, selecciona Editar.
1. Asegúrate de que su tipo de asignación está establecido en **Constante** y su valor establecido en **true**.
1. Seleccione **Aceptar**.
1. En el atributo **displayName**, selecciona **Editar**.
1. Cambia el tipo de asignación a **Expresión**.
1. Quita la expresión preexistente.
1. Selecciona **Usar el Generador de expresiones**.
1. Selecciona la función **Anexar**.
1. En el campo **Seleccionar con atributo**, selecciona el atributo **[displayName]** en la lista desplegable.
1. En el campo **Escribir sufijo**, escribe **" (Contoso)"** incluido el espacio delante del paréntesis, pero sin las comillas.
1. Selecciona **Agregar expresión**. Tu expresión a la derecha tendrá el siguiente aspecto `Append([displayName], " (Contoso)")`
1. Puedes probar la expresión con la selección de un usuario.
1. Selecciona **Aplicar expresión** y selecciona **Aceptar** para dejar el cuadro de diálogo de edición.
1. Seleccione **Guardar**.
1. Selecciona la **X** en la esquina superior derecha para cerrar la página de asignación de atributo.

Ahora te has asegurado de que todos los usuarios sincronizados aparecerán en la lista global de direcciones del otro inquilino. También has agregado una expresión (Contoso) al nombre para mostrar de cada usuario sincronizado dentro del otro inquilino.

### Tarea 7: Habilitar aprovisionamiento y probar con tu asociado de laboratorio

En esta tarea, habilitarás el aprovisionamiento y probarás si tus usuarios aparecen en el otro inquilino de la manera en que los necesitas. Dado que el aprovisionamiento automático puede tardar algún tiempo, desencadenaremos un aprovisionamiento manual.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com** en la configuración de aprovisionamiento de la configuración de sincronización entre inquilinos. Si no, sigue estos 2 pasos para volver a la página de configuración:
   1. En el panel de navegación izquierdo, ve a **Identidad** > **Identidades externas** > **Sincronización entre inquilinos** > **Configuraciones**.
   1. Selecciona **Sincronización entre inquilinos de Contoso**
1. Ve a **Aprovisionamiento a petición**.
1. Busca **`Grady Archie`** como miembro del **Equipo legal** con ámbito.
1. Seleccione **Aprovisionar**.
    - Recibirás una confirmación una vez que se haya realizado el aprovisionamiento.
1. Cierra la página Realizar acción. Para ello, selecciona la **X** de la esquina superior derecha.

Acabas de aprovisionar el primer usuario manualmente y, al comprobar la lista de usuarios del inquilino asociado, verás el usuario Grady Archie (Contoso).

### Tarea 8: Implementar la sincronización completa

Dado que el primer aprovisionamiento de usuarios se realizó correctamente, ahora aprovisionarás el resto de la lista de usuarios en el otro inquilino.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com** en la página **Aprovisionamiento a petición** de la configuración de sincronización entre inquilinos. Si no, sigue estos 2 pasos para volver a la página de configuración:
   1. En el panel de navegación izquierdo, ve a **Identidad** > **Identidades externas** > **Sincronización entre inquilinos** > **Configuraciones**.
   1. Selecciona **Sincronización entre inquilinos de Contoso**
1. Selecciona **Usuarios y grupos**
1. Selecciona **Agregar usuario o grupo**.
1. En la página **Agregar asignación**, selecciona **Ninguna seleccionada**.
1. Selecciona el grupo **Todos los empleados**, ya que es el grupo que contiene **todos los empleados de Contoso**.
1. Confirme la selección.
1. Seleccione **Asignar**.

Ahora has creado correctamente una sincronización entre inquilinos entre tu inquilino y otro inquilino. Debes poder adaptar todo lo que has hecho en el inquilino de demostración al sistema productivo de Tailwind Traders y ayudarles a integrarse en Contoso.
