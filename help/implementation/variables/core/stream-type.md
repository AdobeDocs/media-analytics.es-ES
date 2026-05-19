---
title: Tipo de emisión
description: Establezca el tipo de flujo para identificar si un flujo de medios es contenido de audio o vídeo.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 10%

---


# Tipo de emisión

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Tipo de flujo**. Consulte [Tipo de emisión](/help/reporting/dimensions/stream-type.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de tipo de flujo identifica si un flujo de medios es contenido de audio o vídeo. Es obligatorio para todas las implementaciones de medios de streaming y debe configurarse al principio de cada sesión de medios.

Configurar el tipo de flujo correctamente es fundamental para la creación de informes de medios de streaming. Habilita los segmentos integrados de **Tipo de emisión de medio** en Adobe Analytics (todos los medios, solo audio y solo vídeo) y genera informes de audio y vídeo independientes en Customer Journey Analytics. También garantiza que los datos de sesión se clasifiquen correctamente en toda la canalización de análisis de medios. Las sesiones con un tipo de flujo no establecido o no válido se pueden desagrupar o clasificar de forma incorrecta en los informes descendentes.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.streamType` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.streamType` |
| **Requerido** | Sí |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md), cierre de sesión |

## SDK web

Establecer `streamType` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
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

Pase `Media.MediaType.Video` o `Media.MediaType.Audio` como el argumento `mediaType` a `createMediaObject`. Tenga en cuenta que el argumento `streamType` de `createMediaObject` controla la variable de tipo Content (VOD, Live, etc.), no esta variable.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Establecer `streamType` dentro de `mediaCollection.sessionDetails` al llamar a `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
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

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `streamType` dentro de `mediaCollection.sessionDetails`:

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
          "streamType": "video"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pase `ADB.Media.MediaType.Video` o `ADB.Media.MediaType.Audio` como el quinto argumento a `Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.streamType` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener toda la estructura de solicitudes y todos los campos obligatorios.
