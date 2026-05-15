---
title: Pausa publicitaria completa
description: Señal de que todos los anuncios de una pausa publicitaria han finalizado.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 16%

---


# Pausa publicitaria completa

El evento de finalización de una pausa publicitaria indica que todos los anuncios de una pausa publicitaria han finalizado (tanto completados como omitidos). Cierra la pausa publicitaria abierta por [inicio de la pausa publicitaria](ad-break-start.md).

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de pausa publicitaria](ad-break-start.md)
* **Métrica asociada**: ninguna

>[!IMPORTANT]
>
>Cada `adBreakStart` debe tener un(a) `adBreakComplete` coincidente. Sin el bookend de cierre, los eventos de publicidad se ignoran y la duración de la publicidad se atribuye al contenido principal.

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adBreakComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvil

Llamar a `trackEvent` con el tipo de evento `AdBreakComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.adBreakComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## API de Media Edge

Llamar al extremo [adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Llamar a `trackEvent` con el tipo de evento `AdBreakComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

## API de Media Collection

Enviar un POST de `adBreakComplete` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```
