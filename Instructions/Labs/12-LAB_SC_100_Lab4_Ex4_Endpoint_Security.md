# seguridad de los puntos de conexión

Contoso usa Microsoft Intune para administrar sus dispositivos y proporciona a sus empleados dispositivos Windows 10 y Windows 11. La empresa ha implementado varios perfiles de configuración en el pasado. Sin embargo, un análisis de infraestructura de toda la empresa reveló que las directivas existentes se crearon de forma independiente, lo que dificulta su visualización holística y seguimiento. Como arquitecto de ciberseguridad de la empresa, has decidido consolidar todas las configuraciones necesarias y críticas en un solo lugar. 

Además, el análisis reveló que Tailwind Traders usa dispositivos macOS en su entorno. Como parte de la próxima fusión, planea preparar el inquilino de Contoso para los nuevos dispositivos macOS.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para abordar los desafíos a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

En ese escenario concreto, se pueden detallar los siguientes requisitos:

- Consolidar todas las configuraciones para dispositivos Windows en un solo lugar
- Protección de dispositivos MacOS

Microsoft Endpoint Manager, con líneas base de seguridad, administra y protege de forma centralizada los puntos de conexión, incluidos escritorios, portátiles, dispositivos móviles y servidores. Integra herramientas como Intune y Configuration Manager, lo que permite una implementación eficaz de aplicaciones, cumplimiento de directivas, cumplimiento normativo y supervisión de dispositivos. 

Una directiva de línea base de seguridad consta de un conjunto de opciones de configuración recomendadas por Microsoft, detallando sus implicaciones de seguridad. Estas opciones de configuración se basan en comentarios de los equipos de ingeniería de seguridad de Microsoft, los grupos de productos, los partners y los clientes. Estas líneas de base abarcan opciones de configuración de dispositivos similares a las de varias directivas de Intune. La personalización de cada línea base implementada permite aplicar la configuración y los valores necesarios. Al establecer un perfil de línea base de seguridad en Intune, básicamente vas a crear una plantilla que comprende varios perfiles de configuración de dispositivos. Estas recomendaciones deben revisarse y adaptarse periódicamente según los requisitos empresariales correspondientes.

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Consolidar todas las configuraciones para dispositivos Windows en un solo lugar|Microsoft Endpoint Manager: Seguridad de puntos de conexión|Implementación de las directivas de la línea base de seguridad
|Protección de dispositivos MacOS|Microsoft Endpoint Manager|Implementación del antivirus en dispositivos macOS|

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Implementación de directivas de línea base de seguridad de puntos de conexión

El objetivo general es proteger los puntos de conexión de forma adecuada y consolidar tantas directivas como sea posible en un solo lugar. Para ello, crearás directivas de línea base de seguridad de puntos de conexión para dispositivos Windows en Intune.

1. Inicia sesión en la máquina virtual cliente Windows **LON-SC1** con la cuenta de **Administrador** local. El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. Inicia sesión en el centro de administración de Microsoft Intune **`https://intune.microsoft.com`** como **Administrador MOD**admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje de laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña del usuario.
1. Si ves un cuadro de información en la parte superior derecha de la pantalla que indica **Administrar autenticación multifactor**, selecciona la **X** para cerrarlo.
1. En el Centro de administración de Microsoft Endpoint Intune, selecciona **Seguridad de punto de conexión** en el panel de navegación de la izquierda.
1. En la página **Seguridad del punto de conexión | Información general**, en **Información general**, selecciona **Líneas base de seguridad**.
1. En la página **Seguridad del punto de conexión | Líneas de base de seguridad**, selecciona **Línea base de seguridad para Windows 10 y versiones posteriores**.
1. En la página **línea base de seguridad para Windows 10 y versiones posteriores | Perfiles**, selecciona **+ Crear perfil**.
1. Revisa la descripción de la hoja **Crear un perfil** y selecciona **Crear**.
1. En la hoja **Datos básicos**, escribe:
    1. Nombre: **`Secure Windows Endpoints`**
    1. Descripción: **`The Security Baseline for Windows 10 and later represents the recommendations for configuring Windows.`**.
1. Seleccione **Siguiente**.
1. En la hoja **Configuración **, investiga las distintas opciones de configuración. Cuando hayas terminado, haz clic en **Siguiente**.
1. En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**.
1. En la hoja **Asignaciones** en **Grupos incluidos**, selecciona **Agregar todos los usuarios** y selecciona **Siguiente**.
1. En la hoja **Revisar y crear**, selecciona **Crear**.
1. Volver a la página **Seguridad de los puntos de conexión | Líneas base de seguridad**.
1. En la página **Seguridad del punto de conexión | Líneas base de seguridad**, selecciona **Línea base de seguridad de Microsoft Defender para punto de conexión**.
1. En la **línea base de seguridad de Microsoft Defender para punto de conexión | Perfiles** selecciona **+ Crear perfil**.
1. Revisa la descripción de la hoja **Crear un perfil** y selecciona **Crear**.
1. En la hoja **Datos básicos**, escribe:
    1. Nombre: **`Defender for Endpoint Security Baseline`**
    1. Descripción: **`Security best practices for the Microsoft security stack on devices managed by Intune`**.
1. Seleccione **Siguiente**.
1. En la hoja **Configuración **, investiga las distintas opciones de configuración. Cuando hayas terminado, haz clic en **Siguiente**.
1. En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**.
1. En la hoja **Asignaciones** , en **Grupos incluidos**, selecciona **Agregar todos los usuarios** y selecciona **Siguiente**.
1. En la hoja **Revisar y crear**, selecciona **Crear**.

Has creado correctamente dos directivas de línea base de seguridad para dispositivos Windows.

