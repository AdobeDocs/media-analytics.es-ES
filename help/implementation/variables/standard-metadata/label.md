---
title: Etiqueta
description: Establezca la discográfica que liberó el contenido de audio.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 16%

---


# Etiqueta

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Label**. Ver [Etiqueta](/help/reporting/dimensions/label.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable label es el nombre de la etiqueta de registro que publicó el contenido de audio (por ejemplo, `"Capitol Records"`). Utilícelo para comparar la participación entre etiquetas en un catálogo de música o podcast.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.label` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.label`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Requerido** | No |
| **Enviado con** | Inicio de sesión, cierre de sesión |

## SDK web

Establecer `label` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        label: "Capitol Records"
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase la etiqueta como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.AudioMetadataKeys.LABEL`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para establecer `label` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "label": "Capitol Records"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `label` dentro de `mediaCollection.sessionDetails`:

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
          "label": "Capitol Records"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pasar la etiqueta en el objeto `contextData` mediante `ADB.Media.AudioMetadataKeys.Label`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Label] = "Capitol Records";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.label` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.label": "Capitol Records"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
