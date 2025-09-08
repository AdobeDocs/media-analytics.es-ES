---
title: Carga de datos de programación para rastrear contenido en directo
description: Obtenga información sobre cómo cargar datos de programación para rastrear contenido en directo.
feature: Streaming Media
role: User, Admin, Data Engineer
hide: true
hidefromtoc: true
source-git-commit: e38a83853e85418611e17015b661d8592a7c95a1
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 2%

---

# Carga de datos de programación para rastrear contenido en directo

Puede cargar datos de programación del contenido de medios de streaming en directo anterior para rastrear la audiencia de contenido en directo de forma más fácil y precisa. Puede realizar un seguimiento de la audiencia de programas individuales e incluso temas o segmentos de programas específicos.

Los siguientes son ejemplos de contenidos en directo compatibles con la carga de datos de programación:

* Plataformas FAST (Free Ad Supported TV)

* Streams locales

* Deportes en directo

* Noticias o programación actual

## Competencias

Hay varias funciones disponibles al utilizar la programación de cargas de datos de contenido de medios de streaming en directo anterior. En esta sección se describen algunas de las funciones clave que ayudan a analizar el rendimiento del programa.

Estas funciones están disponibles independientemente de cómo haya implementado la recopilación de medios de streaming.

* **Realizar un seguimiento preciso de las programaciones de los programas**: identifique las horas de inicio y finalización de cada programa individual en el flujo en directo durante el período de tiempo que desee analizar. Con tiempos de inicio y finalización precisos, el tiempo de ejecución preciso se refleja con precisión y se puede analizar con cada sesión del visualizador.

  Por ejemplo, no siempre se conocen los momentos precisos de inicio y finalización de un evento deportivo en directo hasta que termina el evento. Las cargas de datos programadas le permiten obtener informes precisos al actualizar las horas de inicio y finalización una vez finalizado el programa.

* **Rastrear temas o segmentos de programa individuales**: cree nuevas dimensiones basadas en el tiempo para temas específicos o segmentos de programa (espacios de tiempo) dentro de un programa determinado. Estas dimensiones basadas en el tiempo le permiten analizar la audiencia de un programa en un nivel más específico, lo que ayuda a recopilar perspectivas sobre qué temas o segmentos del programa resonaron mejor.

  Por ejemplo, al analizar un evento deportivo en directo, como un partido de fútbol, puede crear dimensiones independientes para la primera mitad, la mitad del tiempo y la segunda mitad. El seguimiento de temas o segmentos específicos dentro de un programa de esta manera permite desgloses más detallados del comportamiento del visualizador.

* **Generar recorridos de usuario en Journey Optimizer**: haga un seguimiento de los programas que vio una persona en una sesión determinada (o incluso de los temas o segmentos de programa que vio la persona) y, a continuación, utilice estos datos en Adobe Journey Optimizer para crear recorridos de usuario para los clientes que vieron un programa determinado o que mostraron interés en un tema determinado.

## Comprender cómo funcionan los datos de programación para los medios de streaming

La funcionalidad de programación de datos para medios de streaming funciona de la siguiente manera:

1. Lee del conjunto de datos del programa de programación para registros del programa de programación, filtrando por la fecha de la programación.

   Solo funciona para programas que se produjeron entre 24 horas y 48 horas antes.

2. Lee los eventos de cierre de medios del conjunto de datos de medios, filtrando por fecha y por la ruta XDM en los registros del programa de programación.

3. Para cada evento de cierre de contenidos, se genera el mismo número de eventos de inicio de programación de contenidos que de programas que se superponen con la sesión de contenidos.

   Cada evento de inicio de programación de medios contiene el nombre y la duración de la programación.

   Además, una nueva métrica de tiempo llamada **scheduleTimePlayed** contiene el número de segundos que la sesión multimedia se superpuso con el programa programado. La marca de tiempo del evento de inicio de programación es la marca de tiempo del momento en el que comenzó el programa.

4. Escribe los nuevos eventos de inicio de programación en el conjunto de datos de AEP media.

## Requisitos previos

Para cargar datos de programación de contenido en directo anterior, el entorno de medios de streaming debe cumplir los siguientes requisitos previos:

* La recopilación de medios de streaming debe estar habilitada para realizar el seguimiento del contenido cuyos datos de programación desea cargar, tal como se describe en [Resumen del seguimiento](/help/use-cases/track-av-playback/track-core-overview.md). <!--specifics??? -->

* Utilice la recopilación de medios de streaming con Customer Journey Analytics. La capacidad de cargar datos de programación no está disponible con Adobe Analytics.

## Crear un conjunto de datos de programación en AEP

Para poder insertar la información de programación, debe crear un conjunto de datos de programación en Experience Platform:

