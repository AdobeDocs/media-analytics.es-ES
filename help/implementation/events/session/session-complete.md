---
title: Sesión completa
description: Indica que el visualizador ha llegado al final del contenido principal.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 16%

---


# Sesión completa

El evento de sesión completa indica que el visor ha llegado al final del contenido principal. No cierra inmediatamente la sesión; la sesión permanece abierta hasta que caduca de forma natural. Si desea cerrar inmediatamente la sesión, llame a [Fin de sesión](session-end.md) en su lugar.

* **Requisitos previos**: [Inicio de sesión](session-start.md)
* **Métrica asociada**: [El contenido finaliza](/help/reporting/metrics/content-completes.md)

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.sessionComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

## SDK móvil

Invoque `trackComplete` cuando el reproductor multimedia llegue al final del contenido.

**iOS (Swift)**

```swift
tracker.trackComplete()
```

**Android (Kotlin)**

```kotlin
tracker.trackComplete()
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.sessionComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Invoque `trackComplete` cuando el reproductor multimedia llegue al final del contenido:

```javascript
tracker.trackComplete();
```

## API de Media Collection

Enviar un POST de `sessionComplete` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```
