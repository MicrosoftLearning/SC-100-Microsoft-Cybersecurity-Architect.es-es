# Evaluación del cumplimiento

## Introducción al escenario de laboratorio

Eres Allan Deyoung, miembro del departamento de TI en Contoso Ltd. Recientemente te han transferido a la división seguridad de TI. Tu nuevo rol consiste en evaluar la preparación de Confianza cero de Contoso y desarrollar un plan de acción para establecer una iniciativa de Confianza cero, siguiendo los pilares de Confianza cero. Contoso es una gran corporación multinacional con presencia global en varios sectores. La empresa tiene una gran superficie de nube y una infraestructura híbrida. El centro de operaciones de seguridad (SOC) de Contoso es responsable de supervisar y responder a incidentes de seguridad en toda la empresa. El SOC cuenta con personal compuesto por analistas de seguridad, ingenieros de seguridad e ingenieros de red. El SOC usa Microsoft Sentinel como su solución de Administración de eventos e información de seguridad (SIEM). El SOC tiene un área de trabajo de Log Analytics que se usa para recopilar y analizar registros de seguridad de toda la empresa.

Contoso Ltd. se está expandiendo a Europa para aumentar las ventas, pero tiene problemas para satisfacer las demandas de seguridad de TI del cliente. Los clientes quieren que Contoso mantenga un entorno seguro para facilitar la colaboración segura y minimizar el riesgo de fugas de datos y activos de la empresa en peligro. Muchos clientes requieren evidencia de procesos empresariales de TI bien establecidos y un marco de seguridad sólido, que a menudo tiene la forma de una certificación ISO-27001. Para abordar esto, Contoso ha decidido contratar a una firma de auditoría externa para llevar a cabo la auditoría ISO-27001 y obtener la certificación. Es necesario evaluar la postura actual de la organización y desarrollar un plan de acción para cumplir los requisitos ISO-27001. Como arquitecto de ciberseguridad de la empresa, tienes la tarea de identificar las brechas existentes y asignar tareas específicas a las personas de la organización para resolverlas.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los desafíos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

Para abordar el problema descrito de forma eficaz, es fundamental comprender exhaustivamente la norma ISO 27001. Evaluar la configuración de Contoso con respecto a los estándares ISO 27001 es esencial, resaltando las incoherencias para el análisis. Este proceso puede llevar mucho tiempo debido a la complejidad del entorno M365 y de las regulaciones 27001. Sin embargo, la evaluación del Administrador de cumplimiento de Microsoft simplifica este análisis.

Las evaluaciones del Administrador de cumplimiento de Microsoft son agrupaciones de controles de normativas, estándares o directivas específicos. Te ayudan a asegurarte de que tu organización cumple los requisitos de diversos estándares, reglamentos o leyes. Por ejemplo, completar todas las acciones dentro de una evaluación puede alinear la configuración de Microsoft 365 con los requisitos ISO 27001. Las evaluaciones abarcan varios componentes y proporcionan plantillas para más de 360 regulaciones, ofreciendo los controles y pasos necesarios para evaluar el cumplimiento de forma eficaz. 

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Comparación del entorno M365 con las normativas ISO 27001|Administrador de cumplimiento de Microsoft Purview|Crear una valoración|
|Creación de un plan de acción|Administrador de cumplimiento de Microsoft Purview|Asignar tareas a un ingeniero técnico|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Realización de una evaluación ISO-27001

El primer paso es analizar el entorno actual de la empresa. Realizas una evaluación de cumplimiento para analizar la medida en que el entorno de Contoso cumple con las normativas ISO-27001.

