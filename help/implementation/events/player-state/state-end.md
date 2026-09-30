---
title: Fin de estado
description: Indica que el reproductor de contenido ha salido del estado de reproductor rastreado.
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
source-wordcount: '229'
ht-degree: 6%
---

# Fin de estado

El evento de finalización de estado indica que el reproductor de contenido ha salido de un estado rastreado, como pantalla completa, silencio o subtítulos. Enviarlo para cerrar un estado abierto por [Inicio de estado](state-start.md). Los estados se pueden iniciar y finalizar en la misma llamada de evento. Un reproductor puede salir de varios estados simultáneamente.

Nombres de estado válidos: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de estado](state-start.md)
* **Métrica asociada**: Varía según el estado; consulte [Seguimiento de estados de los reproductores](/help/implementation/events/player-state/overview.md)

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Use `trackPlayerStateEnd` con un objeto de estado creado a partir de la constante `MediaConstants.PlayerState` apropiada.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

>[!TAB Android]

Use `trackPlayerStateEnd` con un objeto de estado creado a partir de la constante `MediaConstants.PlayerState` apropiada.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Use `ADB.Media.createStateObject` con la constante `ADB.Media.PlayerState` adecuada:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Use `ADBMobile.media.createStateObject` con la constante `ADBMobile.media.PlayerState` adecuada:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

El seguimiento del estado del reproductor no está disponible en SDK Roku 2.x. Para rastrear estados de reproductor, usa [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API de recopilación de medios]

Enviar un POST de `stateEnd` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
