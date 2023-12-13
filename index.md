---
title: Instrucciones hospedadas en línea
permalink: index.html
layout: home
---

# Directorio de contenido

A continuación, se enumeran los hipervínculos a cada caso práctico.


## Casos prácticos reorganizados para la actualización de contenido de mayo de 2023

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudyv2/'" %}
| Módulo | Caso práctico |
| --- | --- | 
{% for activity in casestudy %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}


## Organización de casos prácticos antiguos

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudy/'" %}
| Módulo | Caso práctico |
| --- | --- | 
{% for activity in casestudy %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}