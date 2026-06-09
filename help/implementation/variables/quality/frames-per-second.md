---
title: Fotogramas por segundo
description: Establezca la velocidad de fotogramas actual en el objeto QoE de modo que el backend tenga contexto de velocidad de fotogramas para los informes de calidad.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 7%

---


# Fotogramas por segundo

La variable fotogramas por segundo es la velocidad de fotogramas actual del flujo. Configúrelo en el objeto QoE junto con la velocidad de bits y los fotogramas perdidos para que el back-end tenga un contexto de calidad total para cada sesión de reproducción. Adobe Analytics no crea automáticamente una variable de informe de velocidad de fotogramas; cree una regla de procesamiento personalizada si desea que aparezca como un informe.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | Ninguno (Adobe Analytics no asigna una clave de datos de contexto reservada para la velocidad de fotogramas) |
| **Campo de colección XDM** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **rasgo de Audience Manager** | N/A |
| **Requerido** | No |
| **Enviado con** | Eventos de calidad ([cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md), [inicio del búfer](/help/implementation/events/playback/buffer-start.md), [error](/help/implementation/events/error.md)), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `framesPerSecond` dentro de `xdm.mediaCollection.qoeDataDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Pase la velocidad de fotogramas como tercer argumento (`fps`) a `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Pase la velocidad de fotogramas como tercer argumento (`fps`) a `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

Establecer `framesPerSecond` dentro de `xdm.mediaCollection.qoeDataDetails` al llamar a `sendMediaEvent`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `framesPerSecond` dentro de `xdm.mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
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

Pase la velocidad de fotogramas como tercer argumento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Pase la velocidad de fotogramas como tercer argumento (`fps`) a `ADBMobile.media.createQoSObject` y actualice el rastreador:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Pase la velocidad de fotogramas como tercer argumento (`fps`) a `adb_media_init_qosinfo` y actualice el rastreador con `mediaUpdateQoS`:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB API de recopilación de medios]

Incluir `media.qoe.framesPerSecond` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
