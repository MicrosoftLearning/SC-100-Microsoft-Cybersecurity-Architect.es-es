---
lab: 4
title: 'Ejercicio 3: Prevención de pérdida de datos'
---

# Laboratorio 4: Ejercicio 3: Prevención de pérdida de datos

Contoso Ltd. está integrando actualmente Tailwind Traders en sus proyectos. Aunque la fusión sigue en curso, ambas empresas operan dentro de inquilinos independientes. Los empleados de Tailwind Traders se consideran usuarios externos y se invitan como invitados al inquilino de Contoso para facilitar el uso compartido de archivos y sitios de SharePoint. En determinados proyectos, los empleados de Tailwind Traders seleccionados reciben clientes de Windows 11 administrados por Contoso Ltd. para garantizar el acceso total a los recursos internos a la vez que se mantiene la supervisión de la seguridad. El acceso a las aplicaciones de escritorio de M365 está bloqueado para dispositivos no administrados y estos usuarios solo pueden acceder al entorno a través de aplicaciones web. Los dispositivos administrados se protegen mediante varias directivas de Endpoint Manager. Contoso Ltd. ha implementado Microsoft Purview Information Protection para cifrar documentos confidenciales en función del tipo de información que contienen. 

Como arquitecto de ciberseguridad, recientemente has examinado varias actividades en el registro de actividad de Defender for Cloud Apps y has descubierto que algunos documentos marcados como confidenciales se copian en unidades USB externas. También has descubierto que los usuarios pueden almacenar los datos de empresa a los que tienen acceso en sus dispositivos personales no administrados. Esto plantea un problema importante que debe solucionarse. Como solución, diseñarás una directiva de seguridad para restringir el almacenamiento de datos de empresa en dispositivos personales no administrados. Esto ayudará a minimizar el riesgo de que se ponga en peligro la información confidencial.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los riesgos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del problema descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Prevenir la transferencia de datos a unidades USB
- Limitar el acceso a datos confidenciales desde dispositivos no administrados
- Bloquear la descarga de información confidencial desde dispositivos no administrados

En el segundo paso, examina el entorno existente de Contoso Ltd. Microsoft Purview y Microsoft Defender ofrecen varias soluciones para administrar el flujo de datos, que abarcan Microsoft Purview Information Protection, prevención de pérdida de datos, acceso condicional y directivas de retención. Investiga qué controles ya están en vigor. Accede a varios portales para revisar las configuraciones y directivas actuales, determinar si es necesario realizar ajustes o si es necesario implementar nuevas configuraciones o directivas.

La tercera fase implica la elaboración del concepto de la solución. Tras la investigación, es evidente que ninguna de las directivas actuales cumple los requisitos definidos. Por lo tanto, es esencial un nuevo conjunto de directivas.

### Solución propuesta

Diseña una directiva de seguridad para restringir el almacenamiento de datos de empresa en dispositivos personales no administrados. Esto ayudará a minimizar el riesgo de que se ponga en peligro la información confidencial. La directiva debe describir los tipos de datos que se consideran confidenciales y los dispositivos aceptables en los que se pueden almacenar. Además, la directiva debe proporcionar directrices para la transferencia segura de datos a dispositivos externos. Se debe requerir a los empleados que firmen un acuerdo que reconozca su comprensión de la directiva y su compromiso de cumplirla. La directiva debe comunicarse a todos los empleados y aplicarse a través de auditorías periódicas y medidas disciplinarias para el incumplimiento. También se deben realizar sesiones de formación periódicas para garantizar que los empleados conozcan los riesgos asociados con el almacenamiento de datos de empresa en dispositivos personales y la importancia de seguir la directiva. Por último, la directiva debe revisarse y actualizarse periódicamente para asegurarse de que sigue siendo eficaz y pertinente. 

|Requisito|Solución|Plan de acción|
|----|----|----|
|Bloquear el movimiento de datos a unidades USB|Prevención de pérdida de datos en punto de conexión|Impedir que todos los datos con una etiqueta confidencial se copien en una unidad USB|
|Restringir el acceso a datos confidenciales desde dispositivos no administrados|Aplicaciones Defender for Cloud|Bloquear copiar, cortar y pegar datos para dispositivos no administrados|
|Bloquear la descarga de información confidencial desde dispositivos no administrados|Aplicaciones Defender for Cloud|Bloquear la descarga de datos desde dispositivos no administrados|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Implementar una directiva de prevención contra la pérdida de datos

El primer paso del diseño de la solución implica la creación de una regla de prevención de pérdida de datos para puntos de conexión. Implementarás una regla DLP para bloquear la copia de datos en unidades USB. 

