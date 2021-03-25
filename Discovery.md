# Demostración de Process mining aplicado a procesos ITIL

![Alt Text](https://img.shields.io/badge/IBM%20MyInvenio-blue.svg?style=plastic)

![Alt Text](https://img.shields.io/badge/Phase-Released-green.svg?style=plastic)

## Process Discovery

Es la primera fase de todo proyecto de minería de procesos,
descubrir el proceso tal como es para poder determinar KPIs, ineficiencias, errores y oportunidades de
automatización

![Alt Text](/img/Process%20mining%20journey.PNG)

Las disciplinas involucradas en esta primera etapa son:

* __Proceso as-is__: Representación gráfica del proceso tal
como se realiza hoy día. Es relevado de las trazas de los
sistemas involucrados.

* __Minería de tareas__: Captura de las tareas realizadas por
los participantes de los procesos. Esta, consiste en tomar
los tiempos para poder calcular el esfuerzo que cada tarea toma.

* __Minería de reglas de negocio__: Descubrimiento de reglas de negocio que aparecen en el proceso as-is. Desde este punto se derivan recomendaciones y posibles mejoras en los procesos.

* __Minería de procesos multinivel__: Permite hacer drill down dentro de los procesos para descubrir el impacto de ciertas actividades y detectar cuellos de botella y candidatos de automatización.

Los pasos para abordar un proceso de discovery son los siguientes:

1. __Determinación de objetivos y alcance__: En esta fase se define el proceso a minar y cuáles son los resultados esperados del procesos

2. __Extracción y preparación de datos__: Se toman los datos de las trazas de los sistemas que intervienen en el proceso. La data es revisada, depurada y consolidada en un solo archivo de eventos. Esta es la fuente que alimentará a la herramienta de minería para producir el modelo as-is

3. __Minería del proceso__: Carga y validación del modelo. Se realiza un trabajo para producir un modelo ajustado que nos permita hacer analítica de tiempos, fecuencias y recursos teniendo foco en los objetivos planteados

4. __Análisis__: Se realiza una revisión del modelo generado y sobre el se trabajan KPIs, se deducen reglas de negocio y buscan escenarios favorables de automatización

---
[Caso Rabobank >](/Rabobank.md)
