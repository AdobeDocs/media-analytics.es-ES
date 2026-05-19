---
title: Formato de flujo
description: Configure el formato de flujo para identificar el nivel de calidad (HD, SD u otra etiqueta que utilice su canalización de envíos).
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# Formato de flujo

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Formato de flujo**. Consulte [Formato de emisión](/help/reporting/dimensions/stream-format.md) para la dimensión de informes correspondiente.*

>[!ENDSHADEBOX]

La variable de formato de secuencia identifica el nivel de calidad de la secuencia (normalmente `"HD"` o `"SD"`, pero se acepta cualquier cadena). Configúrelo cuando desee dividir la participación, la finalización o la calidad en niveles de calidad de entrega.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.format` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.streamFormat`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.format` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## SDK web

Establecer `streamFormat` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        streamFormat: "HD"
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase el formato de flujo como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.STREAM_FORMAT`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para establecer `streamFormat` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "streamFormat": "HD"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `streamFormat` dentro de `mediaCollection.sessionDetails`:

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
          "streamFormat": "HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pasar el formato de secuencia en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.StreamFormat`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.StreamFormat] = "HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.streamFormat` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamFormat": "HD"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
