---
title: Longitud de contenido
description: Establezca la duración del contenido en segundos al inicio de la sesión. Controla los marcadores de progreso y la audiencia media por minuto.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 7%
---

# Longitud de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Longitud del contenido**. Ver [Longitud del contenido](/help/reporting/dimensions/content-length.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de duración del contenido es la duración total del contenido en segundos. Es obligatorio para todas las implementaciones de medios de streaming y debe configurarse al inicio de la sesión. La longitud del contenido impulsa varias métricas calculadas por el back-end, incluidos los marcadores de progreso (10/25/50/75/95 %) y la audiencia media por minuto. Si la longitud del contenido no está establecida o no es mayor que cero, esas métricas no se generan. Para las transmisiones en vivo de duración desconocida, use `86400` (24 horas).

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.length` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.length` |
| **Requerido** | Sí |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `length` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase la duración del contenido en segundos como el argumento `length` a `createMediaObject`.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Pase la duración del contenido en segundos como el argumento `length` a `createMediaObject`.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

Establecer `length` dentro de `xdm.mediaCollection.sessionDetails` al llamar a `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `length` dentro de `xdm.mediaCollection.sessionDetails`:

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

Pase la duración del contenido en segundos como tercer argumento a `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,                      // length in seconds
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Pase la duración del contenido en segundos como tercer argumento a `ADBMobile.media.createMediaObject`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Pase la duración del contenido en segundos como tercer argumento a `adb_media_init_mediainfo`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API de recopilación de medios]

Incluir `media.length` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.length": 128
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
