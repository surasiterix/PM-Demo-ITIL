# Demostración de Process mining aplicado a procesos ITIL

![Alt Text](https://img.shields.io/badge/IBM%20MyInvenio-blue.svg?style=plastic)

![Alt Text](https://img.shields.io/badge/Phase-Released-green.svg?style=plastic)

Demostración de process mining usando data de los procesos de incidencia y
gestión del cambio para un entidad financiera. Esta demostración está basada en
el *challenge* de BPI de 2014 (más info [acá](https://www.win.tue.nl/bpi/doku.php?id=2014:challenge&redirect=1id=2014/challenge))

## Descripción de la demo

Rabobank Group ICT ha implementado  procesos ITIL para gestión de cambios. El
objetivo que se plantearon fue incrementar la cantidad de cambios y la velocidad
para llevarlos a producción. El objetivo final es colocar más rápido productos
en el mercado.

Después de 6 meses funcionando con los nuevos procesos y herramientas de soporte,
empezaron a ver un aumento de intracciones del *service desk* y de operaciones.
Preocupados por estos nuevos impactos, Rabobank, toma la decisión de revisar los
procesos y las interacciones entre *service desk* y Gestión del cambio para
descubrir cuellos de botella y potenciales procesos a automatizar

## Contexto de los procesos involucrados ##

Rabobank, como parte de su adopción de procesos de ITL, decide implementar una
solución de gestión de cambios donde todos los *releases* y *Fixes* son
planificados y se registran las distintas etapas por las que evoluciona cada
cambio.

![Alt Text](/img/Contexto%20de%20procesos.PNG)

La información prestada por Rabobank son las trazas de los siguientes:

* **Interacciones**: Los agentes del *service desk* registran las interacciones
con los clientes, ya sea por teléfono o por correo electrónico. Las interacciones
pueden ser resueltas directamente por el agente (*First call resolution*) o, en
su defecto, abrir un ticket de incidencia en la herramienta de trouble tickets

* **Incidentes**: Herramienta de gestión de tickets para tareas del equipo de
operaciones de TI corporativos. Cada equipo tiene responsabilidades y atiende
de acuerdo a sus capacidades.

* **Gestión de cambios**: Herramienta que da soporte a los procesos de cambios
en los activos de TI del banco, permitiendo medir y dirigir los esfuerzos de los
distintos equipos de TI para colocar el poducto o fix en producción.

## Objetivos de la demostración ##

Rabobank precisa determinar como aceitar sus procesos ITIL recién adoptados para
disminuir la presión que se está generando en su *service desk* y en los equipos
de operaciones. Para ello realizaremos un **discovery** de procesos a partir la
información de Interacciones, Incidentes y Cambios que se gestionan en las
herramientas de soporte del Banco.

Los resultados de esperados son:

* Un modelo de proceso para apoyar a gestión de cambios a reducir impactos en *service desk* y operaciones
* Determinar candidatos de automatización de procesos

Para ello, contamos con los siguientes activos:

* Traza de las intracciones del *service desk*: [detail_interacition.zip](/asssets/detail_interaction.zip)
* Traza de los incidentes: [detail_incident.zip](assets/detail_incidents.zip)
* Traza de las actividades realizadas por incidente: [detail_incident_activity.zip](/assets/detail_incident_activity.zip)
* Traza de gestión de cambios: [detail_change.zip](/assets/detail_change.zip)

---

[Taller de Discovery >](/Discovery.md)
