---
title: Cambio de velocidad de bits
description: Active un evento de cambio de velocidad de bits cada vez que el reproductor cambie a una velocidad de bits diferente.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%

---


# Cambio de velocidad de bits

>[!BEGINSHADEBOX]

*Esta página explica cómo implementar eventos de cambio de velocidad de bits. Vea [[!UICONTROL Cambios de velocidad de bits] (dimensión)](/help/reporting/dimensions/bitrate-changes.md) y [[!UICONTROL Cambios de velocidad de bits] (métrica)](/help/reporting/metrics/bitrate-changes.md) para las variables de informes correspondientes.*

>[!ENDSHADEBOX]

El evento de cambio de velocidad de bits indica que el reproductor ha cambiado a una velocidad de bits diferente. Actualice primero el valor [Velocidad de bits](/help/implementation/variables/quality/bitrate.md) en el objeto QoE y, a continuación, active el evento de cambio de velocidad de bits. El servidor usa el recuento de estos eventos para calcular la dimensión [[!UICONTROL cambios de velocidad de bits]](/help/reporting/dimensions/bitrate-changes.md) y la métrica [[!UICONTROL cambios de velocidad de bits]](/help/reporting/metrics/bitrate-changes.md), y los valores de velocidad de bits resultantes alimentan [[!UICONTROL Velocidad de bits media]](/help/reporting/metrics/average-bitrate.md).

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | (ninguno — contabilizado por el backend) |
| **Tipo de evento XDM** | `media.bitrateChange` |
| **rasgo de Audience Manager** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **Requerido** | No |
| **Enviado con** | [Cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md) |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Actualice el objeto QoE con la nueva velocidad de bits y, a continuación, active el evento de cambio de velocidad de bits.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Actualice el objeto QoE con la nueva velocidad de bits y, a continuación, active el evento de cambio de velocidad de bits.

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Actualice el objeto QoE y active el evento:

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

Actualice el objeto QoS con la nueva velocidad de bits y, a continuación, active el evento de cambio de velocidad de bits:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  4500,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

Actualice el objeto QoS con la nueva velocidad de bits y, a continuación, active el evento de cambio de velocidad de bits:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(4500.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB API de recopilación de medios]

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

>[!ENDTABS]
