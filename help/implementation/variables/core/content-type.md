---
title: Tipo de contenido
description: Establezca el tipo de contenido para identificar el formato de la emisión (VOD, en directo, lineal, podcast, canción, etc.).
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 10%

---


# Tipo de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Tipo de contenido**. Ver [Tipo de contenido](/help/reporting/dimensions/content-type.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de tipo de contenido identifica el formato del flujo (por ejemplo, VOD, Live o Linear para vídeo, podcast o audiolibro para audio). Es obligatorio para todas las implementaciones de medios de streaming y debe configurarse al inicio de la sesión. Los valores definidos por Adobe rellenan los segmentos y los informes de Tipo de contenido integrado. Las cadenas personalizadas también se aceptan, pero no coinciden con los segmentos integrados. Si no se establece, el valor predeterminado es `missing_content_type`.

Valores recomendados:

* **Vídeo:** `vod`, `live`, `linear`, `ugc`, `dvod`
* **Audio:** `song`, `podcast`, `audiobook`, `radio`

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.contentType` |
| **Campo de colección XDM** | [`mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Requerido** | Sí |
| **Enviado con** | Inicio de sesión, cierre de sesión |

## SDK web

Establecer `contentType` dentro de `mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Pase la constante de tipo de contenido como el argumento `streamType` a `createMediaObject`. Use `MediaConstants.StreamType.*` valores como `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Nota: en el SDK móvil, el argumento `streamType` controla el tipo de contenido. La variable Tipo de flujo (audio vs. vídeo) es el argumento `mediaType` independiente.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Establecer `contentType` dentro de `mediaCollection.sessionDetails` al llamar a `createMediaSession`:

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

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `contentType` dentro de `mediaCollection.sessionDetails`:

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

Pase una constante `ADB.Media.StreamType.*` como cuarto argumento a `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## API de Media Collection

Incluir `media.contentType` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.
