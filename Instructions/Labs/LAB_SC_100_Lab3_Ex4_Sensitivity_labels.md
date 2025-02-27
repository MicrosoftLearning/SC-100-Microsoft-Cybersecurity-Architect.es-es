---
lab: 3
title: 'Ejercicio 4: Etiquetas de confidencialidad'
---

# Laboratorio 3 - Ejercicio 4: Etiquetas de confidencialidad

Contoso Ltd. está en proceso de adquirir Tailwind Traders. La administración ha decidido tratar todos los documentos de este proceso como estrictamente confidenciales para minimizar el riesgo de filtración de datos.

Se te han proporcionado los siguientes requisitos de seguridad para la etiqueta:

- El contenido solo se puede compartir con empleados internos de Contoso Ltd.
- El contenido debe cifrarse.
- Es posible que no se reenvíen archivos y correos electrónicos.
- Se prohíbe el acceso al contenido desde dispositivos no corporativos.
- El ámbito de esta etiqueta es la administración.

## Parte 1: Diseñar una solución (necesaria)

En esta tarea, diseñarás un concepto para solucionar los problemas a los que se enfrenta Contoso Ltd.

### Enfoque de diseño

Contoso tiene varias soluciones para proteger tus datos. El enfoque inicial sería analizar la configuración actual y decidir si cumplen los requisitos actuales. 

En función del escenario anterior, Microsoft Purview Information Protection se puede usar para cumplir los requisitos y proteger los datos adecuadamente. Las etiquetas de confidencialidad de Microsoft Purview Information Protection te permiten clasificar y proteger los datos de tu organización, a la vez que garantizan que las funcionalidades de colaboración y productividad del usuario permanezcan libres de obstáculos. 

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Cifrado de documentos y correos electrónicos|Microsoft Purview Information Protection|Implementación de una etiqueta de sensibilidad|
|Restricción del acceso a los datos desde dispositivos no administrados|Microsoft Purview Information Protection|Crear una etiqueta de confidencialidad|
|Restringir el acceso solo a usuarios internos|Microsoft Purview Information Protection|Crear una etiqueta de confidencialidad

## Parte 2: Implementar la solución (opcional)

### Tarea 1: Investigar las etiquetas de confidencialidad existentes

En esta tarea, investigarás las etiquetas de confidencialidad existentes y decidirás si es necesario crear una nueva etiqueta.

>[!NOTE] Ya debes haber instalado el módulo de PowerShell de Exchange Online. Si falta el módulo, sigue las instrucciones para instalar el módulo.

1. Abre una ventana de PowerShell elevada. Para ello, selecciona el botón Windows con el botón secundario del mouse y, a continuación, selecciona **Windows PowerShell (Admin)**.
1. Confirma la ventana **Control de cuentas de usuario** con **Sí**.
1. Escribe el siguiente cmdlet para instalar la versión más reciente del módulo Exchange Online PowerShell:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirma el cuadro de diálogo de seguridad de repositorio no de confianza con **Y** para Sí y presiona **Entrar**.  Este proceso puede tardar un tiempo en finalizar.
1. Escribe el siguiente cmdlet para conectarte a Security & Compliance PowerShell:

    ```powershell
    Connect-IPPSSession
    ```
1. Cuando se muestra la ventana **Iniciar sesión**, deberás iniciar sesión como `admin@WWLxZZZZZZ.onmicrosoft.com` (donde ZZZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje de laboratorio) y utilizar la contraseña administrativa para el inquilino.
1. Escribe el siguiente cmdlet para obtener una lista de todas las etiquetas de confidencialidad implementadas.

    ```powershell
    Get-Label | Format-Table -wrap ParentLabelDisplay,DisplayName,LabelActions
    ```
Este cmdlet muestra todas las etiquetas de confidencialidad implementadas y las acciones correspondientes. Examina las etiquetas. Decide si las etiquetas existentes cumplen los requisitos empresariales o si se requiere un nuevo etiquetado. Cuando hayas terminado, continúa con la siguiente tarea.

