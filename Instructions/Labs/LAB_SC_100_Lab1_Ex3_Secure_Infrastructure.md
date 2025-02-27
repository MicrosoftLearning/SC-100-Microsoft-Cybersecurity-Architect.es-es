# Laboratorio 1: Ejercicio 3: Protección de la infraestructura

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
|Evaluación del estado de cumplimiento de los recursos de implementación | Directivas de seguridad de Microsoft Defender for Cloud| Habilita el cumplimiento de NIST SP 800-53 Rev.5 y evalúa tu estado de cumplimiento.|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Crear un área de trabajo de Log Analytics

En esta tarea, crearás un área de trabajo de Log Analytics que es necesaria para hospedar los datos que se envían desde distintos recursos.

1. Inicia sesión en la máquina virtual Cliente 1 (LON-SC1) como cuenta **lon-sc1\admin**. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **https://portal.azure.com** e inicia sesión en Azure Portal como usuario **User1-*******@LODSUATMCA.onmicrosoft.com** (donde ****** es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
3. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla No volver a mostrar esto y, a continuación, selecciona **No**.
4. Cierra el cuadro de diálogo guardar contraseña de la parte inferior. Para ello, selecciona Nunca, para no guardar las credenciales predeterminadas de administradores globales en el explorador.
5. Cancela la pantalla Bienvenida a Microsoft Azure.
6. Selecciona **Crear un recurso** y busca **área de trabajo de Log Analytics**
7. Busca el icono **Área de trabajo de Log Analytics** y selecciona **Crear**.
8. En el sitio Crear área de trabajo de Log Analytics, crea un nuevo **Grupo de recursos** y asígnale el nombre **ContosoRG**.
9. En Detalles de la instancia, escribe el nombre **ContosoLA** y selecciona **Este de EE. UU.** para región.
10. Selecciona **Revisar y crear**
11. Seleccione **Crear** para iniciar la implementación.

Has creado correctamente el área de trabajo de Log Analytics.

### Tarea 2: Habilitar Defender for Cloud

Antes de que Defender for Cloud pueda aplicar protecciones a los recursos, debes habilitar los planes de Defender para los tipos de recursos que deseas proteger.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
2. Busca y abre **Microsoft Defender for Cloud**.
3. En el panel de navegación izquierdo, expanda **Administración** y selecciona **Configuración del entorno**.
4. Haz clic en **Expandir todo** y selecciona tu suscripción.
5. Si la suscripción se muestra como **no registrada**, vuelve a cargar la página.
6. Selecciona los puntos suspensivos (...) junto a la suscripción y selecciona **Editar configuración**.
7. En **Protección de cargas de trabajo en la nube**, establece el control deslizante **Plan de servidores** de la derecha en **Activado**.
8. En la parte superior de la página, selecciona **Guardar**.
   
Al habilitar el plan para servidores, puedes ver que Defender for Cloud admite muchos más tipos de recursos.

### Tarea 3: Habilitación del servidor local en Azure Arc

Azure Arc es necesario para que se pueda usar para enviar datos al área de trabajo de Log Analytics que usa Defender for Cloud.

1. Cambia a la máquina virtual **LON-SC2** e inicia sesión en Azure Portal**https://portal.azure.com**.
2. Busca y abre **Azure Arc**.
3. En el panel de navegación de la izquierda, expande **Recursos de Azure Arc** y selecciona **Máquinas**.
4. Selecciona **Agregar o crear** > **Agregar máquina**.
5. En Agregar un solo servidor, selecciona **Generar script**.
6. Elige **ContosoRG** en el grupo de recursos.
7. Selecciona la región **Este de EE. UU**.
8. Seleccione **Descargar y ejecutar el script**.
9. Selecciona **Descargar** y ejecutar script en el segundo **LON-SC2** del cliente de laboratorio para incorporar el servidor local a Azure.
10. Ejecute Windows PowerShell como administrador.
11. Establece la directiva de ejecución en Sin restricciones.
```Powershell
Set-ExecutionPolicy -ExecutionPolicy unrestricted
```
12. Copia el script de incorporación.
13. Cuando aparezca el elemento emergente de autenticación, inicia sesión con la misma cuenta que usas para Azure Portal.
14. Espera a que el trabajo se complete correctamente.
15. Vuelve a LON-SC1 y abre Azure Arc.
16. Selecciona **Máquinas**, selecciona **Actualizar** en la parte superior de la página y comprueba que el servidor se ha implementado correctamente en Azure Arc.

