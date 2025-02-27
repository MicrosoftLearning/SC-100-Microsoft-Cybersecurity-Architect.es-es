# Marco de clasificación de datos

Se te ha asignado la tarea de estructuración de la clasificación de datos para Contoso Ltd. como preparación para una auditoría ISO-27001:2022. El objetivo es establecer un marco sólido que sea fundamental para garantizar una protección eficaz de los datos contra la pérdida, eliminación y pérdida. Tu rol implica la integración de un nuevo sistema de identificadores de proyecto para proyectos de construcción dentro de la empresa. Para cumplir con las regulaciones gubernamentales, todos los documentos que contengan un determinado identificador de proyecto deben conservarse durante 5 años.

Se te dieron los ejemplos siguientes para clasificar los identificadores de proyecto:

|Id. de proyecto|
|----|
|PAR-1023-DA|
|BER-0822-AB|
|Rom-0419-bm|
|sTr*1223-Se|
|BaR#0418-ag|
|dui0522-in|

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para solucionar los problemas a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

Esta introducción de un nuevo identificador de proyecto requiere la creación de un tipo de información confidencial correspondiente (SIT), que requiere el desarrollo de un patrón personalizado que incorpora una expresión regular. Posteriormente, este SIT se puede usar para diseñar una etiqueta de retención y una directiva de etiquetado automático asociada.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Identificación de documentos que contienen identificadores de proyecto|Microsoft Purview Information Protection|Creación de tipos de información confidencial personalizados|
|Cumplimiento de la normativa gubernamental para conservar los datos durante 5 años| Administración del ciclo de vida de los datos de Microsoft Purview|Implementar una directiva de retención|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Creación de tipos de información confidencial personalizados

Crearás un tipo de información confidencial personalizado para detectar documentos que contienen identificadores de proyecto.

1. Inicia sesión en el portal de cumplimiento Microsoft Purview **`https://purview.microsoft.com/`** como Allan Deyoung con su cuenta de administrador **MOD Administrator**.
1. Si se te pide que configures la autenticación multifactor, sigue las instrucciones.
1. Se te lleva a la nueva página de aterrizaje de Microsoft Purview portal. Selecciona el cuadro situado junto a la instrucción, **Acepto los términos de divulgación del flujo de datos y las Declaraciones de privacidad** y, luego, selecciona **Comenzar**.
1. En el panel de navegación izquierdo, selecciona **Soluciones** y **Protección de información**. Como alternativa, en la ventana principal puedes seleccionar el icono **Ver todas las soluciones** y, a continuación, seleccionar el icono **Protección de información** que aparece en Seguridad de datos.
1. Expande **Clasificadores** y, a continuación, selecciona **Tipos de información confidencial**.
1. En la página **Tipos de información confidencial**, selecciona **Crear tipo de información confidencial**.
1. En la página **Nombre de tipo de información confidencial**, escribe la siguiente información:
    - Nombre: **`Project Identification Number`**
    - Description (Descripción): **`Identifies project identification number`**
1. Selecciona **Siguiente**.
1. En la página **Definir patrones para este tipo de información confidencial**, selecciona **Crear patrón**.
1. En la página **Nuevo patrón**, selecciona **Agregar elemento principal** y, después, **Expresión regular**.
1. En la página **Agregar una expresión regular** en el cuadro de texto **ID**, escribe **`ProjectID`**.
1. En el cuadro de texto **Expresión regular**, escribe la siguiente expresión:

    **`[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}`**

    >[!NOTE] La expresión regular proporcionada se crea para identificar una secuencia que se caracteriza por tener tres letras, seguidas de caracteres opcionales que no sean palabras, después de cuatro dígitos, seguidos una vez más por caracteres opcionales que no sean palabras y, en última instancia, terminan con dos letras. La presencia de caracteres que no sean palabras es discrecional y el patrón general está pensado para corresponder a un formato o estructura específicos dentro de los datos.

1. En el cuadro de texto Expresión regular, selecciona **Coincidencia de cadena** y, después, **Listo**.
1. En la ventana **Nuevo patrón**, en el **nivel Confianza**, selecciona **Confianza alta**, **Crear** y, después, **Siguiente**.
1. En la página **Elegir el nivel de confianza recomendado para mostrar en las directivas de cumplimiento**, deja la configuración en **Confianza alta** y, a continuación, selecciona **Siguiente**.
1. En **Revisar la configuración y finalizar**, comprueba la configuración, selecciona **Crear** y luego cuando se cree la directiva, selecciona **Listo**.

Has creado correctamente un nuevo tipo de información confidencial para identificar identificadores de proyecto.

### Tarea 2: Crear una etiqueta de retención

Crearás una etiqueta de retención para conservar todos los documentos relacionados con los proyectos de construcción durante 5 años.

