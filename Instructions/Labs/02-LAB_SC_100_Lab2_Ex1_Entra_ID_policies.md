# Configuración de Entra ID

Eres Allan Deyoung, el recién ascendido especialista en seguridad de TI de Contoso Ltd. Cuando la empresa adquirió Tailwind Traders, revisaste el inquilino de Entra ID y decidiste sobre nuevos requisitos de seguridad. La tarea consiste en administrar las tareas e implementar directivas para cumplir los requisitos que se incluyen con la adquisición.

Has revisado las aplicaciones empresariales y has indicado que algunos usuarios han proporcionado permisos para que una aplicación de terceros acceda a sus datos de buzón. Se trata de un riesgo potencial para la pérdida de datos de la correspondencia por correo electrónico. Por lo tanto, deseas restringir este comportamiento pero permitir que los usuarios inicien sesión y compartan los identificadores de inicio de sesión en sitios web que Microsoft ha validado. También quieres permitir que los usuarios soliciten acceso específico a nuevos productos SaaS mediante su identidad de Entra ID. 

Dado que se ha atacado recientemente una organización asociada mediante la interceptación de SMS, quieres aplicar la comprobación de la autenticación después de NIST. Para ello, crearás una directiva de fortaleza de autenticación para desactivar OTP de SMS y restringir el uso de métodos de autenticación AAL1 en la organización. Crearás esta configuración en el portal de Entra ID.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los riesgos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

El paso inicial implica analizar los requisitos en función del problema descrito, comprender los objetivos y definir los requisitos.

En función del caso de uso proporcionado, se pueden indicar los siguientes requisitos:

- Restringir el acceso no controlado desde aplicaciones de terceros
- Permitir que los usuarios compartan identificadores de inicio de sesión para servicios validados
- Permitir que los usuarios soliciten acceso a productos SaaS
- Mejora de la intensidad de la autenticación

En el segundo paso, examina el entorno existente de Contoso Ltd. Microsoft Entra ID ofrece soluciones para administrar y restringir el acceso de la aplicación en la nube y del usuario con el uso de directivas de Entra ID. Investiga qué controles existen y qué directivas ya están en vigor. Usa el portal de Entra ID para revisar las configuraciones y directivas actuales y determinar si es necesario realizar ajustes o si es necesario implementar nuevas directivas.

La tercera fase implica la elaboración del concepto de la solución. Tras la investigación, es evidente que ninguna de las directivas actuales cumple los requisitos definidos. Por lo tanto, los ajustes en la configuración de Entra ID son esenciales.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Bloquear el acceso no controlado desde aplicaciones de terceros|Directiva de aplicación de Entra ID|Restringir el consentimiento del usuario a los permisos clasificados como de "bajo impacto", para las aplicaciones de publicadores verificados o aplicaciones registradas en esta organización.|
|Permitir que los usuarios compartan identificadores de inicio de sesión para servicios validados|Directiva de aplicación de Entra ID|Restringir el consentimiento del usuario a los permisos clasificados como de "bajo impacto", para las aplicaciones de publicadores verificados o aplicaciones registradas en esta organización.|
|Permitir que los usuarios soliciten acceso a productos SaaS|Directiva de aplicación de Entra ID|Definir usuarios que son aptos para aprobar aplicaciones que son seguras para usar|
|Restringir el uso de métodos de autenticación no seguros|Métodos de autenticación de Entra ID|Crear una intensidad de autenticación excluyendo los métodos SMS y Voz|

## Parte 2: Implementar la solución (opcional)

**Nota:** Estos pasos de laboratorio deben ejecutarse en el perfil de laboratorio de M365.

### Tarea 1: Restringir el uso de aplicaciones de terceros a los servicios comprobados de Microsoft

En esta tarea restringirás el nivel de acceso que un usuario puede conceder a las aplicaciones. También agregarás la funcionalidad para que los usuarios soliciten acceso que no puedan permitirse a sí mismos. 

