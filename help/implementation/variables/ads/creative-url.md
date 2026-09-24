---
title: URL del anuncio
description: Establezca la dirección URL del creador de la publicidad para cada anuncio.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 9%
---

# URL del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **URL de Creative**. Ver [URL de Creative](/help/reporting/dimensions/creative-url.md) para la dimensión de informes correspondiente.*

>[!ENDSHADEBOX]

La variable URL creativa es la dirección URL del creador de la publicidad. Utilice la variable para rastrear la ubicación de los recursos de cada creativo cuando la propia URL sea significativa para el análisis (por ejemplo, distinguir rutas de CDN o versiones creativas).

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.creativeURL` |
| **Campo de colección XDM** | [`xdm.mediaCollection.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.creativeURL` |
| **Requerido** | No |
| **Enviado con** | [Inicio del anuncio](/help/implementation/events/ads/ad-start.md), cierre del anuncio |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `creativeURL` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeURL: "https://cdn.example.com/ads/creative-987.mp4"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Pase la dirección URL de creatividad como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.CREATIVE_URL`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Pase la dirección URL de creatividad como clave de metadatos en el argumento HashMap a `trackEvent(AdStart)`. Utilice `MediaConstants.AdMetadataKeys.CREATIVE_URL`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

Establecer `creativeURL` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `creativeURL` dentro de `xdm.mediaCollection.advertisingDetails`:

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
          "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
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

Pase la dirección URL de creatividad en el objeto `contextData` mediante `ADB.Media.AdMetadataKeys.CreativeUrl`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeUrl] = "https://cdn.example.com/ads/creative-987.mp4";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Establezca la URL creativa con `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` en el objeto de metadatos de publicidad estándar:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Establezca la URL creativa con `MEDIA_AdMetadataKeyCREATIVE_URL` en el objeto de metadatos de publicidad estándar:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API de recopilación de medios]

Incluir `media.ad.creativeURL` en el objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
