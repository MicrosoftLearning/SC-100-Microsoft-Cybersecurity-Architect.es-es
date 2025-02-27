---
lab: 4
title: 'Ejercicio 4: Seguridad de los puntos de conexión'
---

# Laboratorio 4 - Ejercicio 4: Seguridad de los puntos de conexión

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

1. Inicia sesión en el **https://intune.microsoft.com** Centro de administración de Microsoft Intune como Allan Deyoung con su cuenta **de administrador MOD**,
2. En el Centro de administración de Microsoft Endpoint Intune, selecciona **Seguridad de punto de conexión** en el panel de navegación de la izquierda.
3. En la página **Seguridad del punto de conexión | Información general**, en **Información general**, selecciona **Líneas base de seguridad**.
4. En la página **Seguridad del punto de conexión | Líneas de base de seguridad**, selecciona **Línea base de seguridad para Windows 10 y versiones posteriores**.
5. En la página **Línea base de seguridad de MDM | Perfiles**, selecciona **+ Crear perfil**.
1. Revisa la descripción de la hoja **Crear un perfil** y selecciona **Crear**.
1. En la hoja **Datos básicos** , escribe un nombre y una descripción.
1. Selecciona **Siguiente**.
1. En la hoja **Configuración **, investiga las distintas opciones de configuración. Cuando hayas terminado, haz clic en **Siguiente**.
1. En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**.
1. En la hoja **Asignaciones** en **Grupos incluidos**, selecciona **Agregar todos los usuarios** y selecciona **Siguiente**.
1. En la hoja **Revisar y crear**, selecciona **Crear**.
1. Volver a la página **Seguridad de los puntos de conexión | Líneas base de seguridad**.
1. En la página **Seguridad del punto de conexión | Líneas base de seguridad**, selecciona **Línea base de seguridad de Microsoft Defender para punto de conexión**.
1. En la **línea base de seguridad de Microsoft Defender para punto de conexión | Perfiles** selecciona **+ Crear perfil**.
1. Revisa la descripción de la hoja **Crear un perfil** y selecciona **Crear**.
1. En la hoja **Datos básicos** , escribe un nombre y una descripción.
1. Seleccione **Siguiente**.
1. En la hoja **Configuración **, investiga las distintas opciones de configuración. Cuando hayas terminado, haz clic en **Siguiente**.
1. En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**. 
1. En la hoja **Asignaciones** , en **Grupos incluidos**, selecciona **Agregar todos los usuarios** y selecciona **Siguiente**.
1. En la hoja **Revisar y crear**, selecciona **Crear**.

Has creado correctamente dos directivas de línea base de seguridad para dispositivos Windows.

### Tarea 2: Implementar antivirus en dispositivos macOS

Después de proteger los dispositivos Windows con directivas de línea base de seguridad de puntos de conexión, implementarás antivirus y habilitarás el cifrado en dispositivos macOS para preparar el entorno para la combinación con Trailwind Traders.

1. Todavía debes iniciar sesión en el Centro de administración de Microsoft Intune**https://intune.microsoft.com**.
2. En el Centro de administración de Microsoft Endpoint Intune, selecciona **Seguridad de punto de conexión** en el panel de navegación de la izquierda.
3. En la página **Seguridad del punto de conexión | Información general** en **Administrar** , selecciona **Antivirus**.
4. En la página **Seguridad del punto de conexión | Antivirus** , selecciona **+ Crear directiva**.
5. En el panel **Crear un perfil**, en **Plataforma**, selecciona **macOS** y, en **Perfil**, selecciona **Antivirus de Microsoft Defender**.
6. Seleccione **Crear**.
7. En la hoja **Datos básicos** , escribe un nombre y una descripción.
8. Seleccione **Siguiente**.
9. En la hoja **Configuración**, asegúrate de que las opciones están configuradas de la siguiente manera:

#### Preferencias de protección entregadas en la nube