Habilitaste correctamente Azure Arc en el servidor de pruebas y los datos deben empezar a fluir al área de trabajo de Log Analytics. Este proceso puede tardar algún tiempo hasta que puedas ver algo en el panel de información.

### Tarea 4: Agregar servidor a Defender for Cloud y recopilar registros.

Implementarás una regla de recopilación de datos para obtener registros de eventos del servidor local. La regla implementará automáticamente el agente de supervisión en el servidor y reenviará los registros al área de trabajo de Log Analytics creada anteriormente.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
2. Abre Defender for Cloud y selecciona la pestaña **Introducción** en la parte superior de la página.
3. En **Servidores que no son de Azure**, selecciona **Configurar**.
4. Encontrarás el área de trabajo de Log Analytics creada anteriormente. Junto a ella, selecciona **Actualizar**.
5. Si se realiza la actualización, selecciona **+ Agregar servidores**.
6. Selecciona **Reglas de recopilación de datos**
7. Seleccione **Crear**.
8. - Nombre de regla: ContosoDCR
   - Grupo de recursos: ContosoRG
9. Seleccione **Siguiente: Recursos**.
10. Seleccione **Agregar recursos**. Expande el ámbito del grupo de recursos. Comprueba la máquina de Azure Arc incorporada anteriormente y selecciona **Aplicar**.
11. Seleccione **Siguiente: Recopilar y entregar**.
12. Seleccione **Add data source**(Agregar origen de datos).
13. Elige el tipo de origen de datos **Registros de eventos de Windows**.
14. Selecciona cada opción en **Configurar los niveles y registros de eventos que se van a recopilar:**.
15. Seleccione **Siguiente: Destino**.
16. Selecciona **Agregar destino**.
17.  - Tipo de destino: registros de Azure Monitor
     - Cuenta o espacio de nombres: ContosoLA
18. Seleccione **Add data source**(Agregar origen de datos).
19. Selecciona **Revisar y crear**.
20. Seleccione **Crear**.

El recurso puede tardar unas horas en incorporarse completamente en Defender for Cloud. El siguiente paso consiste en examinar la recomendación que Defender for Cloud genera para este recurso.

### Tarea 5: Adición de estándares de cumplimiento normativo

En función de la recomendación, puedes empezar a proteger el recurso y asignar directivas de seguridad, por ejemplo, NIST SP 800-53 Rev.5 para asegurarte de que los recursos de Tailwind Traders cumplan con nuestras normativas de cumplimiento.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
2. Abre Defender for Cloud, expande **Administración** y selecciona **Configuración del entorno**.
3. Seleccione **Expandir todo**.
4. Selecciona los puntos suspensivos (...) junto a la suscripción y selecciona **Editar configuración**.
5. En el menú de navegación de la izquierda, selecciona **Directivas de seguridad**. Es posible que la carga de la lista tarde un poco.
6. Busca **NIST SP 800-53 Rev. 5**. Cambie el control deslizante de estado a **Activado**. 
7. Vuelve a Defender for Cloud y selecciona **Cumplimiento normativo**.

Debido a la limitación del entorno de laboratorio, no puedes ver los recursos ni las recomendaciones de cumplimiento. Pasará un tiempo hasta que los recursos implementados están visibles en Defender for Cloud.

En el panel Cumplimiento normativo, ahora puedes revisar las evaluaciones con errores que aparecen en el panel para comprender los detalles de las recomendaciones.
Al evaluar continuamente los recursos con estos controles, Defender for Cloud identifica los problemas que pueden dificultar la obtención de certificaciones de cumplimiento específicas. Mantener el cumplimiento normativo es fundamental para proteger los datos de tu organización y garantizar un entorno de nube seguro.
