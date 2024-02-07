---
casestudy:
  title: 'Caso práctico: Evaluación de cumplimiento normativo'
  module: 'Module 05: Design solutions for regulatory compliance'
---

Este ejercicio de caso práctico está diseñado para proporcionar experiencia en la realización de algunas tareas de diseño conceptual relacionadas con los temas aprendidos en este módulo.

## Caso práctico: Evaluación del cumplimiento normativo

Contoso Pharma es una industria farmacéutica internacional con presencia en Norteamérica y Europa. Contoso Pharma tiene cargas de trabajo en el entorno local y en Azure. El objetivo es que, en los próximos dos años, todas las cargas de trabajo estén íntegramente en Azure y que la cantidad de cargas de trabajo en el entorno local sea mínima. A continuación se muestra una lista de sus principales cargas de trabajo:

- Máquinas virtuales (Windows y Linux)
- Cuentas de almacenamiento
- Key Vault
- PaaS de SQL y SQL en máquinas virtuales

Contoso Pharma también tiene una VPN de sitio a sitio entre la oficina central en Redmond y la oficina principal en Londres. Esta VPN se usa para permitir la comunicación de los recursos locales.

Contoso Pharma tiene un entorno heredado en Redmond compuesto por un par de equipos con Windows Server 2012 que ejecutan un servidor web que usa la aplicación que consulta la base de datos en busca de información del cliente. Tras la investigación, se observó que la comunicación del servidor web heredado con la base de datos se realiza a través de HTTP.

### Requisitos de diseño

Contoso Pharma tiene diferentes necesidades de cumplimiento según sus cargas de trabajo, como se muestra en la tabla siguiente:

| **Carga de trabajo** | **Tipo de datos** | **Estándar de cumplimiento** |
|:---:|:---:|:---:|
| Máquinas virtuales Windows | Información del titular de la tarjeta de crédito | PCI DSS |
| SQL PaaS | Información de la salud de un paciente | HIPAA |
| Cuentas de almacenamiento | Información del titular de la tarjeta de crédito | Cuentas de PCI DSS |

Para cumplir con estos estándares, Contoso Pharma debe poder:

- Supervisar el progreso del cumplimiento con el tiempo
- Prohibir que los propietarios de cargas de trabajo aprovisionen recursos que no cumplan con esos estándares
- Asegurarse de que las nuevas suscripciones implementadas en el entorno usan los estándares necesarios de manera predeterminada
- Asegurarse de que los recursos aprovisionados en cada geolocalización conservan los datos en la región de origen con fines de soberanía de datos

### Tareas de diseño

* Para asegurarse de que Contoso Pharma puede analizar su estado de cumplimiento con el tiempo, ¿qué herramienta se debe usar? Seleccione la opción más adecuada.
* ¿Qué servicio de Azure se debe usar para hacer que los propietarios de cargas de trabajo creen solo aquellos recursos que cumplan con los estándares necesarios?
* ¿Qué opción se debe usar para garantizar que, cuando los propietarios de cargas de trabajo creen los recursos, conservarán los datos en la geolocalización correcta?
* ¿Cómo puede Contoso Pharma validar si las máquinas virtuales aprovisionadas son compatibles con PCI DSS? Si la respuesta es negativa, ¿qué se debe hacer para corregir esto?
* El cifrado de datos es un componente imperativo para satisfacer los requisitos de privacidad. ¿Cuáles son las fases de datos en las que debe aplicar el cifrado?
* ¿Qué servicio de Azure puede usar para aplicar el cifrado de datos entre las cargas de trabajo?
