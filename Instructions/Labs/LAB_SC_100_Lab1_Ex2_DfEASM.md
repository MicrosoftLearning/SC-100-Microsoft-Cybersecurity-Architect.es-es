# Laboratorio 1- Ejercicio 2: Administración de la superficie expuesta a ataques externos

## Información general del ejercicio

Contoso tiene como objetivo mejorar su posición de ciberseguridad mediante la identificación y administración de su superficie expuesta a ataques externos. Esta superficie incluye recursos hospedados en diferentes proveedores de nube. Para lograr este objetivo, Contoso quiere integrar sus datos de superficie expuesta a ataques con Sentinel, su solución SIEM nativa de la nube. Esta integración mejorará sus funcionalidades de supervisión de seguridad y respuesta a incidentes. 

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para obtener información general sobre los recursos orientados al exterior y su superficie expuesta a ataques.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Los recursos externos de Contoso deben supervisarse y protegerse
- Detección de todos los recursos asociados a Contoso
- Integra los datos en la solución SIEM de Contoso.
- Los recursos deben administrarse y etiquetarse

En el segundo paso, examina el entorno existente de Contoso Ltd. Administración de superficie expuesta a ataques externos de Microsoft Defender (EASM) detecta y asigna continuamente la superficie expuesta a ataques digitales para proporcionar una visión externa de la infraestructura en línea de la organización. Identifica los recursos expuestos, prioriza las tareas y amplía el control de vulnerabilidades y exposición más allá del firewall.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Los recursos externos de Contoso deben supervisarse y protegerse| Defender EASM | Creación de un recurso Microsoft Defender EASM|
|detección de todos los recursos asociados a Contoso | Defender EASM |Creación de un trabajo de detección en los recursos de Contoso  |
|Integración de datos en la solución SIEM de Contoso |Defender EASM, área de trabajo de Log Analytics | Conectar el área de trabajo de Log Analytics a Defender EASM |
|Los recursos deben administrarse y etiquetarse | Defender EASM | Administración de activos y etiquetas facturables |


## Parte 2: Implementar la solución (opcional)

### Tarea 1: Configuración de Defender EASM

En esta tarea, creará un área de trabajo de Defender EASM.

1. Inicia sesión en la máquina virtual cliente 1 (LON-Sc1) como cuenta **lon-sc1\admin** . El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
2. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **<https://portal.azure.com>** e inicia sesión en Azure Portal como el usuario <user1-ZZZZZZZ@LODSUATMCA.onmicrosoft.com>. La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.
3. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla No volver a mostrar esto y, a continuación, selecciona Sí.
4. Cierra el cuadro de diálogo Guardar la contraseña de la parte inferior. Para ello, selecciona **Nunca** para no guardar las credenciales predeterminadas de administradores globales en el navegador.
5. En el cuadro de búsqueda superior, busca **Microsoft Defender EASM**.
6. Seleccione **Crear**.
7. En Crear recurso de Microsoft Defender EASM, selecciona el grupo de recursos existente **rg_eastus_soc**.
8. En Detalles de la instancia, escribe el nombre **EASM**, selecciona **Este de EE. UU** para la región.
9. Seleccione **Revisar y crear**.
10. Seleccione **Crear**.

Has creado correctamente el área de trabajo de Defender EASM.

### Tarea 2: Crear detección

En esta tarea, crearás una detección en Contoso Ltd. fuera de los recursos orientados. Después de crear una instancia, debes rellenarla con datos reales. Por lo tanto, ahora crearás una detección.

1. Todavía deberías tener iniciada la sesión en el portal de Azure **<https://portal.azure.com>**.
2. En la barra de búsqueda de la parte superior, busca **Microsoft Defender EASM** y ábrelo.
3. Selecciona el área de trabajo de **EASM** que creaste en la última tarea.
4. **Busca Contoso** en el campo de búsqueda **Buscar una organización**.
5. Selecciona **Contoso Ltd.**.
6. Selecciona **Iniciar detección de superficie expuesta a ataques**.

Has creado correctamente la detección de la superficie expuesta a ataques externos de Contoso y has rellenado la instancia de EASM con datos accionables.

### Tarea 3: Configuración del conector de datos y del área de trabajo de Log Analytics

En esta tarea, configurarás una conexión de datos de Defender EASM a un área de trabajo de Log Analytics que se usará para Sentinel. La información de información o recursos de Administración de superficie expuesta a ataques externos de Microsoft Defender se puede usar en Log Analytics para enriquecer los flujos de trabajo existentes con otros datos de seguridad.

