---
title: Desplazamiento de capítulo
description: Establezca el desplazamiento del capítulo dentro del contenido, en segundos desde el inicio.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 7%

---


# Desplazamiento de capítulo

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Desplazamiento de capítulo**. Ver [Desplazamiento de capítulo](/help/reporting/dimensions/chapter-offset.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de desplazamiento del capítulo es el desplazamiento del capítulo dentro del contenido, medido en segundos desde el inicio. El primer capítulo generalmente tiene un desplazamiento de `0`; los capítulos subsiguientes tienen desplazamientos que coinciden con la hora de inicio del cabezal de reproducción.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.chapter.offset` |
| **Campo de colección XDM** | [`xdm.mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.chapter.offset` |
| **Requerido** | No (Mobile SDK); Sí (Edge, API de Media Collection) |
| **Enviado con** | [Inicio del capítulo](/help/implementation/events/chapters/chapter-start.md), cierre del capítulo |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `offset` dentro de `xdm.mediaCollection.chapterDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

>[!TAB iOS]

Pase el desplazamiento en segundos como el cuarto argumento (`startTime`) a `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Pase el desplazamiento en segundos como el cuarto argumento (`startTime`) a `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku]

Establecer `offset` dentro de `xdm.mediaCollection.chapterDetails` al llamar a `sendMediaEvent` para `media.chapterStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) con `offset` dentro de `xdm.mediaCollection.chapterDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pase el desplazamiento como cuarto argumento a `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

Pase el desplazamiento del capítulo en segundos como el cuarto argumento (`startTime`) a `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime (seconds from content start)
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB API de recopilación de medios]

Incluir `media.chapter.offset` en el objeto `params` de su solicitud POST de `chapterStart`:

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