1. Inicia sesión en el portal de cumplimiento Microsoft Purview **`https://purview.microsoft.com/`** como Allan Deyoung con su cuenta de administrador **MOD Administrator**.
1. Si se te pide que configures la autenticación multifactor, sigue las instrucciones.
1. Se te lleva a la nueva página de aterrizaje de Microsoft Purview portal. Selecciona el cuadro situado junto a la instrucción, **Acepto los términos de divulgación del flujo de datos y las Declaraciones de privacidad** y, luego, selecciona **Comenzar**.
1. En el panel de navegación izquierdo, selecciona **Soluciones** y luego selecciona **Administrador de cumplimiento**. Como alternativa, en la ventana principal puedes seleccionar el icono **Ver todas las soluciones** y luego seleccionar el icono **Administrador de cumplimiento** que aparece en Riesgo y cumplimiento.
1. En el panel **Administrador de cumplimiento** de la izquierda, selecciona **Evaluaciones**.
1. En la ventana **Evaluaciones**, selecciona **+ Agregar evaluación**.
1. En la ventana **Basar evaluación en una regulación**, selecciona **Seleccionar regulación**.
1. En el cuadro de texto de búsqueda, escribe **`ISO/IEC 27001:2022`**, selecciona la regulación y, a continuación, selecciona **Guardar** y luego selecciona **Siguiente**.
1. En la página **Agregar nombre y grupo**, en el cuadro de texto **Nombre de evaluación**, escribe **`ISO-27001 Audit assessment`**. Deja el ajuste **Grupo de evaluación** en **Usar grupo existente** con el **Grupo predeterminado** y, a continuación, selecciona **Siguiente**.
1. En la página **Seleccionar servicios**, el servicio **Microsoft 365** ya debería aparecer.  Si no es así, selecciona **Seleccionar servicios**, selecciona **Microsoft 365** y selecciona **Agregar**. Seleccione **Siguiente**.
1. En la página **Revisar y finalizar**, selecciona **Crear la evaluación**. La evaluación tardará unos segundos en crearse y, después, selecciona **Listo**.
1. Ahora deberías estar en la página de **evaluación de auditoría ISO-27001** recién creada.
1. Deja esta pestaña del navegador abierta para la siguiente tarea.

Has creado correctamente una evaluación basada en ISO-27001.

### Tarea 2: Asignar tareas a un ingeniero técnico

Los resultados de la evaluación muestran diferentes áreas y acciones esenciales para cumplir con las normativas ISO-27011. Investigarás las acciones de mejora y asignarás una tarea a un ingeniero técnico.

1. Todavía debes estar en la página de la evaluación que acabas de crear, **evaluación de auditoría ISO-27001**.  Si no es así, ve a Microsoft Purview portal **`https://purview.microsoft.com/`** y, desde allí, selecciona **Soluciones** > **Administrador de cumplimiento** > **Evaluaciones** > **Evaluación de auditoría ISO-27001**
1. En la página **Evaluación de auditoría ISO-27001**, selecciona **Tus acciones de mejora**.
1. Establece el filtro de la **familia de controles** en **Controles físicos**.
1. Selecciona el cuadro situado junto a **Acción de mejora** para seleccionar todas las acciones de mejora mostradas y, a continuación, selecciona **Asignar al usuario** (que aparece encima de las opciones de filtros).
1. En la nueva ventana **Asignar acciones de mejora**, en el cuadro de texto de búsqueda, escribe **`Nestor`** y presiona Entrar.
1. Selecciona el usuario y selecciona **Asignar**.
1. Mantén esta pestaña del navegador abierta para la siguiente tarea.

Has visto y asignado correctamente una acción de mejora a un ingeniero técnico

### Tarea 3: Proporcionar acceso a un ingeniero técnico para las acciones de mejora

Los usuarios necesitan acceso para ver las tareas que tienen asignadas. Concederás acceso a Nestor Wilke a la evaluación.

1. Todavía debes estar en la pestaña **Tus acciones de mejora** para la página **Evaluación de auditoría ISO-27001**.  Si no es así, ve a Microsoft Purview portal **`https://purview.microsoft.com/`** y, desde allí, selecciona **Soluciones** > **Administrador de cumplimiento** > **Evaluaciones** > **Evaluación de auditoría ISO-27001** > **Tus acciones de mejora**.
1. En la esquina superior derecha de la página **ISO/IEC 27001:Evaluación**, selecciona **Administrar acceso de usuario**.
1. En la nueva ventana **Administrar acceso de usuario**, selecciona la pestaña **Evaluador** y selecciona **Agregar evaluadores**.
1. En el cuadro de texto **Buscar usuarios**, escribe **`Nestor`** y presiona Entrar.
1. Selecciona el usuario, selecciona **Aplicar** y, a continuación, selecciona **Guardar**.
1. Has concedido correctamente a Nestor Wilke el rol de Evaluador para esta evaluación.
1. Ahora puedes cerrar la pestaña del navegador para salir de Microsoft Purview portal.

Has concedido correctamente a Nestor Wilke el rol de Evaluador para esta evaluación.