1. Todavía deberías tener iniciada la sesión en el portal de Azure **<https://portal.azure.com>**.
2. En el cuadro de búsqueda, busca **Áreas de trabajo de Log Analytics**.
3. Selecciona el **área de trabajo de Law-Sentinel** en el último ejercicio.
4. En el panel de navegación izquierdo, selecciona **Valores de configuración** y selecciona **Agentes**.
5. Deja la página tal y como está y abre otra pestaña e inicia sesión en Azure Portal **<https://portal.azure.com>**.
6.  En la barra de búsqueda de la parte superior, busca **Microsoft Defender EASM** y ábrelo.
7.  Selecciona el área de trabajo **EASM**.
8.  En el panel de navegación izquierda, expande **Administrar** y selecciona **Conexiones de datos**.
9.  En Log Analytics, selecciona **Agregar conexión**.
10. Asígnale el nombre **law-sentinel**
11. Cambia a la pestaña anterior con el área de trabajo de Log Analytics que debe estar abierta.
12. Expande **Instrucciones del agente de Log Analytics**.
13. Copia el **identificador del área de trabajo** y la **clave principal** en el campo correspondiente de Defender EASM: Agregar conexión de datos.
14. En Contenido, selecciona **Todo**.
15. En Frecuencia, selecciona **Diariamente**.
16. Seleccione **Agregar**.

Una vez creada la conexión, las tablas de registro personalizadas se crean en el área de trabajo de Log Analytics. En Sentinel, estos datos se pueden usar para crear o enriquecer incidentes de seguridad, crear cuadernos de estrategias de investigación, entrenar algoritmos de aprendizaje automático o desencadenar acciones de corrección.

Has configurado correctamente la conexión entre Defender EASM y un área de trabajo de Log Analytics.

### Tarea 4: Revisar paneles y etiquetar recursos

En esta tarea, revisarás la posición de seguridad de Defender EASM y obtendrás información sobre los resultados.

1. Todavía deberías tener iniciada la sesión en el portal de Azure **<https://portal.azure.com>**.
2. En la barra de búsqueda de la parte superior, busca **Microsoft Defender EASM** y ábrelo.
3. Selecciona el área de trabajo **EASM**.
4. En el panel de navegación izquierdo, expande **Paneles** y selecciona **Resumen de la superficie expuesta a ataques**.

Los paneles Resumen de la superficie expuesta a ataques proporcionan información clave y información general de alto nivel de los recursos principales afectados de la superficie expuesta a ataques.

5. Revisa el **panel de resumen** de la superficie expuesta a ataques.
6. En el panel de navegación izquierdo, selecciona **Posición de seguridad**.
7. Revisa las distintas categorías para detectar vulnerabilidades abiertas.
8. En la categoría **Puertos abiertos**, selecciona **Servidores web**.
9.  Selecciona la dirección IP encontrada **34.223.124.45**.

Decides etiquetar el recurso para una investigación más detallada.

10. Selecciona **Modificar recurso**.
11. Selecciona **Crear nueva etiqueta**.
12. Asígnale el nombre **Abrir puertos** y selecciona **Agregar**.
13. Asigna la etiqueta recién creada en el campo **Etiquetas**.
14. Selecciona **Actualización**.

Has revisado correctamente la posición de seguridad y has etiquetado un recurso para una investigación más detallada.

### Tarea 5: Administrar recursos

En esta tarea, administrarás y clasificarás los recursos detectados.

1. Todavía deberías tener iniciada la sesión en el portal de Azure **<https://portal.azure.com>**.
2. En la barra de búsqueda de la parte superior, busca **Microsoft Defender EASM** y ábrelo.
3. Selecciona el área de trabajo **EASM**.
4. En el panel de navegación de la izquierda, expande **General** y selecciona **Inventario**.
5. En Buscar en el menú desplegable, selecciona **Etiqueta.**
6. En el menú desplegable siguiente, elige la etiqueta que hemos creado recientemente en la tarea 4 **Abrir puertos**.
7. Seleccione **Buscar**.
8. Abre el recurso encontrado **34.223.124.45**.
9. Selecciona la columna **Componentes web**.

Identifica que este recurso se hospeda en Amazon, también hay CVE abiertos en algunos de los componentes, pero estos no están activos, como puedes ver en la columna **Reciente** y **Última conexión**. Se originan en ejecuciones de detección anteriores.
Dado que este recurso está hospedado por un tercero, pero aún pertenece a la superficie expuesta a ataques, la categorizas en función de su rol en la organización.

10. Selecciona **Modificar recurso**.
11. Selecciona **Dependencia**.
12. Selecciona **Actualización**.

>[!NOTE]En este caso, eliges Dependencia; porque el recurso es Infraestructura, que es propiedad de un tercero, pero que forma parte de la superficie expuesta a ataques porque permite directamente el funcionamiento de los recursos de su propiedad.

13. Vuelve a Inventario. Para ello, selecciona **X** en la parte superior derecha y crea una nueva búsqueda.
14. Modifica la consulta de búsqueda en **Nombre de componente web - contains - Amazon**.
15. Seleccione **Buscar**.
16. Selecciona todos los recursos.
17. Selecciona **Modificar recursos**.
18. Elige **Dependencia** en Estado y selecciona **Actualizar**.

Solo si el Estado está establecido en **Inventario aprobado**, los recursos se representan en los gráficos del panel y se examinan diariamente. Por esa razón, es importante revisar los recursos recién detectados y cambiar su estado en consecuencia.

Como parte de este ejercicio, configuraste Defender EASM, creaste la detección del entorno orientado a externos de Contoso, obtuviste información más detallada de los recursos y su configuración, y has administrado recursos para que los paneles solo incluyan datos para los que Contoso es responsable directamente.