- **Habilitar o deshabilitar la protección entregada en la nube**: habilitado (valor predeterminado)
- **Habilitar o deshabilitar envíos automáticos de ejemplo**: habilitado (valor predeterminado)
- **Nivel de recopilación de diagnóstico**: opcional (valor predeterminado)
- **Actualización de inteligencia de seguridad automática**: habilitada (valor predeterminado)

#### Programa antivirus

- **Habilitar la protección en tiempo real**: habilitado (valor predeterminado)
- **Habilitar el modo pasivo**: Deshabilitado (valor predeterminado)
- **Combinación de exclusión** : admin_only
- En **Configuración del tipo de amenaza**, selecciona **+ Agregar.**
  - **Tipo de amenaza**: potentially_unwanted_application
  - **Acción que se va a realizar**: bloquear
- **Combinación de la configuración del tipo de amenaza**: admin_only
- **Habilitación del cálculo de hash de archivos**: True
- **Ejecutar un examen después de actualizar las definiciones**: Habilitado (valor predeterminado)
- **Nivel de cumplimiento**: real_time

#### Protección de red

- **Nivel de cumplimiento**: bloque
  
#### Protección contra alteraciones

- **Nivel de cumplimiento**: bloque (valor predeterminado)

#### Preferencias de la interfaz de usuario

- **Controlar el inicio de sesión en la versión del consumidor**: habilitado (valor predeterminado)
- **Icono de menú Mostrar u ocultar estado**: Deshabilitado (valor predeterminado)
- **Comentarios iniciados por el usuario**: habilitado (valor predeterminado)

1.  Seleccione **Siguiente**.
2.  En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**.
3.  En la hoja **Asignaciones** del cuadro de texto, escribe **Todos los usuarios** y selecciónalo.
4.  Seleccione **Siguiente**.
5.  En la hoja **Revisar y crear**, selecciona **Guardar**.

Has configurado e implementado correctamente el antivirus para dispositivos macOS.

### Tarea 3 Cifrar dispositivos macOS

En esta tarea, cifrarás los dispositivos macOS.

1. Todavía debes iniciar sesión en el Centro de administración de Microsoft Intune**https://intune.microsoft.com**.
2. En el Centro de administración de Microsoft Endpoint Intune, selecciona **Seguridad de punto de conexión** en el panel de navegación de la izquierda.
3. En la página **Seguridad del punto de conexión | Información general** , en **Administrar** , selecciona **Cifrado de disco**.
4. En la página **Seguridad del punto de conexión | Cifrado de disco** selecciona **+ Crear directiva**.
5. En el panel **Crear un perfil** , en **Plataforma** , selecciona **macOS** y, en **Perfil** , selecciona **FileVault**.
6. Seleccione **Crear**.
7. En la hoja **Básico** , escribe un nombre y una descripción. Seleccione **Siguiente**.
8. En la hoja **Configuración** , en **Cifrado** , configura las opciones siguientes:
   - **Habilitar FileVault**: Sí
   - **Rotación de claves de recuperación personal**: 6 meses
   - **Descripción de la ubicación de depósito en garantía de la clave de recuperación personal**: para recuperar una clave de recuperación perdida o rotada recientemente, inicia sesión en el sitio web de Portal de empresa de Intune mediante cualquier dispositivo. Ve a la sección Dispositivos del portal, elige el dispositivo con FileVault habilitado y luego selecciona la opción para recuperar la clave de recuperación. El portal mostrará la clave de recuperación actual para ese dispositivo.
   - **Número de veces que se permite omitir**: 3
   - **Permitir aplazamiento hasta cerrar la sesión**: Sí
   - **Deshabilitar la solicitud al cerrar sesión**: Sí
   - **Ocultar clave de recuperación**: Sí
  
9.  Seleccione **Siguiente**.
10. En la hoja **Etiquetas de ámbito** , selecciona **Siguiente**.
11. En la hoja **Asignaciones**, en **Grupos incluidos**, selecciona **Agregar todos los usuarios**.
12. Seleccione **Siguiente**.
13. En la hoja **Revisar y crear**, selecciona **Crear**.

Has configurado e implementado correctamente un perfil de FileVault para cifrar dispositivos macOS.