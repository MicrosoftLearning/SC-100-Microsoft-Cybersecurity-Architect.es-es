---
lab: 3
title: 'Ejercicio 3: Preparación de la administración de riesgos de privacidad'
---


# Laboratorio 3- Ejercicio 3: Preparación de la administración de riesgos de privacidad

Como experto arquitecto en ciberseguridad de Contoso, has sido encargado de mejorar la posición de cumplimiento de la empresa como parte de su expansión europea. En concreto, trabajarás para mejorar la puntuación de Administración de riesgo de privacidad Priva. Para ello, usarás el Administrador de cumplimiento para identificar las acciones de mejora y delegar su implementación. Esto dará lugar a una mejora en la puntuación de cumplimiento de la administración de riesgos de privacidad. Además, agregarás una nueva directiva para las regiones de EE. UU. y EU. 

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los requisitos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del escenario descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Los administradores y otros usuarios con acceso a los informes no deben ver los nombres de los usuarios.
- Los riesgos de privacidad deben administrarse mediante un equipo designado
- Las directrices deben existir para los riesgos de privacidad

En el segundo paso, examina el entorno existente de Contoso Ltd. Microsoft Priva ofrece soluciones para administrar los riesgos de privacidad. Investiga qué controles existen y qué directivas ya están en vigor. Usa el portal de cumplimiento de Microsoft Purview para revisar las configuraciones actuales y determinar a qué ajustes se deben implementar para cumplir los requisitos de la región a la que se expanden.

La tercera fase implica la elaboración del concepto de la solución. Tras la investigación, es evidente que la creación de directivas para supervisar posibles riesgos es la mejor manera de cumplir los requisitos.  

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Los administradores y otros usuarios con acceso a los informes no deben ver los nombres de los usuarios.|Acción de mejora del cumplimiento|Asignar e implementar la acción de mejora **Anonimizar nombres de usuario a los usuarios en determinados roles**|
|Los riesgos de privacidad deben administrarse mediante un equipo designado|Roles de Microsoft Purview|Crear un grupo de roles con permisos para controlar los riesgos de privacidad y asignar los empleados designados|
|Las directrices deben existir para los riesgos de privacidad|Directiva de administración del riesgo de privacidad|Creación de una directiva de administración de riesgos de privacidad para alertar al equipo de administración de riesgos de privacidad de riesgos potenciales|

## Parte 2: Implementar la solución (opcional)

## Tarea 1: Examinar las posibles acciones de mejora del Administrador de cumplimiento para la administración de riesgos de privacidad y asignarles propietarios

En esta tarea obtendrás información general sobre las posibles acciones de mejora de la administración de riesgos de privacidad y las delegarás.

1. **Inicia sesión** en el **portal de cumplimiento Microsoft Purview****https://compliance.microsoft.com/**.
2. En el panel izquierdo, selecciona **Información general sobre la administración de riesgos de privacidad**.
3. Desplázate hacia abajo hasta la tarjeta **Mantente al día con las regulaciones y mejora tu posición de privacidad**.
4. Selecciona el botón **Ver acciones de mejora**.
5. Examina las posibles acciones de mejora. Piensa en qué acciones de mejora se pueden configurar preliminarmente y cuáles se pueden delegar en el equipo de seguridad.
6. Selecciona la acción de mejora **Habilitar administradores de operaciones de privacidad para crear y admitir las solicitudes de cumplimiento de derechos del interesado**.
7. Lee los detalles de la mejora.
8. Asigna **Megan Bowen** como Propietario de la acción de mejora mediante el menú desplegable.
9. Seleccione **Editar detalles** en la parte superior de la página.
10. Establece el **estado de implementación** en **Implementado**. Dado que asignaste **a Megan Bowen** los roles de administrador de solicitudes de derechos del interesado y los grupos de roles de administrador de administración de riesgos de privacidad en el último ejercicio.
11. En la parte inferior de la página, selecciona **Guardar y cerrar**.

Has asignado correctamente una acción de mejora a un empleado de seguridad.

