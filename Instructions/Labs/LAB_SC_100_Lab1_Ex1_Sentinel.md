# Laboratorio 1: Ejercicio 1: Centro de operaciones de seguridad

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
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **https://portal.azure.com** e inicia sesión en Azure Portal como usuario **User1-*******@LODSUATMCA.onmicrosoft.com** (donde ****** es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
3. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla No volver a mostrar esto y, a continuación, selecciona **No**.
4. Cierra el cuadro de diálogo guardar contraseña de la parte inferior. Para ello, selecciona Nunca, para no guardar las credenciales predeterminadas de administradores globales en el explorador.
5. Cancela la pantalla Bienvenida a Microsoft Azure.
6. Selecciona **Crear un recurso** y busca **área de trabajo de Log Analytics**
7. Busca el icono **Área de trabajo de Log Analytics** y selecciona **Crear**.
8. En Crear sitio del área de trabajo de Log Analytics, crea un nuevo **grupo de recursos** y asígnale el nombre **rg_eastus_soc**.
9. En Detalles de la instancia, escribe el nombre **law-sentinel** y selecciona **Este de EE. UU** para región.
10. Selecciona **Revisar y crear**
11. Seleccione **Crear** para iniciar la implementación.

Has creado correctamente el área de trabajo de Log Analytics para la implementación de Sentinel.

### Tarea 2: Creación de Sentinel

En esta tarea, agregarás Sentinel al área de trabajo de Log Analytics creada y agregarás registros de demostración, ya que el inquilino de demostración no tiene datos existentes en el área de trabajo de Log Analytics, importarás los registros de demostración para tener una mejor idea de cómo funciona Sentinel.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
2. Selecciona **Crear un recurso** y busca **Microsoft Sentinel**, Filtrar por **Tipo de producto: Servicios de Azure**.
3. Selecciona el **mosaico Microsoft Sentinel** y selecciona **Crear**.
4. Selecciona **Agregar** y busca el área de trabajo de Log Analytics creada anteriormente **law-sentinel**.
5. Confirma haciendo clic en **Agregar**.
6. En el panel de navegación de la izquierda, selecciona **Centro de conectividad del contenido**.
7. Busca **Laboratorio de entrenamiento de Microsoft Sentinel**, **selecciona** e **instala** la solución.
8. Seleccione **Crear**.
9. Elige el grupo de recursos **rg_eastus_soc** y el área de trabajo **law-sentinel**.
10. Seleccione **Revisar y crear**.
11. Confirma la implementación de ** Crear**.
12. Espera hasta que la solución admitida se instale correctamente.

Has implementado correctamente Sentinel en el área de trabajo de Log Analytics y has agregado datos. 

### Tarea 3: Configurar RBAC

Tienes que proteger el acceso en función de los privilegios mínimos, crearás asignaciones de roles para los requisitos de roles específicos. En la próxima implementación productiva, habrá dos roles diferentes en el Centro de operaciones de seguridad.
Además, el equipo de red necesita acceso a los registros de Cisco Umbrella. Debes asegurarte de que el equipo de red solo puede acceder a estos registros.

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
2. En la barra de búsqueda superior, busca **Grupos de recursos** y selecciona el grupo de recursos creado anteriormente **rg_eastus_soc**.
3. En el panel de navegación de la izquierda, seleccione **Control de acceso (IAM)**.
4. Selecciona ** Agregar** de la lista desplegable, selecciona **Agregar asignación de roles**.
5. Busca **Respondedor de Microsoft Sentinel** y selecciona **Ver** en la columna Detalles.
6. Revisa los permisos que coincidan con los requisitos.
7. Cierra la ventana con **X** en la esquina superior derecha.
8. Selecciona **Siguiente**.
9. Elija **+ Seleccionar miembros**.
10. Busca **SOC Analysts** Group (Grupo de analistas de SOC) y agrega la asignación de roles.
11. Seleccione **Revisar y asignar**.
12. Selecciona ** Agregar** de la lista desplegable, selecciona **Agregar asignación de roles**.
13. Busca **Colaborador de Microsoft Sentinel** y selecciona el rol.
14. Selecciona **Siguiente**.
15. Elija **+ Seleccionar miembros**.
16. En la hoja **Seleccionar miembros** , busca Grupo de** ingenieros de SOC** y **selecciona** la asignación de roles.
17. Seleccione **Revisar y asignar** dos veces.
18. Selecciona la **pestaña Asignaciones de roles** y Confirma que se han establecido las asignaciones de roles.
19. Selecciona **Agregar**, en el elemento desplegable, y selecciona **Agregar rol personalizado**.
20. Asígnale el nombre **NOC-CiscoUmbrellaCL-Read**.
21. Para **Permiso de línea base**, selecciona **Empezar de cero**.
22. Seleccione **Siguiente**.
23. En la pestaña **Permisos**, selecciona **Agregar permisos**.
24. Busca **Microsoft.OperationalInsights** y selecciona la tarjeta **Azure Log Analytics**.
25. Agrega los permisos siguientes.

```
Microsoft.OperationalInsights/workspaces
Read : Get Workspace
Other : Search Workspace Data

Microsoft.OperationalInsights/workspaces/analytics
Other : Search 

Microsoft.OperationalInsights/workspaces/query
Read : Query Data in Workspace 

Microsoft.OperationalInsights/workspaces/tables/query
Read : Query workspace table data 
```

