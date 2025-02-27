---
lab: 3
title: 'Ejercicio 2: delegar solicitudes de derechos del interesado'
---


# Laboratorio 3: ejercicio 2: delegar solicitudes de derechos del interesado

Contoso Ltd. está preparando la certificación ISO-27001. Como parte de esta preparación, tiene que implementar un proceso para las solicitudes de derechos del interesado del RGPD. La empresa usará la característica Solicitudes de datos personales Microsoft Priva e integrará el nuevo flujo de trabajo en su proceso de auditoría de cumplimiento interno. 

Como arquitecto de ciberseguridad experto, delegarás el control de las DSR europeas y configurarás permisos de lectura para la auditoría. Para asegurarte de que los empleados que controlan los casos de DSR no controlan también la característica Administración de riesgos de Privacidad, crearás un grupo de roles de solo vista personalizado. Los grupos de roles integrados conceden demasiados permisos para la auditoría. 

Asignarás a los empleados elegidos los roles necesarios para controlar las solicitudes de derechos del interesado o la auditoría, siguiendo el principio de privilegios mínimos. Para completar la POC, usarás la versión de prueba de Microsoft Priva y te asegurarás de que los registros de auditoría estén activados en el inquilino. Dado que la auditoría de cumplimiento se realiza de forma bimensual, aumentarás la duración de la retención de solicitudes de derechos del interesado para eliminar los puntos ciegos entre las auditorías. 

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los requisitos que Contoso Ltd. enfrenta con su expansión a Europa.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Permite que el entorno controle las solicitudes de los interesados
- Un equipo designado debe controlar las DSR
- Es necesario modificar los límites de retención de las DSR para cumplir con la programación de auditorías

En el segundo paso, examina el entorno existente de Contoso Ltd. Microsoft Priva ofrece soluciones para administrar las solicitudes de los interesados. Investiga qué controles existen y qué directivas ya están en vigor. Usa el portal de cumplimiento de Microsoft Purview para revisar las configuraciones actuales y determinar a qué ajustes se deben implementar para cumplir los requisitos de la región a la que se expanden.

La tercera fase implica la elaboración del concepto de la solución. Tras la investigación, es evidente que permitir que empleados específicos administren las DSR es la mejor manera de cumplir todos los requisitos.  

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Permite que el entorno controle las solicitudes de los interesados|Microsoft Purview y Centro de administración|Asigna licencias Priva y comprueba que el registro de auditoría unificado está habilitado|
|Un equipo designado debe controlar las DSR|Roles de Microsoft Purview|Crea un grupo de roles con permisos para controlar las solicitudes del interesado y asigna a los empleados designados|
|Es necesario modificar los límites de retención de las DSR para cumplir con la programación de auditorías|Administración de riesgos de Privacidad de Microsoft Purview|Usa una acción de mejora para establecer un límite de retención de 90 días para DSR|

## Parte 2: Implementar la solución (opcional)

## Tarea 1: activar la licencia de prueba de Microsoft Priva

En las dos primeras tareas, comprobarás las condiciones previas necesarias para usar las características de Microsoft Priva. Tienes que activar la licencia de prueba de Microsoft Priva y asegurarte de que los registros de auditoría estén habilitados en el inquilino.

1. Inicia sesión en **VM** con tus credenciales de administrador.
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **https://compliance.microsoft.com** e inicia sesión en el portal de cumplimiento Microsoft Purview como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje de laboratorio). Escribe la contraseña de administrador que debería haberte proporcionado tu proveedor de hospedaje de laboratorio.
3. Cuando se te pregunte si deseas mantener la sesión iniciada, selecciona **No**.
4. En el panel izquierdo, selecciona **Administración de riesgos de privacidad: información general**) o **Solicitudes de derechos del interesado**.
5. Si la versión de prueba no está activa, selecciona **Activar prueba** en la parte superior de la página.

Si la versión de prueba ya está activa en el laboratorio, todavía tienes que comprobar la cantidad exacta de casos de solicitudes de derechos del interesado contenidas en la licencia en el centro de administración.

6. **Inicia sesión** en el **Centro de administración de Microsoft 365****https://admin.microsoft.com/**.
7. En el panel izquierdo, selecciona **Facturación** y **Tus productos**.
8. Busca la licencia de **Administración de riesgo de privacidad Priva**.
9. Busca la **Administración de privacidad: licencia de solicitud de derechos del interesado** y el número de casos incluidos.

Has comprobado correctamente si el inquilino de M365 tiene licencias activas de Microsoft Priva.

## Tarea 2: Comprobación de si los registros de auditoría están habilitados

Para que las características de administración de riesgos de privacidad funcionen, el registro de auditoría debe estar activo en el inquilino.

1. Abre una ventana de **PowerShell** con permisos elevados. Para ello, selecciona el menú Inicio con el botón derecho del ratón y luego selecciona **Windows PowerShell** y **Ejecutar como administrador**.
2. Escribe el siguiente cmdlet para instalar la versión más reciente del módulo Exchange Online:
    ```powershell
    Install-Module -Name ExchangeOnlineManagement
    ```
3. Confirma el cuadro de diálogo seguridad de Nuget y el cuadro de diálogo seguridad de repositorio no de confianza con Y para Sí y presiona Entrar. Este proceso puede tardar en completarse.
4. Escribe el siguiente cmdlet para conectarte al servicio Exchange Online:
    ```powershell
    Connect-ExchangeOnline
    ```
