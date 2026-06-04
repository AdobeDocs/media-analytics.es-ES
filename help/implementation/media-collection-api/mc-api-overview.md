---
seo-title: Overview
title: Información general sobre la API de Streaming Media Collection
description: Obtenga información acerca de la API de Media Collection y cómo el reproductor puede realizar un seguimiento de eventos de audio y vídeo mediante llamadas HTTP de RESTful.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/79XLYzuvi3neUuCrt3LcGEwnnaR038-mWHMuSrY797M
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 347
ht-degree: 91%

---

# Información general sobre la API de Media Collection {#overview}

La API de recopilación de medios es la alternativa RESTful de Adobe al SDK de medios del lado del cliente. Con la API de recopilación de medios, el reproductor puede realizar el seguimiento de eventos de audio y vídeo mediante llamadas HTTP RESTful.

La API de recopilación de medios es esencialmente un adaptador que actúa como una versión del SDK de medios en el lado del servidor. Los datos recopilados del seguimiento de medios de streaming llevan a los mismos [Informes y análisis](/help/reporting/setup/analytics-reporting.md).

## Flujos de datos del seguimiento de contenidos {#media-tracking-data-flows}

Un reproductor de contenido que implementa la API de recopilación de contenido realiza llamadas de seguimiento de API RESTful directamente al servidor back-end de seguimiento de contenido, mientras que un reproductor que implementa Media SDK hace llamadas de seguimiento a las API de SDK en la aplicación del reproductor. Realizar llamadas a través de la web hace que el reproductor que implementa la API de Media Collection necesite gestionar parte del procesamiento que el Media SDK controla automáticamente. (Detalles de la [implementación de recopilación de contenido.](mc-api-impl/mc-api-quick-start.md))

Los datos de seguimiento capturados con la API de recopilación de contenido se envían y se procesan inicialmente de forma distinta a los datos de seguimiento capturados en un reproductor de Media SDK, pero se utiliza el mismo motor de procesamiento de en el servidor para ambas soluciones.

![](assets/col_api_overview_simple.png)

## Información general de API {#api-overview}

**URI:** Puede obtenerla de su representante de Adobe.

**Método HTTP:** POST, con el cuerpo de solicitud JSON.

### Llamadas de API {#mc-api-calls}

* **`sessions`-** Establece una sesión con el servidor y devuelve un ID de sesión utilizado en las llamadas a `events` posteriores. La aplicación invocará una vez al principio de una sesión de seguimiento.

  `{uri}/api/v1/sessions`

* **`events`-** Enviar datos de seguimiento de contenidos.

  `{uri}/api/v1/sessions/{session-id}/events`

### Cuerpo de la solicitud {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` - obligatorio para todas las solicitudes.
* `eventType` - obligatorio para todas las solicitudes.
* `params` - obligatorio para determinados `eventTypes`. Compruebe el [esquema de validación JSON](mc-api-ref/mc-api-json-validation.md) para determinar qué tipos de evento eventTypes son obligatorios y cuáles son opcionales.

* `qoeData` - opcional para todas las solicitudes.
* `customMetadata` - opcional para todas las peticiones, pero solo se envía con los tipos de evento `sessionStart`, `adStart` y `chapterStart`.

Para cada `eventType`, hay [un esquema de validación JSON](mc-api-ref/mc-api-json-validation.md) disponible públicamente que debe utilizarse para verificar tipos de parámetros y si uno de estos es opcional o necesario para un evento determinado.

### Tipos de eventos {#mc-api-event-types}

Para obtener la lista completa de tipos de eventos con ejemplos de implementación por SDK, consulte [Información general sobre eventos](/help/implementation/events/overview.md).