1. Todavía deberias tener iniciada la sesión en Microsoft Purview portal **https://purview.microsoft.com/**.
1. En el panel de navegación izquierdo, selecciona **Soluciones** y, después, selecciona **Administración del ciclo de vida de datos**.
1. Selecciona **Etiquetas de retención**.
1. En la página **Etiquetas**, selecciona **Crear una etiqueta**.
1. En la página **Nombrar etiqueta de retención**, escribe la información siguiente:

    - Nombre: **`Retention of Construction Project Documentation`**
    - Descripción para los usuarios: **`The construction project documentation Retention Policy dictates the retention of all project-related documents for five years following project completion.`**
    - Descripción para los administradores: **`This label is applied to retain construction project documents for a period of five years, and it is utilized in conjunction with auto-labeling.`**

1. Seleccione **Siguiente**.
1. En la página **Definir configuración de etiqueta**, elige **Conservar elementos para siempre o durante un período específico** y, después, selecciona **Siguiente**.
1. En la página **Definir el período de retención**, escribe la siguiente información:

    - Conservar los elementos durante: **5 años**
    - Iniciar el período de retención en función de: **cuándo se crearon los elementos**

1. Seleccione **Siguiente**.
1. En la página **Elegir lo que sucede después del período de retención**, selecciona **Desactivar la configuración de retención** y, después, selecciona **Siguiente**.
1. En la página **Revisar y finalizar**, revisa la configuración y a continuación, selecciona **Crear etiqueta**.
1. En la página **La etiqueta de retención se crea**, tienes varias opciones.  Selecciona **No hacer nada** y, a continuación, selecciona **Listo**.  Crearás la directiva de aplicación automática en la siguiente tarea. Al seleccionar Aplicar automáticamente esta etiqueta a un tipo específico de contenido, se te guiará por los pasos de la tarea posterior, comenzando en el paso 4.

1. Deja la pestaña del explorador abierta para la siguiente tarea.

Has creado correctamente una etiqueta de retención con un período de retención de 5 años.

### Tarea 3: Aplicar automáticamente la etiqueta de retención

Usarás el tipo de información confidencial que creaste en este ejercicio para aplicar automáticamente la etiqueta de retención.

1. Todavía deberías tener iniciada la sesión en la solución Administración del ciclo de vida de datos en Microsoft Purview portal.  Si no es así, ve a **`https://purview.microsoft.com/`** > **Soluciones** > **Administración del ciclo de vida de datos**.
1. En el panel **Administración del ciclo de vida de datos**, selecciona **Directivas de etiquetas**.
1. En la hoja **Directivas de etiquetas**, selecciona **Aplicar automáticamente una etiqueta**.
1. En la página **Comencemos**, escribe la siguiente información:

    - Nombre: **`Label documents related to construction projects`**
    - Description (Descripción): **`This policy automatically enforces the "Construction Project Documentation Retention" policy on any document pertaining to construction projects.`**

1. Seleccione **Siguiente**.
1. En la página **Elegir el tipo de contenido al que deseas aplicar esta etiqueta**, selecciona **Aplicar etiqueta al contenido que contiene información confidencial** y selecciona **Siguiente**.
1. En la página **Contenido que contiene información confidencial**, selecciona **Personalizado**, después, selecciona **Directiva personalizada** y selecciona **Siguiente**.

1. En **Definir contenido que contiene información confidencial**, especifica la siguiente configuración:
    - Nombre de grupo: **`Project ID lookup`**
    - En Tipos de información confidencial, selecciona **Agregar** y, después, selecciona **Tipos de información confidencial**.  
    - En la página Tipos de información confidencial, en el campo de búsqueda, escribe el nombre de la etiqueta que creaste **`Project Identification number`** y presiona Entrar.  Selecciona **Número de identificación del proyecto** y, después, **Agregar**.
    - Deja el nivel de confianza en **Confianza alta**.
    - Deja el recuento de instancias como **1 a cualquiera**.
    - Seleccione **Siguiente**.
1. En la página **Ámbito de directiva**, deja la configuración Unidades de administración en **Directorio completo** y selecciona **Siguiente**.
1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Estático** y luego **Siguiente**.
1. En **Elegir dónde aplicar automáticamente la etiqueta**, comprueba que el estado se ha establecido en **Activado** para todas las ubicaciones disponibles y luego selecciona **Siguiente**.
1. En **Elegir una etiqueta para aplicar automáticamente**, selecciona **Agregar etiqueta** y, a continuación, selecciona la etiqueta **Retención de la documentación del proyecto de construcción** que creaste en la tarea anterior, selecciona después **Agregar** y, a continuación, selecciona **Siguiente**.
1. En **Decidir si se va a probar o ejecutar la directiva**, selecciona **Activar directiva** y, después, selecciona **Siguiente**.
1. En la página **Revisar y finalizar**, revisa la configuración, selecciona **Enviar** y, después, selecciona **Listo**.

Has publicado correctamente y aplicado automáticamente la etiqueta de retención a todos los documentos que contienen identificadores de proyecto.
