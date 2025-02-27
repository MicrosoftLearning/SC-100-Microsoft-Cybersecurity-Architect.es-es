---
lab: 3
title: 'Ejercicio 4: Marco de clasificación de datos'
---


# Laboratorio 3- Ejercicio 4: Marco de clasificación de datos

Se te ha asignado la tarea de estructuración de la clasificación de datos para Contoso Ltd. como preparación para una auditoría ISO-27001:2022. El objetivo es establecer un marco sólido que sea fundamental para garantizar una protección eficaz de los datos contra la pérdida, eliminación y pérdida. Tu rol implica la integración de un nuevo sistema de identificadores de proyecto para proyectos de construcción dentro de la empresa. Para cumplir con las regulaciones gubernamentales, todos los documentos que contengan un determinado identificador de proyecto deben conservarse durante 5 años.

Se te dieron los ejemplos siguientes para clasificar los identificadores de proyecto:

|Id. de proyecto|
|----|
|PAR-1023-DA
|BER-0822-AB
|Rom-0419-bm
|sTr*1223-Se
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

1. Inicia sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung con su cuenta de administrador **Administrador de MOD**.
1. En el portal de cumplimiento de Microsoft Purview, expande **Clasificación de datos** y luego elige **Clasificadores**.
3. En la página **Clasificadores**, selecciona **Tipos de información confidencial** > **Crear tipo de información confidencial**.
4. En la página **Nombre de tipo de información confidencial**, escribe la siguiente información:
    - **Nombre**: Número de identificación del proyecto
    - **Descripción**: identifica el número de identificación del proyecto
1. Seleccione **Siguiente**.
1. En la página **Definir patrones para este tipo de información confidencial**, selecciona **Crear patrón**.
1. En la página **Nuevo patrón**, selecciona **Agregar elemento principal** y, después, **Expresión regular**.
1. En la página **Agregar una expresión regular** en el cuadro de texto **ID**, escribe **ProjectID**.
1. En el cuadro de texto **Expresión regular**, escribe la siguiente expresión:
```regex   
[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}
```
> [!NOTE] La expresión regular proporcionada se crea para identificar una secuencia que se caracteriza por tener tres letras, seguidas de caracteres opcionales que no sean palabras, después de cuatro dígitos, seguidos una vez más por caracteres opcionales que no sean palabras y, en última instancia, terminan con dos letras. La presencia de caracteres que no sean palabras es discrecional y el patrón general está pensado para corresponder a un formato o estructura específicos dentro de los datos.

1. Selecciona **Coincidencia de cadena** para las **expresiones regulares** y selecciona **Listo**.
1. Selecciona **Confianza alta** para **Nivel de confianza** en la parte superior y selecciona **Crear**.
1. Finaliza la configuración y crea el tipo de información confidencial.

Has creado correctamente un nuevo tipo de información confidencial para identificar identificadores de proyecto.

### Tarea 2: Crear una etiqueta de retención

Crearás una etiqueta de retención para conservar todos los documentos relacionados con los proyectos de construcción durante 5 años.

1. Todavía deberías tener iniciada la sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/**.
1. En el portal de cumplimiento de Microsoft Purview, en el panel de navegación izquierdo, expande **Administración del ciclo de vida de datos** y selecciona **Microsoft 365**.
1. En la página **Administración del ciclo de vida de datos**, selecciona la hoja **Etiquetas**.
1. En la hoja **Etiquetas**, selecciona **Nueva etiqueta**.
1. En la página **Nombrar directiva de retención**, escribe la información siguiente:

    - **Nombre**: Retención de documentación del proyecto de construcción
    - **Descripción para los usuarios**: la directiva de retención de documentación del proyecto de construcción dicta la retención de todos los documentos relacionados con el proyecto durante cinco años después de la finalización del proyecto
    - **Descripción para los administradores**: esta etiqueta se aplica para conservar los documentos del proyecto de construcción durante un período de cinco años y se utiliza junto con el etiquetado automático.

1. Seleccione **Siguiente**.
1. En la página **Definir configuración de etiqueta**, elige **Conservar elementos para siempre o durante un período específico** y, después, selecciona **Siguiente**.
1. En la página **Definir el período de retención**, escribe la siguiente información:

    - **Conservar elementos durante**: 5 años
    - **Iniciar el período de retención en función de**: cuándo se crean los elementos.
    - **Al final del período de retención**: no hacer nada

1. Seleccione **Siguiente**.
1. En la página **Elegir lo que sucede después del período de retención**, selecciona **Desactivar configuración de retención**.
1. Finaliza la configuración y crea la etiqueta de retención sin publicarla.

Has creado correctamente una etiqueta de retención con un período de retención de 5 años.

### Tarea 3: Aplicar automáticamente la etiqueta de retención

Usarás el tipo de información confidencial que creaste en este ejercicio para aplicar automáticamente la etiqueta de retención.

1. Todavía deberías tener iniciada la sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/**.
1. Abre el portal de cumplimiento de Microsoft Purview, expande **Administración del ciclo de vida de datos** y selecciona **Microsoft 365**.
1. En el panel **Administración del ciclo de vida de datos**, selecciona la hoja **Directivas de etiquetas**.
1. En la hoja **Directivas de etiquetas**, selecciona **Aplicar automáticamente una etiqueta**.
1. En la página **Comencemos**, escribe la siguiente información:

    - **Nombre**: etiquetar documentos relacionados con proyectos de construcción
    - **Descripción**: esta directiva aplica automáticamente la directiva "Retención de documentación del proyecto de construcción" en cualquier documento relacionado con proyectos de construcción.

1. Seleccione **Siguiente**.
1. En la página **Elegir el tipo de contenido al que deseas aplicar esta etiqueta**, selecciona **Aplicar etiqueta al contenido que contiene información confidencial** y selecciona **Siguiente**.
1. En la página **Contenido que contiene información confidencial**, selecciona **Personalizado**, después, selecciona **Directiva personalizada** y selecciona **Siguiente**.
En **Definir contenido que contiene información confidencial**, agrega el tipo de información confidencial personalizado que creaste **Número de identificación del proyecto**. A continuación, especifica la configuración siguiente:

    - **Nombre de grupo**: búsqueda de id. de proyecto
    - **Nivel de confianza**: confianza alta
    - **Recuento de instancias**: de 1 a cualquiera

1. Seleccione **Siguiente**.
1. En la página **Ámbito de directiva**, selecciona **Siguiente**.
1. En la página **Elegir el tipo de directiva de retención que se va a crear**, selecciona **Estático** y luego **Siguiente**.
1. Aplica la etiqueta a todas las ubicaciones disponibles.
1. En **Elegir una etiqueta para aplicar automáticamente**, selecciona **Agregar etiqueta**, a continuación, selecciona la etiqueta **Retención de documentación de proyecto de construcción** que creaste en la tarea 2 y selecciona **Agregar**.
1. Activa y finaliza la configuración para crear la directiva de etiquetado automático.

Has publicado correctamente y aplicado automáticamente la etiqueta de retención a todos los documentos que contienen identificadores de proyecto.