### Tarea 2: Implementar antivirus en dispositivos macOS

Después de proteger los dispositivos Windows con directivas de línea base de seguridad de puntos de conexión, implementarás antivirus y habilitarás el cifrado en dispositivos macOS para preparar el entorno para la combinación con Trailwind Traders.

1. Todavía debes iniciar sesión en el Centro de administración de Microsoft Intune**https://intune.microsoft.com**.
1. En el Centro de administración de Microsoft Endpoint Intune, selecciona **Seguridad de punto de conexión** en el panel de navegación de la izquierda.
1. En la página **Seguridad del punto de conexión | Información general** en **Administrar** , selecciona **Antivirus**.
1. En la página **Seguridad del punto de conexión | Antivirus** , selecciona **+ Crear directiva**.
1. En el panel **Crear un perfil**, en **Plataforma**, selecciona **macOS** y, en **Perfil**, selecciona **Antivirus de Microsoft Defender**.
1. Seleccione **Crear**.
1. En la hoja **Datos básicos**, escribe:
    1. Nombre: **`Deploy antivirus on macOS devices`**
    1. Description (Descripción): **`Deploy antivirus and enable encryption on macOS devices to prepare your environment for merging with Trailwind Traders.`**
1. Seleccione **Siguiente**.
1. En la pestaña **Parámetros de configuración**, asegúrate de que las opciones están configuradas de la siguiente manera:
1. En **Preferencias de protección entregadas en la nube**:
    - Habilitar o deshabilitar protección entregada en la nube: **habilitado (valor predeterminado)**
    - Habilitar o deshabilitar envíos automáticos de muestra: **habilitado (valor predeterminado)**
    - Nivel de recopilación de diagnóstico: **opcional (valor predeterminado)**
    - Actualización automática de inteligencia de seguridad: **habilitado (valor predeterminado)**
1. En **Programa antivirus**:
    - Habilitar protección en tiempo real: **habilitado (valor predeterminado)**
    - Habilitar modo pasivo: **deshabilitado (valor predeterminado)**
    - Combinación de exclusión: **admin_only**
1. En **Configuración de tipo de amenaza**, selecciona **+ Agregar**:
    - En el cuadro de texto de Tipo de amenaza, escribe: **potentially_unwanted_application**
    - Acción que se va a realizar: **bloquear**
    - Combinación de la configuración del tipo de amenaza: **admin_only**
1. Habilitación del cálculo de hash de archivo: **True****
1. Ejecutar un examen después de actualizar las definiciones: **habilitado (valor predeterminado)**
1. Nivel de cumplimiento: **real_time**
1. En **Protección de red**:
    - Nivel de cumplimiento: bloquear
1. En **Protección contra alteraciones**:
    - Nivel de cumplimiento: **bloque (valor predeterminado)**
1. En las **Preferencias de la interfaz de usuario**
    - Controlar el inicio de sesión en la versión del consumidor: **habilitado (valor predeterminado)**
    - Icono de menú Mostrar u ocultar estado: **Deshabilitado (valor predeterminado)**
    - Comentarios iniciados por el usuario: **habilitado (valor predeterminado)**
1. Seleccione **Siguiente**.
1. En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**.
1. En la pestaña **Asignaciones**, en el cuadro de texto, escribe **Todos los usuarios** y selecciónalo.
1. Seleccione **Siguiente**.
1. En la pestaña **Revisar y crear**, selecciona **Guardar**.

Has configurado e implementado correctamente el antivirus para dispositivos macOS.

### Tarea 3 Cifrar dispositivos macOS

En esta tarea, cifrarás los dispositivos macOS.

1. Todavía debes iniciar sesión en el Centro de administración de Microsoft Intune**https://intune.microsoft.com**.
1. En el Centro de administración de Microsoft Endpoint Intune, selecciona **Seguridad de punto de conexión** en el panel de navegación de la izquierda.
1. En la página **Seguridad del punto de conexión | Información general** , en **Administrar** , selecciona **Cifrado de disco**.
1. En la página **Seguridad del punto de conexión | Cifrado de disco** selecciona **+ Crear directiva**.
1. En el panel **Crear un perfil** , en **Plataforma** , selecciona **macOS** y, en **Perfil** , selecciona **FileVault**.
1. Seleccione **Crear**.
1. En la hoja **Básico** , escribe:
    1. Nombre: **`Encrypt macOS devices`**
    1. Description (Descripción): **`FileVault provides built-in Full Disk Encryption for macOS devices.`**
    1. Seleccione **Siguiente**.
1. En la hoja **Configuración** , en **Cifrado** , configura las opciones siguientes:
   - Habilitar FileVault: **Sí**
   - Rotación de claves de recuperación personal: **6 meses**
   - Descripción de la ubicación del depósito en garantía de la clave de recuperación personal: **`To recover a lost or recently rotated recovery key, log in to the Intune Company Portal website using any device. Navigate to the Devices section within the portal, choose the device with FileVault enabled, and then select the option to retrieve the recovery key. The portal will display the current recovery key for that device.`**
   - Número de veces que se permite omitir: **3**
   - Permitir aplazamiento hasta cerrar la sesión: **Sí**
   - Deshabilitar la solicitud al cerrar sesión: **Sí**
   - Ocultar clave de recuperación: **Sí**
   - Seleccione **Siguiente**.
1. En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**.
1. En la hoja **Asignaciones** , en **Grupos incluidos**, selecciona **Agregar todos los usuarios** y, a continuación, selecciona **Siguiente**.
1. En la hoja **Revisar y crear**, selecciona **Crear**.

Has configurado e implementado correctamente un perfil de FileVault para cifrar dispositivos macOS.
