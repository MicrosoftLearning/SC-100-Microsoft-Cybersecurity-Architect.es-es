# Acceso condicional

Has descubierto que los empleados acceden a Microsoft 365 desde ubicaciones desconocidas, a pesar de que las directivas de acceso condicional solo permiten el acceso desde ubicaciones y dispositivos específicos. Tu investigación ha revelado que estos empleados acceden a Microsoft 365 mientras viajan a casa desde su oficina en transporte público. Este comportamiento infringe las regulaciones del sector y quieres usar la evaluación continua de acceso para evitarlo. Además, quieres implementar la intensidad de la autenticación que preparaste en el ejercicio anterior para proteger determinadas aplicaciones que controlan los datos del cliente. 

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los riesgos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del problema descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Restringir el acceso desde ubicaciones no seguras o desconocidas
- Requerir autenticación sólida para las aplicaciones que contienen información confidencial

En el segundo paso, examina el entorno existente de Contoso Ltd. Microsoft Entra ID ofrece soluciones para administrar y restringir el acceso de los usuarios con el uso de directivas de acceso condicional de Entra ID. Investiga qué controles existen y qué directivas ya están en vigor. Usa el portal de Entra ID para revisar las configuraciones y directivas actuales y determinar si es necesario realizar ajustes o si es necesario implementar nuevas directivas.

La tercera fase implica la elaboración del concepto de la solución. Tras la investigación, es evidente que aún no hay ninguna red de confianza configurada y ninguna de las directivas actuales cumple los requisitos definidos. Por lo tanto, es esencial un nuevo conjunto de directivas de acceso condicional. 

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Restringir el acceso desde ubicaciones no seguras o desconocidas|Directiva de acceso condicional de Entra ID|Definir las redes de la empresa actual como red de confianza y restringir el acceso a los dispositivos dentro de esta red|
|Requerir autenticación sólida para las aplicaciones que contienen información confidencial|Directiva de acceso condicional de Entra ID|Crear una nueva directiva de acceso condicional con ámbito a aplicaciones confidenciales que requieran la intensidad de la autenticación protegida recién creada que excluye métodos de autenticación no seguros, como SMS y Voz|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Crear una red de confianza

En esta tarea, crearás una ubicación con nombre mediante la dirección IP externa de la máquina virtual para definir una red de confianza que puedes usar en una directiva de acceso condicional en las siguientes tareas. Usarás esta dirección porque tu máquina se encuentra dentro de la red de la empresa.

1. Inicia sesión en la máquina virtual cliente 1 (LON-Sc1) como cuenta **lon-sc1\admin** . El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Abre una ventana de **PowerShell**. Para ello, selecciona el menú Inicio con el botón derecho del ratón y luego selecciona **Terminal**.
1. Escribe el siguiente cmdlet para comprobar tu dirección IP externa actual:
    ```powershell
    curl ifconfig.me | Select-String -Pattern '.'
    ```
1. Anota la dirección IP de PowerShell devuelta.
1. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **`https://entra.microsoft.com`** e inicia sesión en el portal de Entra ID como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). La contraseña de administrador te la debería haber proporcionado tu proveedor de servicios de hospedaje de laboratorio.
1. Si se te pide que configures la autenticación multifactor, sigue las instrucciones.
1. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla **No volver a mostrar esto** y, a continuación, selecciona **No**.
1. Cierra el cuadro de diálogo Guardar contraseña. Para ello, selecciona **No ahora** para no guardar las credenciales predeterminadas del administrador global en el explorador.
1. En el panel de navegación izquierdo, ve a **Protección** > **Acceso condicional** > **Ubicaciones con nombre**.
1. Selecciona **+ Ubicación de los intervalos de direcciones IP**.
1. Escribe el nombre **Red de confianza Contoso**.
1. Seleccione **Marcar como ubicación de confianza**.
1. Selecciona **+** para agregar la dirección IP que anotaste en el **Paso 4.**
1. La entrada debe ser similar a ``168.245.***.***/32`` (*** puede ser diferente en función del proveedor de hospedaje del laboratorio).
1. Seleccione **Agregar**.
1. Seleccione **Crear**.

