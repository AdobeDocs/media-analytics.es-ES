---
title: Capítulo completado
description: Indica que ha terminado de reproducirse un segmento de capítulo.
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
source-wordcount: '150'
ht-degree: 10%
---

# Capítulo completado

El evento de capítulo completado indica que se ha terminado de reproducir un capítulo. Enviarlo cuando el usuario llegue al final de un capítulo. Si el visor omite el capítulo, envía [omitir capítulo](chapter-skip.md) en su lugar.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de capítulo](chapter-start.md)
* **Métrica asociada**: [[!UICONTROL El capítulo finaliza]](/help/reporting/metrics/chapter-completes.md)

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.chapterComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

>[!TAB iOS]

Llamar a `trackEvent` con el tipo de evento `ChapterComplete`.

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Llamar a `trackEvent` con el tipo de evento `ChapterComplete`.

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

>[!TAB Roku Edge]

Llamar a `sendMediaEvent` con `eventType: "media.chapterComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
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

Llamar a `trackEvent` con el tipo de evento `ChapterComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

>[!TAB Chromecast]

Llamar a `trackEvent` con el tipo de evento `ChapterComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
```

>[!TAB Roku 2.x]

Llamar a `mediaTrackEvent` con el tipo de evento `MEDIA_CHAPTER_COMPLETE`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_COMPLETE)
```

>[!TAB API de recopilación de medios]

Enviar un POST de `chapterComplete` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```

>[!ENDTABS]
