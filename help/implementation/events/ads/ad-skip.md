---
title: Omisión de publicidad
description: Señal de que el visualizador ha omitido un anuncio.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---


# Omisión de publicidad

El evento de omisión de anuncio indica que el visor omitió un anuncio antes de que finalizara. Enviarlo cuando el visor seleccione el botón de omisión. Enviar [anuncio completado](ad-complete.md) en su lugar si el anuncio se reproduce hasta su finalización.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de pausa publicitaria](ad-break-start.md), [Inicio de publicidad](ad-start.md)
* **Métrica asociada**: ninguna

>[!IMPORTANT]
>
>Este evento debe estar comprendido entre `adBreakStart` y `adBreakComplete` bookends, incluso cuando se reproduce un solo anuncio. Sin estos bookends, los eventos de anuncio se ignoran y la duración del anuncio se cuenta como la duración del contenido principal.

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

## SDK móvil

Llamar a `trackEvent` con el tipo de evento `AdSkip`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.adSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

## API de Media Edge

Llamar al extremo [adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Llamar a `trackEvent` con el tipo de evento `AdSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

## API de Media Collection

Enviar un POST de `adSkip` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```
