---
title: Nombre del reproductor del anuncio
description: Defina el nombre del reproductor que procesa los anuncios. El reproductor de anuncios puede diferir del reproductor de contenido principal.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 6%

---


# Nombre del reproductor del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Nombre del reproductor del anuncio**. Ver [Nombre del reproductor del anuncio](/help/reporting/dimensions/ad-player-name.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable del nombre del reproductor del anuncio identifica qué reproductor procesó cada anuncio (por ejemplo, `"Freewheel"`, `"Google IMA"`). El reproductor de anuncios puede diferir del reproductor de contenido principal cuando un servicio de inserción de anuncios del lado del servidor vincula los anuncios. Utilice esta variable para comparar la calidad y la finalización en las pilas de servidores de publicidad.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.playerName` |
| **Campo de colección XDM** | [`xdm.mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.playerName` |
| **Requerido** | Sí |
| **Enviado con** | [Inicio del anuncio](/help/implementation/events/ads/ad-start.md), cierre del anuncio |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `playerName` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Pase el nombre del reproductor de anuncios como clave `MediaConstants.AdMetadataKeys.AD_PLAYER` en el argumento HashMap de metadatos a `trackEvent(AdStart)`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Pase el nombre del reproductor de anuncios como clave `MediaConstants.AdMetadataKeys.AD_PLAYER` en el argumento HashMap de metadatos a `trackEvent(AdStart)`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

Establecer `playerName` dentro de `xdm.mediaCollection.advertisingDetails` al llamar a `sendMediaEvent` para `media.adStart`:

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

>[!TAB API de Media Edge]

Llame al extremo [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `playerName` dentro de `xdm.mediaCollection.advertisingDetails`:

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pase el nombre del reproductor de anuncios en el objeto `contextData` mediante `ADB.Media.AdMetadataKeys.AdPlayer`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Pase el nombre del reproductor de publicidad en el objeto de metadatos de contexto al rastrear el evento de inicio de publicidad:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var metadata = { "a.media.ad.playerName": "Chromecast Player" };
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, metadata);
```

>[!TAB Roku 2.x]

Pase el nombre del reproductor de publicidad en el objeto de datos de contexto al rastrear el evento de inicio de publicidad:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

contextData = { "a.media.ad.playerName": "Roku Player" }
adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo, contextData)
```

>[!TAB API de recopilación de medios]

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

>[!ENDTABS]