1. Inicia sesión en el portal de cumplimiento Microsoft Purview **https://compliance.microsoft.com** como Allan Deyoung con su cuenta de administrador **Administrador MOD**.
1. Si se te pide que vuelvas al portal de cumplimiento Microsoft Purview clásico, selecciona **Cambiar**.
1. En el portal de Microsoft Purview, en el panel de navegación izquierdo, expande **Prevención de pérdida de datos** y selecciona **Directivas**.
1. En la página **Directivas**, selecciona **+ Crear directiva**.
1. En la página **Empezar con una plantilla o crear una directiva personalizada**, selecciona **Personalizado**, **Directiva personalizada** y luego **Siguiente**.
1. En la página **Nombre de la directiva DLP**, escribe un nombre y una descripción y selecciona **Siguiente**.
1. En la página **Asignar unidades de administración**, selecciona **Siguiente**.
1. En la página **Elegir dónde aplicar la directiva**, selecciona solo **Dispositivos** y selecciona **Siguiente**.
1. En la página **Definir configuración de directivas** selecciona **Siguiente**.
1. En **Personalizar reglas avanzadas de DLP**, selecciona **+ Crear regla**.
1. Escribe un nombre y una descripción para la regla. 
1. En **Condiciones**, selecciona **+ Agregar condición** y, después, selecciona **Contenido incluye**.
1. Comprueba las condiciones siguientes:

    - **El contenido incluye**: 
      - Selecciona **Agregar** y luego **Etiquetas de confidencialidad**. Selecciona las etiquetas **Trusted People**, **Project - Falcon**, **Confidential**, **Highly Confidential**, **Confidential - Finance**. Haz clic en **Agregar**.
13. En **Acciones** , selecciona **+ Agregar una acción** y selecciona **Auditar o restringir actividades en dispositivos**.
14. Especifica las acciones siguientes:
   -    En **Actividades de archivo para todas las aplicaciones**, selecciona **Aplicar restricciones a una actividad específica**.
      - Asegúrate de que **Copiar en un dispositivo USB extraíble** está seleccionado y selecciona la opción **Bloquear** en el menú desplegable de esta configuración.
      - Deja intactos los valores restantes.
15. Seleccione **Guardar**.
16. Seleccione **Siguiente**.
17. En la página **Modo de directiva**, selecciona **Activar la directiva inmediatamente**. Seleccione **Siguiente**.
18.  En la página **Revisar y finalizar**, seleccione **Enviar**.

Has implementado correctamente una directiva de prevención de pérdida de datos que bloquea cualquier copia de datos en unidades USB.

### Tarea 2: Incorporación de aplicaciones al control de aplicaciones de acceso condicional

Parte de la solución consiste en crear directivas de sesión en Defender for Cloud apps. Las directivas de sesión ofrecen información completa sobre las aplicaciones en la nube a través de la supervisión en tiempo real de las sesiones. Estas directivas permiten acciones adaptadas según la directiva especificada para cada sesión de usuario. Para crear una directiva de sesión, el control de aplicaciones de acceso condicional debe implementarse en las aplicaciones. El Control de aplicaciones de acceso condicional agrega la supervisión en tiempo real y funcionalidades de control a las aplicaciones. La creación de una directiva de sesión sin incorporar ninguna aplicación al control de aplicaciones de acceso condicional no funcionará. El primer paso es incorporar aplicaciones que quieras proteger para el control de aplicaciones de acceso condicional. 

Hay dos maneras de incorporar aplicaciones al control de aplicaciones de acceso condicional:

- Agrega una aplicación manualmente en el portal de Microsoft Defender (Configuración > Aplicaciones en la nube > Aplicaciones conectadas > Aplicaciones de Control de aplicaciones de acceso condicional).
- Configura una directiva de acceso condicional para proteger aplicaciones con Defender for Cloud Apps.

Una directiva de acceso condicional reenvía todas las aplicaciones especificadas en la directiva a "Control de aplicaciones de acceso condicional de Defender for Cloud Apps". La próxima vez que un usuario inicie sesión en las aplicaciones especificadas, la aplicación correspondiente se agrega automáticamente al control de aplicaciones de acceso condicional. Puedes ver estas aplicaciones en el portal de Microsoft Defender. 
 
>**Sugerencia:** Antes de iniciar esta tarea, debes comprobar las aplicaciones de control de aplicaciones de acceso condicional existentes. Observarás que aún no se han incorporado aplicaciones. En esta fase, intenta crear una directiva de sesión en Defender for Cloud Apps y comprueba los mensajes de error que se producen.

