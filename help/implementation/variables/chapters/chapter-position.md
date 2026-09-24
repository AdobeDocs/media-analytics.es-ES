---
title: Posición del capítulo
description: Establezca el índice del capítulo dentro del contenido. La posición del capítulo es necesaria para que el ID de capítulo se genere automáticamente correctamente.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 6%
---

# Posición del capítulo

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Posición del capítulo**. Ver [Posición del capítulo](/help/reporting/dimensions/chapter-position.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de posición del capítulo es el índice del capítulo dentro del contenido, comenzando en `1` (típico) o `0` (según la convención). Utilice un índice estable por capítulo para que el mismo capítulo se acumule entre sesiones.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.chapter.position` |
| **Campo de colección XDM** | [`xdm.mediaCollection.chapterDetails.index`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.chapter.position` |
| **Requerido** | No (Mobile SDK); Sí (Edge, API de Media Collection) |
| **Enviado con** | [Inicio del capítulo](/help/implementation/events/chapters/chapter-start.md), cierre del capítulo |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `index` dentro de `xdm.mediaCollection.chapterDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Pase la posición del capítulo como segundo argumento a `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Pase la posición del capítulo como segundo argumento a `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku Edge]

Establecer `index` dentro de `xdm.mediaCollection.chapterDetails` al llamar a `sendMediaEvent` para `media.chapterStart`:

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

>[!TAB API de Media Edge]

Llame al extremo [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) con `index` dentro de `xdm.mediaCollection.chapterDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pase la posición del capítulo como segundo argumento a `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",
  1,
  240,
  0
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

Pase la posición del capítulo como segundo argumento a `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

Pase la posición del capítulo como segundo argumento (`position`) a `adb_media_init_chapterinfo`:

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB API de recopilación de medios]

Incluir `media.chapter.index` en el objeto `params` de su solicitud POST de `chapterStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.index": 1
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