5. En el formulario **Iniciar sesión en tu cuenta** , inicia sesión con tus credenciales de administrador.
6. Después de conectarte correctamente a Exchange Online PowerShell, escribe:
    ```powershell
    Get-AdminAuditLogConfig | Format-List UnifiedAuditLogIngestionEnabled
    ```
7. Se devuelve un **valor True** para _UnifiedAuditLogIngestionEnabled_ .
8. Si se devuelve un **valor False** , habilita el registro de auditoría con el comando:
    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```
9. Se devuelve una advertencia de que el cambio puede tardar hasta 60 minutos en surtir efecto. El registro de auditoría ahora está activado en el inquilino. Puedes volver a comprobarlo más adelante con el comando mencionado antes.

Has confirmado correctamente que los registros de auditoría están habilitados en el inquilino.

## Tarea 3: Crear un grupo de roles personalizado y asignarle los empleados designados

En esta tarea, crearás el grupo de roles de solo lectura personalizado para la auditoría de cumplimiento de Contoso Ltd. y asignarás a los empleados designados.

1. Inicia sesión en el **portal de cumplimiento Microsoft Purview****https://compliance.microsoft.com/**.
2. Selecciona la pestaña **Permisos** en la pestaña **Roles y ámbitos** del panel izquierdo.
3. Selecciona **Roles** en el elemento de soluciones de Microsoft Purview.
4. Crea un nuevo grupo de roles con la siguiente configuración:
    |Configuración|Valor|
    |----|----|
    |Nombre|Solo vista de auditoría de cumplimiento interno|
    |Descripción|Este grupo de roles contiene todos los roles necesarios para la auditoría bimensual de la posición de cumplimiento de Contoso Ltd.|
    |Roles|Registros de auditoría de solo vista, Caso de solo vista, Visor de administración de Priva|
    |Usuarios|Grady Archie|
5. Selecciona **Siguiente** en **Agregar roles al grupo de roles** y continúa con la siguiente tarea sin cerrar el diálogo.

Has creado correctamente un grupo de roles personalizado con los permisos mínimos necesarios y le has asignado los empleados designados.

## Tarea 4: Asignar empleados y a ti mismo a los grupos de roles integrados

Ahora tienes que asignar los permisos restantes para la administración de solicitudes de derechos del interesado mediante los grupos de roles integrados.

*(Ve a 4. si todavía estás en el menú Roles y ámbitos)*
1. **Inicia sesión** en el **portal de cumplimiento Microsoft Purview****https://compliance.microsoft.com/**.
2. Selecciona **Roles y ámbitos** > **Permisos** en el panel izquierdo.
3. Selecciona **Roles** en **Soluciones de Microsoft Purview**.
4. Agrega **Irvin Sayers** al grupo de roles **Administradores de solicitudes de derechos del interesado**.
5. Agrega **Alex Wilber** y **Joni Sherman** al grupo de roles **Aprobadores de solicitudes de derechos del interesado**.
6. Agrega la cuenta de administrador **Administrador MOD** y **Megan Bowen** a los grupos de roles **Administradores de administración de privacidad** y **Administradores de solicitudes de derechos del interesado**.

Ahora has asignado todos los permisos necesarios a todos los empleados para controlar las solicitudes de derechos del interesado.

## Tarea 5: Configurar el límite máximo de retención de datos para las solicitudes de derechos del interesado

Para la auditoría de cumplimiento bimensual, debes configurar el límite de retención para las solicitudes de derechos del interesado en esta tarea.

[!NOTE] Los cambios en los grupos de roles pueden tardar hasta 30 minutos en aplicarse, por lo que debes ver la característica de solicitud de derechos del interesado. Si acabas de concederte los permisos en la tarea 4, es posible que tengas que esperar a que los cambios surtan efecto.

1. **Inicia sesión** en el **portal de cumplimiento Microsoft Purview****https://compliance.microsoft.com/**.
2. En el panel izquierdo, selecciona **Administrador de cumplimiento** y, a continuación, selecciona la pestaña **Acciones de mejora**.
3. En la parte superior de la página, selecciona el filtro **Soluciones:** y activa **Administración de riesgo de privacidad Priva** y **Solicitudes de los interesados Priva**.
4. Selecciona **Habilitar y aplicar límites de retención de datos para los datos implicados en la solicitud de derechos del interesado**
5. Haz clic en **Asignar al usuario** > Buscar **Administrador MOD** > **Asignar**, que asigna el Administrador MOD como propietario de la acción de mejora.
6. Lee los detalles de la mejora.
7. Selecciona **Iniciar ahora** en la parte inferior de la descripción para especificar directamente la configuración de la solicitud de derechos del interesado.
8.  Selecciona la pestaña **Períodos de retención de datos**.
9.  Establece el valor **Datos recopilados e informes** en 90 días y selecciona **Guardar**
10. Cierra la pestaña en Edge.
11. Selecciona **Editar detalles** en la parte superior de la página de la acción de mejora.
12. Establece el **estado de implementación** en **Implementado**.
13. En la parte inferior de la página, selecciona **Guardar y cerrar**.

Has aumentado correctamente el límite de retención de datos de solicitud de derechos del interesado y has actualizado la acción de mejora.

Has terminado la configuración de la característica de solicitudes de derechos del interesado y los casos de control delegados en consecuencia. Puedes continuar con el ejercicio siguiente.
