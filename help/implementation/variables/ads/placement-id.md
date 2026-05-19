---
title: ID de colocación
description: Defina el ID de colocación de cada anuncio para habilitar los desgloses por ubicación de anuncio.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 17%

---


# ID de colocación

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **ID de ubicación**. Ver [ID. de ubicación](/help/reporting/dimensions/placement-id.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de ID de ubicación identifica la ubicación de la publicidad (normalmente una ranura o zona definida en la plataforma del servidor de publicidad).

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.placement` |
| **Campo de colección XDM** | [`mediaCollection.advertisingDetails.placementID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.placement` |
| **Requerido** | No |
| **Enviado con** | [Inicio del anuncio](/help/implementation/events/ads/ad-start.md), cierre del anuncio |

## SDK web

Establecer `placementID` dentro de `mediaCollection.advertisingDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        placementID: "placement-12"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase el ID de ubicación como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.PLACEMENT_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Establecer `placementID` dentro de `mediaCollection.advertisingDetails` al llamar a `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "placementID": "placement-12"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `placementID` dentro de `mediaCollection.advertisingDetails`:

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
          "podPosition": 0,
          "placementID": "placement-12"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pasar el identificador de ubicación en el objeto `contextData` mediante `ADB.Media.AdMetadataKeys.PlacementId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.PlacementId] = "placement-12";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API de Media Collection

Incluir `media.ad.placementId` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.placementId": "placement-12"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
