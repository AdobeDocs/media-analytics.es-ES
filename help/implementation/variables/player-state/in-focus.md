---
title: En el centro
description: Rastree cuándo el reproductor está enfocado en la pantalla del visualizador para que el backend pueda informar sobre la participación en el enfoque.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 8%

---


# En el centro

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para el estado del reproductor **Enfocado**. Ver [Transmisiones afectadas por enfoque](/help/reporting/metrics/in-focus-streams-impacted.md), [Recuentos de enfoque](/help/reporting/metrics/in-focus-count.md) y [Duración total del enfoque](/help/reporting/metrics/in-focus-total-duration.md) para las métricas de informes correspondientes.*

>[!ENDSHADEBOX]

El estado del reproductor enfocado rastrea cuándo el reproductor recibe la atención del usuario. Activa un evento de inicio de estado cuando el reproductor recibe Focus (normalmente cuando la pestaña o ventana del reproductor se activa) y un evento de fin de estado cuando el reproductor pierde Focus. El servidor calcula tres métricas a partir de estos eventos: flujos afectados, recuento de entradas de estado y tiempo total en el estado.

| Propiedad | Valor |
| --- | --- |
| **Variables de datos de contexto** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **Campo de colección XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) y [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entradas con `name: "inFocus"`) |
| **rasgos de Audience Manager** | `c_contextdata.a.media.states.infocus.set`, `c_contextdata.a.media.states.infocus.count`, `c_contextdata.a.media.states.infocus.time` |
| **Requerido** | No |
| **Enviado con** | [Inicio de estado](/help/implementation/events/player-state/state-start.md), [fin de estado](/help/implementation/events/player-state/state-end.md) |

## SDK web

Use [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar un evento `media.statesUpdate` con el estado agregado a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Cuando el reproductor pierde el enfoque, envíe otro evento con el estado `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvil

Use `tracker.trackPlayerStateStart()` y `tracker.trackPlayerStateEnd()` con la constante `MediaConstants.PlayerState.IN_FOCUS`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

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
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

Cuando el reproductor pierde el enfoque, envíe otro evento con el estado `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

## API de Media Edge

Llamar al extremo [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `inFocus` en `statesStart` (o `statesEnd` cuando el reproductor pierde el enfoque):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

Use `ADB.Media.createStateObject` y la constante `ADB.Media.PlayerState.InFocus`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API de Media Collection

Envíe una solicitud POST de `stateStart` cuando el reproductor recibe Focus y una POST de `stateEnd` cuando pierde Focus:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
