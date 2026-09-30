---
title: Omisión de capítulo
description: Señal de que el visualizador ha omitido un capítulo.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 9%
---

# Omisión de capítulo

El evento de omisión de capítulo indica que el visor omitió un capítulo antes de finalizar. Enviarlo cuando el visor navegue más allá del límite del capítulo sin verlo hasta su finalización. Enviar [capítulo completado](chapter-complete.md) si el capítulo se reproduce hasta su final.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de capítulo](chapter-start.md)
* **Métrica asociada**: ninguna

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.chapterSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

Llamar a `trackEvent` con el tipo de evento `ChapterSkip`.

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Llamar a `trackEvent` con el tipo de evento `ChapterSkip`.

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

>[!TAB Roku Edge]

Llamar a `sendMediaEvent` con `eventType: "media.chapterSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Llamar a `trackEvent` con el tipo de evento `ChapterSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

>[!TAB Chromecast]

Llamar a `trackEvent` con el tipo de evento `ChapterSkip`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
```

>[!TAB Roku 2.x]

Llamar a `mediaTrackEvent` con el tipo de evento `MEDIA_CHAPTER_SKIP`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_SKIP)
```

>[!TAB API de recopilación de medios]

Enviar un POST de `chapterSkip` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```

>[!ENDTABS]
