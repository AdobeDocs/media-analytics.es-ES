---
title: Cambio de velocidad de bits
description: Active un evento de cambio de velocidad de bits cada vez que el reproductor cambie a una velocidad de bits diferente.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 11%

---


# Cambio de velocidad de bits

>[!BEGINSHADEBOX]

*Esta página explica cómo implementar eventos de cambio de velocidad de bits. Consulte [Cambios de velocidad de bits (dimensión)](/help/reporting/dimensions/bitrate-changes.md) y [Cambios de velocidad de bits (métrica)](/help/reporting/metrics/bitrate-changes.md) para las variables de informes correspondientes.*

>[!ENDSHADEBOX]

El evento de cambio de velocidad de bits indica que el reproductor ha cambiado a una velocidad de bits diferente. Actualice primero el valor [Velocidad de bits](/help/implementation/variables/quality/bitrate.md) en el objeto QoE y, a continuación, active el evento de cambio de velocidad de bits. El servidor utiliza el recuento de estos eventos para calcular la dimensión y la métrica de cambios de velocidad de bits, y los valores de velocidad de bits resultantes alimentan la velocidad de bits media.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | (ninguno — contabilizado por el backend) |
| **Tipo de evento XDM** | `media.bitrateChange` |
| **rasgo de Audience Manager** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **Requerido** | No |
| **Enviado con** | [Cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md) |

## SDK web

Use [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar un evento `media.bitrateChange` con la nueva velocidad de bits:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## SDK móvil

Actualice el objeto QoE con la nueva velocidad de bits y, a continuación, active el evento de cambio de velocidad de bits.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

Use `sendMediaEvent` con `media.bitrateChange` para indicar un cambio en la velocidad de bits. Incluir la nueva velocidad de bits en `qoeDataDetails`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## API de Media Edge

Llame al extremo [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con el `qoeDataDetails` actualizado:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## Media SDK

Actualice el objeto QoE y active el evento:

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## API de Media Collection

Enviar una solicitud POST `bitrateChange` con la nueva velocidad de bits:

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
