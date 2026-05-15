---
title: Indicador de medios descargados
description: Marque una sesión como reproducida sin conexión descargada para que se informe separadamente de las sesiones retransmitidas.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 10%

---


# Indicador de medios descargados

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Indicador de medios descargados**. Ver [Medios descargados](/help/reporting/dimensions/media-downloaded-flag.md) para la dimensión de informes correspondiente.*

>[!ENDSHADEBOX]

El indicador de medios descargados indica que una sesión es una reproducción de contenido sin conexión previamente descargado en lugar de un flujo en directo desde Internet. Configúrelo al inicializar el rastreador (Mobile SDK) o inclúyalo en la carga `sessionStart` (API de recopilación de medios/Edge). Utilice este indicador para separar la reproducción sin conexión de las sesiones transmitidas en los informes.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.downloaded` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.downloaded` |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## SDK web

Establecer `isDownloaded` en `true` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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
        streamType: "video",
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

## SDK móvil

Establezca la marca de contenido descargado en la configuración del rastreador al crear el rastreador con `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`.

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Kotlin)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

Establecer `isDownloaded` en `true` dentro de `mediaCollection.sessionDetails` al llamar a `createMediaSession`:

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
                "streamType": "video",
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [downloaded](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded) después de que el dispositivo vuelva a estar en línea, agrupando toda la sesión sin conexión dentro de `mediaDownloadedEvents`. Adobe establece automáticamente `isDownloaded` en `true` y asigna un ID de sesión; no incluya ninguno de los dos en la carga útil.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
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
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

## Media SDK

Establezca `downloadedContent` en `ADB.MediaConfig` antes de crear el rastreador:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API de Media Collection

Incluir `media.downloaded` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
