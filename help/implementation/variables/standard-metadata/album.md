---
title: Álbum
description: Defina el nombre del álbum para el contenido de audio.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 9%

---


# Álbum

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Album**. Ver [Álbum](/help/reporting/dimensions/album.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable album es el nombre del álbum al que pertenece la pista de audio (por ejemplo, `"Pinegrove"`). Utilícelo para resumir la participación en todas las pistas del mismo álbum.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.album` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.album` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `album` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        album: "Pinegrove"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase el álbum como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.AudioMetadataKeys.ALBUM`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Pase el álbum como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.AudioMetadataKeys.ALBUM`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para establecer `album` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "album": "Pinegrove"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `album` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "album": "Pinegrove"
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

Pasar el álbum en el objeto `contextData` mediante `ADB.Media.AudioMetadataKeys.Album`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Album] = "Pinegrove";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.AudioMetadataKeys.ALBUM` para establecer el álbum en la propiedad `StandardMediaMetadata` del objeto multimedia antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "Pinegrove";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_AudioMetadataKeyALBUM` para establecer el álbum en los metadatos estándar del objeto multimedia antes de llamar a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeyALBUM] = "Pinegrove"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API de recopilación de medios]

Incluir `media.album` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.album": "Pinegrove"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
