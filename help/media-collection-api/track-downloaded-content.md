---
title: Seguimiento del contenido descargado
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: be68a7abf7d5fd4cc725b040583801f2308ab066
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 56%

---


# Seguimiento del contenido descargado {#track-downloaded-content}

## Información general {#overview}

La función Contenido descargado proporciona la capacidad de realizar un seguimiento del consumo de contenido cuando un usuario está sin conexión. Por ejemplo, un usuario descarga e instala una aplicación en un dispositivo móvil y, a continuación, utiliza la aplicación para descargar contenido en el almacenamiento local del dispositivo. Para rastrear los datos descargados, Adobe desarrolló la función Contenido descargado. Con esta función, cuando el usuario reproduce contenido desde el almacenamiento de un dispositivo, los datos de seguimiento se almacenan en el dispositivo independientemente de la conectividad del mismo. Cuando el usuario finaliza la sesión de reproducción y el dispositivo vuelve a estar en línea, la información de seguimiento almacenada se envía al back-end de la API de Media Collection dentro de una única carga útil. A continuación, la información de seguimiento almacenada se procesa y se comunica como de costumbre en la API de recopilación de medios.

Contrastar los dos enfoques:

* En línea

   Con este enfoque en tiempo real, el reproductor de medios envía datos de seguimiento para cada evento del reproductor y envía ping de red cada diez segundos (cada segundo para anuncios), uno por uno al servidor.

* Sin conexión (función Contenido descargado)

   Con este método de procesamiento por lotes, es necesario generar los mismos eventos de sesión, pero se almacenan en el dispositivo hasta que se envían al back-end como una sola sesión (ver ejemplo a continuación).

Cada enfoque tiene sus ventajas y desventajas:
* El seguimiento del escenario en línea se realiza en tiempo real; esto requiere una comprobación de conectividad antes de cada llamada de red.
* El escenario sin conexión (función Contenido descargado) solo necesita una comprobación de conectividad de red, pero también requiere un espacio de memoria mayor en el dispositivo.

## Implementación {#implementation}

### Plataformas admitidas

El seguimiento de contenido es compatible con dispositivos móviles iOS y Android.

### Esquemas de eventos

La función de contenido descargado es la versión sin conexión de la API (estándar) de recopilación de medios en línea, por lo que los datos de evento que el reproductor envía al back-end y que se procesa por lotes deben utilizar los mismos esquemas de evento que se utilizan al realizar llamadas en línea. Para obtener más información sobre estos esquemas, consulte:
* [Información general;](/help/media-collection-api/mc-api-overview.md)
* [Validación de solicitudes de eventos](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Orden de los eventos

* El primer evento de la carga útil por lotes debe ser `sessionStart`, como es habitual con la API de recopilación de contenido.
* **Debe incluir`media.downloaded: true`** en los parámetros de metadatos estándar (clave`params`) del evento`sessionStart`para indicar al back-end que está enviando contenido descargado. Si este parámetro no está presente o se establece como falso, la API de Contenido descargado devolverá un código de respuesta 400 (solicitud no válida). Este parámetro distingue entre el contenido descargado y el contenido en directo en el back-end. If`media.downloaded: true`is set on a live session, this will likewise result in a 400 response from the API.
* Es responsabilidad de la implementación almacenar correctamente los eventos del reproductor por orden de aparición.

### Códigos de respuesta

* 201: Creado, la solicitud correcta; los datos son válidos y la sesión se creó y se procesará.
* 400: Solicitud incorrecta, error en la validación del esquema, se descartan todos los datos y no se procesan los datos de las sesiones.

## Integración con Adobe Analtyics {#integration-with-adobe-analtyics}

Al calcular las llamadas de inicio y cierre de Analytics para el escenario de contenido descargado, el back-end establece un campo adicional de Analytics llamado `ts.` Estas son marcas de hora para el primer y último evento recibido (inicio y finalización). Este mecanismo permite colocar una sesión de contenido finalizada en el momento correcto (es decir, incluso si el usuario no vuelve a estar en línea durante varios días, la sesión de contenido se registra como si hubiera tenido lugar en el momento en el que el contenido se visualizó). Debe habilitar este mecanismo en Adobe Analytics. Para ello, cree un _grupo de informes con marca de hora opcional._ Para habilitar un grupo de informes con marca de hora opcional, consulte [Marcas de hora opcionales.](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/timestamp-optional.html)

## Comparación de sesión de muestra {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### Contenido en línea

```
{
  eventType: "sessionStart",
  playerTime: {
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ }
}
```

### Contenido descargado

```
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    },
    customMetadata:{},  
    qoeData:{}
},
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}},
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}},
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}},
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},},
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559}
}]
```

## Referencia de API de Media Tracker

Para obtener información sobre cómo configurar el contenido descargado, consulte la referencia [de la API de](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference)Media Tracker.
