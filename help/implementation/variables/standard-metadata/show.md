---
title: Show
description: Establezca el nombre para mostrar del contenido de vídeo que forma parte de una serie, de modo que los episodios se acumulen en un solo programa del sistema de informes.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 13%

---


# Show

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Mostrar**. Ver [Mostrar](/help/reporting/dimensions/show.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable show es el nombre del programa o serie (por ejemplo, `"Blinding Light"` o `"Coastline Mysteries"`). Configúrelo en cada sesión cuyo contenido pertenezca a una serie, de modo que los episodios de varias temporadas se acumulen en un solo elemento de línea en la dimensión Mostrar. Deje sin configurar el contenido único que no forma parte de una serie.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.show` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.show`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Requerido** | No |
| **Enviado con** | Inicio de sesión, cierre de sesión |

## SDK web

Establecer `show` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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

## SDK móvil

Pase el nombre para mostrar como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.SHOW`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `show` dentro de `mediaCollection.sessionDetails`:

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

## Media SDK

Pasar el nombre para mostrar en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.Show`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Show] = "Blinding Light";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

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

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
