---
title: Red
description: Configure el nombre de la red o canal de difusión.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 9%
---

# Red

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Red**. Ver [Red](/help/reporting/dimensions/network.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de red es el nombre de canal o red de difusión (por ejemplo, `"Fox"`, `"ESPN"` o `"HBO"`). Utilícelo para comparar la participación en redes dentro de la misma propiedad de flujo continuo.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.network` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.network`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.network` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `network` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        network: "ESPN"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase el nombre de red como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.NETWORK`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.NETWORK] = "ESPN"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Pase el nombre de red como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.NETWORK`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.NETWORK] = "ESPN"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para establecer `network` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "network": "ESPN"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `network` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "channel": "Sports",
          "network": "ESPN"
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

Pasar la red en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.Network`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Network] = "ESPN";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.NETWORK` para establecer el nombre de red en la propiedad `StandardMediaMetadata` del objeto multimedia antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "ESPN";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_VideoMetadataKeyNETWORK` para establecer el nombre de red en los metadatos estándar del objeto de medios antes de llamar a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyNETWORK] = "ESPN"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API de recopilación de medios]

Incluir `media.network` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.network": "ESPN"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
