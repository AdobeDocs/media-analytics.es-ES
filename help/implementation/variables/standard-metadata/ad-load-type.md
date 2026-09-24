---
title: Tipo de carga de anuncio
description: Defina el tipo de carga de publicidad para la sesión de flujo continuo.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%
---

# Tipo de carga de anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Tipo de carga de anuncio**. Consulte [Cargas de publicidad](/help/reporting/dimensions/ad-load-type.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de tipo de carga de anuncio identifica el tipo de anuncio cargado al principio de la sesión. El sistema de entrega de anuncios interno de su organización define este valor, que no se limita a una enumeración estándar. Puede utilizar cualquier cadena que sea significativa para su implementación, como `"linear"`, `"dynamic"` o `"programmatic"`.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.adLoad` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.adLoad` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `adLoad` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`createMediaSession`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/createmediasession):

```javascript
alloy("createMediaSession", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 300,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        adLoad: "linear"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase el tipo de carga de publicidad como clave de metadatos en el argumento del diccionario a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```swift
var videoMetadata: [String: String] = [:]
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

>[!TAB Android]

Pase el tipo de carga de publicidad como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```kotlin
val videoMetadata = HashMap<String, String>()
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(mediaInfo, videoMetadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para establecer `adLoad` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "adLoad": "linear"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `adLoad` dentro de `xdm.mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "adLoad": "linear"
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

Pasar el tipo de carga de anuncio en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.AdLoad`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AdLoad] = "linear";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.AD_LOAD` para establecer el tipo de carga de anuncio en la propiedad `StandardMediaMetadata` del objeto de medios antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 300,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "linear";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_VideoMetadataKeyAD_LOAD` para establecer el tipo de carga de anuncio en los metadatos estándar del objeto de medios antes de llamar a `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyAD_LOAD] = "linear"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API de recopilación de medios]

Incluir `media.adLoad` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.adLoad": "linear"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
