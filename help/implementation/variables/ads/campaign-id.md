---
title: ID de campaña
description: Establezca el identificador de campaña de cada anuncio para que se pueda acumular la participación por campaña.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 9%
---

# ID de campaña

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **ID de campaña**. Ver [ID de campaña](/help/reporting/dimensions/campaign-id.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable del ID de campaña identifica la campaña de publicidad a la que pertenece el creativo. Cualquier valor de cadena (normalmente un ID de campaña de su plataforma de servidor de publicidad) es aceptable. Utilice la variable para resumir la participación de varios creativos que comparten una campaña.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.campaign` |
| **Campo de colección XDM** | [`xdm.mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.campaign` |
| **Requerido** | No |
| **Enviado con** | [Inicio del anuncio](/help/implementation/events/ads/ad-start.md), cierre del anuncio |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `campaignID` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase el identificador de campaña como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Pase el identificador de campaña como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

Establecer `campaignID` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `campaignID` dentro de `xdm.mediaCollection.advertisingDetails`:

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
          "campaignID": "fall-2024"
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

Pase el identificador de campaña en el objeto `contextData` mediante `ADB.Media.AdMetadataKeys.CampaignId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Establezca el ID de campaña usando `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` en el objeto de metadatos de publicidad estándar:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Establezca el ID de campaña usando `MEDIA_AdMetadataKeyCAMPAIGN_ID` en el objeto de metadatos de publicidad estándar:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCAMPAIGN_ID] = "fall-2024"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API de recopilación de medios]

Incluir `media.ad.campaignId` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
