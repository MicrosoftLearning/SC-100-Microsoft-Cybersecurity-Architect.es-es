---
casestudy:
  title: 'Caso práctico: Diseño de soluciones con procedimientos recomendados de MCRA y MCSB'
  module: 'Module 03: Design solutions that align with MCRA and MCSB'
---

Este ejercicio de caso práctico está diseñado para aportar experiencia en la realización de algunas tareas de diseño conceptual relacionadas con los temas aprendidos en este módulo.

## Caso práctico: Diseño de soluciones con procedimientos recomendados de MCRA y MCSB
 
CONTOSO es una empresa de servicios médicos cuyas oficinas principales se encuentran en Chicago y en Londres, Reino Unido.  
La empresa presta servicios sanitarios a los clientes en sus instalaciones de Chicago y Londres, así como del área metropolitana del Reino Unido.  Las instalaciones de Contoso constan de numerosos hospitales que cuentan con médicos, enfermeras y otros profesionales sanitarios. Contoso ha iniciado una migración de todos los servicios críticos de la empresa a la nube. Esta migración incluye servidores locales, máquinas virtuales y dispositivos de administración y supervisión de apoyo.

Contoso ha iniciado su migración a la nube, excepto en el caso de algunos datos y aplicaciones que deben hospedarse en el entorno local debido a los requisitos normativos y de cumplimiento. Contoso establece un inquilino de Azure Active Directory (Azure AD). Esta instancia de Azure AD se sincroniza con Active Directory Domain Services (AD DS), que se mantiene en los controladores de dominio locales. A medida que avance la migración, se crearán suscripciones de Azure adicionales según sea necesario para cada departamento, incluidas las aplicaciones SaaS. Para facilitar su trabajo diario, la mayoría de los empleados tienen acceso a las aplicaciones de Microsoft 365.  
 
Para que la conectividad sea continua, se han iniciado pruebas básicas de Infraestructura de escritorio virtual (VDI)  
para la mayoría de las categorías de empleados, como administradores de cuentas, personal de soporte  
técnico y personal empresarial, de finanzas y RR. HH. Se proporciona una conectividad segura a través de una puerta de enlace  
VPN (red privada virtual) para un conjunto limitado de usuarios y dispositivos. Además,   
se ha implementado un firewall de terceros para proteger las redes de área local virtuales  
del servidor virtual (VLAN).  
 
Cuando los médicos se encuentran en las instalaciones de los clientes, usan dispositivos móviles con  
datos de seguimiento y supervisión almacenados localmente. Estos datos están protegidos mediante cifrado de almacenamiento propietario  
y cada profesional de la salud debe iniciar sesión en su dispositivo mediante credenciales almacenadas localmente antes de acceder a los datos. 
 
### Requisitos

A medida que la migración a la nube continúa y se expande, Contoso tiene previsto mover todos los datos  
y aplicaciones locales a la nube, excepto las aplicaciones fuera del ámbito. 

* Implementación de Microsoft 365 Defender y Defender for Cloud para mejorar las posturas de seguridad de Contoso frente a los adversarios. 
* La directiva de cumplimiento de Microsoft MCSB debe aplicarse a la suscripción de Azure 
* Contoso quiere buscar de forma proactiva posibles amenazas y administrar activamente la superficie expuesta a ataques 
* Contoso quiere administrar de forma centralizada identidades para contratistas externos y pacientes y empleados internos 
* Todos los dispositivos de punto de conexión deben administrarse de forma centralizada y evaluarse continuamente para comprobar su cumplimiento. 
* La información médica protegida (PHI) almacenada en dispositivos móviles utilizados por profesionales de la salud se trasladará a la nube siguiendo la directiva de residencia de datos para cumplir con las normativas regionales. 
* El acceso a dispositivos móviles mientras se está sobre el terreno debe estar restringido por geolocalización y requiere biométrica como autenticación multifactor  
* Debe controlarse el uso compartido de datos entre aplicaciones del mismo dispositivo.  
* Cumplimiento de los requisitos de la Ley de transferencia y responsabilidad de seguros de salud (HIPAA) y los Servicios nacionales de salud (NHS). 
* Contoso quiere gestionar los administradores de privilegios siguiendo los principios de privilegios mínimos y aplicar políticas de acceso Just-In-Time. 
* Contoso quiere recuperar sus datos ante cualquier desastre y también quiere mantener esos datos de copia de seguridad en una ubicación segura. En caso de desastre en su región primaria, Contoso quiere conmutar por error a la región secundaria. 
* Contoso quiere asegurarse de que se sigue el principio de confianza cero para validar todo el acceso entrante.
* A medida que los datos y el procesamiento se trasladan a Azure, la puerta de enlace de VPN debe configurarse para  
que las conexiones P2S sean seguras desde dispositivos que ejecutan una variedad de sistemas operativos de escritorio  
y móviles, incluidos Windows, macOS, Android y otros.  

### Tareas de diseño

* ¿Qué plan de Defender necesita Contoso para cumplir sus requisitos empresariales y de seguridad? 
* ¿Qué podría hacer Contoso para validar todo el acceso entrante y seguir el principio de confianza cero al mismo tiempo? 
* ¿Cómo podría Contoso aplicar políticas NHS e HIPAA en su entorno de nube? 
* ¿Qué debería usar Contoso para tener visibilidad de todas las amenazas y vulnerabilidades existentes? 
* ¿Cómo se debería implementar y mantener la configuración de seguridad en los dispositivos de punto de conexión? 
* ¿Cómo puede Contoso tener visibilidad sobre las aplicaciones en la nube usadas y los datos compartidos externamente? 
