---
title: Capítulo completado
description: Indica que ha terminado de reproducirse un segmento de capítulo.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 20%

---


# Capítulo completado

El evento de capítulo completado indica que se ha terminado de reproducir un capítulo. Enviarlo cuando el usuario llegue al final de un capítulo. Si el visor omite el capítulo, envía [omitir capítulo](chapter-skip.md) en su lugar.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de capítulo](chapter-start.md)
* **Métrica asociada**: [El capítulo finaliza](/help/reporting/metrics/chapter-completes.md)

## SDK web

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

## SDK móvil

Llamar a `trackEvent` con el tipo de evento `ChapterComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

## Roku (BrightScript)

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

## API de Media Edge

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

## Media SDK

Llamar a `trackEvent` con el tipo de evento `ChapterComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

## API de Media Collection

Enviar un POST de `chapterComplete` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```