Ahora has definido la dirección IP externa de la empresa denominada y la ubicación de confianza que puedes usar para restringir el acceso fuera de la red de la empresa.

### Tarea 2: Crear una nueva directiva de acceso condicional con ámbito limitado

Como has creado correctamente una red de confianza, ahora la usarás para crear la directiva de acceso condicional para restringir el acceso fuera de la red corporativa con un ámbito limitado a tu usuario personal para poder probar y evitar que un bloqueo de cuenta en toda la empresa se bloquee con Entra ID.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com**.
2. En el panel de navegación izquierdo, ve a **Protección** > **Acceso condicional** > **Directivas**.
3. Selecciona **+ Nueva directiva**.
4. Escribe el nombre **Bloquear acceso fuera de la red de confianza**.
5. Selecciona **0 usuarios y grupos seleccionados**.
6. En la pestaña **Incluir**, elige **Seleccionar usuarios y grupos** y, luego, elige **Usuarios y grupos**.
7. Selecciona **Allan Deyoung** como el único usuario de prueba de la directiva.
8. Selecciona **Ningún recursos de destino seleccionado**y en **Incluir**, selecciona **Todas las aplicaciones en la nube**.
9. Selecciona **0 condiciones seleccionadas** y, en **Ubicaciones** , selecciona **No configurado**.
10. Selecciona **Sí** para configurar la condición de ubicación.
11. En **Incluir**, selecciona **Cualquier ubicación**.
12. En **Excluir**, selecciona **Todas las ubicaciones de confianza**.
13. En **Conceder** , selecciona **0 controles seleccionados** y cámbialo de **Conceder acceso** a **Bloquear acceso** y elige **Seleccionar** en la parte inferior de la página.
14. En **Sesión**, selecciona **0 controles seleccionados**.
15. Habilita **Personalizar la evaluación de acceso continuo** y selecciona **Aplicar estrictamente directivas de ubicación (versión preliminar)** y elige **Seleccionar** en la parte inferior para confirmar.
16. En **Habilitar directiva**, selecciona **Activar** y después selecciona **Crear**.

Ahora has creado y habilitado la directiva de CA para restringir el acceso fuera de las redes de confianza que solo afectan a tu propia cuenta de usuario de prueba.

### Tarea 3: probar la directiva configurada

Puesto que has creado una directiva de acceso condicional que limita el acceso a todas las aplicaciones en la nube de tu empresa, debes asegurarte de que el acceso sigue siendo posible.

>[! ALERT] Esta tarea se abrevia significativamente con fines ilustrativos.
En un escenario real, haría un período de prueba más largo con un grupo más grande y representativo para asegurarse de que ningún incidente imprevisible distorsiona el resultado.

1. Abre una nueva ventana **InPrivate** en el navegador **Microsoft Edge**. Para ello, selecciona el icono de barra de tareas con el botón derecho del ratón y luego selecciona **Nueva ventana InPrivate**.
1. Selecciona la barra de direcciones, ve a **`https://portal.microsoft.com`** e inicia sesión en el portal de M365 como **Allan Deyoung**alland@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
1. En el cuadro de diálogo ¿Mantener la sesión iniciada?, activa la casilla **No volver a mostrar esto** y, a continuación, selecciona **No**.
1. Dado que el inicio de sesión se realizó correctamente, puedes cerrar la ventana **InPrivate**.
1. Vuelve a la ventana del explorador Edge en la que todavía debes iniciar sesión en el portal de Entra ID**https://entra.microsoft.com**.
1. En el panel de navegación izquierdo, ve a **Protección** > **Acceso condicional** > **Supervisión** > **Registros de inicio de sesión**.
1. Selecciona **Agregar filtros** y filtra por el **usuario** de **Allan Deyoung**.
1. Selecciona la entrada de registro más reciente de **Allan Deyoung**.
1. En la pestaña **Acceso condicional**, selecciona **Bloquear acceso fuera de la red de confianza**.
1. Selecciona la asignación de **usuario** y deberías ver que **coincide ** con la **asignación directa**.
1. Selecciona la asignación de **aplicación** y deberías ver que **coincide** con **todas las aplicaciones incluidas**.
1. También deberías ver que la condición **Ubicación** no** coincide**, ya que está dentro de la red de confianza que se excluye.
Si intentaste iniciar sesión desde una red con una dirección IP externa diferente, esta condición coincidiría y bloquearía el intento de inicio de sesión.
1. Cierra los **detalles de la directiva de acceso condicional** y los **detalles de la actividad: inicios de sesión**.