1. Cree un esquema basado en la clase XDM **Programa programado de Media Analytics**.

   ![Esquema del programa de programación de Media Analytics](assets/media_schedule_finish_schema_creation.png)

   Definición XDM de la clase de programa programado de Media Analytics.

   [https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. Cree un conjunto de datos basado en el esquema que ha creado.

1. Continúe con la sección siguiente, [Información de programación push](#push-schedule-information).

## Información de programación push

Después de [crear un conjunto de datos de programación de programa](#create-a-program-schedule-dataset-in-aep), puede insertar la información de programación:

1. Cree un archivo .json con la información de programación.

   El archivo .json debe contener una matriz de objetos Schedule Program, de acuerdo con el esquema XDM.

1. Cargue el archivo .json:

   >[!NOTE]
   >
   >Los ejemplos de cURL de esta sección utilizan las siguientes variables:
   >
   >* Para la autenticación con Adobe Developer:
   >     * CUSTOMER_API_KEY
   >     * AUTH_TOKEN
   >* id de organización: CUSTOMER_ORG_ID
   >* id del conjunto de datos de registro creado en la configuración: DATASET_ID
   >* ID de lote creado en la primera solicitud utilizada en la carga del archivo: BATCH_ID
   >* Nombre del archivo utilizado para insertar registros: FILE_NAME

   1. Cree un nuevo lote y, a continuación, obtenga el ID de lote de la respuesta.

      Considere el siguiente ejemplo de uso de cURL para crear un nuevo lote de AEP:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. Inserte el archivo .json que contiene los registros de datos de programación del programa utilizando el ID de lote.

      Para insertar la información de programación, debe usar las API por lotes de AEP, tal como se describe en [Información general de la API de ingesta por lotes](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/batch/overview).

      Considere el siguiente ejemplo de uso de cURL para insertar un archivo con los registros de programación:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. Complete el lote.

      Considere el siguiente ejemplo de uso de cURL para completar el lote:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. Continúe con la sección siguiente, [Registrar un ticket de asistencia con el Servicio de atención al cliente de Adobe](#log-a-support-ticket-with-adobe-customer-care).

## Registre un ticket de asistencia con el Servicio de atención al cliente de Adobe

Registre un vale de soporte con el Servicio de atención al cliente de Adobe con la siguiente información:

* **Conjunto de datos de medios**: especifique el ID del conjunto de datos desde el que se leen los datos de las sesiones de medios.

* **Conjunto de datos de programación**: especifique el ID del conjunto de datos al que se insertan los registros de programación.

* **Conjunto de datos de medios de salida**: especifique el identificador del conjunto de datos en el que se guardan los eventos de inicio de programación.

  Este ID de conjunto de datos puede ser el mismo ID de conjunto de datos que se utiliza para el conjunto de datos de medios. Si es un ID de conjunto de datos diferente, debe seguir teniendo el mismo esquema XDM que el conjunto de datos de medios.

* **ID de organización**: especifique su ID de organización.

## Ejemplo de un archivo .json de programación con dos registros

El siguiente ejemplo es un archivo .json de programación con dos registros. Cada archivo .json debe contener todos los programas programados para un día.

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### Comprenda los campos de programación en el ejemplo

1. **mediaProgramDetails**: debe contener la información mínima necesaria para crear el evento de inicio de programación:
   * **startTimestamp**: hora a la que comenzó el programa.
   * **nombre**: El nombre descriptivo del programa.
   * **length**: El número de segundos que duró el programa.

     >[!IMPORTANT]
     >
     >Si tiene varias solicitudes de datos de programación, no pueden tener horas de inicio y finalización superpuestas.

1. **scheduleDate**: La fecha en que se emitió el programa. El formato debe ser AAAA-MM-DD. Se utiliza para filtrar el conjunto de datos de programación y obtener todas las programaciones para las que adobe crea inicios de programación.
1. **scheduleFilter**: se usa para filtrar todos los eventos de cierre de sesión multimedia.
   * **filterPath**: una ruta XDM al campo que se usa para el filtrado.
   * **filterValue**: Valor utilizado para el filtrado.
1. **customMetadata**: metadatos personalizados que desea agregar a los eventos de inicio de programación. Estos metadatos se utilizan para sobrescribir los metadatos personalizados presentes en los eventos de cierre de sesión.
1. **defaultMetadata**: una lista específica de dimensiones que pueden agregar o sobrescribir los metadatos predeterminados presentes en las llamadas de cierre de medios.

   Considere los siguientes ejemplos de dimensiones que puede crear y luego informar en Customer Journey Analytics:

   * **[&quot;_Nombre del episodio_&quot;](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)**: Esta dimensión podría ayudarle a saber qué episodios de una serie en particular tienen el mejor rendimiento.

   * **[ID de recurso](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. Continuar con [Analizar datos en Customer Journey Analytics](#analyze-data-in-customer-journey-analytics).

## Analizar datos en Customer Journey Analytics

Un día después de cargar el archivo de datos como se describe en [Solicite y cargue el archivo de datos de programación](#request-and-upload-the-schedule-data-file), sus datos estarán listos para informar en Customer Journey Analytics.

Para informar sobre los datos de medios de streaming en directo anteriores en Customer Journey Analytics:

1. Cree un nuevo proyecto o abra uno existente.

1. Cree el proyecto creando las tablas o visualizaciones que necesite para analizar los datos de medios de streaming en directo anteriores.

   Al crear el proyecto, utilice la información que incluyó en el archivo de datos de programación y que se envió al Servicio de atención al cliente de Adobe. Esto incluye la clave coincidente, las dimensiones y cualquier metadato adicional. Para obtener más información, consulte [Solicitar y cargar el archivo de datos de programación](#request-and-upload-the-schedule-data-file).




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->
