---
title: Imagen en imagen
description: Realice un seguimiento cuando el usuario entra y sale de la reproducción de imagen en imagen para que el servidor pueda informar sobre la participación de PiP.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 8%

---


# Imagen en imagen

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos del estado del reproductor **Imagen en imagen**. Vea [Transmisiones afectadas por imagen en imagen](/help/reporting/metrics/picture-in-picture-streams-impacted.md), [Recuentos de imagen en imagen](/help/reporting/metrics/picture-in-picture-count.md) y [Duración total de imagen en imagen](/help/reporting/metrics/picture-in-picture-total-duration.md) para las métricas de informes correspondientes.*

>[!ENDSHADEBOX]

El estado del reproductor de imagen en imagen se registra cuando el usuario entra y sale de la reproducción de imagen en imagen. Active un evento de inicio de estado cuando comience la imagen en imagen y un evento de fin de estado cuando termine. El servidor calcula tres métricas a partir de estos eventos: flujos afectados, recuento de entradas de estado y tiempo total en el estado.

| Propiedad | Valor |
| --- | --- |
| **Variables de datos de contexto** | `a.media.states.pictureinpicture.set`, `a.media.states.pictureinpicture.count`, `a.media.states.pictureinpicture.time` |
| **Campo de colección XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-collection-details) y [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-collection-details) (entradas con `name: "pictureInPicture"`) |
| **Requerido** | No |
| **Enviado con** | Inicio de estado, fin de estado |

## SDK web

Use [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar un evento `media.statesUpdate` con el estado agregado a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Cuando el visor salga de imagen en imagen, envíe otro evento con el estado en `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvil

Use `tracker.trackPlayerStateStart()` y `tracker.trackPlayerStateEnd()` con la constante `MediaConstants.PlayerState.PICTURE_IN_PICTURE`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)

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
            "statesStart": [{ "name": "pictureInPicture" }],
            "playhead": 60
        }
    }
})
```

Cuando el visor salga de imagen en imagen, envíe otro evento con el estado en `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "pictureInPicture" }],
            "playhead": 90
        }
    }
})
```

## API de Media Edge

Llame al extremo [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `pictureInPicture` en `statesStart` (o `statesEnd` cuando el visor salga de la PiP):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "pictureInPicture" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

Use `ADB.Media.createStateObject` y la constante `ADB.Media.PlayerState.PictureInPicture`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API de Media Collection

Envíe una solicitud POST de `stateStart` cuando comience la imagen en imagen y una POST de `stateEnd` cuando termine:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "pictureInPicture"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
