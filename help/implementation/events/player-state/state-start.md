---
title: Inicio del estado
description: Indica que el reproductor de contenidos ha entrado en el estado de reproductor rastreado.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 6%

---


# Inicio del estado

El evento de inicio de estado indica que el reproductor de contenido ha entrado en un estado rastreado, como pantalla completa, silencio o subtítulos. Un reproductor puede estar en varios estados simultáneamente, y los estados pueden iniciarse y finalizarse en la misma llamada de evento. Cierre cada estado con un evento [State end](state-end.md).

Nombres de estado válidos: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: Varía según el estado; consulte [Seguimiento de estados de los reproductores](/help/implementation/events/player-state/overview.md)

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.statesUpdate"` y el nombre de estado en `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Se pueden iniciar varios estados en la misma llamada:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

Use `trackPlayerStateStart` con un objeto de estado creado a partir de la constante `MediaConstants.PlayerState` apropiada.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

>[!TAB Android]

Use `trackPlayerStateStart` con un objeto de estado creado a partir de la constante `MediaConstants.PlayerState` apropiada.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

>[!TAB Roku Edge]

Llamar a `sendMediaEvent` con `eventType: "media.statesUpdate"` y el nombre de estado en `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con el nombre de estado en `statesStart`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
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

tracker.trackPlayerStateStart(stateObject);
```

>[!TAB Chromecast]

Use `ADBMobile.media.createStateObject` con la constante `ADBMobile.media.PlayerState` adecuada:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
```

>[!TAB Roku 2.x]

El seguimiento del estado del reproductor no está disponible en SDK Roku 2.x. Para rastrear estados de reproductor, usa [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API de recopilación de medios]

Enviar un POST de `stateStart` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
