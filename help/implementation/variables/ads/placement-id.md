---
title: ID de colocación
description: Defina el ID de colocación de cada anuncio para habilitar los desgloses por ubicación de anuncio.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 10%
---

# ID de colocación

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **ID de ubicación**. Ver [ID. de ubicación](/help/reporting/dimensions/placement-id.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de ID de ubicación identifica la ubicación de la publicidad (normalmente una ranura o zona definida en la plataforma del servidor de publicidad).

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.placement` |
| **Campo de colección XDM** | [`xdm.mediaCollection.advertisingDetails.placementID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.placement` |
| **Requerido** | No |
| **Enviado con** | [Inicio del anuncio](/help/implementation/events/ads/ad-start.md), cierre del anuncio |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `placementID` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Pase el ID de ubicación como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.PLACEMENT_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Pase el ID de ubicación como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.PLACEMENT_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

Establecer `placementID` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a `sendMediaEvent` para `media.adStart`:

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

>[!TAB API de Media Edge]

Llame al extremo [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `placementID` dentro de `xdm.mediaCollection.advertisingDetails`:

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pasar el identificador de ubicación en el objeto `contextData` mediante `ADB.Media.AdMetadataKeys.PlacementId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.PlacementId] = "placement-12";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Establezca el identificador de ubicación con `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` en el objeto de metadatos de publicidad estándar:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "placement-12";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Establezca el identificador de ubicación con `MEDIA_AdMetadataKeyPLACEMENT_ID` en el objeto de metadatos de publicidad estándar:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyPLACEMENT_ID] = "placement-12"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API de recopilación de medios]

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

Consulte la [referencia de eventos de API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
