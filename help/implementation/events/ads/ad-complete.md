---
title: Anuncio completado
description: Indica que se ha terminado de reproducir un anuncio individual.
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
source-wordcount: '182'
ht-degree: 8%
---

# Anuncio completado

El evento de finalización de anuncio indica que se ha terminado de reproducir un anuncio individual. Enviarlo después de que el anuncio se reproduzca hasta su finalización. Si el visor omite el anuncio, envía [Omisión de anuncio](ad-skip.md) en su lugar.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md), [Inicio de pausa publicitaria](ad-break-start.md), [Inicio de publicidad](ad-start.md)
* **Métrica asociada**: [[!UICONTROL El anuncio finaliza]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Este evento debe estar comprendido entre `adBreakStart` y `adBreakComplete` bookends, incluso cuando se reproduce un solo anuncio. Sin estos bookends, los eventos de anuncio se ignoran y la duración del anuncio se cuenta como la duración del contenido principal.

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Llamar a `trackEvent` con el tipo de evento `AdComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Llamar a `trackEvent` con el tipo de evento `AdComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Llamar a `trackEvent` con el tipo de evento `AdComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

Llamar a `trackEvent` con el tipo de evento `AdComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB Roku 2.x]

Llamar a `mediaTrackEvent` con el tipo de evento `MEDIA_AD_COMPLETE`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_COMPLETE)
```

>[!TAB API de recopilación de medios]

Enviar un POST de `adComplete` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
