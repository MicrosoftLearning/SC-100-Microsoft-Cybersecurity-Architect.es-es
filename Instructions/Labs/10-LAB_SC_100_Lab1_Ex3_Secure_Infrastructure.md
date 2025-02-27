# Protección de la infraestructura

Contoso Ltd. adquirió recientemente Tailwind Traders, que todavía usa servidores de archivos locales para el almacenamiento. Como arquitecto de ciberseguridad de Contoso Ltd., quieres evaluar una solución para proteger estos servidores de archivos con tu entorno de nube existente. Tailwind Traders te proporcionó un servidor de prueba (The Lab VM 2) que puedes usar para la implementación de la POC. En este ejercicio, configurarás el servidor y lo integrarás en tu entorno de infraestructura y seguridad en la nube mediante Azure Arc y enviarás registros del servidor a Defender for Cloud.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para proteger el entorno local dentro de la infraestructura en la nube.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Habilitación de Defender for Cloud en la suscripción
- Los servidores locales deben protegerse
- Los registros deben almacenarse de manera que la solución SIEM de Contoso pueda procesarlos.
- Evaluación del estado de cumplimiento de los recursos de implementación

En el segundo paso, examina el entorno existente de Contoso Ltd. Defender for Cloud proporciona recomendaciones para proteger los recursos locales y en la nube mediante la identificación de los pasos para mejorar la configuración y la implementación. Al supervisar activamente las cargas de trabajo, mejora la posición general de seguridad y reduce la exposición a las amenazas.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Habilitación de Defender for Cloud en la suscripción| Defender para la nube | Activación de planes de Defender en Defender for Cloud |
|Los servidores locales deben protegerse | Azure Arc | Incorporación del servidor local al entorno en la nube |
|Los registros deben almacenarse de manera que la solución SIEM de Contoso pueda procesarlos. |Defender for Cloud, DataCollectionRules, Agente de AzureMonitoring, área de trabajo de Log Analytics | Creación de una regla de recopilación de datos para recopilar registros del servidor local de Contoso |
|Evaluación del estado de cumplimiento de los recursos de implementación | Directivas de seguridad de Microsoft Defender for Cloud| Habilita el cumplimiento de NIST SP 800-53 Rev.5 y evalúa el estado de cumplimiento.|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Crear un área de trabajo de Log Analytics

En esta tarea, crearás un área de trabajo de Log Analytics que es necesaria para hospedar los datos que se envían desde distintos recursos.

