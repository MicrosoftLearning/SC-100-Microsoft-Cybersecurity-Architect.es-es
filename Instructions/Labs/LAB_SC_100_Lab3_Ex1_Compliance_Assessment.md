---
lab: 3
title: 'Ejercicio 1: Evaluación del cumplimiento'
---

# Laboratorio 3- Ejercicio 1: Evaluación del cumplimiento

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

1. Inicia sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung con su cuenta de administrador **Administrador de MOD**.
2. Se te pedirá que configures la autenticación multifactor y sigas las instrucciones.
3. En el panel de navegación izquierdo del Portal de cumplimiento de Microsoft Purview, selecciona **Administrador de cumplimiento**.
4. En la página **Administrador de cumplimiento**, selecciona **Evaluaciones**.
5. En la página **Evaluaciones\| del Administrador de cumplimiento**, selecciona **+ Agregar evaluación**.
6. En la página **Base de tu evaluación en una regulación** , selecciona **Seleccionar regulación**.
7. En el cuadro de texto de búsqueda, escribe **ISO-27001:2022**, selecciona el reglamento, selecciona **Guardar** y, por último, selecciona **Siguiente**.
8. En la página **Agregar nombre y grupo**, en el cuadro de texto **Nombre de evaluación**, escribe **Evaluación de auditoría ISO-27001** y selecciona **Siguiente**.
9. En la página **Seleccionar servicios** , selecciona **Seleccionar servicios** y selecciona **Microsoft 365**, después selecciona **Agregar** y, fnalmente, Selecciona **Siguiente**.
10. Finaliza la configuración y crea la evaluación.

Has creado correctamente una evaluación basada en ISO-27001.

### Tarea 2: Asignar tareas a un ingeniero técnico

Los resultados de la evaluación muestran diferentes áreas y acciones esenciales para cumplir con las normativas ISO-27011. Investigarás las acciones de mejora y asignarás una tarea a un ingeniero técnico.

1. Todavía deberías tener iniciada la sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/**.
2. En el panel de navegación izquierdo del Portal de cumplimiento de Microsoft Purview, selecciona **Administrador de cumplimiento**.
3. En la página **Administrador de cumplimiento**, selecciona la evaluación **ISO/IEC-27001:2022** que creaste.
4. En la página de evaluación, selecciona la hoja **Acciones de mejora**.
5. Establece el filtro de la **familia de controles** en **Controles físicos**.
6. Selecciona todas las acciones de mejora mostradas y, a continuación, selecciona **Asignar al usuario**.
7. En la nueva página **Asignar acciones de mejora**, en el cuadro de texto de búsqueda, escribe **Nestor Wilke**.
8. Selecciona el usuario y selecciona **Asignar**.

Has visto y asignado correctamente una acción de mejora a un ingeniero técnico

### Tarea 3: Proporcionar acceso a un ingeniero técnico para las acciones de mejora.

Los usuarios necesitan acceso para ver las tareas que tienen asignadas. Concederás acceso a Nestor Wilke a la evaluación.

1. Todavía deberías tener iniciada la sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/**.
2. En el panel de navegación izquierdo del portal de cumplimiento de Microsoft Purview, selecciona **Administrador de cumplimiento**.
3. En la página **Administrador de cumplimiento**, selecciona **el panel Evaluación** y, a continuación, selecciona la evaluación de la **evaluación de auditoría ISO-27001**.
4. En la página **ISO/IEC 27001: Evaluación** , en la esquina superior derecha, selecciona **Administrar acceso de usuario**.
5. En la nueva página **Administrar acceso de usuario**, selecciona **Evaluador** y selecciona **Agregar evaluadores**.
6. En el cuadro de texto **Buscar usuarios** , escribe **Nestor Wilke**.
7. Selecciona el usuario y, después, **Guardar**.

Has concedido acceso correctamente a Nestor Wilke a la evaluación.