Ahora has probado y asegurado el acceso a todas las aplicaciones en la nube desde la red de la empresa. También has comprobado los registros de inicio de sesión para asegurarte de que la directiva funciona según lo previsto y usa las asignaciones y condiciones correctas para restringir el acceso a las aplicaciones en la nube desde fuera de la red de la empresa.

### Tarea 4: implementación de directivas para toda la empresa

Después de la prueba correcta en la tarea anterior, ahora puedes habilitar la directiva para toda la empresa. Para ello, editarás el ámbito de usuario de la directiva existente.

>[! ALERT] Las acciones implementadas en esta tarea pueden provocar el bloqueo de la cuenta.
Asegúrate de que tienes al menos una cuenta de administrador de emergencia que se excluye de esta directiva en un escenario productivo y real. 

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com**.
2. En el panel de navegación izquierdo, ve a **Protección** > **Acceso condicional** > **Directivas**.
3. Selecciona la directiva **Bloquear el acceso fuera de la red de confianza**.
4. En Usuarios, selecciona **Usuarios específicos incluidos**.
5. Seleccione **Todos los usuarios**.
6. En la advertencia que aparece en la parte inferior de la ventana, selecciona **Excluir usuario actual, admin@WWLxZZZZZZ.onmicrosoft.com, de esta directiva**.
7. Seleccione **Guardar**.

Ahora has configurado una directiva de acceso condicional activa que impide que los usuarios inicien sesión fuera de la red de confianza que definiste como dirección IP externa de la empresa. Esto se probó mediante un ámbito de usuario limitado para asegurar que todas las aplicaciones en la nube siguen siendo accesibles. Por último, has implementado la directiva de CA para todos los usuarios.

Has restringido correctamente el acceso desde fuera de la red de confianza.

### Tarea 5: Requerir MFA para Salesforce

En esta Tarea, crearás una directiva de CA para aplicar la intensidad de autenticación que creaste en el ejercicio anterior al iniciar sesión en Salesforce. 

>[!IMPORTANT] Importante: esta tarea omitirá la fase de prueba. En un escenario real, probarías primero con un ámbito de usuario limitado, como se ve en las tareas anteriores y realizarás un lanzamiento completo después de una fase de prueba correcta.

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com**.
2. En el panel de navegación izquierdo, ve a **Protección** > **Acceso condicional** > **Directivas**.
3. Selecciona **+ Nueva directiva**.
4. Escribe el nombre **Intensidad de autenticación de Salesforce**.
5. Selecciona **0 usuarios y grupos seleccionados**.
6. En la pestaña **Incluir**, elige **Seleccionar usuarios y grupos** y, luego, elige **Usuarios y grupos**.
7. Selecciona **Alex Wilber** en Ventas como el único usuario de prueba de la directiva.
8. Selecciona **No hay recursos de destino seleccionados** y, en **Incluir**, selecciona **Seleccionar aplicaciones**.
9. En **Seleccionar**, selecciona **Ninguno** y busca **Salesforce**.
10. Para confirmar tu elección, selecciona **Seleccionar**.
11. En **Conceder**, selecciona **0 controles seleccionados** y habilita **Requerir intensidad de autenticación**.
12. Selecciona tu intensidad de autenticación creada personalizada **MFA protegida** y confirma con el botón **Seleccionar**.
13. Ahora establece la directiva en **Activado** con la barra de control de la parte inferior y selecciona **Crear**.
14. Después de una fase de prueba correcta con el ámbito de usuario limitado, selecciona **Intensidad de autenticación de Salesforce**.
15. En Usuarios, selecciona **Usuarios específicos incluidos**.
16. Seleccione **Todos los usuarios**.
17. Seleccione **Guardar**.

Ahora has creado una directiva de CA para aplicar la directiva de intensidad de autenticación a Salesforce excepto SMS OTP y, por tanto, evitar ataques correctos mediante la interceptación de SMS.
