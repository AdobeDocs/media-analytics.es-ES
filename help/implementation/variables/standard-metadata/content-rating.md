---
title: Calificación de contenido
description: Defina la clasificación de contenido según las pautas de clasificación parental de TV o su sistema de clasificación regional.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%
---

# Calificación de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Clasificación del contenido**. Ver [Clasificación del contenido](/help/reporting/dimensions/content-rating.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de clasificación de contenido es la clasificación de audiencia definida por las pautas de clasificación parental de TV (`"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`) o cualquier sistema de clasificación regional que utilice. Utilícela para comparar la participación y la carga de anuncios en los distintos niveles de clasificación.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.rating` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.rating`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.rating` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `rating` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        rating: "TVPG"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase la clasificación como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.RATING`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Pase la clasificación como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.RATING`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para establecer `rating` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "rating": "TVPG"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `rating` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "rating": "TVPG"
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

Pasar la clasificación en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.Rating`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Rating] = "TVPG";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.RATING` para establecer la clasificación de contenido en la propiedad `StandardMediaMetadata` del objeto multimedia antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "TVPG";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_VideoMetadataKeyRATING` para establecer la clasificación de contenido en los metadatos estándar del objeto de medios antes de llamar a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyRATING] = "TVPG"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API de recopilación de medios]

Incluir `media.rating` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.rating": "TVPG"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
