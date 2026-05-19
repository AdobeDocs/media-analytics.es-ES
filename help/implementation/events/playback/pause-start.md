---
title: Pausar inicio
description: Indicación de que el usuario ha pausado la reproducción de contenido.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 19%

---


# Pausar inicio

El evento de inicio de pausa indica que el usuario pausó la reproducción. No hay un evento de reanudación independiente; envíe un evento [Play](play.md) cuando se reanude la reproducción.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: [Pausar eventos](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>No hay ningún tipo de evento de reanudación. La reanudación se infiere al enviar un evento [`play`](play.md) después de `pauseStart`.

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.pauseStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

## SDK móvil

Invoque `trackPause` cuando el usuario detenga la reproducción.

**iOS (Swift)**

```swift
tracker.trackPause()
```

**Android (Kotlin)**

```kotlin
tracker.trackPause()
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.pauseStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

## API de Media Edge

Llame al extremo [pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Invoque `trackPause` cuando el usuario ponga en pausa la reproducción:

```javascript
tracker.trackPause();
```

## API de Media Collection

Enviar un POST de `pauseStart` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```
