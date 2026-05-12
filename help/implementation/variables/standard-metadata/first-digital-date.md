---
title: Primera fecha digital
description: Establezca la fecha en la que el contenido se emitió por primera vez en una plataforma digital. Adobe recomienda el formato AAAA-MM-DD.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---


# Primera fecha digital

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Primera fecha digital**. Ver [Primera fecha digital](/help/reporting/dimensions/first-digital-date.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La primera variable de fecha digital es la fecha en la que el contenido se emitió por primera vez en cualquier plataforma digital. Se acepta cualquier formato de fecha, pero Adobe recomienda `YYYY-MM-DD` para mantener la coherencia. Use junto con [Primera fecha de emisión](/help/implementation/variables/standard-metadata/first-air-date.md) para comparar el tiempo de lanzamiento digital con la difusión original.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.digitalDate` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Requerido** | No |
| **Enviado con** | Inicio de sesión, cierre de sesión |

## SDK web

Establecer `firstDigitalDate` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase la primera fecha digital como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para establecer `firstDigitalDate` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `firstDigitalDate` dentro de `mediaCollection.sessionDetails`:

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
          "firstDigitalDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pasar la primera fecha digital en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.FirstDigitalDate`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.firstDigitalDate` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
