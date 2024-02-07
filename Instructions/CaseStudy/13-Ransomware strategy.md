---
casestudy:
  title: 'Caso práctico: Estrategia de ransomware'
  module: 'Module 13: Recommend a ransomware strategy by using Microsoft Security Best Practices'
---
Este ejercicio de caso práctico está diseñado para aportar experiencia en la realización de algunas tareas de diseño conceptual relacionadas con los temas aprendidos en este módulo.

## Caso práctico: Recomendación de una estrategia de ransomware mediante procedimientos recomendados de seguridad de Microsoft
 
CONTOSO es una empresa de servicios médicos cuyas oficinas principales se encuentran en Chicago y en Londres, Reino Unido.  
La empresa presta servicios sanitarios a los clientes en sus instalaciones de Chicago y Londres, así como del área metropolitana del Reino Unido.  Las instalaciones de Contoso constan de numerosos hospitales que cuentan con médicos, enfermeras y otros profesionales sanitarios. Contoso ha iniciado una migración de todos los servicios críticos de la empresa a la nube. Esta migración incluye servidores locales, máquinas virtuales y dispositivos de administración y supervisión de apoyo.

Contoso ha iniciado su migración a la nube, excepto en el caso de algunos datos y aplicaciones que deben hospedarse en el entorno local debido a los requisitos normativos y de cumplimiento. Contoso tiene un inquilino de Azure Active Directory (Azure AD). Esta instancia de Azure AD se sincroniza con Active Directory Domain Services (AD DS), que se mantiene en los controladores de dominio locales. A medida que avance la migración, se crearán suscripciones de Azure adicionales según sea necesario para cada departamento, incluidas las aplicaciones SaaS. Para facilitar su trabajo diario, la mayoría de los empleados tienen acceso a las aplicaciones de Microsoft 365.  
 
Ha habido varios casos recientes de ransomware de alto perfil que implican a competidores de Contoso en el mercado de servicios sanitarios. El CEO y el CISO están preocupados porque Contoso todavía no tiene implantado un plan para mitigar el riesgo de un ataque de ransomware. El CISO ha solicitado personalmente que redactes una respuesta de ransomware y un plan de mitigación que se presentará a los ejecutivos de la empresa en dos semanas. Parte del personal de TI sénior ha manifestado que se está exagerando la amenaza del ransomware y que lo único que la empresa necesita en realidad son buenas copias de seguridad y una sólida seguridad perimetral.
 
### Requisitos

* El plan de respuesta y mitigación de ransomware debe incluir no solo la infraestructura local y los servicios en la nube críticos, sino también los datos de la empresa almacenados en equipos portátiles de la empresa y dispositivos móviles usados por los empleados sobre el terreno
* El CEO y el CISO han adoptado un enfoque de línea dura en el sentido de que nunca negociarán ni pagarán a hackers de ransomware. Han señalado que, en caso de un ataque ransomware, su objetivo es que los sistemas críticos vuelvan a funcionar en un plazo de 12 horas y la funcionalidad completa se restablezca en un plazo de 48 horas.
* Las estrategias de tratamiento de datos deben cumplir los requisitos de privacidad, incluida la HIPAA en Estados Unidos y cualquier norma relacionada del Reino Unido.
* Su plan también debe detallar por qué una buena copia de seguridad no es suficiente para mitigar la amenaza de ransomware.

### Preguntas iniciales

* ¿Qué departamentos y personal deben participar en la creación del plan de mitigación de ransomware? 
* ¿Qué servicios y elementos de infraestructura debe abordar el plan? 
* ¿Cuáles son las escalas de tiempo realistas para crear un plan sólido de respuesta al ransomware?
* ¿Cuáles son las principales medidas de éxito para la implementación de tu plan de protección contra ransomware?

### Tareas de diseño

* La lista de los servicios de Azure y M365 será fundamental para realizar copias de seguridad y proteger los datos. Explica por qué cada servicio es una parte importante de la respuesta al ransomware y las ventajas y desventajas de cada uno.
* Toma nota de los requisitos especiales que tenga tu empresa y que no contemplen las soluciones de Azure y M365 existentes.
* Enumera los servicios y los elementos de infraestructura que debe abordar el plan.
* Calcula algunas escalas de tiempo realistas para crear un plan sólido de respuesta al ransomware y luego ejecutar ese plan. 