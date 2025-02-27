---
lab: 3
title: 'Ejercicio 5: Directivas de retención'
---

# Laboratorio 3 - Ejercicio 5: Directivas de retención

Recientemente, el gobierno alemán modificó leyes específicas que rigen los períodos de retención para las empresas. Un cambio significativo es que todos los documentos financieros ahora deben conservarse durante 11 años, en lugar del requisito anterior de 10 años. Otro cambio es que la correspondencia comercial o empresarial, incluidas las copias de la correspondencia comercial o empresarial enviada, ahora se pueden conservar durante 5 años en lugar de 7. Actualmente, tu empresa se adhiere a una directiva de retención que mantiene todos los documentos durante un período de 7 años. Sin embargo, Contoso Ltd. ha encontrado dificultades en los últimos años debido a la acumulación de un gran volumen de datos en su entorno. Esto ha provocado un aumento de los costos de mantenimiento y un consumo significativo de espacio de almacenamiento. Tu asignación consiste en optimizar la directiva de retención de tu empresa para cumplir las normativas legales, a la vez que se minimizan los requisitos de almacenamiento de datos. La directiva de la empresa dicta que todos los datos deben conservarse durante al menos cinco años después de su creación, en cumplimiento estricto de todas las leyes aplicables que rigen la retención de datos.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los desafíos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del problema descrito y comprender los objetivos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Conservar todos los datos financieros durante 11 años
- Conservar toda la correspondencia comercial durante 5 años
- Minimización de la sobrecarga de almacenamiento de datos

En el segundo paso, examina el entorno existente de Contoso Ltd. Contoso tiene varias soluciones para conservar los datos durante un tiempo específico. Tu tarea consiste en analizar la configuración actual y decidir si cumplen los requisitos legales. 

La tercera fase implica la elaboración del concepto de la solución. Después de una investigación exhaustiva, queda claro que ninguna de las directivas existentes cumple los criterios especificados. Por lo tanto, es esencial un nuevo conjunto de directivas.

En función del escenario anterior, se puede usar Administración del ciclo de vida de Microsoft Purview para conservar los datos adecuadamente.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Conservar todos los datos financieros durante 11 años| Administración del ciclo de vida de los datos de Microsoft Purview|Crear y aplicar automáticamente una etiqueta de retención|
|Conservar toda la correspondencia comercial durante 5 años| Administración del ciclo de vida de los datos de Microsoft Purview|Implementar una directiva de retención|


## Parte 2: Implementar la solución (opcional)

### Tarea 1: Analizar la estructura actual de la directiva de retención

En esta tarea, te familiarizarás con la directiva de retención existente de tu empresa. Echarás un vistazo a diferentes directivas de retención, etiquetas y directivas de etiquetas. Usarás el módulo PowerShell Seguridad y Cumplimiento y verás las directivas existentes. Investigarás la configuración actual y decidirás si las directivas de retención existentes son suficientes para que Contoso Ltd. cumpla los requisitos legales. 

>[!NOTE] Ya debes haber instalado el módulo de PowerShell de Exchange Online. Si falta el módulo, sigue las instrucciones para instalar el módulo.

1. Abre una ventana de PowerShell elevada. Para ello, selecciona el botón Windows con el botón secundario del mouse y, a continuación, selecciona **Windows PowerShell (Admin)**.
1. Confirma la ventana **Control de cuentas de usuario** con **Sí**.
1. Escribe el siguiente cmdlet para instalar la versión más reciente del módulo Exchange Online PowerShell:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirma el cuadro de diálogo de seguridad de repositorio no de confianza con **Y** para Sí y presiona **Entrar**.  Este proceso puede tardar un tiempo en finalizar.
1. Escribe el siguiente cmdlet para conectarte a Security & Compliance PowerShell:

    ```powershell
    Connect-IPPSSession
    ```
1. Escribe el siguiente cmdlet para ver las directivas de retención y la configuración existentes:

    ```powershell
     Get-ComplianceTag | Format-Table -Auto Name,Priority,RetentionAction,RetentionDuration,Workload
    ```
1. Dedica algo de tiempo a evaluar la tabla resultante.

>[!NOTE] También puedes acceder al portal de cumplimiento de Microsoft Purview para ver las directivas de retención, pero tienes que examinar cada directiva una por una en lugar de obtener información general sobre todas las directivas de un vistazo.

Has visto correctamente las etiquetas y la configuración existentes para decidir si cumplen los requisitos legales.

### Tarea 2: Crear una directiva de retención

Has evaluado eficazmente las directivas de retención de Contoso Ltd., y has descubierto una configuración obsoleta que no cumple los estándares legales. Tu investigación reveló cinco directivas de retención que comparten una configuración idéntica, con solo una etiqueta de retención aplicada, ninguna de las cuales aborda adecuadamente los requisitos legales.

El plan implica implementar una nueva directiva de retención para toda la empresa con un período de retención de cinco años. Después de este período de tiempo, se pueden conservar los datos, pero no es obligatorio para su eliminación. Este ajuste satisface los requisitos legales para los períodos de retención mínimos y reduce la sobrecarga de los datos.

