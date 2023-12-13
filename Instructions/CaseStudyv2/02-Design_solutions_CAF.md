---
casestudy:
  title: 'Caso práctico: Diseño de soluciones que se amoldan a Cloud Adoption Framework (CAF)'
  module: 'Module 02: Design solutions that align with CAF and WAF'
---
Este ejercicio de caso práctico está diseñado para aportar experiencia en la realización de algunas tareas de diseño conceptual relacionadas con los temas aprendidos en este módulo.

## Caso práctico: Diseño de soluciones que se amoldan a Cloud Adoption Framework (CAF)

- Contoso Banking es una filial de Contoso Group que se está convirtiendo en una entidad empresarial independiente. Contoso Banking será una empresa independiente con su propia infraestructura y organización de TI. 
- La infraestructura de Contoso Banking se basará completamente en la nube de Microsoft Azure. Para crear una plataforma segura en la nube desde los inicios de la empresa, debes diseñar una zona de aterrizaje de Azure segura.
- Los términos del acuerdo establecen que la transición debe durar un máximo de seis meses.
- Contoso Banking tiene previsto crear la solución FinTech de próxima generación mediante soluciones nativas de nube. La versión MVP 1 debe estar lista en seis semanas.

### Requisitos

Contoso Group no usa ningún servicio en la nube; la infraestructura se hospeda completamente en su propio centro de datos. El entorno que formará parte de Contoso Banking incluye:

- Entorno 1: Sistemas bancarios principales: 20 aplicaciones. La seguridad es fundamental.
- Entorno 2: Aplicación Fintech/Next-Gen basada en Azure Kubernetes Service y Azure Data Lake. Cien versiones al mes

#### Cambios planeados

Entorno 1: Contoso Banking tiene previsto trasladar toda la infraestructura bancaria principal a la nube. El enfoque debe incluir lo siguiente:

- Implementación de una zona de aterrizaje donde se hospeden las aplicaciones principales.
- Los usuarios necesitan acceder a las aplicaciones principales desde estaciones de trabajo seguras basadas en la nube. Los usuarios deben tener una experiencia de usuario coherente para acceder a las aplicaciones.
- La solución debe garantizar el cumplimiento de los procedimiento recomendados en materia de administración de identidades y accesos, gobernanza, seguridad, red y registro.

El entorno 2 (aplicación Fintech) debe cumplir los requisitos siguientes:

- Versión 100x/mes
- Estar siempre preparado para las auditorías
- Cumplimiento de la norma PCI-DSS

### Tareas de diseño

- ¿Cuáles son los componentes que deben implementarse en la zona de aterrizaje?
- ¿Cómo afectará la elección de cargas de trabajo a la duración y a la complejidad de implementación?
- ¿Cómo implementarías el acceso seguro a las aplicaciones principales?
- ¿Qué zona de aterrizaje de Azure deberías recomendar a Contoso Banking que implemente para el Entorno 1?
- ¿Qué zona de aterrizaje de Azure deberías recomendar a Contoso Banking que implemente para el Entorno 2?
