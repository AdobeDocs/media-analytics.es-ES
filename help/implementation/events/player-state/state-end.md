---
title: Fin de estado
description: Indica que el reproductor de contenido ha salido del estado de reproductor rastreado.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 13%

---


# Fin de estado

El evento de finalización de estado indica que el reproductor de contenido ha salido de un estado rastreado, como pantalla completa, silencio o subtítulos. Enviarlo para cerrar un estado abierto por [Inicio de estado](state-start.md). Los estados se pueden iniciar y finalizar en la misma llamada de evento. Un reproductor puede salir de varios estados simultáneamente.

Nombres de estado válidos: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de estado](state-start.md)
* **Métrica asociada**: Varía según el estado; consulte [Seguimiento del estado del reproductor](/help/use-cases/player-state-tracking/implementation-and-reporting.md)

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.statesUpdate"` y el nombre de estado en `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

Los estados se pueden iniciar y finalizar en la misma llamada:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvil

Use `trackPlayerStateEnd` con un objeto de estado creado a partir de la constante `MediaConstants.PlayerState` apropiada.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.statesUpdate"` y el nombre de estado en `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

## API de Media Edge

Llame al extremo [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con el nombre de estado en `statesEnd`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Use `ADB.Media.createStateObject` con la constante `ADB.Media.PlayerState` adecuada:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

## API de Media Collection

Enviar un POST de `stateEnd` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
