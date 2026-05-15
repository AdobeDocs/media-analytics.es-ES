---
title: Nombre de pausa publicitaria
description: Establezca un nombre descriptivo para el salto de anuncio principal.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 11%

---


# Nombre de pausa publicitaria

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Nombre del salto de anuncio**. Ver [Nombre de secuencia](/help/reporting/dimensions/pod-name.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable del nombre de la pausa publicitaria es el nombre descriptivo de la pausa publicitaria (por ejemplo, `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). El valor se establece en el objeto de pausa publicitaria, no en anuncios individuales.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.podFriendlyName` |
| **Campo de colección XDM** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.podFriendlyName` |
| **Requerido** | Sí (Mobile SDK); No (Edge, API de recopilación de medios) |
| **Enviado con** | [Inicio de la pausa publicitaria](/help/implementation/events/ads/ad-break-start.md), cierre del anuncio |

## SDK web

Establecer `friendlyName` dentro de `mediaCollection.advertisingPodDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) para `media.adBreakStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvil

Pase el nombre de la pausa publicitaria como el primer argumento (`name`) a `createAdBreakObject` y, a continuación, realice un seguimiento del evento de inicio de la pausa publicitaria antes del evento de inicio de la misma.

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Establecer `friendlyName` dentro de `mediaCollection.advertisingPodDetails` al llamar a `sendMediaEvent` para `media.adBreakStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llame al extremo [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) con `friendlyName` dentro de `mediaCollection.advertisingPodDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Pase el nombre de la pausa publicitaria como primer argumento a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API de Media Collection

Incluir `media.ad.podFriendlyName` en el objeto `params` de su solicitud POST de `adBreakStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
