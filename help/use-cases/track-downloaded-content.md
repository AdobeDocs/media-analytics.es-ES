---
title: Seguimiento del contenido descargado sin conexión en la colección de medios de streaming
description: Aprenda a utilizar la funcionalidad Contenido descargado para seguir el consumo de medios cuando un usuario está sin conexión.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 98%

---

# Seguimiento del contenido descargado {#track-downloaded-content}

## Información general {#overview}

La funcionalidad Contenido descargado proporciona la capacidad de realizar un seguimiento del consumo de medios cuando un usuario está sin conexión. Por ejemplo, un usuario descarga e instala una aplicación en un dispositivo móvil y, a continuación, utiliza la aplicación para descargar contenido en el almacenamiento local del dispositivo. Para realizar un seguimiento de los datos descargados, Adobe ha desarrollado la funcionalidad Contenido descargado. Con esta funcionalidad, cuando el usuario reproduce contenido desde el almacenamiento de un dispositivo, los datos de seguimiento se almacenan en el dispositivo, independientemente de su conectividad. Cuando el usuario termina la sesión de reproducción y el dispositivo vuelve a estar en línea, la información de seguimiento almacenada se envía al back-end de la API de recopilación de contenido en una única carga. A continuación, la información de seguimiento almacenada se procesa y se comunica como de costumbre en la API de recopilación de medios.

Contrastar los dos enfoques:

* En línea

  Con este enfoque en tiempo real, el reproductor de contenido envía los datos de seguimiento con cada evento del reproductor, y envía pings de red cada diez segundos (cada segundo en el caso de los anuncios), uno a uno al back-end.

* Sin conexión (función Contenido descargado)

  Con este método de procesamiento por lotes, es necesario que se generen los mismos eventos de sesión, pero estos se almacenan en el dispositivo hasta que se envían al back-end como una sola sesión (ver ejemplo a continuación).

Cada enfoque tiene sus ventajas y desventajas:
* El seguimiento del escenario en línea se realiza en tiempo real; esto requiere una comprobación de conectividad antes de cada llamada de red.
* El escenario sin conexión (función Contenido descargado) solo necesita una comprobación de conectividad de red, pero también requiere un espacio de memoria mayor en el dispositivo.

## Implementación {#implementation}

### Plataformas compatibles

El seguimiento de contenido es compatible con dispositivos móviles iOS y Android.

### Esquemas de eventos

La función Contenido descargado es la versión sin conexión de la API (estándar) de recopilación de contenido en línea, por lo que los datos del evento que el reproductor envía al back-end deben utilizar los mismos esquemas de eventos que utiliza al realizar llamadas en línea. Para obtener más información sobre estos esquemas, consulte:
* [Información general;](/help/implementation/media-collection-api/mc-api-overview.md)
* [Validación de solicitudes de eventos](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Orden de los eventos

* El primer evento de la carga útil por lotes debe ser `sessionStart`, como es habitual con la API de recopilación de contenido.
* **Debe incluir `media.downloaded: true`** en los parámetros de metadatos estándar (clave `params`) del evento `sessionStart` para indicar al back-end que está enviando contenido descargado. Si este parámetro no está presente o se establece como falso, la API de Contenido descargado devolverá un código de respuesta 400 (solicitud no válida). Este parámetro distingue entre el contenido descargado y el contenido en directo en el back-end. (Si `media.downloaded: true` se establece en una sesión activa, la API emitirá igualmente una respuesta 400).
* Es responsabilidad de la implementación almacenar correctamente los eventos del reproductor por orden de aparición.

### Códigos de respuesta

* 201: Creado, la solicitud correcta; los datos son válidos y la sesión se creó y se procesará.
* 400: Solicitud incorrecta, error en la validación del esquema, se descartan todos los datos y no se procesan los datos de las sesiones.

## Integración con Adobe Analtyics {#integration-with-adobe-analtyics}

Al calcular las llamadas de inicio y cierre de Analytics para el escenario de contenido descargado, el back-end establece un campo adicional de Analytics llamado `ts.` Estas son marcas de hora para el primer y último evento recibido (inicio y finalización). Este mecanismo permite colocar una sesión de contenido finalizada en el momento correcto (es decir, incluso si el usuario no vuelve a estar en línea durante varios días, la sesión de contenido se registra como si hubiera tenido lugar en el momento en el que el contenido se visualizó). Debe habilitar este mecanismo en Adobe Analytics. Para ello, cree un _grupo de informes con marca de hora opcional._ Para habilitar un grupo de informes con marca de hora opcional, consulte [Marcas de hora opcionales.](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=es)

## Comparación de sesión de muestra {#sample-session-comparison}

### Contenido en línea

```
POST /api/v1/sessions HTTP/1.1

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
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### Aviso de fin de compatibilidad

>[!IMPORTANT]
>
>Anteriormente, el contenido descargado también se podía enviar a la API `/api/v1/sessions`. Esta forma de seguimiento del contenido descargado está **obsoleta** y se **eliminará** en el futuro.


La API `/api/v1/sessions` solo aceptará eventos de inicialización de sesión.
Al utilizar la nueva API, el indicador `media.downloaded`, antes obligatorio, ya no es necesario.
Le recomendamos encarecidamente que use la API `/api/v1/downloaded` para nuevas implementaciones de contenido descargado, así como para actualizar las existentes que dependen de la API antigua.


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

## Referencia de la API del monitor de medios

Para obtener información sobre cómo configurar el contenido descargado, consulte la referencia de la [API del monitor de medios](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/).
