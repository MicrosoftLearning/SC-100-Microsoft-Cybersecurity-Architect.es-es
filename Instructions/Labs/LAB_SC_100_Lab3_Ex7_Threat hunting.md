---
lab: 3
title: 'Ejercicio 7: Búsqueda de amenazas'
---


# Laboratorio 3- Ejercicio 7: Búsqueda de contenido en Microsoft Purview

Tu empresa se enfrenta a una grave amenaza para su integridad y seguridad. Se ha detectado un número significativo de correos electrónicos malintencionados. Tu tarea es identificar las direcciones del remitente o las líneas de asunto de estos correos electrónicos. Una vez que hayas identificado estos correos electrónicos malintencionados, debes eliminarlos en masa.

## Parte 1: Diseñar una solución (necesaria)

### Enfoque de diseño

El primer paso es identificar correos electrónicos malintencionados. Por lo tanto, es esencial un análisis del flujo de correo actual. El Portal de Microsoft Defender proporciona una información completa de todo el flujo de correo entrante y saliente, junto con otras funcionalidades para investigar este tráfico. La acción de corrección implica eliminar los correos electrónicos malintencionados. 

### Solución propuesta

|Requisito|Solución|Plan de acción|
|----|----|----|
|Identificar correos electrónicos malintencionados|Microsoft Defender para Office 365|Investigar el flujo del correo y analizar los encabezados de correo|
|Eliminación de riesgos que derivan de correos electrónicos malintencionados|Microsoft Defender para Office 365|Eliminar correos malintencionados|

### Tarea 1: Investigar correos malintencionados

Investigarás los correos entrantes en el portal de Microsoft Defender e identificarás qué correos son sospechosos y contendrán contenido malintencionado.

1. Inicia sesión en el portal de Microsoft Defender **https://security.microsoft.com** como Allan Deyoung con su cuenta de administrador **MOD Administrator**.
1. En el portal de seguridad de Microsoft expande **Correo electrónico y colaboración** y, a continuación, selecciona **Explorador**.
1. En la página **Explorador**, ajusta el período de tiempo de la consulta para ver todo el flujo de correo de los últimos 30 días y selecciona **Actualizar**
1. El resultado muestra todos los correos entrantes y salientes. Investiga el flujo de correo y el asunto de los correos.
1. Los correos con el asunto "Tienes tareas que vencen hoy" parecen sospechosos.
1. Selecciona el asunto para realizar una investigación más detallada.
1. En el panel **Tienes tareas que vencen hoy** que aparece nuevo, lee la información proporcionada y selecciona **Ver encabezado**.
1. En el panel **Encabezados de mensaje de correo electrónico**, selecciona **Copiar encabezado de mensaje** y selecciona **Analizador de encabezados de mensajes de Microsoft**.
1. Se abrirá una nueva pestaña en el navegador.
1. En la página **Analizador de encabezados de mensajes**, pega el encabezado de mensaje y selecciona **Analizar encabezados**.
1. Revisa el resultado.

Has revisado correctamente el flujo de correo en el portal de Microsoft Defender.

### Tarea 2: Realizar la eliminación masiva de correos malintencionados

Has llegado a la conclusión de que los correos con el asunto "Tienes tareas que vencen hoy" son ataques de suplantación de identidad (phishing). La acción de corrección implica una eliminación masiva de esos correos mediante PowerShell.

>[!NOTE] Ya debes haber instalado el módulo de PowerShell de Exchange Online. Si falta el módulo, sigue las instrucciones para instalar el módulo.

1. Abre una ventana de PowerShell elevada. Para ello, selecciona el botón Windows con el botón secundario del mouse y, a continuación, selecciona **Windows PowerShell (Admin)**.
1. Confirma la ventana **Control de cuentas de usuario** con **Sí**.
1. Escribe el siguiente cmdlet para instalar la versión más reciente del módulo Exchange Online PowerShell:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirma el cuadro de diálogo de seguridad de repositorio no de confianza con **Y** para Sí y presiona **Entrar**.  Este proceso puede tardar un tiempo en finalizar.
1. Abre una ventana de PowerShell elevada. Para ello, selecciona el botón Windows con el botón secundario del mouse y, a continuación, selecciona **Windows PowerShell (Admin)**.
1. Confirma la ventana **Control de cuentas de usuario** con **Sí**.
1. Escribe el siguiente cmdlet para conectarte a Security & Compliance PowerShell:

    ```powershell
    Connect-IPPSSession
    ```

1. Cuando se muestre la ventana **Iniciar sesión**, inicia sesión como admin@WWLxZZZZZZ.onmicrosoft.com (donde ZZZZZZ es tu identificador de inquilino único proporcionado por el proveedor de hospedaje de laboratorio) y usa la contraseña administrativa para el inquilino.
1. Escribe el siguiente cmdlet para realizar la búsqueda de contenido y especifica el período de tiempo en el cmdlet:

    ```powershell
    $Search=New-ComplianceSearch -Name "Purge phishing messages" -ExchangeLocation All -ContentMatchQuery '(Received:mm/dd/yyyy..mm/dd/yyyy) AND (Subject:"You have tasks due today")'
    Start-ComplianceSearch -Identity $Search.Identity
    ```
1. Escribe el siguiente cmdlet para eliminar mensajes de forma permanente:

    ```powershell
    New-ComplianceSearchAction -SearchName "Purge phishing messages" -Purge -PurgeType HardDelete
    ---
You have successfully performed a mass-deletion of malicious mails.