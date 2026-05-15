---
title: Play
description: Indica que el reproductor multimedia ha entrado en el estado de reproducción.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 17%

---


# Play

El evento de reproducción indica que el reproductor de contenido ha cambiado de estado a reproducción. Enviarlo al inicio del contenido, en la reproducción automática y siempre que el reproductor se reanude tras una pausa o almacenamiento en búfer. No hay un evento de reanudación independiente; un evento de reproducción después de [Pausar inicio](pause-start.md) o [Inicio del búfer](buffer-start.md) sirve como reanudación.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: [El contenido comienza](/help/reporting/metrics/content-starts.md)

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.play"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvil

Invoque `trackPlay` cuando el reproductor de contenido comience o reanude la reproducción.

**iOS (Swift)**

```swift
tracker.trackPlay()
```

**Android (Kotlin)**

```kotlin
tracker.trackPlay()
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.play"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llamar al extremo [play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Invoque `trackPlay` cuando el reproductor de contenido comience o reanude la reproducción:

```javascript
tracker.trackPlay();
```

## API de Media Collection

Enviar un POST de `play` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```
