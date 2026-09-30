---
title: Pausa publicitaria completa
description: Señal de que todos los anuncios de una pausa publicitaria han finalizado.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%
---

# Pausa publicitaria completa

El evento de finalización de una pausa publicitaria indica que todos los anuncios de una pausa publicitaria han finalizado (tanto completados como omitidos). Cierra la pausa publicitaria abierta por [inicio de la pausa publicitaria](ad-break-start.md).

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de pausa publicitaria](ad-break-start.md)
* **Métrica asociada**: ninguna

>[!IMPORTANT]
>
>Cada `adBreakStart` debe tener un(a) `adBreakComplete` coincidente. Sin el bookend de cierre, los eventos de publicidad se ignoran y la duración de la publicidad se atribuye al contenido principal.

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Llamar a `trackEvent` con el tipo de evento `AdBreakComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Llamar a `trackEvent` con el tipo de evento `AdBreakComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Llamar a `trackEvent` con el tipo de evento `AdBreakComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

Llamar a `trackEvent` con el tipo de evento `AdBreakComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB Roku 2.x]

Llamar a `mediaTrackEvent` con el tipo de evento `MEDIA_AD_BREAK_COMPLETE`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_COMPLETE)
```

>[!TAB API de recopilación de medios]

Enviar un POST de `adBreakComplete` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
