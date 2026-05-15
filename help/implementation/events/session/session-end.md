---
title: Fin de sesión
description: Cierre inmediatamente una sesión multimedia cuando el usuario abandone el contenido.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# Fin de sesión

El evento de fin de sesión cierra inmediatamente una sesión de seguimiento de contenido. Utilícelo cuando el visor abandone el contenido antes de llegar al final y no desee que se rastreen los eventos subsiguientes en la misma sesión. Si el visor termina el contenido, llama a [Sesión completa](session-complete.md) en su lugar.

Sin un final de sesión explícito, una sesión se cierra automáticamente tras 10 minutos sin eventos o 30 minutos sin movimiento del cabezal de reproducción.

* **Requisitos previos**: [Inicio de sesión](session-start.md)
* **Métrica asociada**: ninguna

## SDK web

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.sessionEnd"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## SDK móvil

Invoque `trackSessionEnd` cuando el visor cierre el reproductor o salga del mismo.

**iOS (Swift)**

```swift
tracker.trackSessionEnd()
```

**Android (Kotlin)**

```kotlin
tracker.trackSessionEnd()
```

## Roku (BrightScript)

Llamar a `sendMediaEvent` con `eventType: "media.sessionEnd"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## API de Media Edge

Llame al extremo [sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Invoque `trackSessionEnd` cuando el visor cierre el reproductor o salga:

```javascript
tracker.trackSessionEnd();
```

## API de Media Collection

Enviar un POST de `sessionEnd` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