## Tarea 2: Asignar e implementar la acción de mejora **Anonimizar nombres de usuario a los usuarios en determinados roles**

Debes asegurarte de que los usuarios se anonimizan en todos los componentes de Priva para la acción de mejora.

*Ve a 5. si todavía estás en la **introducción a las acciones de mejora.***
1. **Inicia sesión** en el **portal de cumplimiento Microsoft Purview****https://compliance.microsoft.com/**.
1. Selecciona **Administrador de cumplimiento** > **Acciones de mejora**.
1. Selecciona la acción de mejora **Anonimizar nombres de usuario a los usuarios en determinados roles**.
1. Asígnate **Administrador MOD** como Propietario para esta acción de mejora mediante el menú desplegable.
1. En **Detalles**, selecciona el vínculo **Iniciar ahora** al final de la descripción **Cómo implementar**.
1. Comprueba si la opción **Mostrar versiones anónimas de nombres de usuario** está seleccionada; si no es así, selecciónala y selecciona **Guardar**.
1. Cierre la pestaña del navegador.
1. Selecciona **Editar detalles** en la parte superior de la acción de mejora **Mostrar versiones anonimizadas de nombres de usuario**.
1. Establece el **estado de implementación** en **Implementado** y selecciona **Guardar**.
1. En la parte superior de la página, selecciona **Guardar y cerrar**.

Has asignado e implementado correctamente una acción de mejora.

## Tarea 3: Crear una directiva de administración de riesgos de privacidad

Esta última tarea consiste en crear la directiva de administración de riesgos de privacidad personalizada para las regiones de la UE y EE. UU.

1. Ve al **portal de cumplimiento Microsoft Purview****https://compliance.microsoft.com/**
2. En el panel izquierdo, selecciona **Administración de riesgos de privacidad** > **Directivas**.
3. Selecciona **Crear una directiva** en la parte superior derecha.
4. Selecciona **Crear** en la tarjeta **Personalizada**.
5. Selecciona la plantilla de directiva **Minimización de datos**.
6. Escribe el nombre de la directiva:**Minimización de datos EE. UU. y UE**.
7. Escribe la descripción:**Esta directiva está pensada para minimizar los datos relevantes de riesgo de privacidad guardados según las regulaciones de EE. UU. y la UE.**
8. Seleccione **Siguiente**.
9. Selecciona **Agregar grupos de clasificación**.
10. Seleccione:
    - RGPD mejorado
    - Ley Gramm-Leach-Bliley (GLBA) de EE. UU. mejorada
    - Ley de Seguros de Salud (HIPAA) de EE. UU. mejorada
    - Ley Patriota de EE. UU. mejorada
    - Datos de información de identificación personal (PII) de EE. UU. mejorados
    - Leyes de notificación de infracciones de estado de EE. UU. mejoradas
11. Selecciona **Agregar** y **Siguiente**.
12. Selecciona tosos los usuarios y grupos y selecciona **Siguiente**.
13. Selecciona todas las ubicaciones y selecciona **Siguiente**.
14. Establece el ajuste **El elemento no se ha modificado en los anteriores (días)** en 120.
15. En **Elegir frecuencia de notificaciones**, selecciona **Mensual, cada 1**.
16. En el **Vínculo al entrenamiento sobre privacidad**, escribe: https://learn.microsoft.com/en-us/privacy/"
17. Seleccione **Siguiente**.
18. Establece **Crear alertas** en **Activado**.
19. Establece **Alto volumen de datos personales** en 20 instancias.
20. Seleccione **Siguiente**.
21. Seleccione **Siguiente**.
22. Revisa la configuración y selecciona **Enviar**.

Has creado correctamente una directiva de administración de riesgos de privacidad para las leyes de protección de datos de EE. UU. y la UE.

Has terminado correctamente de configurar y delegar algunas acciones de mejora, directivas de administración de riesgos de pricacy y permisos de usuario. Puedes continuar con el ejercicio siguiente.
