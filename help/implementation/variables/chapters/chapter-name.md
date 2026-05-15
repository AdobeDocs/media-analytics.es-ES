---
title: Nombre del capítulo
description: Establezca un nombre descriptivo para cada capítulo, de modo que los informes de nivel de capítulo puedan desglosarse por título de capítulo.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 13%

---


# Nombre del capítulo

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Chapter name**. Consulte [Nombre de capítulo](/help/reporting/dimensions/chapter-name.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable del nombre del capítulo es el título legible en lenguaje natural de un capítulo (por ejemplo, `"Pilot Episode - Opening"`). Configúrelo en cada evento `media.chapterStart` cuyo contenido se divida en capítulos.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.chapter.friendlyName` |
| **Campo de colección XDM** | [`mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.chapter.friendlyName` |
| **Requerido** | No |
| **Enviado con** | [Inicio del capítulo](/help/implementation/events/chapters/chapter-start.md), cierre del capítulo |

## SDK web

Establecer `friendlyName` dentro de `mediaCollection.chapterDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase el nombre del capítulo como el primer argumento (`name`) a `createChapterObject`.

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Establecer `friendlyName` dentro de `mediaCollection.chapterDetails` al llamar a `sendMediaEvent` para `media.chapterStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) con `friendlyName` dentro de `mediaCollection.chapterDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pase el nombre del capítulo como primer argumento a `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## API de Media Collection

Incluir `media.chapter.friendlyName` en el objeto `params` de su solicitud POST de `chapterStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
