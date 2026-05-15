---
title: Subtítulos opcionales
description: Realice un seguimiento cuando el visor active o desactive los subtítulos para que el backend pueda informar sobre la participación en los subtítulos.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 9%

---


# Subtítulos opcionales

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos del estado del reproductor **Subtítulos**. Vea [Transmisiones afectadas por los subtítulos opcionales](/help/reporting/metrics/closed-captioning-streams-impacted.md), [Recuentos de subtítulos opcionales](/help/reporting/metrics/closed-captioning-count.md) y [Duración total de los subtítulos opcionales](/help/reporting/metrics/closed-captioning-total-duration.md) para las métricas de informes correspondientes.*

>[!ENDSHADEBOX]

El estado del reproductor de subtítulos opcionales se registra cuando el visor activa y desactiva los subtítulos. Active un evento de inicio de estado cuando los subtítulos estén habilitados y un evento de fin de estado cuando los subtítulos estén deshabilitados. El servidor calcula tres métricas a partir de estos eventos: flujos afectados, recuento de entradas de estado y tiempo total en el estado.

| Propiedad | Valor |
| --- | --- |
| **Variables de datos de contexto** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **Campo de colección XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-collection-details) y [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-collection-details) (entradas con `name: "closedCaptioning"`) |
| **rasgos de Audience Manager** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
| **Requerido** | No |
| **Enviado con** | [Inicio de estado](/help/implementation/events/player-state/state-start.md), [fin de estado](/help/implementation/events/player-state/state-end.md) |

## SDK web

Use [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar un evento `media.statesUpdate` con el estado agregado a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Cuando el visor deshabilite los subtítulos, envíe otro evento con el estado `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvil

Use `tracker.trackPlayerStateStart()` y `tracker.trackPlayerStateEnd()` con la constante `MediaConstants.PlayerState.CLOSED_CAPTION`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

Use `sendMediaEvent` para enviar un evento `media.statesUpdate` con el estado agregado a `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

Cuando el visor deshabilite los subtítulos, envíe otro evento con el estado `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

## API de Media Edge

Llame al extremo [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `closedCaptioning` en `statesStart` (o `statesEnd` cuando el visor deshabilite los subtítulos):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

Use `ADB.Media.createStateObject` y la constante `ADB.Media.PlayerState.ClosedCaptioning`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API de Media Collection

Envíe una solicitud POST de `stateStart` cuando los subtítulos estén habilitados y una POST de `stateEnd` cuando estén deshabilitados:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
