---
title: Ping
description: Envíe un latido para mantener la sesión de contenido activa y rastrear el progreso de reproducción a intervalos regulares.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Ping

El evento de ping es un latido que mantiene la sesión activa y rastrea el progreso de reproducción. Enviarlo con un temporizador durante toda la reproducción.

* **Contenido principal**: primer ping 10 segundos después de iniciarse la reproducción y, a continuación, cada 10 segundos
* **Contenido de anuncio**: cada 1 segundo durante el seguimiento de anuncios

No incluya un objeto `params` en el cuerpo de la solicitud de ping.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: ninguna

## SDK web

Programar una llamada recurrente de `sendEvent` con `eventType: "media.ping"`. Actualizar `playhead` a la posición de reproducción actual en cada llamada:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

## SDK móvil

Mobile SDK envía eventos de ping automáticamente. No se requiere una llamada explícita.

## Roku (BrightScript)

Programar una llamada recurrente de `sendMediaEvent` con `eventType: "media.ping"`. Actualizar `playhead` a la posición de reproducción actual en cada llamada:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

## API de Media Edge

Llame al extremo [ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/) en un temporizador. Adobe recomienda el primer ping 10 segundos después del inicio de la reproducción principal, cada 10 segundos después y cada 1 segundo durante el seguimiento de anuncios:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Media SDK envía eventos de ping automáticamente. No se requiere una llamada explícita.

## API de Media Collection

Envíe una publicación de `ping` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) en un temporizador. No incluya un objeto `params`:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```
