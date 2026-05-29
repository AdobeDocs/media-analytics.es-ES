---
title: Currículos de contenido
description: Marque una sesión que reanude una reproducción interrumpida anteriormente para que el back-end cuente un evento de reanudación de contenido.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 7%

---


# Currículos de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Reanudación del contenido**. Ver [[!UICONTROL currículos de contenido]](/help/reporting/metrics/content-resumes.md) para la métrica de informes correspondiente.*

>[!ENDSHADEBOX]

La variable de reanudación de contenido marca una sesión que reanuda una reproducción interrumpida previamente. Configúrelo en `media.sessionStart` para que el backend cuente un evento de [[!UICONTROL contenido reanuda]](/help/reporting/metrics/content-resumes.md) para la sesión y lo excluya de los recuentos de nuevo flujo. Para implementaciones directas de API y API de Edge, el cliente es responsable de detectar las sesiones reanudadas (por ejemplo, después de un búfer, una pausa o una detención que supere los 30 minutos) y de establecer este indicador en consecuencia.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.resume` |
| **Campo de colección XDM** | [`xdm.mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-collection) |
| **rasgo de Audience Manager** | N/A |
| **Requerido** | No |
| **Enviado con** | [Inicio de sesión](/help/implementation/events/session/session-start.md) |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `hasResume` en `true` dentro de `xdm.mediaCollection.sessionDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) para la sesión reanudada:

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
        hasResume: true
      },
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

Pase el indicador de reanudación como parte del paquete de configuración opcional del objeto de medios en `trackSessionStart`. Utilice la clave `MediaConstants.MediaObjectKey.RESUMED`.

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Pase el indicador de reanudación como parte del paquete de configuración opcional del objeto de medios en `trackSessionStart`. Utilice la clave `MediaConstants.MediaObjectKey.RESUMED`.

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

Establecer `hasResume` en `true` dentro de `xdm.mediaCollection.sessionDetails` al llamar a `createMediaSession` para la sesión reanudada:

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
                "hasResume": true
            },
            "playhead": 60
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `hasResume` establecido en `true` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Establezca la clave `RESUMED` en el objeto de información multimedia antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Establezca `MediaResumed` en el objeto de información multimedia antes de llamar a `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API de recopilación de medios]

Incluir `media.resume` en el objeto `params` de su solicitud POST de `sessionStart`:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

Consulte la [referencia de sesiones de la API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
