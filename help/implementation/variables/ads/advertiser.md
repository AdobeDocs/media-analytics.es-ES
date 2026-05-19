---
title: Anunciante
description: Establece la compañía o marca que aparece en cada anuncio.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 16%

---


# Anunciante

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Anunciante**. Consulte [Anunciante](/help/reporting/dimensions/advertiser.md) para ver la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable del anunciante es la compañía o marca que aparece en el anuncio (por ejemplo, `"Ford"` o `"Coca-Cola"`). Utilice la variable para dividir la participación y la finalización por anunciante.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.advertiser` |
| **Campo de colección XDM** | [`mediaCollection.advertisingDetails.advertiser`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.advertiser` |
| **Requerido** | No |
| **Enviado con** | [Inicio del anuncio](/help/implementation/events/ads/ad-start.md), cierre del anuncio |

## SDK web

Establecer `advertiser` dentro de `mediaCollection.advertisingDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        advertiser: "Ford"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase el anunciante como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.ADVERTISER`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Establecer `advertiser` dentro de `mediaCollection.advertisingDetails` al llamar a `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "advertiser": "Ford"
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `advertiser` dentro de `mediaCollection.advertisingDetails`:

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
          "advertiser": "Ford"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pase el anunciante en el objeto `contextData` mediante `ADB.Media.AdMetadataKeys.Advertiser`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.Advertiser] = "Ford";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API de Media Collection

Incluir `media.ad.advertiser` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.advertiser": "Ford"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
