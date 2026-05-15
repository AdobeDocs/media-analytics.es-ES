---
title: Anuncio completado
description: Indica que se ha terminado de reproducir un anuncio individual.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 15%

---


# Anuncio completado

El evento de finalización de anuncio indica que se ha terminado de reproducir un anuncio individual. Enviarlo después de que el anuncio se reproduzca hasta su finalización. Si el visor omite el anuncio, envía [Omisión de anuncio](ad-skip.md) en su lugar.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de pausa publicitaria](ad-break-start.md), [Inicio de publicidad](ad-start.md)
* **Métrica asociada**: [El anuncio finaliza](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Este evento debe estar comprendido entre `adBreakStart` y `adBreakComplete` bookends, incluso cuando se reproduce un solo anuncio. Sin estos bookends, los eventos de anuncio se ignoran y la duración del anuncio se cuenta como la duración del contenido principal.

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

## SDK móvil

Llamar a `trackEvent` con el tipo de evento `AdComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.adComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

## API de Media Edge

Llame al extremo [adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Llamar a `trackEvent` con el tipo de evento `AdComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

## API de Media Collection

Enviar un POST de `adComplete` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```
