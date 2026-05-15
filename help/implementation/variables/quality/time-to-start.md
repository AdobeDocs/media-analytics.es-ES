---
title: Tiempo para el inicio
description: Establezca el tiempo de inicio del reproductor, en milisegundos, para que el backend pueda informar del tiempo hasta el primer fotograma de calidad.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 12%

---


# Tiempo para el inicio

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Tiempo para el inicio**. Ver [Tiempo para el inicio](/help/reporting/dimensions/time-to-start.md) para la dimensión y métrica de informes correspondiente.*

>[!ENDSHADEBOX]

La variable tiempo para el inicio es el tiempo, en milisegundos, transcurrido entre el momento en que el reproductor inicia la reproducción y el primer procesamiento del fotograma. Configúrelo en el objeto QoE antes de que se active el evento de inicio de sesión. Adobe almacena e informa del valor en segundos; pasa milisegundos y Adobe se convierte en el momento de la ingesta.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.qoe.timeToStart` |
| **Campo de colección XDM** | [`mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.qoe.timeToStart` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## SDK web

Establecer `timeToStart` dentro de `mediaCollection.qoeDataDetails` en `media.sessionStart` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Pasar el tiempo de inicio como segundo argumento (`startupTime`) a `createQoEObject`.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Establecer `timeToStart` dentro de `mediaCollection.qoeDataDetails` en `media.sessionStart` al llamar a `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `timeToStart` dentro de `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pase el tiempo para comenzar como el segundo argumento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## API de Media Collection

Incluir `media.qoe.timeToStart` en el objeto `params` en `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
