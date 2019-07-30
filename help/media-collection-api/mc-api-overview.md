---
seo-title: Información general
title: Información general
uuid: c 14 bdbef -5846-4 d 31-8 a 14-8 e 9 e 0 e 9 c 9861
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Información general{#overview}

La API de Media Collection es la alternativa de RESTful de Adobe al Media SDK en el lado del cliente. Con la API de Media Collection, el reproductor puede realizar un seguimiento de eventos de vídeo mediante llamadas HTTP de RESTful. La API de Media Collection ofrece el mismo seguimiento en tiempo real del SDK Multimedia, además de una función adicional:

* **Seguimiento de contenido descargado**

   Esta función le permite rastrear medios mientras un usuario está sin conexión, a través de almacenamiento local de datos de eventos hasta que el dispositivo del usuario devuelve en línea. (Consulte [Seguimiento del contenido descargado](track-downloaded-content.md) para obtener más información).

La API de Media Collection es, básicamente, un adaptador que actúa como versión del lado del servidor del Media SDK. Esto significa que algunos aspectos de la documentación del SDK de medios también son relevantes para la API de recopilación de medios. For example, both solutions use the same [Audio and Video Parameters](/help/metrics-and-metadata/audio-video-parameters.md), and the collected Audio and Video tracking data leads to the same [Reporting and Analysis.](/help/media-reports/media-reports-enable.md)

## Flujos de datos del seguimiento de medios {#section_pwq_n34_qbb}

Un reproductor de medios que implementa la API de Media Collection realiza llamadas de seguimiento de API de restful directamente al servidor de seguimiento de medios, mientras que un reproductor que implementa el SDK multimedia realiza llamadas de seguimiento a las API de SDK dentro de la aplicación del reproductor. Realizar llamadas a través de la web hace que el reproductor que implementa la API de Media Collection necesite gestionar parte del procesamiento que el Media SDK controla automáticamente. (Details in [Media Collection Implementation.](mc-api-impl/mc-api-quick-start.md))

Los datos de seguimiento capturados con la API de Media Collection se envían y se procesan inicialmente que los datos de seguimiento capturados en un reproductor de SDK multimedia, pero el mismo motor de procesamiento en el back-end se utiliza para ambas soluciones.

![](assets/col_api_overview_simple.png)

## API Overview {#section_y4n_mcl_kcb}

**URI:** solicite este dato a su representante de Adobe.

**Método HTTP:** POST, con cuerpo de solicitud JSON.

### Llamadas de API {#mc-api-calls}

* **`sessions`-** Establece una sesión con el servidor y devuelve un ID de sesión utilizado en `events` llamadas subsiguientes. La aplicación invocará una vez al principio de una sesión de seguimiento.

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

* `playerTime` - Obligatorio para todas las solicitudes.
* `eventType` - Obligatorio para todas las solicitudes.
* `params`: obligatorio para determinados `eventTypes`. Compruebe el [esquema de validación JSON](mc-api-ref/mc-api-json-validation.md) para determinar qué tipos de evento eventTypes son obligatorios y cuáles son opcionales.

* `qoeData` - Opcional para todas las solicitudes.
* `customMetadata` - Opcional para todas las solicitudes, pero solo se envían con `sessionStart`, `adStart`y tipos `chapterStart` de eventos.

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

