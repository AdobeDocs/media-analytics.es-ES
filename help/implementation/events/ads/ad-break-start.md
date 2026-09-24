---
title: Inicio de pausa publicitaria
description: Indicar el comienzo de una pausa publicitaria (una secuencia de uno o más anuncios).
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%
---

# Inicio de pausa publicitaria

El evento de inicio de pausa publicitaria indica el comienzo de una pausa publicitaria. Una pausa para anuncios es una secuencia de uno o más anuncios. Cada evento de `adStart`, `adComplete` y `adSkip` debe producirse entre un par de `adBreakStart` y `adBreakComplete`, incluso cuando se reproduce un solo anuncio.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: ninguna

>[!IMPORTANT]
>
>Los eventos de anuncio (`adStart`, `adComplete`, `adSkip`) se omiten sin los bookends `adBreakStart` y `adBreakComplete`. Sin ellos, la duración del anuncio se atribuye a la duración del contenido principal, que afecta a los datos de informes agregados.

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Pase el nombre, la posición y la hora de inicio de la pausa publicitaria a `createAdBreakObject` y luego llame a `trackEvent`.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Pase el nombre, la posición y la hora de inicio de la pausa publicitaria a `createAdBreakObject` y luego llame a `trackEvent`.

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pasar el nombre, la posición y la hora de inicio de la pausa publicitaria a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

Pasar el nombre, la posición y la hora de inicio de la pausa publicitaria a `ADBMobile.media.createAdBreakObject`:

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

Cree un objeto de pausa publicitaria con `adb_media_init_adbreakinfo` y luego realice un seguimiento del evento. Observe el orden del parámetro Roku: `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("pre-roll", 0.0, 1)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB API de recopilación de medios]

Enviar un POST de `adBreakStart` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

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

>[!ENDTABS]
