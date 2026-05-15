---
title: Pantalla completa
description: Realice un seguimiento cuando el visualizador entre y salga de la reproducción en pantalla completa para que el back-end pueda informar sobre la participación en pantalla completa.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 10%

---


# Pantalla completa

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos del estado del reproductor **Pantalla completa**. Vea [Transmisiones afectadas por pantalla completa](/help/reporting/metrics/full-screen-streams-impacted.md), [Recuentos de pantalla completa](/help/reporting/metrics/full-screen-count.md) y [Duración total de pantalla completa](/help/reporting/metrics/full-screen-total-duration.md) para las métricas de informes correspondientes.*

>[!ENDSHADEBOX]

El estado del reproductor en pantalla completa rastrea cuando el visualizador entra y sale de la reproducción en pantalla completa. Active un evento de inicio de estado cada vez que el visor entre en modo de pantalla completa y un evento de fin de estado cuando salga el visor. El servidor calcula tres métricas a partir de estos eventos: flujos afectados, recuento de entradas de estado y tiempo total en el estado.

| Propiedad | Valor |
| --- | --- |
| **Variables de datos de contexto** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **Campo de colección XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) y [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entradas con `name: "fullscreen"`) |
| **rasgos de Audience Manager** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
| **Requerido** | No |
| **Enviado con** | [Inicio de estado](/help/implementation/events/player-state/state-start.md), [fin de estado](/help/implementation/events/player-state/state-end.md) |

## SDK web

Use [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar un evento `media.statesUpdate` con el estado agregado a `statesStart`:

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

Cuando el visor salga de pantalla completa, envíe otro evento con el estado `statesEnd`:

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

## SDK móvil

Use `tracker.trackPlayerStateStart()` y `tracker.trackPlayerStateEnd()` con la constante `MediaConstants.PlayerState.FULLSCREEN`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

Use `sendMediaEvent` para enviar un evento `media.statesUpdate` con el estado agregado a `statesStart`:

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

Cuando el visor salga de pantalla completa, envíe otro evento con el estado `statesEnd`:

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

Llame al extremo [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `fullscreen` en `statesStart` (o `statesEnd` cuando se cierre el visor):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

Use `ADB.Media.createStateObject` y la constante `ADB.Media.PlayerState.FullScreen`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

## API de Media Collection

Envíe una solicitud POST de `stateStart` cuando el visor entre en pantalla completa y una POST de `stateEnd` cuando salga:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
