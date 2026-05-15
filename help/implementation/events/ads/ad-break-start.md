---
title: Inicio de pausa publicitaria
description: Indicar el comienzo de una pausa publicitaria (una secuencia de uno o más anuncios).
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 13%

---


# Inicio de pausa publicitaria

El evento de inicio de pausa publicitaria indica el comienzo de una pausa publicitaria. Una pausa para anuncios es una secuencia de uno o más anuncios. Cada evento de `adStart`, `adComplete` y `adSkip` debe producirse entre un par de `adBreakStart` y `adBreakComplete`, incluso cuando se reproduce un solo anuncio.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: ninguna

>[!IMPORTANT]
>
>Los eventos de anuncio (`adStart`, `adComplete`, `adSkip`) se omiten sin los bookends `adBreakStart` y `adBreakComplete`. Sin ellos, la duración del anuncio se atribuye a la duración del contenido principal, que afecta a los datos de informes agregados.

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adBreakStart"` y el `advertisingPodDetails` requerido:

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

Pase el nombre, la posición y la hora de inicio de la pausa publicitaria a `createAdBreakObject` y luego llame a `trackEvent`.

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
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.adBreakStart"` y el `advertisingPodDetails` requerido:

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

Llame al extremo [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) con el elemento `advertisingPodDetails` requerido:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingPodDetails": {
          "index": 0,
          "offset": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Pasar el nombre, la posición y la hora de inicio de la pausa publicitaria a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API de Media Collection

Enviar un POST de `adBreakStart` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll",
    "media.ad.podIndex": 1,
    "media.ad.podSecond": 0
  }
}
```
