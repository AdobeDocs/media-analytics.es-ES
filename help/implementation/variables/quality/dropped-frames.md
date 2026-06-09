---
title: Fotogramas perdidos
description: Defina el número de fotogramas perdidos en el objeto QoE para que el backend pueda informar de la calidad de colocación de fotogramas.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 5%

---


# Fotogramas perdidos

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Marcos perdidos**. Vea [Fotogramas perdidos](/help/reporting/dimensions/dropped-frames.md) para la dimensión y métrica de informes correspondiente.*

>[!ENDSHADEBOX]

La variable de fotogramas perdidos es el número de fotogramas que el reproductor ha perdido durante la sesión. Configúrelo en el objeto QoE y actualice el valor cada vez que el reproductor notifique nuevas caídas. El servidor informa del valor más reciente al cierre de la sesión.

>[!NOTE]
>
>Pasar siempre el **total acumulado** de fotogramas perdidos para toda la sesión hasta ese momento, no un delta por intervalo. Si restablece el valor a `0` entre actualizaciones, el servidor recibe `0` como valor final e informa de cero fotogramas perdidos para la sesión, independientemente de lo que se haya perdido anteriormente.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.qoe.droppedFrameCount` |
| **Campo de colección XDM** | [`xdm.mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **Requerido** | No |
| **Enviado con** | Eventos de calidad ([cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md), [inicio del búfer](/help/implementation/events/playback/buffer-start.md), [error](/help/implementation/events/error.md)), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `droppedFrames` dentro de `xdm.mediaCollection.qoeDataDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Pase los fotogramas perdidos como el cuarto argumento a `createQoEObject`. Actualice el rastreador antes de que se active cualquier evento de calidad.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Pase los fotogramas perdidos como el cuarto argumento a `createQoEObject`. Actualice el rastreador antes de que se active cualquier evento de calidad.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

Establecer `droppedFrames` dentro de `xdm.mediaCollection.qoeDataDetails` al llamar a `sendMediaEvent`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `droppedFrames` dentro de `xdm.mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
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

Pasar fotogramas perdidos como el cuarto argumento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Pase el recuento acumulado de fotogramas perdidos como el cuarto argumento a `ADBMobile.media.createQoSObject` y actualice el rastreador:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames (cumulative total)
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Pase el recuento acumulado de fotogramas perdidos como el cuarto argumento (`droppedFrames`) a `adb_media_init_qosinfo` y actualice el rastreador con `mediaUpdateQoS`:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB API de recopilación de medios]

Incluir `media.qoe.droppedFrames` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
