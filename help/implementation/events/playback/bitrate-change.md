---
title: Cambio de velocidad de bits
description: Indica que la velocidad de bits de reproducción ha cambiado.
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
source-wordcount: '235'
ht-degree: 6%
---

# Cambio de velocidad de bits

El evento de cambio de velocidad de bits indica que el reproductor ha negociado una nueva velocidad de bits de reproducción. Enviarlo siempre que la velocidad de bits cambie durante la reproducción. Incluya el nuevo valor de velocidad de bits en los datos de QoE para que el back-end pueda calcular [[!UICONTROL Velocidad de bits media]](/help/reporting/metrics/average-bitrate.md) y la dimensión del bloque por velocidad de bits.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: [[!UICONTROL Cambios de velocidad de bits]](/help/reporting/metrics/bitrate-changes.md)

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.bitrateChange"` y la nueva velocidad de bits en `qoeDataDetails`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Cree un objeto QoE con la nueva velocidad de bits y actualice el rastreador antes de que se active el evento de cambio de velocidad de bits.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Cree un objeto QoE con la nueva velocidad de bits y actualice el rastreador antes de que se active el evento de cambio de velocidad de bits.

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku Edge]

Llamar a `sendMediaEvent` con `eventType: "media.bitrateChange"` y la nueva velocidad de bits en `qoeDataDetails`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/) con la nueva velocidad de bits en `qoeDataDetails`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
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

Cree un objeto QoE con la nueva velocidad de bits y actualice el rastreador:

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

Actualice el objeto QoS devuelto por el delegado `getQoSObject` y, a continuación, realice un seguimiento del evento:

```javascript
// Update QoS data via the delegate
this._qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // dropped frames
  24,    // fps
  0      // startup time
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

Cree un objeto QoS con la nueva velocidad de bits con `adb_media_init_qosinfo`, actualice el rastreador con `mediaUpdateQoS` y realice un seguimiento del evento. Observe el orden del parámetro Roku: `bitrate, startupTime, fps, droppedFrames`.

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB API de recopilación de medios]

Envíe una publicación de `bitrateChange` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) con la nueva velocidad de bits en `qoeData`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```

>[!ENDTABS]