### Tarea 2: Habilitar la compatibilidad con etiquetas de confidencialidad para grupos y sitios

En una tarea anterior, has revisado las etiquetas existentes y has llegado a la conclusión de que las etiquetas existentes actuales no cumplen el requisito empresarial de la empresa. Para aplicar etiquetas de confidencialidad a grupos y sitios, debes habilitar la compatibilidad con etiquetas de confidencialidad en PowerShell.

1. Abre una ventana de PowerShell con permisos elevados. Para ello, selecciona el menú Inicio con el botón derecho del ratón y luego selecciona Windows PowerShell y Ejecutar como administrador.
1. Confirma la ventana Control de cuentas de usuario con Sí y presiona Entrar.
1. En primer lugar, es necesario instalar el SDK de PowerShell de Microsoft Graph. Puesto que se incluye en dos módulos, Microsoft.Graph y Microsoft.Graph.Beta, es necesario instalar ambos. Escribe el siguiente cmdlet para instalar la versión más reciente de Microsoft.Graph:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```
1. Confirma el cuadro de diálogo seguridad de Nuget y el cuadro de diálogo seguridad de repositorio no de confianza con Y para Sí y presiona Entrar. Este proceso puede tardar en completarse.
1. Escribe el siguiente cmdlet para instalar Microsoft.Graph.Beta:

```powershell
Install-Module Microsoft.Graph.Beta -Scope CurrentUser
```
1. Confirma la ventana Control de cuentas de usuario con Sí y presiona Entrar.
1. Conéctate al inquilino:

```powershell
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
```

1. En el formulario Iniciar sesión en tu cuenta, inicia sesión como admin@WWLxZZZZZZ.onmicrosoft.com, (donde ZZZZZZ es el identificador de inquilino único proporcionado por el proveedor de hospedaje del laboratorio). El proveedor de hospedaje del laboratorio debe proporcionar la contraseña.
1. En la ventana **permisos solicitados** , selecciona **Consentimiento en nombre de la organización** y selecciona **Aceptar**. Después de iniciar sesión, elige la ventana de PowerShell.
1. Escribe el siguiente cmdlet para habilitar etiquetas de confidencialidad:

```powershell
$params = @{
     Values = @(
        @{
            Name = "EnableMIPLabels"
            Value = "True"
        }
     )
}

