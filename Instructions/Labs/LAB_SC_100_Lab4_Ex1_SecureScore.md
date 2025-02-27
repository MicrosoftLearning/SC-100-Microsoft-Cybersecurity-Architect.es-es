# Laboratorio 4: ejercicio 1: Administración de la posición de seguridad

Contoso quiere mejorar su posición de seguridad con la herramienta Puntuación de seguridad de Microsoft, que proporciona recomendaciones e instrucciones sobre cómo reducir la superficie expuesta a ataques y protegerse de las amenazas. Contoso tiene un equipo de seguridad dedicado que administra el panel de Puntuación de seguridad y asigna acciones a diferentes equipos de productos en función de sus roles y responsabilidades. Uno de los equipos de productos, Mark 8 Project Team, es responsable de la administración de dispositivos móviles y necesita asegurarse de que los dispositivos se bloqueen después de un período de inactividad para evitar el acceso no autorizado.

## Parte 1: Diseñar una solución (necesaria)

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Obtener más recomendaciones para aumentar la posición de seguridad
- Conceder acceso limitado a la recomendación 
- Informar al equipo responsable

Puntuación de seguridad de Microsoft evalúa la posición de seguridad de una organización en todas las cargas de trabajo de Microsoft 365. Proporciona visibilidad centralizada, información con priorización de amenazas y controles completos para mejorar la protección contra los ciberataques y optimizar la ciberseguridad.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Añadir más recomendaciones para aumentar la posición de seguridad | Orígenes de datos adicionales | Habilitar orígenes de "no carga de trabajo" adicionales |
|Conceder acceso limitado a la recomendación |Permisos y roles de Defender XDR |Conceder acceso específico a Joni Shermann |
|Informar al equipo responsable |Puntuación segura |Informar a Mark 8 Project Team |

### Diseñar ventajas y soluciones alternativas

## Parte 2: Implementar la solución (opcional)

### Tarea 1: configurar orígenes de datos adicionales en Puntuación de seguridad

En esta tarea, habilitarás orígenes de datos adicionales para Puntuación de seguridad para obtener más recomendaciones sobre la superficie expuesta a ataques.

1. Inicia sesión en la máquina virtual Cliente 1 (LON-SC1) como cuenta **lon-sc1\admin**. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a <https://security.microsoft.com> e inicia sesión en el Centro de administración de Microsoft 365 como **Administrador MOD**<admin@WWLxZZZZZZ.onmicrosoft.com> (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje de laboratorio). La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.
3. En el cuadro de diálogo **¿Mantener la sesión iniciada?**, activa la casilla **No volver a mostrar esto** y, a continuación, selecciona **No**.
4. Se te pedirá que configures la autenticación multifactor y sigas las instrucciones.
5. Cierra el cuadro de diálogo Guardar la contraseña de la parte inferior. Para ello, selecciona **Nunca** para no guardar las credenciales predeterminadas de administradores globales en el navegador.
6. En el panel de navegación de la izquierda, selecciona **Configuración**.
7. Seleccione **Microsoft Defender XDR**.
8. En General, selecciona **Permisos y roles**.
9. Es posible que tengas que esperar unos minutos hasta que Microsoft Defender XDR se configure.
10. Habilita **Orígenes de datos adicionales**.
11. Vuelve al panel de Puntuación de seguridad

Has habilitado correctamente Orígenes de datos adicionales para configurar el acceso basado en roles a recomendaciones de productos específicos.

### Tarea 2: Configurar RBAC para Puntuación de seguridad

En esta tarea, tendrás que asegurarte de que solo las personas seleccionadas puedan acceder a esta información. Habilita RBAC para Puntuación de seguridad y básalo en el concepto de acceso con privilegios mínimos.

1. Deberías seguir con la sesión iniciada en el portal de Microsoft Defender XDR.
2. En el panel de navegación de la izquierda, selecciona **Configuración**.
3. Seleccione **Microsoft Defender XDR**.
4. Selecciona **Permisos y roles**.
5. Selecciona **Ve a roles y permisos**.
6. Selecciona **Crear rol personalizado**.
7. Nombre del rol: SecureScore Apps
8. Seleccione **Siguiente**.
9. Haz clic en **Posición de seguridad**, selecciona **Seleccionar permisos personalizados** y selecciona **Seleccionar permisos personalizados**.
10. Elige **Puntuación segura (administrar)** .
11. Seleccione **Aplicar**.
12. Seleccione **Siguiente**.
13. Seleccione **Agregar asignación**.
14. Nombre de asignación: Administrador de SecureScore
15. Asígnalo a **Joni Sherman**. 
16. En **Orígenes de datos**, **desactiva** todo excepto **Puntuación de seguridad de Microsoft: orígenes de datos adicionales**.
17. Selecciona **Agregar**.
18. Selecciona **Siguiente**.
19. Selecciona **Enviar**.

Has implementado correctamente RBAC para acceder a las recomendaciones de orígenes de datos adicionales para Joni Sherman en la puntuación de seguridad.

### Tarea 3: Delegar una acción

El equipo de proyectos de Mark 8 de Contoso es responsable del desarrollo posterior de la administración de dispositivos móviles, por lo que informará al equipo del proyecto sobre la recomendación de seguridad.

1. Deberías seguir con la sesión iniciada en el portal de Microsoft Defender XDR.
2. Selecciona **Puntuación de seguridad** en el panel de navegación izquierdo.
3. En la pestaña, selecciona **Acciones recomendadas**.
4. Busca **Asegurarse de que los dispositivos se bloquean después de un período de inactividad para evitar el acceso no autorizado** y selecciónalo.
5. Selecciona **Compartir** y, en el menú desplegable, selecciona **Microsoft Teams**.
6. En el campo **Equipo**, selecciona **Mark 8 Project Team** y, en el campo **Canal**, selecciona **Investigación y desarrollo del canal**.
7. Selecciona **Publicar mensaje en Teams**.

Joni Sherman y su equipo de proyectos de Mark 8 recibirán una notificación sobre la acción recomendada en su canal de equipos.

### Tarea 4: Administrar recomendaciones

Igual que Joni Sherman, has recibido la notificación de los equipos de que se ha recomendado una acción específica para aumentar la posición de seguridad y se va a administrar la acción recomendada y documentar la solución.

En esta tarea, administrarás la acción recomendada y documentarás las soluciones.

1. Abre una ventana inPrivate de Microsoft Edge, ve a <https://office.com> e inicia sesión como <JoniS@WWLxZZZZZZ.onmicrosoft.com>.
2. Abre Teams y abre el canal **Investigación y desarrollo** en **equipo de proyectos de Mark 8**.
3. Revisa el mensaje publicado en la acción Puntuación de seguridad.
4. Abre otra pestaña en la ventana inPrivate de Microsoft Edge y ve a <https://security.microsoft.com>.
5. Selecciona **Puntuación de seguridad** en el panel de navegación izquierdo.
6. Selecciona la pestaña **Acciones recomendadas** para ver todas las acciones a las que tienes acceso.
7. Busca **Asegurarse de que los dispositivos se bloquean después de un período de inactividad para evitar el acceso no autorizado** y selecciónalo.
8. Seleccione **Editar estado y plan de acción**.
9. Marca **Resuelto a través de tercero**.
10. Agrega una nota **Protegida actualmente con JAMF** al campo **Plan de acción**.
11. Selecciona **Guardar y cerrar**.

Has configurado correctamente las cargas de trabajo adicionales para la puntuación de seguridad, el permiso asignado en función del acceso con privilegios mínimos y las acciones recomendadas administradas y delegadas para el equipo de identidad de Contoso Ltd.
