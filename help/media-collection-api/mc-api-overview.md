---
seo-title: Información general
title: Información general
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Información general{#overview}

La API de Media Collection es la alternativa de RESTful de Adobe al Media SDK en el lado del cliente. Con la API de Media Collection, el reproductor puede realizar un seguimiento de eventos de vídeo mediante llamadas HTTP de RESTful. La API de Media Collection ofrece el mismo seguimiento en tiempo real del SDK de medios, además de una función adicional:

* **Seguimiento de contenido descargado**

   Esta función le permite rastrear medios mientras un usuario está sin conexión, mediante el almacenamiento local de datos de eventos hasta que el dispositivo del usuario vuelva a estar en línea. (Consulte [Seguimiento del contenido descargado](track-downloaded-content.md) para obtener más información).

La API de Media Collection es, básicamente, un adaptador que actúa como versión del lado del servidor del Media SDK. Esto significa que algunos aspectos de la documentación del SDK de medios también son relevantes para la API de Media Collection. Por ejemplo, ambas soluciones utilizan los mismos parámetros [de](/help/metrics-and-metadata/audio-video-parameters.md)audio y vídeo, y los datos recopilados de seguimiento de audio y vídeo llevan a los mismos [informes y análisis.](/help/media-reports/media-reports-enable.md)

## Flujos de datos del seguimiento de medios {#section_pwq_n34_qbb}

Un reproductor multimedia que implementa la API de Media Collection realiza llamadas de seguimiento de la API RESTful directamente al servidor back-end de seguimiento de medios, mientras que un reproductor que implementa el SDK de medios realiza llamadas de seguimiento a las API del SDK dentro de la aplicación del reproductor. Realizar llamadas a través de la web hace que el reproductor que implementa la API de Media Collection necesite gestionar parte del procesamiento que el Media SDK controla automáticamente. (Detalles de la implementación de [Media Collection.](mc-api-impl/mc-api-quick-start.md))

The tracking data captured with the Media Collection API is sent and initially processed differently than the tracking data captured in a Media SDK player, but the same processing engine on the back-end is used for both solutions.

![](assets/col_api_overview_simple.png)

## Información general de API {#section_y4n_mcl_kcb}

**URI:** solicite este dato a su representante de Adobe.

**Método HTTP:** POST, con cuerpo de solicitud JSON.

### Llamadas de API {#mc-api-calls}

* **`sessions`-** Establece una sesión con el servidor y devuelve un ID de sesión utilizado en `events` llamadas posteriores. La aplicación invocará una vez al principio de una sesión de seguimiento.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** Envía datos de seguimiento de medios.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Cuerpo de la solicitud {#mc-api-request-body}

```
{ 
    "playerTime": { 
        "playhead": {playhead position in seconds}, 
        "ts": {timestamp in milliseconds} 
    }, 
    "eventType": {event-type}, 
    "params": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "qoeData" : { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "customMetadata": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    } 
} 
```

* `playerTime` - Mandatory for all requests.
* `eventType` - Obligatorio para todas las solicitudes.
* `params`: obligatorio para determinados `eventTypes`. Compruebe el [esquema de validación JSON](mc-api-ref/mc-api-json-validation.md) para determinar qué tipos de evento eventTypes son obligatorios y cuáles son opcionales.

* `qoeData` - Optional for all requests.
* `customMetadata` - Opcional para todas las solicitudes, pero solo se envía con tipos `sessionStart`, `adStart`y `chapterStart` eventos.

Para cada `eventType`, hay [un esquema de validación JSON](mc-api-ref/mc-api-json-validation.md) disponible públicamente que debe utilizarse para verificar tipos de parámetros y si uno de estos es opcional o necesario para un evento determinado.

### Tipos de eventos {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`

