# Centro de operaciones de seguridad
          

## Información general del ejercicio

Contoso tiene un centro de operaciones de seguridad (SOC) que supervisa y responde a incidentes de seguridad en toda la empresa. El SOC cuenta con personal compuesto por analistas de seguridad, ingenieros de seguridad e ingenieros de red. El SOC ha decidido usar Microsoft Sentinel como solución de administración de eventos e información de seguridad (SIEM). Para recopilar y analizar registros de seguridad de toda la empresa, el SOC tiene un área de trabajo de Log Analytics. El SOC tiene un requisito para proteger el acceso al área de trabajo de Log Analytics en función del principio de privilegio mínimo. El SOC tiene dos roles diferentes, analista de seguridad e ingeniero de seguridad, con diferentes requisitos de permisos. El equipo de red tiene un requisito para acceder solo a los registros de Cisco Umbrella.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para supervisar y responder a eventos de seguridad con permisos de acceso específicos para el centro de operaciones de seguridad de Contoso.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Implementar la solución SIEM/SOAR
- Limitar el acceso a roles de SOC específicos
- Crear un panel con vistas personalizadas para incidentes y sus alertas

En este escenario, implementarás la solución SIEM SOAR basada en Microsoft Sentinel, configurarás el control de acceso basado en roles en el contexto del área de trabajo y limitarás el acceso del equipo de red a una sola tabla del área de trabajo de Log Analytics. Los libros permiten a los analistas y administradores de seguridad visualizar los datos de seguridad mediante pantallas gráficas. Proporcionan una herramienta para presentar y analizar datos en un panel.

### Solución propuesta

| Requisito | Solución | Plan de acción |
| ---- | ---- | ---- |
| Implementar la solución SIEM/SOAR | Microsoft Sentinel, área de trabajo de Log Analytics | Configurar área de trabajo de Log Analytics e implementar Microsoft Sentinel |
| Limitar el acceso a roles de SOC específicos | Área de trabajo de Log Analytics, control de acceso basado en roles | Configurar RBAC para área de trabajo de Log Analytics |
| Crear un panel con vistas personalizadas para incidentes y sus alertas | Microsoft Sentinel, Libro | Creación de un libro con una vista personalizada sobre incidentes y alertas actuales |

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Crear área de trabajo de Log Analytics

En esta tarea, crearás un área de trabajo de Log Analytics que es necesaria para alojar todos los datos que Microsoft Sentinel va a ingerir y usar para sus detecciones y análisis.

