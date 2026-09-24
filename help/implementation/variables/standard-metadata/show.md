---
title: Show
description: Establezca el nombre para mostrar del contenido de vídeo que forma parte de una serie, de modo que los episodios se acumulen en un solo programa del sistema de informes.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 7%
---

# Show

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Mostrar**. Ver [Mostrar](/help/reporting/dimensions/show.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable show es el nombre del programa o serie (por ejemplo, `"Blinding Light"` o `"Coastline Mysteries"`). Configúrelo en cada sesión cuyo contenido pertenezca a una serie, de modo que los episodios de varias temporadas se acumulen en un solo elemento de línea en la dimensión Mostrar. Deje sin configurar el contenido único que no forma parte de una serie.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.show` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.show` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `show` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        show: "Blinding Light"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase el nombre para mostrar como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.SHOW`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Pase el nombre para mostrar como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.SHOW`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para establecer `show` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "show": "Blinding Light"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `show` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "show": "Blinding Light"
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

Pasar el nombre para mostrar en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.Show`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Show] = "Blinding Light";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.SHOW` para establecer el nombre para mostrar en la propiedad `StandardMediaMetadata` del objeto multimedia antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "Blinding Light";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_VideoMetadataKeySHOW` para establecer el nombre para mostrar en los metadatos estándar del objeto de medios antes de llamar a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeySHOW] = "Blinding Light"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API de recopilación de medios]

Incluir `media.show` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.show": "Blinding Light"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