1. Inicia sesión en la máquina virtual Cliente 1 (LON-SC1) como cuenta **lon-sc1\admin**. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **`https://portal.azure.com`** e inicia sesión en Azure Portal como usuario **User1-*******@LODSUATMCA.onmicrosoft.com** (donde ****** es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
1. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla No volver a mostrar esto y, a continuación, selecciona **No**.
1. Cierra el cuadro de diálogo guardar contraseña de la parte inferior. Para ello, selecciona Nunca, para no guardar las credenciales predeterminadas de administradores globales en el explorador.
1. Cancela la pantalla Bienvenida a Microsoft Azure.
1. Selecciona **Crear un recurso** y busca **área de trabajo de Log Analytics**
1. Busca el icono **Área de trabajo de Log Analytics** y selecciona **Crear**.
1. En el sitio Crear área de trabajo de Log Analytics, crea un nuevo **Grupo de recursos** y asígnale el nombre **`ContosoRG`**.
1. En Detalles de la instancia, escribe el nombre **`ContosoLA`**, selecciona **Este de EE. UU** para la región.
1. Selecciona **Revisar y crear**
1. Seleccione **Crear** para iniciar la implementación.

Has creado correctamente el área de trabajo de Log Analytics.

### Tarea 2: Habilitar Defender for Cloud

Antes de que Defender for Cloud pueda aplicar protecciones a los recursos, debes habilitar los planes de Defender para los tipos de recursos que deseas proteger.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
1. Busca y abre **Microsoft Defender for Cloud**.
1. En el panel de navegación de la izquierda, expande **Administrar** y selecciona **Configuración del entorno**.
1. Selecciona **Expandir todo** y selecciona la suscripción.
1. Si la suscripción se muestra como **no registrada**, vuelve a cargar la página.
1. Selecciona los puntos suspensivos (...) junto a la suscripción y selecciona **Editar configuración**.
1. En **Protección de cargas de trabajo en la nube**, establece el control deslizante **Plan de servidores** de la derecha en **Activado**.
1. En la parte superior de la página, selecciona **Guardar**.

Al habilitar el plan para servidores, puedes ver que Defender for Cloud admite muchos más tipos de recursos.

### Tarea 3: Habilitación del servidor local en Azure Arc

Azure Arc es necesario para que se pueda usar para enviar datos al área de trabajo de Log Analytics que usa Defender for Cloud.

1. Cambia a la máquina virtual **LON-SC2** e inicia sesión en Azure Portal**`https://portal.azure.com`**.
1. Busca **`Azure Arc`** y ábrelo.
1. En el panel de navegación de la izquierda, expande **Recursos de Azure Arc** y selecciona **Máquinas**.
1. Selecciona **Agregar o crear** > **Agregar máquina**.
1. En Agregar un solo servidor, selecciona **Generar script**.
1. En el campo Grupo de recursos, usa el menú desplegable para seleccionar **ContosoRG**.
1. En el campo Región, usa el menú desplegable para seleccionar **Este de EE. UU**.
1. Seleccione **Descargar y ejecutar el script**.
1. Selecciona **Descargar** y ejecutar script en el segundo **LON-SC2** del cliente de laboratorio para incorporar el servidor local a Azure.
1. Ejecute Windows PowerShell como administrador. Para ello, usa el botón derecho del ratón para seleccionar el icono de Windows en la esquina inferior derecha de la ventana y selecciona **Windows PowerShell(Admin)**
1. Establece la directiva de ejecución en Sin restricciones.

    ```Powershell
    Set-ExecutionPolicy -ExecutionPolicy unrestricted
    ```

1. En las ventanas de PowerShell, selecciona Y.
1. Copia el script de incorporación. Para ello, selecciona el explorador de archivos. Debe llevarte a la carpeta de descargas de la unidad C local de la máquina virtual del servidor. Usa la tecla del mouse derecho para seleccionar el archivo **OnboardingScript** y selecciona **Ejecutar con **PowerShell**.
1. Cuando aparezca el elemento emergente de autenticación, inicia sesión con la misma cuenta que usas para Azure Portal.
1. Espera a que el trabajo se complete correctamente.
1. Vuelve a LON-SC1 y abre Azure Arc.
1. Selecciona **Máquinas**, selecciona **Actualizar** en la parte superior de la página y comprueba que el servidor se ha implementado correctamente en Azure Arc.

Habilitaste correctamente Azure Arc en el servidor de pruebas y los datos deben empezar a fluir al área de trabajo de Log Analytics. Este proceso puede tardar algún tiempo hasta que puedas ver algo en el panel de información.

### Tarea 4: Agregar servidor a Defender for Cloud y recopilar registros.

Implementarás una regla de recopilación de datos para obtener registros de eventos del servidor local. La regla implementará automáticamente el agente de supervisión en el servidor y reenviará los registros al área de trabajo de Log Analytics creada anteriormente.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
1. Abre Defender for Cloud.
1. En el panel de navegación de la izquierda, expande **Administrar** y selecciona **Configuración del entorno**.
1. Seleccione **Expandir todo**.
1. Verás el área de trabajo de Log Analytics creada anteriormente, **ContosoLA**.  
1. Selecciona los puntos suspensivos (...) para el **elemento de línea ContosoLA** y, a continuación, selecciona **Editar configuración**.
1. Establece el control deslizante **Plan de servidores** de la derecha en **Activado**.
1. En la parte superior de la página, selecciona **Guardar**.
1. Usa la barra de búsqueda de la parte superior para buscar **reglas de recopilación de datos** y luego selecciona la regla en los resultados de búsqueda.
1. Seleccione **Crear**.
1. - Nombre de la regla: **`ContosoDCR`**
   - Grupo de recursos: **ContosoRG**
1. Seleccione **Siguiente: Recursos**.
1. Seleccione **Agregar recursos**. Expande el ámbito del grupo de recursos. Comprueba la máquina de Azure Arc incorporada anteriormente y selecciona **Aplicar**.
1. Seleccione **Siguiente: Recopilar y entregar**.
1. Seleccione **Add data source**(Agregar origen de datos).
1. Elige el tipo de origen de datos **Registros de eventos de Windows**.
1. Selecciona cada opción en **Configurar los niveles y registros de eventos que se van a recopilar:**.
1. Seleccione **Siguiente: Destino**.
1. Selecciona **Agregar destino**.
   - Tipo de destino: **Registros de Azure Monitor**.
   - Cuenta o espacio de nombres: **ContosoLA**
1. Seleccione **Add data source**(Agregar origen de datos).
1. Selecciona **Revisar y crear**.
1. Seleccione **Crear**.

El recurso puede tardar unas horas en incorporarse completamente en Defender for Cloud. El siguiente paso consiste en examinar la recomendación que Defender for Cloud genera para este recurso.

### Tarea 5: Adición de estándares de cumplimiento normativo

En función de la recomendación, puedes empezar a proteger el recurso y asignar directivas de seguridad, por ejemplo, NIST SP 800-53 Rev.5 para asegurarte de que los recursos de Tailwind Traders cumplan con nuestras normativas de cumplimiento.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
1. Abre Defender for Cloud, expande **Administración** y selecciona **Configuración del entorno**.
1. Seleccione **Expandir todo**.
1. Selecciona los puntos suspensivos (...) junto a la suscripción y selecciona **Editar configuración**.
1. En el menú de navegación de la izquierda, selecciona **Directivas de seguridad**. Es posible que la carga de la lista tarde un poco.
1. Busque **`NIST SP 800-53 Rev. 5`**. Cambie el control deslizante de estado a **Activado**.
1. Vuelve a Defender for Cloud, expande **Seguridad en la nube** y selecciona **Cumplimiento normativo**.

Debido a la limitación del entorno de laboratorio, no puedes ver los recursos ni las recomendaciones de cumplimiento. Pasará un tiempo hasta que los recursos implementados están visibles en Defender for Cloud.

En el panel Cumplimiento normativo, ahora puedes revisar las evaluaciones con errores que aparecen en el panel para comprender los detalles de las recomendaciones.

Al evaluar continuamente los recursos con estos controles, Defender for Cloud identifica los problemas que pueden dificultar la obtención de certificaciones de cumplimiento específicas. Mantener el cumplimiento normativo es fundamental para proteger los datos de tu organización y garantizar un entorno de nube seguro.