Update-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id -BodyParameter $params
```

1. Cierra la ventana PowerShell.

Has habilitado correctamente la compatibilidad con las etiquetas de confidencialidad para sitios y grupos.

### Tarea 3: Crear e implementar una etiqueta de confidencialidad de alta seguridad

Crearás una nueva etiqueta de confidencialidad para cumplir los requisitos.

1. Inicia sesión en el portal de cumplimiento de Microsoft Purview **https://compliance.microsoft.com/** como Allan Deyoung con su cuenta de administrador **Administrador de MOD**.
1. En el portal de Microsoft Purview, en el panel de navegación izquierdo, expande **Protección de información** y selecciona **Etiquetas**.
1. En la página **Etiquetas**, selecciona **+ Crear una etiqueta**.
1. En la página **Proporcione los detalles básicos de esta etiqueta**, escribe la siguiente información:

    - **Nombre**: Confidencial- Proceso de adquisición
    - **Nombre para mostrar**: Confidencial - Proceso de adquisición
    - **Descripción de los usuarios**: datos extremadamente confidenciales relacionados con cualquier proceso de adquisición.
    - **Descripción para los administradores**: esta etiqueta proporciona protección a los datos relacionados con cualquier adquisición de Contoso.

1. Seleccione **Siguiente**.
1. En la página **Definir el ámbito de esta etiqueta**, selecciona **Elementos**, selecciona **Archivos**, **Correos electrónicos** y **Grupos y sitios**. Si se seleccionan otras opciones de esta página, anula la selección de esas opciones.
1. En la página **Elegir la configuración de protección para los elementos etiquetados**, selecciona **Agregar o quitar cifrado**.
1. En la página **Cifrado**, selecciona **Configurar opciones de cifrado**.
1. En la configuración de cifrado, especifica la información siguiente: 
    - **Asignar permisos ahora o permitir que los usuarios decidan?**: permitir que los usuarios asignen permisos cuando apliquen la etiqueta.
    - **En Outlook, aplique una de las restricciones siguientes**: No reenviar.
1. Selecciona **En Word, PowerPoint y Excel, pide a los usuarios que especifiquen permisos** y, después, selecciona **Siguiente**.
1. En la página **Etiquetado automático de archivos y correos electrónicos**, selecciona **Siguiente**.
1. En la **página Definir la configuración de protección para grupos y sitios** , selecciona **Privacidad y acceso de usuario externo** y **Uso compartido externo y Acceso condicional** y, a continuación, selecciona **Siguiente**.
1. En la página **Privacidad de datos y configuración de acceso de usuario externo**, selecciona **Privado** y después selecciona **Siguiente**.
1. En la página **Definir configuración de uso compartido externo y acceso condicional**, selecciona **Controlar el uso compartido externo de sitios de SharePoint etiquetados** y **Usar el Acceso condicional de Microsoft Entra para proteger los sitios de SharePoint etiquetados** y establece la configuración como se indica a continuación:
    - **El contenido solo se puede compartir con** : miembros de la organización.
    - **Determinar si los usuarios pueden acceder a sitios de SharePoint desde dispositivos no administrados**: Bloquear el acceso
1. Seleccione **Siguiente**.
1. En la página **Etiquetado automático para recursos de datos esquematizados (versión preliminar)**, selecciona **Siguiente**.
1. En la página **Revisar la configuración y finalizar**, selecciona **Crear etiqueta**.
1. En la página **Se creó la etiqueta de confidencialidad**, selecciona **Publicar etiqueta en las aplicaciones de los usuarios**.
1. Selecciona **Listo.**
1. En la página **Publicar etiqueta**, selecciona **Crear una nueva directiva de etiquetas**.
1. En la página **Elegir etiqueta de confidencialidad para publicar** , selecciona la etiqueta que acabas de crear y selecciona **Siguiente**.
1. En la página **Asignar unidades de administración**, selecciona **Siguiente**.
1. En la página **Publicar en usuarios y grupos** , selecciona **Usuarios y grupos** y selecciona **Editar**.
1. En la página **Ámbito para usuarios y grupos** , selecciona **Usuarios y grupos específicos** y selecciona **+ Incluir usuarios y grupos** y, a continuación, selecciona **Ejecutivos** y **Liderazgo** y finalmente selecciona **Listo** hasta que finalice la asignación de usuarios.
1. Seleccione **Siguiente**.
1. En la página **Configuración de directiva**, selecciona **Los usuarios deben proporcionar una justificación para quitar una etiqueta o rebajar su clasificación** y **Requerir que los usuarios apliquen una etiqueta al correo electrónico y a los documentos**.
1. Seleccione **Siguiente**.
1. En la página **Configuración predeterminada de documentos** , selecciona **Correo electrónico hereda la etiqueta de prioridad más alta de los datos adjuntos** y selecciona **Siguiente**.
1. En la página **Configuración predeterminada para reuniones y eventos de calendario**, selecciona **Siguiente**.
1. En la página **Configuración predeterminada para grupos y sitios**, selecciona **Siguiente**.
1. En la página **Configuración predeterminada del contenido de Fabric y Power BI**, selecciona **Siguiente**.
1. En la página **Nombrar directiva**, escribe la información siguiente:
    - **Nombre**: Directiva de etiqueta de confidencialidad de administración
    - **Descripción**: esta directiva está diseñada para la administración de la protección en relación con la adquisición de empresas
1. Seleccione **Siguiente**.
1. En la página **Revisar y finalizar**, seleccione **Enviar**.

Has creado y publicado correctamente una etiqueta de confidencialidad.