1. Inicia sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung con su cuenta de administrador **Administrador de MOD**.
1. Selecciona **Administración del ciclo de vida de datos** > **Microsoft 365**.
1. En la página **Administración del ciclo de vida de datos**, selecciona la pestaña **Directivas de retención** y selecciona **+ Nueva directiva de retención**.
1. En la página **Nombrar directiva de retención**, escribe la información siguiente:
    - **Nombre**: Directiva de retención general
    - **Descripción**: esta directiva es la directiva de retención predeterminada para toda la organización. Todos los datos deben conservarse durante al menos 5 años. 
1. Seleccione **Siguiente**.
1. En la página **Ámbito de directiva**, selecciona **Siguiente**.
1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Estático** y selecciona **Siguiente**.
1. En la página **Elegir dónde aplicar esta directiva**, habilita las siguientes ubicaciones:

    - Buzones de Exchange
    - Sitios clásicos y de communciación de SharePoint
    - Cuentas de OneDrive
    - Buzones y sitios de grupo de Microsoft 365

1. Seleccione**Siguiente**.
1. En la página **Decidir si deseas conservar el contenido, eliminarlo o ambos**, escribe la siguiente configuración:

    - **Retener los elementos durante un período específico**: 5 años.
    - **Iniciar el período de retención en función de**: cuándo se crearon los elementos
    - **Al final del período de retención**: no hacer nada

1. Seleccione **Siguiente**.
1. En la página **Revisar y finalizar**, seleccione **Enviar**.

Has creado correctamente una directiva de retención. Ahora puedes eliminar todas las directivas de retención restantes, ya que no cumplen los requisitos de la empresa.

### Tarea 3: Crear una etiqueta de retención

Para cumplir las regulaciones alemanas, ahora crearás una etiqueta de retención con un período de retención de 11 años y la aplicarás automáticamente a todos los documentos que contienen datos financieros alemanes.

1. Todavía deberías tener iniciada la sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/**.
1. En el portal de cumplimiento de Microsoft Purview, en la página de navegación izquierda, expande **Administración del ciclo de vida de datos** y selecciona **Microsoft 365**.
1. En la página **Administración del ciclo de vida de datos**, selecciona la pestaña **Etiquetas** y selecciona **+ Crear una etiqueta**.
1. En la página **Nombrar etiqueta de retención**, escribe la información siguiente:

    - **Nombre**: Datos financieros alemanes
    - **Descripción para los usuarios**: esta etiqueta conserva todos los datos financieros alemanes durante 11 años
    - **Descripción para los administradores**: la etiqueta conserva todos los datos financieros durante 11 años y se aplica automáticamente.

1. Seleccione **Siguiente**.
1. En la página **Definir configuración de etiqueta**, selecciona **Aplicar acciones después de un período específico** y selecciona **Siguiente**.
1. En la página **Definir el periodo**, escribe la siguiente información:

    - **¿Cuánto tiempo dura el periodo?**: 11 años
    - **¿Cuándo debe comenzar el período?**: cuándo se crean los elementos

1. Seleccione **Siguiente**.
1. En la página **Elegir lo que sucede después del periodo**, selecciona **Eliminar elementos automáticamente**.
1. En la página **Revisar y finalizar**, selecciona **Crear etiqueta**.
1. En la página **Se ha creado la etiqueta de retención**, selecciona **Aplicar automáticamente esta etiqueta a un tipo de contenido específico** y selecciona **Listo**.
1. En la página **Comencemos**, escribe la siguiente información:

    - **Nombre**: Conservar automáticamente todos los datos financieros alemanes durante 11 años
    - **Descripciones**: esta directiva aplica automáticamente la etiqueta **Datos financieros alemanes**.

1. Seleccione **Siguiente**.
1. En la página **Elegir el tipo de contenido al que deseas aplicar esta etiqueta**, selecciona **Aplicar etiqueta al contenido que contiene información confidencial** y selecciona **Siguiente**.
1. En la página **Contenido que contiene información confidencial**, establece el filtro en **Alemania**, selecciona **Datos financieros alemanes**, a continuación, **Datos financieros de Alemania** y, a continuación, selecciona **Siguiente**.
1. En la página **Definir contenido que contiene información confidencial**, selecciona **Siguiente**.
1. En la página **Ámbito de directiva**, selecciona **Siguiente**.
1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Estático**.
1. En la página **Elegir dónde aplicar automáticamente la etiqueta**, habilita las siguientes ubicaciones:

    - Buzones de Exchange
    - Sitios de SharePoint de comunicación y clásicos
    - Cuentas de OneDrive
    - Buzones y sitios de grupo de Microsoft 365

1. Seleccione **Siguiente**.
1. En la página **Elegir una etiqueta para aplicar automáticamente**, selecciona **Siguiente**.
1. En la página **Decidir si se va a probar o ejecutar la directiva**, selecciona **Activar directiva** y, después, selecciona **Siguiente**.
1. En la página **Revisar y finalizar**, seleccione **Enviar**.

Has creado correctamente y aplicado automáticamente una etiqueta de retención.