En esta tarea, implementarás el control de aplicaciones de acceso condicional en las aplicaciones mediante la creación de una directiva de acceso condicional en Microsoft Entra. 

1. Inicia sesión en el portal de Microsoft Entra **https://entra.microsoft.com** como Allan Deyoung con su cuenta de administrador **Administrador MOD**.
2. En el portal de Microsoft Entra, expande **Protección** y selecciona **Acceso condicional**.
3. En la página **Acceso condicional | Información general**, selecciona **Directivas** y selecciona **+ Nueva directiva**.
4. Introduzca un nombre para la directiva.
5. En **Asignaciones**, selecciona **Usuarios** e incluye **Todos los usuarios**.
6. En **Asignaciones**, selecciona **Recursos de destino** e incluye **Todas las aplicaciones en la nube**.
7. En **Controles de acceso**, selecciona **Sesión**.
8. En el panel **Sesión**, selecciona **Utilizar el Control de aplicaciones de acceso condicional** y selecciona **Usar directiva personalizada...**. Luego cierra el panel **Sesión** con el botón **Seleccionar**.
9. En **Habilitar directiva**, selecciona **Activar**.
10. Si recibes una advertencia para excluir al usuario actual de la directiva, selecciona **Entiendo que mi cuenta se verá afectada por esta directiva. Continuar de todos modos.**.
11. Opcionalmente, especifica las condiciones y concede controles.
12. Seleccione **Crear**.

Ahora, inicia sesión en una de las aplicaciones web de Microsoft, como [Outlook](https://outlook.office365.com). La aplicación en la que inicies sesión se incorporará automáticamente al control de aplicaciones de acceso condicional. Inicia sesión en el portal de Microsoft Defender y ve las aplicaciones en el control de aplicaciones de acceso condicional.

Has creado correctamente una directiva de acceso condicional para reenviar todas las aplicaciones a Defender for Cloud Apps y las aplicaciones incorporadas al control de aplicaciones de acceso condicional.

### Tarea 3: Crear directivas de sesión en Defender for Cloud Apps

Crearás dos directivas de sesión en Defender for Cloud apps para bloquear las descargas de datos y restringir los permisos de los dispositivos no administrados.

1. Inicia sesión en el portal de Microsoft Defender **https://security.microsoft.com** como Allan Deyoung con su cuenta de administrador **MOD Administrator**.
1. En el portal de Microsoft Defender, selecciona **Cloud apps** > **Directivas** > **Administración de directivas**.
1. En la página **Directivas**, selecciona **+ Crear directiva** > **Directiva de sesión**.
1. En la página **Crear directiva de sesión**, selecciona la plantilla de directiva **Bloquear descarga en función de la inspección de contenido en tiempo real**.
1. Escribir un nombre de directiva.
1. Selecciona una gravedad de directiva y una categoría.
1. Escriba una descripción.
1. En **Tipo de control de sesión**, selecciona **Controlar la descarga de archivos (con inspección)**.
1. En **Origen de actividad**, en la sección **Actividades que coinciden con todo lo siguiente**, establece el siguiente filtro:

    - **Etiqueta de dispositivo**: selecciona **No es igual a** y selecciona **Compatible con Intune**.

10. En la sección **Archivos que coinciden con todo lo siguiente**, selecciona el siguiente filtro:

    - **Etiqueta de confidencialidad**: selecciona **Igual a** y selecciona las etiquetas **Confidencial**, **Extremadamente confidencial** y **Confidencial - Finanzas**.

11. En **Método de inspección**, selecciona **Servicio de clasificación de datos**, a continuación, selecciona **Cualquiera**, después, selecciona **Tipo de información confidencial...** y selecciona el tipo de información confidencial a la que quieres aplicar esta directiva.
12. En **Acciones**, selecciona **Bloquear**.
13. Seleccione **Crear** para crear la directiva.
14. Crea una segunda directiva como se describió anteriormente y selecciona la plantilla de directiva **Bloquear cortar o copiar y pegar en función de la inspección de contenido en tiempo real**.
15. En **Origen de actividad**, en **Actividades que coinciden con todo lo siguiente**, especifica la siguiente información: 

    - **Tipo de actividad**: selecciona **Igual a** y selecciona **Cortar o copiar elemento, Pegar elemento**
    - **Etiqueta de dispositivo**: selecciona **No es igual a** y selecciona **Compatible con Intune**

16. Deshabilita **Usar inspección de contenido** y selecciona **Crear** para crear la directiva.

Has creado correctamente dos directivas de sesión en Defender for Cloud Apps.
