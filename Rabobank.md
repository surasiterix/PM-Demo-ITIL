# Demostración de Process mining aplicado a procesos ITIL

![Alt Text](https://img.shields.io/badge/IBM%20MyInvenio-blue.svg?style=plastic)

![Alt Text](https://img.shields.io/badge/Phase-Released-green.svg?style=plastic)

## Caso Rabobank

1. __Objectivos y alcances__

 El objetivo de este _discovery_ es "Revisar los procesos y las interacciones entre _service desk_ y Gestión del cambio para descubrir cuellos de botella y potenciales procesos a automatizar". Para esto, nos proponemos lograr:

 * Un modelo que permita evaluar y enteder como está funcionando la organización
 * Detectar tareas y recursos críticos
 * Proponer una automatización significativa para el Banco


 2. __Extracción y preparación de datos__

   Rabobank extrajo la información de los tres sistemas involucrados en el estudio: Registro de interacciones del _service desk_, Sistema de Trouble Tickets y Gestor de Cambios. La semántica de los campos que vienen en los respectivos logs se encuentra en [este enlace](/assets/quick_reference_bpi_challenge_2014.pdf)

   * __Análisis de interacciones con el *service desk*__

   De la revisión de los datos de este sistema, generamos el siguiente dashboard

   ![Alt Text](/img/Dashboard-Interacciones.PNG)

   En una primera mirada de los datos, podemos apreciar que las interacciones se desarrollan más por: **Incidencias**, sobre **componentes de software**, para **aplicación Web y Cliente / Servidor**.

   * __Análisis de Incidentes__

   De la revisión de datos para este sistema, se generaron dos dashboards. Uno para los casos y otro para las actividades

   Casos:
   ![Alt Text](/img/Dashboard-Incidentes.PNG)

   Tareas:
   ![Alt Text](/img/Dashboard-Incidentes-Tareas.PNG)

   De esta información se desprende lo siguiente: Casos generados son mayormente incidencias, los casos generados son para Aplicación Web y Cliente / Servidor, el recurso más afectado es "TEAM008" y la actividad que más veces se realiza es "Asignación de caso"

   Estos valores se alienan con lo visto en las interacciones. Por lo que hay concordancia con los valores esperados

   * __Análisis de Gestión del Cambio__

   Para la gestión de cambios se desarrolló el siguiente Dashboard:

   ![Alt Text](/img/Dashboard-Cambios.PNG)

   De los datos podemos ver los siguientes comportamientos: Los cambios mayormente son menores y hay 90 cambios de emergencias. Por el lado de los cambios, tenemos que: Se afectan aplicaciones Cliente / Servidor y los cambios son estándar 81 y release 09.

   * __Correlación Interacción - Cambio__

   Uno de los puntos focales del estudio es ver si los cambios han aumentado la interacción del *service desk*. Para ello, haremos una gráfica donde veamos los cambios vs. Interacciones para identificar una posible Interacción

   ![Alt Text](/img/Correlacion.PNG)

   Podemos ver que cada vez que se genera un cambio, hay un incremento en las interacciones. Es una situación esperada, con cada cambio hay un incremento de interacciones. Ahora, consideramos que podemos apoyar en las interacciones mejorando los tiempos de respuestas por la gestión de incidentes.

   3. __Minería del proceso__

   Nuestro estudio va tomar las incidencias y sus actividades para generar el archivo de eventos que procesará nuestra herramienta de minería. Del análisis de los datos llegamos a las siguientes relaciones.

   ![Alt Text](/img/datos-relaciones.PNG)

   De estas, se generó un archivo de eventos consolodido y aplicando procesos de limpieza de datos llegamos a lo siguientes

   ![Alt Text](/img/Dashboard-Eventos.PNG)

   El archivo de eventos utilizado está disponible en [este enlace](/assets/EventLog.csv)

   Definimos los campos necesarios en el mapeo de datos del log para ser procesado por la herramienta

   ![Alt Text](/img/PM-Datasource.PNG)

   Nuestro foco va a ser analizar los incidentes registrados. Después de revisar las frecuencias, tenemos un modelo que se ajusta al 70% de las actividades con un 1% de las relaciones. Esto nos arroja cobertura del 86% con un mínimo de 53% y 100% máximo

   ![Alt Text](/img/Process-Model.PNG)

   En el diagrama vemos las frecuencias de las actividades y sus transiciones. En una primera mirada, vemos las actividades que más se realizan son:
   
    * Open
    * Assignment
    * Operator Update
    * Status Change
    * Reassignment
    * Close

    Primer análisis que realizaremos es buscar actividades críticas y recursos críticos.

    ![Alt Text](/img/Process-Activity-Breakdown.PNG)

    Contamos con unas gráficas predeterminadas para analizar el comportamiento de actividades y recursos para determinar posibles cuellos de botellas para proponer posibles mejoras.

    Hasta ahora, tenemos valores esperados para un proceso de Incidencia.

    ![Alt Text](/img/Process-Dashboards.PNG)

    La herramienta nos muestra dos puntos de atención: Recurso TEAM008 y Actividad "Assignment"

    Veamos donde están la mayor cantidad de retrabajos.

    ![Alt Text](/img/Process-Rework.PNG)

    Las asignaciones, con un 86% de cobertura, tienden a repetirse 4,6 veces en promedio dentro de una incidencia. En la cadena vemos que se hace por reasignación (Asignación > Actualización operador > Reasignación). Acá __hemos detectado que en promedio, ocurren 4 reasignaciones por incidencia__.

    Revisemos el impacto en tiempo de espera entre actividaes. En nuestro archivo de eventos no contamos con duración de la tarea, es normal que esa condición se de. En nuestro caso sabemos que una actividad espera por otra viendo los tiempos de inicios entre ellas. En promedio, los impactos en espera se ven en el modelo de esta información

    ![Alt Text](/img/Process-Waiting-Time.PNG)

    Hacemos foco en la actividad "Customer Update" y como influye en los tiempos de la actividad de Asignación

    ![Alt Text](/img/CustomerUpdate-Reworks.PNG)

    Vemos que en la línea de retabajos afecta de forma importante en los tiempos de resolución del proceso

    Cuando revisamos el impacto de la actividad, en particular los casos fueras de SLA, vemos que la mayor interacción proviene de las Aplicaciones Web

    ![Alt Text](/img/UpdateCustomer-Impact.PNG)

    __En Resumen__: La mayor afectación se produce por reasignaciones donde impactan los tiempos de respuesta del cliente. El recurso crítico es TEAM008

    4. __Análisis__

    Lo primero que haremos es generar un modelo BPMN de nuestro proceso, para ello mantendremos los criterios de 70% de actividades y 1% de relaciones.

    El resultado arrojado por la herramienta es UpdateCustomer

    ![ALt Text](/img/Process-BPMN.PNG)

    El BPMN generado está en [este enlace](/assets/Rabobank_itil_V1.PNG)

    De las reglas obtenidas nos fijamos en los casos para aplicaciones Web.

    * Reasignaciones

    ![Alt Text](/img/Reassignment-Rules.PNG)

    * Asignaciones:

    ![Alt Text](/img/Assignment-Rules.PNG)

    * Actualización del Cliente:

    ![Alt Text](/img/UpdateCustomer-Rules-Migrants.PNG)

    También podemos hacer un análisis de colaboración por actividad para detectar interlocutores para procesos de automatización

    ![Alt Text](/img/Reassignment-Social.PNG)

    Del análisis del impacto sobre los recursos y las colaboraciones que hay entre los equipos, podemos revisar el diagrama de colaboración que se generar

    ![Alt Text](/img/Team-Colaboration.PNG)

    5. __Resumen__

    Vimos como utilizar la herramienta de minería de datos para generar un modelo de negocio utilizando los logs de los sistemas involucrados en el proceso. De este modelo pudimos visualizar cuellos de botella, tantos de actividades críticas como de recursos críticos. Con esa primera mirada, podemos indicar que la afectación mayor en las incidencias ocurren en ciclos de reasignación y actualización por parte del cliente

    Con el modelo generado, podemos proponer un proyecto de automatización para producir ganancias que impacten en tiempo y dinero. Queda para otro taller, hacer simulaciones para mostrar como es el impacto.
