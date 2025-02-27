---
lab: 3
title: 'Ejercicio 4: Shadow-IT'
---


# Laboratorio 2- Ejercicio 4: Shadow-IT

La infraestructura de TI de Contoso ha evolucionado en las últimas décadas, lo que proporciona varias instancias de servidor, aplicaciones y servicios. Recientemente, la empresa ha priorizado la protección de su entorno mediante la implementación de Administración de dispositivos, gobernanza de datos e Identidad y Protección de aplicaciones en los últimos dos años. Sin embargo, aún no se ha establecido el proceso de restringir a los usuarios a aplicaciones específicas implementadas por la empresa, lo que permite a los usuarios instalar aplicaciones desde varios orígenes. Como arquitecto de ciberseguridad de la organización, tu objetivo es tener una visión general completa de todas las aplicaciones que usan los empleados. La medida de protección consiste en bloquear aplicaciones no seguras en tu entorno. 

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los desafíos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

En este escenario concreto, la acción inicial es analizar y descubrir todas las aplicaciones actualmente en uso por parte de los empleados. Las aplicaciones no autorizadas instaladas por los usuarios pueden suponer riesgos de seguridad para la empresa, lo que resalta la necesidad de identificar Shadow IT. El paso posterior implica la solución de los riesgos que plantean estas aplicaciones no seguras.

Defender for Cloud Apps es una solución de seguridad diseñada para abordar los riesgos de Shadow IT en entornos en la nube. Ayuda a las organizaciones a detectar y supervisar aplicaciones en la nube no autorizadas utilizadas por los empleados, evaluar su posición de seguridad y aplicar directivas para garantizar el cumplimiento y proteger los datos. Al ofrecer visibilidad y control sobre Shadow IT, Defender for Cloud Apps ayuda a las organizaciones a mitigar los riesgos de seguridad asociados con el uso no autorizado de la nube, lo que mejora la seguridad de su entorno de nube.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Detección de shadow IT|Microsoft Defender para aplicaciones en la nube|Investigación de todas las aplicaciones en el entorno de Contoso|
|Bloquear todas las aplicaciones no seguras|Microsoft Defender para aplicaciones en la nube|Marcar aplicaciones no seguras como no autorizadas|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Integración de Microsoft Defender para punto de conexión con Defender for Cloud Apps

Para controlar el uso de la aplicación en los dispositivos de usuario que sean propiedad de la empresa, debes integrar Defender para punto de conexión con Defender for Cloud Apps.

1. Inicia sesión en el portal de Microsoft Defender **https://security.microsoft.com/** como Allan Deyoung con su cuenta de **Administrador MOD.**
2. En el portal de Microsoft Defender, expande **Búsqueda** y selecciona **búsqueda avanzada de amenazas**. Espera a que finalice la preparación de los nuevos espacios.
3. En el portal de Microsoft Defender, en el menú de navegación izquierdo, selecciona **Configuración**.
4. Selecciona **Puntos de conexión** en la página **Configuración**.
5. En la página **Puntos de conexión**, en **General**, selecciona **Características avanzadas**.
6. Habilitar **Microsoft Defender for Cloud Apps**.
7. Selecciona **Guardar preferencias** en la parte inferior.

Has habilitado correctamente Microsoft Defender for Cloud Apps para punto de conexión. Con esta configuración, todas las señales procedentes de Microsoft Defender para punto de conexión se reenvían a Defender for Cloud Apps, lo que te ofrece la capacidad de bloquear aplicaciones no seguras. Todas las aplicaciones etiquetadas como **No autorizadas** ahora se bloquearán.

### Tarea 2: Investigar Shadow-IT de Contoso Ltd.

En esta tarea, analizarás todas las aplicaciones que se usan actualmente en tu empresa. Se examinarán más detenidamente varias aplicaciones y su respectiva evaluación de riesgos, así como su estructura de evaluación.

1. Todavía deberías tener iniciada la sesión en el portal de Microsoft Defender **https://security.microsoft.com/**.
2. En el portal de Microsoft Defender, en la página de navegación izquierda, expande **Aplicaciones en la nube** y selecciona **Cloud Discovery**.
3. En la página **Cloud Discovery**, selecciona **Aplicaciones detectadas**.
4. En la hoja **Aplicaciones detectadas** se muestran todas las aplicaciones que se usan actualmente en la organización. Explora varias aplicaciones y sus puntuaciones de riesgo asociadas seleccionando cada aplicación respectiva.

> [!NOTE] Defender for Cloud Apps evalúa el riesgo en función de certificaciones normativas, estándares del sector y procedimientos recomendados. La puntuación refleja la madurez de la idoneidad de la aplicación para el uso empresarial. Calcula una puntuación total para cada aplicación mediante el promedio de subscores ponderados en varias categorías de riesgo que incluyen consideraciones para la confiabilidad.

Has revisado correctamente varias aplicaciones que se usan actualmente en Contoso.

### Tarea 3: Bloquear aplicaciones no seguras

Una vez que hayas obtenido correctamente información general sobre el uso de aplicaciones en tu entorno, tu primera acción de corrección es bloquear aplicaciones no seguras.

1. Todavía deberías tener iniciada la sesión en el portal de Microsoft Defender **https://security.microsoft.com/**.
2. En el portal de Microsoft Defender, en la página de navegación izquierda, expande **Aplicaciones en la nube** y selecciona **Cloud Discovery**.
3. En la página **Cloud Discovery**, selecciona **Aplicaciones detectadas**.
4. Establece el filtro para **Puntuación de riesgo** en 0 - 4.
5. Selecciona **Selección en masa** y, después, **Todo**.
6. Selecciona los tres puntos para **Más acciones**.
7. Selecciona **Etiquetar como no autorizado**.
8. Seleccione **Guardar**.
   
Has bloqueado correctamente que los usuarios usen las aplicaciones vulnerables.

### Tarea 4: Bloquear aplicaciones no seguras automáticamente

Para bloquear automáticamente las aplicaciones no seguras en el futuro, crearás una directiva de detección de aplicaciones personalizada. Esta directiva etiquetará las aplicaciones no seguras como **No autorizadas**. Como has integrado Defender para punto de conexión con Defender for Cloud Apps, estas aplicaciones se bloquearán automáticamente.

1. Todavía deberías tener iniciada la sesión en el portal de Microsoft Defender **https://security.microsoft.com/**.
2. En el portal de Microsoft Defender, en la página de navegación izquierda, expande **Aplicaciones en la nube** y selecciona **Cloud Discovery**.
3. En la página **Aplicaciones detectadas**, selecciona **+ Nueva directiva a partir de búsqueda**.
4. Escriba la siguiente información:
    - **Nombre de directiva**: etiquetar aplicaciones no seguras como no autorizadas
    - **Gravedad de la directiva**: media
    - **Descripción para los usuarios**: las aplicaciones con una puntuación de riesgo de 4 o menos serán no autorizadas y se bloquearán automáticamente.
5. En **Aplicaciones que coincidan con todo lo siguiente**, agrega un filtro y establécelo en **Puntuación de riesgo igual a 0-4**.
6. En **Alertas**, selecciona **Crear una alerta para cada evento coincidente con la gravedad de la directiva** y establece el valor de **Límite de alertas diarias por directiva** en 5.
7. En **Acciones de gobernanza**, selecciona **Etiquetar aplicación como no autorizada**.
8. Seleccione **Crear**.

Has creado correctamente una directiva para etiquetar aplicaciones con una puntuación de riesgo de 5 o inferior como no autorizada.