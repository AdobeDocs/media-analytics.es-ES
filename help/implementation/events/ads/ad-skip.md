---
title: Omisión de publicidad
description: Señal de que el visualizador ha omitido un anuncio.
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
source-wordcount: '185'
ht-degree: 8%
---

# Omisión de publicidad

El evento de omisión de anuncio indica que el visor omitió un anuncio antes de que finalizara. Enviarlo cuando el visor seleccione el botón de omisión. Enviar [anuncio completado](ad-complete.md) en su lugar si el anuncio se reproduce hasta su finalización.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de pausa publicitaria](ad-break-start.md), [Inicio de publicidad](ad-start.md)
* **Métrica asociada**: ninguna

>[!IMPORTANT]
>
>Este evento debe estar comprendido entre `adBreakStart` y `adBreakComplete` bookends, incluso cuando se reproduce un solo anuncio. Sin estos bookends, los eventos de anuncio se ignoran y la duración del anuncio se cuenta como la duración del contenido principal.

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Llamar a `trackEvent` con el tipo de evento `AdSkip`.

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Llamar a `trackEvent` con el tipo de evento `AdSkip`.

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Llamar a `trackEvent` con el tipo de evento `AdSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

>[!TAB Chromecast]

Llamar a `trackEvent` con el tipo de evento `AdSkip`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdSkip);
```

>[!TAB Roku 2.x]

Llamar a `mediaTrackEvent` con el tipo de evento `MEDIA_AD_SKIP`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_SKIP)
```

>[!TAB API de recopilación de medios]

Enviar un POST de `adSkip` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```

>[!ENDTABS]