1. Inicia sesión en la máquina virtual Cliente 1 (LON-SC1) como cuenta **lon-sc1\admin**. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **`https://portal.azure.com`** e inicia sesión en Azure Portal como usuario **User1-*******@LODSUATMCA.onmicrosoft.com** (donde ****** es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
3. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla No volver a mostrar esto y, a continuación, selecciona **No**.
4. Cierra el cuadro de diálogo guardar contraseña de la parte inferior. Para ello, selecciona Nunca, para no guardar las credenciales predeterminadas de administradores globales en el explorador.
5. Cancela la pantalla Bienvenida a Microsoft Azure.
6. Selecciona **Crear un recurso** y busca **área de trabajo de Log Analytics**
7. Busca el icono **Área de trabajo de Log Analytics** y selecciona **Crear**.
8. En el sitio Crear área de trabajo de Log Analytics, crea un nuevo **Grupo de recursos** y asígnale el nombre **`rg_eastus_soc`**.
9. En Detalles de la instancia, escribe el nombre **`law-sentinel`**, selecciona **Este de EE. UU.** para región.
10. Selecciona **Revisar y crear**
11. Seleccione **Crear** para iniciar la implementación.

Has creado correctamente el área de trabajo de Log Analytics para la implementación de Sentinel.

### Tarea 2: Creación de Sentinel

En esta tarea, agregarás Sentinel al área de trabajo de Log Analytics creada y agregarás registros de demostración, ya que el inquilino de demostración no tiene datos existentes en el área de trabajo de Log Analytics, importarás los registros de demostración para tener una mejor idea de cómo funciona Sentinel.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
1. En la barra de búsqueda, en el banner azul de la parte superior de la página, escribe **Microsoft Sentinel** y selecciónalo en los resultados de búsqueda que aparecen en los servicios.
1. En la página **Microsoft Sentinel**, selecciona **Crear**.
1. En la **página Agregar Microsoft Sentinel a un área de trabajo**, debe aparecer el área de trabajo de Log Analytics creada anteriormente.  Selecciona **law-sentinel** y, a continuación, selecciona **Agregar**.
1. Se puede tardar unos minutos en agregar Sentinel al área de trabajo.  Una vez agregada la nueva área de trabajo, se mostrará la página **Microsoft Sentinel | Noticias y guías**.  Se te notifica que se activa la versión de prueba gratuita de Microsoft Sentinel.  Seleccione **Aceptar**.
1. En el centro de la página, selecciona **Ir al centro de contenido**.  En el panel de navegación izquierdo, expande **Gestión de contenidos** y, luego, selecciona **Centro de contenidos**.
1. En el centro de contenido, instalarás el **Laboratorio de entrenamiento de Microsoft Sentinel**.  Para encontrar esta solución, filtre por **Provider = Microsoft** y **Category = Training and Tutorials**. Una vez establecidos y aplicados estos filtros, se mostrará el **Laboratorio de entrenamiento de Microsoft Sentinel**. Selecciónalo en los resultados de búsqueda e **Instala** la solución.
1. Seleccione **Crear**.
1. Elige el grupo de recursos **rg_eastus_soc** y el área de trabajo **law-sentinel**.
1. Selecciona **Revisar + crear** y, luego, **Crear**.
1. Espera hasta que la solución admitida se instale correctamente.

Has implementado correctamente Sentinel en el área de trabajo de Log Analytics y has agregado datos. 

### Tarea 3: Configurar RBAC

Tienes que proteger el acceso en función de los privilegios mínimos, y crearás asignaciones de roles para los requisitos de rol específicos. En la próxima implementación productiva, habrá dos roles diferentes en el Centro de operaciones de seguridad.
Además, el equipo de red necesita acceso a los registros del paraguas de Cisco. Debes asegurarte de que el equipo de red solo puede acceder a estos registros.

#### Requisitos de permisos de

| Rol | Permisos |
|---|---|
| Analista de seguridad | Ver datos, incidentes, libros y otros recursos de Sentinel |
| | Asignar o descartar incidentes |
| Ingeniero de seguridad | Creación y edición de libros y reglas de análisis |
| | Instala y actualiza las soluciones desde el centro de contenido |
| Equipo de red | Permisos de lectura para grupo: **NOC** en la tabla: **Cisco_Umbrella_dns_CL**|

---

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
1. En la barra de búsqueda superior, busca **Grupos de recursos** y selecciona el grupo de recursos creado anteriormente **rg_eastus_soc**.
1. En el panel de navegación de la izquierda, seleccione **Control de acceso (IAM)**.
1. Selecciona **Agregar** y **Agregar asignación de roles** en la lista desplegable.
1. Busca **`Microsoft Sentinel Responder`** y selecciona **Ver** en la columna Detalles.
1. Revisa los permisos que coincidan con los requisitos.
1. Cierra la ventana con **X** en la esquina superior derecha.
1. Seleccione **Siguiente**.
1. Elija **+ Seleccionar miembros**.
1. **`SOC Analysts`** Busca Grupo, selecciona **Analistas de SOC** en los resultados de la búsqueda, presiona **Seleccionar** y agrega la asignación de roles.
1. Seleccione **Revisar y asignar**.
1. Repetirás los pasos del rol Colaborador de Sentinel. Selecciona **Agregar** y, en el elemento desplegable, selecciona **Agregar asignación de roles**.
1. Busca **`Microsoft Sentinel Contributor`** y selecciona el rol.
1. Seleccione **Siguiente**.
1. Elija **+ Seleccionar miembros**.
1. En la hoja **Seleccionar miembros**, busca el grupo **Ingenieros de SOC**.  En los resultados de la búsqueda, selecciona **Ingenieros de SOC**, presiona **Seleccionar** para agregar la asignación de roles.
1. Seleccione **Revisar y asignar** dos veces.
1. Selecciona la **pestaña Asignaciones de roles** y Confirma que se han establecido las asignaciones de roles.
1. Ahora agregarás un rol personalizado. Selecciona **Agregar**, en el elemento desplegable, y selecciona **Agregar rol personalizado**.
1. Asígnale el nombre **`NOC-CiscoUmbrellaCL-Read`**.
1. Para **Permiso de línea base**, selecciona **Empezar de cero**.
1. Seleccione **Siguiente**.
1. En la pestaña **Permisos**, selecciona **Agregar permisos**.
1. Busca **`Microsoft.OperationalInsights`** y selecciona la tarjeta **Azure Log Analytics**.
1. Agrega los permisos siguientes.
    - Microsoft.OperationalInsights/workspaces
        - Lectura: Obtener área de trabajo
        - Otros: Buscar datos del área de trabajo

    - Microsoft.OperationalInsights/workspaces/analytics
        - Otros : Buscar

    - Microsoft.OperationalInsights/workspaces/query
        - Lectura: Consultar datos en el área de trabajo

    - Microsoft.OperationalInsights/workspaces/tables/query
        - Lectura: Consultar datos de tabla del área de trabajo

1. Seleccione **Revisar + crear**.
1. Selecciona **Crear** y, después, selecciona **Aceptar**.
1. En la barra de búsqueda superior, busca **`Resource groups`** y selecciona **rg_eastus_soc**.
1. Abre el área de trabajo de Log Analytics **law-sentinel**.
1. En el panel de navegación izquierdo, expande **Configuración** y selecciona **Tablas**.
1. Busque **`Cisco_Umbrella_dns_CL`**.
1. Haz clic en los puntos suspensivos (...), selecciona **Control de acceso (IAM)**.
1. Seleccione **Agregar** > **Agregar asignación de roles**.
1. Busca **`NOC-CiscoUmbrellaCL-Read`** y selecciona el rol personalizado.
1. Seleccione **Siguiente**.
1. Selecciona **Seleccionar miembros**, busca **NOC**, selecciónalo en los resultados de la búsqueda y presiona **Seleccionar**
1. Seleccione **Revisar y asignar** dos veces.

Has creado correctamente el modelo de acceso basado en roles para los requisitos de rol del equipo de operaciones de seguridad de Contoso y has creado un rol personalizado para el equipo de red y has asignado el rol en la tabla específica del área de trabajo de Log Analytics.

### Tarea 4: Crear libro

En esta tarea, crearás un libro para obtener un panel con vistas personalizadas e incidentes actuales y sus alertas.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
1. En la barra de búsqueda de la parte superior, busca **`Microsoft Sentinel`** y ábrelo.
1. Selecciona **law-sentinel**.
1. En el panel de navegación izquierdo, expande **Administración de amenazas** y selecciona **Libros**.
1. Selecciona **Agregar libro**.
1. Seleccione **Editar**.
1. Selecciona el primer botón **Editar** del lado derecho.
1. Seleccione **Agregar** > **Agregar parámetros**.
1. Selecciona **Agregar parámetro** y rellena la siguiente información:
     - **Nombre del parámetro:** TimeRange
     - **Tipo de parámetro:** selector de intervalo de tiempo
1. Utilice la siguiente configuración:
     - **¿Necesario?**
1. Seleccione **Guardar**.
1. En el menú desplegable **TimeRange:** en la parte inferior izquierda, selecciona **Últimos 7 días**.
1. Selecciona **Agregar parámetro** y rellena la siguiente información:
     - **Nombre del parámetro:** AlertSeverity
     - **Tipo de parámetro:** desplegable
1. Utilice la siguiente configuración:
     - **¿Necesario?**
     - **Permitir selecciones múltiples**
     - **Ocultar el parámetro en modo de lectura**
1. En **Consulta de registros del área de trabajo de Log Analytics**, pega:

    ```KQL
    SecurityAlert
    | summarize Count = count() by AlertSeverity
    | order by Count desc, AlertSeverity
    | project Value = AlertSeverity, Label = strcat(AlertSeverity, ' - ', Count)
    ```

1. En el menú desplegable de **Intervalo de tiempo**, selecciona **TimeRange**.
1. Desplázate hacia abajo hasta **Incluir en la lista desplegable**, activa **Todo** y establece **Elemento seleccionado predeterminado** en **Todos**.
1. Seleccione **Guardar**.
1. Selecciona **Agregar parámetro** y rellena la siguiente información:
     - **Nombre del parámetro:** ProductName
     - **Tipo de parámetro:** desplegable
1. Utilice la siguiente configuración:
     - **¿Necesario?**
     - **Permitir selecciones múltiples**
     - **Ocultar el parámetro en modo de lectura**

1. En **Consulta de registros del área de trabajo de Log Analytics**, pega:

    ```KQL
    SecurityAlert
    | summarize Count = count() by ProductName
    | order by Count desc, ProductName asc
    | project Value = ProductName, Label = strcat(ProductName, ' - ', Count)
    ```

1. En el menú desplegable de **Intervalo de tiempo**, selecciona **TimeRange**
1. Desplázate hacia abajo hasta **Incluir en la lista desplegable**, activa **Todo** y establece **Elemento seleccionado predeterminado** en **Todos**.
1. Seleccione **Guardar**.
1. Selecciona **Agregar** y elige **Agregar consulta**.
1. En **Consulta de registros del área de trabajo de Log Analytics**, pega:

    ```KQL
    SecurityIncident
    | where CreatedTime {TimeRange:value}
    | summarize arg_max(TimeGenerated,*) by tostring(IncidentNumber)
    | extend IncidentID = IncidentName
    | extend Alerts = extract("\\[(.*?)\\]", 1, tostring(AlertIds))
    | mv-expand AlertIds to typeof(string)
    | join
    (
        SecurityAlert
        | extend AlertEntities = parse_json(Entities)
        | mv-expand AlertEntities
    ) on $left.AlertIds == $right.SystemAlertId
    | summarize AlertCount=dcount(AlertIds) by IncidentNumber, Status, Severity, Title, Alerts, IncidentUrl, IncidentID
    | project IncidentNumber, IncidentID, Title, Severity, Status, AlertCount, Alerts, IncidentUrl
    | order by Severity
    ```

1. Selecciona **TimeRange** en el menú desplegable de Intervalo de tiempo.
Configurarás contenido dinámico para obtener todas las alertas del incidente seleccionado. Las alertas se exportarán y estarán disponibles fuera de esta consulta.
1. Selecciona la pestaña **Configuración avanzada** en la parte superior de la ventana **Consulta de edición**.
1. Utilice la siguiente configuración:
    - **Cuando se seleccionan elementos, exportar parámetros** 
1. Seleccione **Agregar parámetro** y rellene la siguiente información:
    - **Campo para exportar:** alertas
    - **Nombre del parámetro:** Alerts
1. Seleccione **Guardar**.
1. Ve a la pestaña **Configuración**.
1. Seleccione **Ejecutar consulta**.
1. Seleccione **Configuración de columnas**.
1. Selecciona **IncidentUrl**.
1. Establece Representador de columnas en **Vínculo**.
1. En Configuración del vínculo, establece **Ver para abrir** en **URL**.
1. Selecciona **Guardar y cerrar**.
1. A continuación, crearás la vista de alertas en función de qué incidente está seleccionado.
1. Selecciona **+ Agregar** en la parte inferior de la ventana **Elemento de consulta de edición**. Seleccione **Agregar consulta**.
1. Pega el KQL en la consulta de registros del área de trabajo de Log Analytics

    ```KQL
    SecurityAlert
    | where SystemAlertId in ({Alerts})
    | summarize by  DisplayName, StartTime, EndTime,  SystemAlertId
    | sort by EndTime desc
    ```

1. Elige **TimeRange** en la lista desplegable Intervalo de tiempo.
1. Seleccione **Edición finalizada**.
1. Selecciona **Edición finalizada** en la barra superior de la ventana **Nuevo libro**.
1. Selecciona un **incidente**.
1. Las alertas al incidente vinculado se mostrarán a continuación.
1. Guarda la consulta seleccionando el icono Guardar.  
1. En la ventana **Guardar como** , escribe un título para el nuevo libro, selecciona el grupo de recursos **rg_eastus_soc** en la lista desplegable y, a continuación, selecciona **Guardar como**.

Has creado correctamente un panel con vistas personalizadas para incidentes y las alertas asociadas.