1. Inicia sesión en la máquina virtual cliente 1 (LON-Sc1) como cuenta **lon-sc1\admin** . El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Abre **Microsoft Edge**, selecciona la barra de direcciones, ve a **`https://entra.microsoft.com`** e inicia sesión en el portal de Entra ID como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). Escribe la contraseña de administrador que debería haberte proporcionado tu proveedor de hospedaje de laboratorio.
1. Si se te pide que configures la autenticación multifactor, sigue las instrucciones.
1. En el cuadro de diálogo **¿Mantener la sesión iniciada?**, activa la casilla **No volver a mostrar esto** y, a continuación, selecciona **No**.
1. Cierra el cuadro de diálogo Guardar contraseña. Para ello, selecciona **No ahora** para no guardar las credenciales predeterminadas del administrador global en el explorador.
1. En el panel de navegación izquierdo, ve a **Aplicaciones** > ** de identidad** > **Aplicaciones empresariales** > **Seguridad** > **Consentimiento y permisos de seguridad**.
1. Ve a **Clasificaciones de permisos**.
1. Entra sugerirá los permisos más usados para los permisos de **bajo riesgo** .
1. Comprueba todos estos permisos y selecciona **Sí, agregar permisos seleccionados** para clasificarlos como de **bajo riesgo** en el inquilino de Entra ID.
1. Ve a **Configuración del consentimiento del usuario**.
1. En **Consentimiento del usuario para aplicaciones**, selecciona la opción recomendada **Permitir el consentimiento del usuario para aplicaciones de editores verificados, para los permisos seleccionados**. Esto permite a los usuarios dar su consentimiento para los permisos clasificados como de "bajo impacto" (que seleccionó anteriormente), para las aplicaciones de publicadores comprobados.
1. Seleccione **Guardar**.
1. Ve a **Configuración de consentimiento del administrador** y habilita Solicitudes de consentimiento del administrador seleccionando **Sí**, para permitir a los usuarios solicitar el consentimiento del administrador a las aplicaciones que no pueden acceder al contenido.
1. Selecciona **+ Agregar usuarios** para agregar **`Lidia Holloway`** y **`MOD Administrator`** como usuarios que pueden revisar las solicitudes de consentimiento del administrador.
1. Selecciona **Guardar** en la ventana **Configuración del consentimiento del administrador**.
1. Mantén esta pestaña del navegador abierta para la siguiente tarea.

Ahora has configurado las opciones de consentimiento de la aplicación que limitan el acceso que cada usuario puede conceder a las aplicaciones. Los usuarios pueden seguir solicitando consentimiento de permisos a las aplicaciones y el equipo de administración de aplicaciones puede aprobarlas después de evaluar la necesidad y el riesgo de la aplicación específica.

### Tarea 2: crear un nivel de intensidad de autenticación

En esta tarea, usarás el portal Entra ID para crear un nivel de intensidad de autenticación propio para restringir el uso de una OTP por SMS en tu organización. 

1. Todavía deberías tener iniciada la sesión en el portal de Entra ID **https://entra.microsoft.com**.
2. En el panel de navegación izquierdo, ve a **Protección** > **Métodos de autenticación** > **Niveles de intensidad de autenticación**.
3. Selecciona **+ Nuevos niveles de intensidad de autenticación**.
4. Escribe el nombre **MFA protegida**.
5. Comprueba **MFA resistente a la suplantación de identidad**, **MFA sin contraseña** y **Autenticación multifactor**.
6. En Autenticación multifactor, desactiva los siguientes factores:
   - **Pase de acceso temporal (multiuso)**
   - **Contraseña + SMS**
   - **Contraseña + voz**
   - **Factor único federado + SMS**
   - **Factor único federado+ voz**
7. Seleccione **Siguiente**.
8. Revisa y comprueba que no quede ninguno de los factores anteriores en el nivel de intensidad de autenticación.
9.  Seleccione **Crear**.

Ahora has creado un nivel de intensidad de autenticación que restringe el uso de una OTP por SMS como factor de autenticación.
