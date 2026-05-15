---
title: Hora de inicio de la pausa publicitaria
description: Establezca el tiempo de inicio (desplazamiento) de la pausa publicitaria dentro del contenido, en segundos.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 12%

---


# Hora de inicio de la pausa publicitaria

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Hora de inicio de las pausas publicitarias**. Ver [Posición de la secuencia](/help/reporting/dimensions/pod-position.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de tiempo de inicio de la pausa publicitaria es el desplazamiento de la pausa publicitaria dentro del contenido, medido en segundos. Para una emisión previa el valor es `0`; para una emisión intermedia, el valor es la posición del cabezal de reproducción en la que comienza la pausa.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.podSecond` |
| **Campo de colección XDM** | [`mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.podSecond` |
| **Requerido** | Sí |
| **Enviado con** | [Inicio de la pausa publicitaria](/help/implementation/events/ads/ad-break-start.md), cierre del anuncio |

## SDK web

Establecer `offset` dentro de `mediaCollection.advertisingPodDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvil

Pase el tiempo de inicio en segundos como tercer argumento a `createAdBreakObject`.

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Establecer `offset` dentro de `mediaCollection.advertisingPodDetails` al llamar a `sendMediaEvent` para `media.adBreakStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

## API de Media Edge

Llame al extremo [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) con `offset` dentro de `mediaCollection.advertisingPodDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

Pasar la hora de inicio como tercer argumento a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API de Media Collection

Incluir `media.ad.podSecond` en el objeto `params` de su solicitud POST de `adBreakStart`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obtener la estructura de solicitudes completa.