26.  Seleccione **Revisar + crear**.
27. Seleccione **Crear**.
28. En la barra de búsqueda superior, busca y selecciona **Grupos de recursos** y selecciona **rg_eastus_soc**.
29. Abre el área de trabajo de Log Analytics **law-sentinel**.
30. En el panel de navegación izquierdo, expande **Configuración** y selecciona **Tablas**.
31. Busca **Cisco_Umbrella_dns_CL**.
32. Haz clic en los puntos suspensivos (...), selecciona **Control de acceso (IAM)**.
33. Seleccione **Agregar** > **Agregar asignación de roles**.
34. Busca **NOC-CiscoUmbrellaCL-Read** y selecciona el rol personalizado.
35. Seleccione Siguiente.
36. Selecciona **Seleccionar miembros**, busca NOC y **Selecciona** el grupo.
37. Seleccione **Revisar y asignar**.

Has creado correctamente el modelo de acceso basado en roles para los requisitos de rol del equipo de operaciones de seguridad de Contoso y has creado un rol personalizado para el equipo de red y has asignado el rol en la tabla específica del área de trabajo de Log Analytics.

### Tarea 4: Crear libro

En esta tarea, crearás un libro para obtener un panel con vistas personalizadas e incidentes actuales y sus alertas.

1. Todavía debes iniciar sesión en Azure Portal **https://portal.azure.com**.
2. En la barra de búsqueda de la parte superior, busca **Microsoft Sentinel** y ábrelo.
3. Selecciona **law-sentinel**.
4. En el panel de navegación izquierdo, expande **Administración de amenazas** y selecciona **Libros**.
5. Selecciona **Agregar libro**.
6. Seleccione **Editar**.
7. Selecciona el primer botón **Editar** del lado derecho.
8. Seleccione **Agregar** > **Agregar parámetros**.
9.  Selecciona **Agregar parámetro** y rellena la siguiente información:
 - **Nombre del parámetro:** TimeRange
 - **Tipo de parámetro:** selector de intervalo de tiempo
10. Utilice la siguiente configuración:
 - **¿Necesario?**
11. Seleccione **Guardar**.
12. En el menú desplegable **TimeRange:** en la parte inferior izquierda, selecciona **Últimos 7 días**.
13. Selecciona **Agregar parámetro** y rellena la siguiente información:
 - **Nombre del parámetro:** AlertSeverity
 - **Tipo de parámetro:** desplegable
14. Utilice la siguiente configuración:
 - **¿Necesario?**
 - **Permitir selecciones múltiples**
 - **Ocultar el parámetro en modo de lectura**
15. En **Consulta de registros del área de trabajo de Log Analytics**, pega:
```KQL
SecurityAlert
| summarize Count = count() by AlertSeverity
| order by Count desc, AlertSeverity asc
| project Value = AlertSeverity, Label = strcat(AlertSeverity, ' - ', Count)
```
16.  En el menú desplegable de **Intervalo de tiempo**, selecciona **TimeRange**.
17. Desplázate hacia abajo hasta **Incluir en la lista desplegable**, activa **Todo** y establece **Elemento seleccionado predeterminado** en **Todos**.
18. Seleccione **Guardar**.
19. Selecciona **Agregar parámetro** y rellena la siguiente información:
 - **Nombre del parámetro:** ProductName
 - **Tipo de parámetro:** desplegable
20. Utilice la siguiente configuración:
 - **¿Necesario?**
 - **Permitir selecciones múltiples**
 - **Ocultar el parámetro en modo de lectura**
21. En **Consulta de registros del área de trabajo de Log Analytics**, pega:
```KQL
SecurityAlert
| summarize Count = count() by ProductName
| order by Count desc, ProductName asc
| project Value = ProductName, Label = strcat(ProductName, ' - ', Count)
```
22.  En el menú desplegable de **Intervalo de tiempo**, selecciona **TimeRange**
23. Desplázate hacia abajo hasta **Incluir en la lista desplegable**, activa **Todo** y establece **Elemento seleccionado predeterminado** en **Todos**.
24. Seleccione **Guardar**.
25. Selecciona **Agregar** y elige **Agregar consulta**.
26. En **Consulta de registros del área de trabajo de Log Analytics**, pega:
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
27. Selecciona **TimeRange** en el menú desplegable de Intervalo de tiempo.
Configurarás contenido dinámico para obtener todas las alertas del incidente seleccionado. Las alertas se exportarán y estarán disponibles fuera de esta consulta. 
28.  Selecciona la pestaña **Configuración avanzada** en la parte superior de la ventana **Consulta de edición**.
29. Utilice la siguiente configuración:
- **Cuando se seleccionan elementos, exportar parámetros** 
30.  Seleccione **Agregar parámetro** y rellene la siguiente información:
   - **Campo para exportar:** alertas
   - **Nombre del parámetro:** Alerts
31.  Seleccione **Guardar**. 
32. Ve a la pestaña **Configuración**.
33. Seleccione **Ejecutar consulta**.
34. Seleccione **Configuración de columnas**.
35. Selecciona **IncidentUrl**.
36. Establece Representador de columnas en **Vínculo**.
37. En Configuración del vínculo, establece **Ver para abrir** en **URL**.
38. Selecciona **Guardar y cerrar**.

Crearás la vista de alertas en función del incidente seleccionado. 

39. Selecciona **+ Agregar** en la parte inferior de la ventana **Elemento de consulta de edición**. Seleccione **Agregar consulta**.
40. Pega el KQL en la consulta de registros del área de trabajo de Log Analytics 
```KQL
SecurityAlert
| where SystemAlertId in ({Alerts})
| summarize by  DisplayName, StartTime, EndTime,  SystemAlertId
| sort by EndTime desc
```
41. Elige **TimeRange** en la lista desplegable Intervalo de tiempo.
42. Seleccione **Edición finalizada**.
43. Selecciona **Edición finalizada** en la barra superior de la ventana **Nuevo libro**.
44. Selecciona un **incidente**.
45. Las alertas al incidente vinculado se mostrarán a continuación.

Has creado correctamente un panel con vistas personalizadas para incidentes y las alertas asociadas.
