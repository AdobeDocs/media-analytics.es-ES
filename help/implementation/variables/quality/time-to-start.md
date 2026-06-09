---
title: Tiempo para el inicio
description: Establezca el tiempo de inicio del reproductor, en milisegundos, para que el backend pueda informar del tiempo hasta el primer fotograma de calidad.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 5%

---


# Tiempo para el inicio

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Tiempo para el inicio**. Ver [[!UICONTROL Tiempo para el inicio]](/help/reporting/dimensions/time-to-start.md) para la dimensión y métrica de informes correspondiente.*

>[!ENDSHADEBOX]

La variable tiempo para el inicio es el tiempo, en milisegundos, transcurrido entre el momento en que el reproductor inicia la reproducción y el primer procesamiento del fotograma. Configúrelo en el objeto QoE antes de que se active el evento de inicio de sesión. Adobe almacena e informa del valor en segundos; pasa milisegundos y Adobe se convierte en el momento de la ingesta.

>[!IMPORTANT]
>
>Una vez que el reproductor comience a procesar fotogramas de contenido, deje de actualizar `timeToStart`. El valor puede aumentar durante la fase inicial de almacenamiento en búfer o de carga, pero debe tratarse como fijo desde el momento en que comienza la reproducción. Si continúa actualizándolo después de que el primer fotograma se procese, se producirá una métrica [[!UICONTROL Tiempo para el inicio]](/help/reporting/metrics/time-to-start.md) inflada o incorrecta.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.qoe.timeToStart` |
| **Campo de colección XDM** | [`xdm.mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.qoe.timeToStart` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `timeToStart` dentro de `xdm.mediaCollection.qoeDataDetails` en `media.sessionStart` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Pasar el tiempo de inicio como segundo argumento (`startupTime`) a `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Pasar el tiempo de inicio como segundo argumento (`startupTime`) a `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

Establecer `timeToStart` dentro de `xdm.mediaCollection.qoeDataDetails` en `media.sessionStart` al llamar a `createMediaSession`:

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

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `timeToStart` dentro de `xdm.mediaCollection.qoeDataDetails`:

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pase el tiempo para comenzar como el segundo argumento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Pase el tiempo de inicio en milisegundos como segundo argumento (`startupTime`) a `ADBMobile.media.createQoSObject` y actualice el rastreador:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,   // bitrate
  0,      // startupTime (ms)
  24,     // fps
  0       // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Pase el tiempo de inicio como segundo argumento (`startupTime`) a `adb_media_init_qosinfo` y actualice el rastreador con `mediaUpdateQoS`:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB API de recopilación de medios]

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

>[!ENDTABS]
