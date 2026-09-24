---
title: Temporada
description: Defina el número de temporada del contenido episódico para que la participación se pueda desglosar por temporada.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 8%
---

# Temporada

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Season**. Consulte [Temporada](/help/reporting/dimensions/season.md) para ver la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable season es el número de temporada del programa (normalmente un entero de cadena como `"2"`). Configúrelo para el contenido que forma parte de una serie, de modo que la participación se pueda dividir por temporada. Emparejar con [Show](/help/implementation/variables/standard-metadata/show.md) y [Episode](/help/implementation/variables/standard-metadata/episode.md) para obtener un contexto episódico completo.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.season` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.season` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `season` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        season: "2"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase la temporada como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.SEASON`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Pase la temporada como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.SEASON`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para establecer `season` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "season": "2"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `season` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "season": "2"
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

Pasar la temporada en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.Season`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Season] = "2";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.SEASON` para establecer el número de temporada en la propiedad `StandardMediaMetadata` del objeto multimedia antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "2";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_VideoMetadataKeySEASON` para establecer el número de temporada en los metadatos estándar del objeto de medios antes de llamar a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeySEASON] = "2"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API de recopilación de medios]

Incluir `media.season` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.season": "2"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
