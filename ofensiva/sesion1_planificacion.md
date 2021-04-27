# Sesión 1 - Planificación

Gente potente en el mundo del Hacking

- Pepe Vila https://twitter.com/cgvwzq

- El grupo de Daniel Gruss en TU Graz, que descubrió meltdown y spectre: https://www.tugraz.at/en/tu-graz/services/news-stories/tu-graz-news/singleview/article/nach-meltdown-und-spectre-tu-graz-forscher-entdecken-neue-sicherheitsluecken0/

- M. Vanhoef, que descubrió DragonBlood, KrackAttack y otras cosas potentes sobre ataques WiFi: https://twitter.com/vanhoefm

- Ricardo J. Rodríguez, de UNIZAR: https://ricardojrdez.github.io/

- Alfonso Muñoz https://twitter.com/mindcrypt

- Pablo Caro

- Carlos Brendel

- Eduardo 'farenain', muy metido en el mundo del reversing

Terminología:

* Hacking ético:

Proceso de __utilización de técnicas ofensivas__ sobre redes y sistemas informáticos con el __consentimiento del dueño__ de los activos y el __objetivo__ de mejorar la seguridad de los sistemas bajo revisión.

* Test de penetración
  * Subconjunto de hacking ético
  * Modelo de técnicas empleadas por atacantes reales para __encontrar vulnerabilidades__ y, en __circunstancias controladas__, aprovecharlas de forma profesional y segura de acuerdo con un __alcance__ y unas reglas para determinar el __riesgo de negocio__ y el impacto potencial con el __objetivo de mejorar la seguridad__ de una organización.

* Análisis de vulnerabilidades
  * Parecido a un pentesting pero __orientado__ más a __encontrar vulnerabilidades que a aprovecharlas.__
  * Objetivo: encontrar vulnerabilidades en una organización, suele incluir __revisión de políticas y procedimientos__, que no se suelen incluir en un pentesting.

* Auditoría de seguridad
  * Revisión del cumplimento de distintos aspectos de seguridad de acuerdo con estándares fijos. Cumplimiento normativo

## ¿Qué aporta a una organización?


* Es necesario __priorizar la inversión de recursos__, si el análisis y escaneos se pueden realizar de manera sencilla, organiza tu dinero en otras cosas. Eso depende del nivel de madurez de la organización.

* Problema: Mucha gente no conoce el riesgo que supone determinadas amenazas.

* Posible solución: En varias empresas se realizan revisiones automáticas de seguimiento

* Emulación de adversarios


## Metodologías

* Proveen una estandarización
* Distintas pruebas/metodologías deben dar los mismo resultados
* Debe ser un análisis exhaustivo
* Todos los elementos deben ser susceptibles de ser testeados

### OSSTMM (Open Source Security Testing Methodology Manual)

* Cubre el testeo de seguridad externo
* Distintas fases:
  * Seguridad de la información
  * Seguridad de los procesos
  * Seguridad en las Tecnologías de Internet
  * Seguridad en las Comunicaciones
  * Seguridad inalámbrica
  * Seguridad física


## Planificación de un test de penetración

* __Objetivos alineados__ con las __prioridades__ de la __organización__
  * Evitar esfuerzos no alineados con el nivel de madurez de la empresa
  * Sed honestos: "tu empresa no va a aprovechar un red team"
* Se debe partir de un análisis de riesgos o de consideraciones más generales:
  * Filtrado de información
  * Daño reputacional
  * Cumplimiento legal o normativo


## Alcance

* Debe estar bien definido el contrato, evitar dejad requisitos difusos
  * Va a ser nuestro escudo cuando la empresa nos acuse de algo
  * Definir bajo qué __condiciones__ el test se ha __finalizado__
  * ¿Tu me vas a __dar__ lo que __necesito__ para __cuando empiece__? Credenciales, acceso, etc
  * ¿Caja negra / gris / blanca ?
* __Muy importante:__ Deberemos indicar qué debe revisarse y sobre todo __¡qué no!__
  * __Ver elementos que bajo ningún concepto deberían estar afectado por la revisión__
* Consentimiento ezpuesto de tercercas partes (la empresa debe avisar al SaaS, Cloud, infraestuctura de red, hosting web, nosotros nos lavamos las manos en ese sentido)
* Si __aparecen nuevos activos__, debe informarse al cliente si incluirlo o no!
  * Si hemos realizado las horas pero creemos que __podemos descubrir algo más__ si nos contratan unas horas más, comentarlo al cliente

## Informe

* 3 apartados:
  * Descripción de la __aproximación__ que se ha empleado para la realización de la prueba
  * __Resultados__ del análisis de vulnerabilidades
  * Conjunto de __recomendaciones__ de cómo mitigar los riesgos identificados
    * Propuestas de mitigación
    * Utilización de maquetas para actualizar
    * Si no puedes parchear, para eso están las mitigaciones


* Ejemplo pentesting:
  * https://www.offensive-security.com/reports/sample-penetration-testing-report.pdf

* Plantilla de informe de pentesting, pasado en la metodologóa PTES
  * http://www.vulnerabilityassessment.co.uk/report%20template.html

* Plantilla para un informe de un test de penetración para el examen de la certificación OSCP
  * http://www.offensive-security.com/pwk-online/PWKv1-REPORT.doc 


### Pasos de un informe

* Planificación del informe
  * __Por qué__ se realiza la prueba y qué se espera obener de ella
  * Estructura jerárquica
  * Niveles de clasificación de información
  * Control de distribución

* Recopilación de información
  * Desde el comienzo del test se debe ir __guardando__ y __organizando__ la __información__
  * __Recopilación__ de __evidencias__ sobre vulnerabilidades
  * Asegurar que la auditoría será __reproducible__ y replicable
  * __Documentar__ herramientas y __procedimientos__
  * Herramientas útiles: [Kvasir](https://github.com/KvasirSecurity/Kvasir) y [Dradis](https://dradisframework.com/ce/)

* Escritura de un primer borrado
  * Disponer de un primer borrador
  * Refleja el ciclo completo y la __estructura del informe final__
  * Ciclo de __revisión__ por una __segunda persona__
  * Mecanismo de __control de versiones__ y __aprobación de cambios__
  * Gestor de referencias: zotero
* Revisión y finalización


* Modelo de un informe
  * Hoja de control del documento: Página principal, nombre, versión, fecha y auditor, propiedades del documento, control de versiones
  * Tabla de contenidos: Índice, lista de figuras y lista de tablas
  * Resumen ejecutivo: Ámbito y alcance del trabajo, objetivo, precondiciones y asunciones, temporización, rsumen de descubrimientos, resumen de recomendaciones
  * Metodologías
  * Descripción de las vulnerabilidades
  * Referencias
  * Apéndices



* Que esté bien redactado
  * ¡No pensar que lo vayamos a presentar en alguna con!
* Distintos niveles de sensibilidad y confidencialidad
* Entregar el reporte y __borrarlo de ti__, puedes terminar en __problemas__ si te roban y filtran los documentos


## Conclusiones

* __Definir bien al alcance y responsabilidads__! 
  * Posibilidad de efectos secundarios no deseados que te jodan (caída servidor, análisis ficheros no deseados, etc)
* Definir bien los objetivos
* Importancia del informe, ¡no técnico!
* Conseguir que la prueba sirva para algo




