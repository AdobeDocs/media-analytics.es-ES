---
title: Fin de sesión
description: Cierre inmediatamente una sesión multimedia cuando el usuario abandone el contenido.
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 11%

---


# Fin de sesión

El evento de fin de sesión cierra de forma inmediata e irreversible una sesión de seguimiento de contenido. El final de la sesión es un cierre forzoso: una vez enviada, la sesión finaliza y no se pueden rastrear más eventos debajo de ella. Utilice Finalizar sesión únicamente cuando esté seguro de que no se producirán eventos adicionales, como cuando se destruya el reproductor o se descargue la página. En la mayoría de los casos, es más seguro permitir que la sesión caduque de forma natural, en lugar de arriesgarse a interrumpir eventos que podrían llegar. Si el visor termina el contenido, llama a [Sesión completa](session-complete.md) en su lugar.

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
