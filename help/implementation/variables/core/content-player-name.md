---
title: Nombre del reproductor de contenido
description: Configure el nombre del reproductor para identificar qué reproductor procesó el contenido.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 11%

---


# Nombre del reproductor de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Nombre del reproductor de contenido**. Ver [Nombre del reproductor de contenido](/help/reporting/dimensions/content-player-name.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de nombre del reproductor de contenido identifica qué reproductor procesó el contenido (por ejemplo, `HTML5 Player`, `Brightcove` o `Roku Player`). Es obligatorio para todas las implementaciones de medios de streaming y debe configurarse al inicio de la sesión. El valor se utiliza en la dimensión Nombre del reproductor de contenido para comparar la participación y la calidad entre reproductores de la misma propiedad.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.playerName` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Requerido** | Sí |
| **Enviado con** | Inicio de sesión, cierre de sesión |

## SDK web

Establecer `playerName` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Defina el nombre del reproductor mediante la configuración del rastreador al crear el rastreador con `MediaConstants.TrackerConfig.PLAYER_NAME`. El nombre del reproductor no forma parte del objeto multimedia.

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Kotlin)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

Establecer `playerName` dentro de `mediaCollection.sessionDetails` al llamar a `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `playerName` dentro de `mediaCollection.sessionDetails`:

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
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Establezca el nombre del reproductor en `ADB.MediaConfig` antes de crear el rastreador:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API de Media Collection

Incluir `media.playerName` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
