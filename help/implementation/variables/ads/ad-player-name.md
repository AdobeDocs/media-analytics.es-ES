---
title: Nombre del reproductor del anuncio
description: Defina el nombre del reproductor que procesa los anuncios. El reproductor de anuncios puede diferir del reproductor de contenido principal.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 11%

---


# Nombre del reproductor del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Nombre del reproductor del anuncio**. Ver [Nombre del reproductor del anuncio](/help/reporting/dimensions/ad-player-name.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable del nombre del reproductor del anuncio identifica qué reproductor procesó cada anuncio (por ejemplo, `"Freewheel"`, `"Google IMA"`). El reproductor de anuncios puede diferir del reproductor de contenido principal cuando un servicio de inserción de anuncios del lado del servidor vincula los anuncios. Utilice esta variable para comparar la calidad y la finalización en las pilas de servidores de publicidad.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.playerName` |
| **Campo de colección XDM** | [`mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Requerido** | Sí |
| **Enviado con** | Inicio del anuncio y cierre del anuncio |

## SDK web

Establecer `playerName` dentro de `mediaCollection.advertisingDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase el nombre del reproductor de anuncios como clave `MediaConstants.AdMetadataKeys.AD_PLAYER` en el argumento HashMap de metadatos a `trackEvent(AdStart)`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Establecer `playerName` dentro de `mediaCollection.advertisingDetails` al llamar a `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `playerName` dentro de `mediaCollection.advertisingDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pase el nombre del reproductor de anuncios en el objeto `contextData` mediante `ADB.Media.AdMetadataKeys.AdPlayer`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API de Media Collection

Incluir `media.ad.playerName` en el objeto `params` de su solicitud POST de `adStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
