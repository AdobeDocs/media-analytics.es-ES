---
title: Parte del día
description: Establezca el período de hora del día (mañana, tarde, horario de máxima audiencia, noche tardía) cuando se emite o reproduce el contenido.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 13%

---


# Parte del día

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Parte del día**. Ver [Parte del día](/help/reporting/dimensions/day-part.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de la parte del día es el período de tiempo del día en el que se emitió o reprodujo el contenido (por ejemplo, `"Morning"`, `"Afternoon"`, `"Primetime"` o `"Late Night"`). Se acepta cualquier cadena. Utilícelo para comparar la participación en varias partes del día independientemente de la zona horaria local del visualizador.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.dayPart` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.dayPart`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Requerido** | No |
| **Enviado con** | Inicio de sesión, cierre de sesión |

## SDK web

Establecer `dayPart` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        dayPart: "Primetime"
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase la parte del día como clave de metadatos en el argumento HashMap a `trackSessionStart`. Utilice `MediaConstants.VideoMetadataKeys.DAY_PART`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para establecer `dayPart` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "dayPart": "Primetime"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `dayPart` dentro de `mediaCollection.sessionDetails`:

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
          "dayPart": "Primetime"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pasar la parte del día en el objeto `contextData` mediante `ADB.Media.VideoMetadataKeys.DayPart`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.DayPart] = "Primetime";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.dayPart` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.dayPart": "Primetime"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
