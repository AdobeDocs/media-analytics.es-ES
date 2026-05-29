---
title: Velocidad de bits
description: Establezca la velocidad de bits de reproducción actual (en kbps) en el objeto QoE para que el servidor pueda calcular las métricas de velocidad de bits.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 6%

---


# Velocidad de bits

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Velocidad de bits**. Vea [[!UICONTROL Velocidad de bits promedio] (dimensión)](/help/reporting/dimensions/average-bitrate.md) y [[!UICONTROL Velocidad de bits promedio] (métrica)](/help/reporting/metrics/average-bitrate.md) para las variables de informes correspondientes.*

>[!ENDSHADEBOX]

La variable de velocidad de bits es la velocidad de bits de reproducción actual, en kilobits por segundo. Configúrelo en el objeto QoE siempre que el reproductor negocie una velocidad de bits y actualice el objeto QoE cuando esta cambie. El servidor usa valores de velocidad de bits para calcular [[!UICONTROL Velocidad de bits promedio]](/help/reporting/metrics/average-bitrate.md), la dimensión por bloque de velocidad de bits y la métrica [[!UICONTROL Cambios de velocidad de bits]](/help/reporting/metrics/bitrate-changes.md).

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.qoe.bitrateAverageBucket` |
| **Campo de colección XDM** | [`xdm.mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **Requerido** | No |
| **Enviado con** | Eventos de calidad ([cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md), [inicio del búfer](/help/implementation/events/playback/buffer-start.md), [error](/help/implementation/events/error.md)), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `bitrate` dentro de `xdm.mediaCollection.qoeDataDetails` en `media.bitrateChange` (o cualquier evento relacionado con la calidad) al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Pase la velocidad de bits como primer argumento a `createQoEObject`. Actualice el objeto QoE en el rastreador antes de que se active cualquier evento de calidad.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Pase la velocidad de bits como primer argumento a `createQoEObject`. Actualice el objeto QoE en el rastreador antes de que se active cualquier evento de calidad.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

Establecer `bitrate` dentro de `xdm.mediaCollection.qoeDataDetails` al llamar a `sendMediaEvent` para eventos de calidad como `media.bitrateChange`:

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

Llame al extremo [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `bitrate` dentro de `xdm.mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pase la velocidad de bits como primer argumento a `ADB.Media.createQoEObject` y actualice el rastreador:

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Pase la velocidad de bits en kbps como primer argumento a `ADBMobile.media.createQoSObject` y actualice el rastreador:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB API de recopilación de medios]

Incluir `media.qoe.bitrate` en el objeto `params` de su solicitud POST de `bitrateChange`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
