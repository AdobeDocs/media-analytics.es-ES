---
title: Género
description: Establezca el género de contenido como una cadena delimitada por comas. El contenido de varios géneros se divide en elementos de línea en los informes.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 12%

---


# Género

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Genre**. Ver [Género](/help/reporting/dimensions/genre.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable genre es el género de contenido definido por el productor (por ejemplo, `"Drama"`, `"Comedy"` o `"Drama,Action"`). Delimite varios valores con comas cuando el contenido se ajuste a más de un género. En los informes, la variable de lista divide cada valor en un elemento de línea independiente, y cada elemento de línea recibe el mismo peso de métrica.

>[!NOTE]
>
>En la canalización de informes, el valor de género se expone como `mediaReporting.sessionDetails.genreList` (un campo de lista). La ruta de acceso `mediaReporting.sessionDetails.genre` más antigua sigue funcionando, pero se recomienda `genreList`.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.genre` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.genre` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## SDK web

Establecer `genre` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase la cadena de género como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.GENRE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para establecer `genre` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `genre` dentro de `mediaCollection.sessionDetails`:

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
          "genre": "Drama,Action"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pasar el género en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.Genre`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.genre` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
