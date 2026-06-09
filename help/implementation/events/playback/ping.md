---
title: Ping
description: Envíe un latido para mantener la sesión de contenido activa y rastrear el progreso de reproducción a intervalos regulares.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# Ping

El evento de ping es un latido que mantiene la sesión activa y rastrea el progreso de reproducción. Enviarlo con un temporizador durante toda la reproducción. En los SDK móviles, los pings se envían automáticamente; en todas las demás plataformas deben enviarse manualmente en el intervalo especificado.

* **Contenido principal**: primer ping 10 segundos después de iniciarse la reproducción y, a continuación, cada 10 segundos
* **Contenido de anuncio**: cada 1 segundo durante el seguimiento de anuncios

No incluya un objeto `params` en el cuerpo de la solicitud de ping.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: ninguna

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Mobile SDK envía eventos de ping automáticamente. No se requiere una llamada explícita.

>[!TAB Android]

Mobile SDK envía eventos de ping automáticamente. No se requiere una llamada explícita.

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK envía eventos de ping automáticamente. No se requiere una llamada explícita.

>[!TAB Chromecast]

Chromecast SDK envía eventos de ping automáticamente. No se requiere una llamada explícita.

>[!TAB Roku 2.x]

Media SDK envía eventos ping automáticamente siempre y cuando se realice una llamada a `processMediaMessages` en el bucle de eventos. Actualice el cabezal de reproducción para que cada ping informe de la posición actual:

```brightscript
ADBMobile().mediaUpdatePlayhead(10)
```

>[!TAB API de recopilación de medios]

Envíe una publicación de `ping` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) en un temporizador. No incluya un objeto `params`:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```

>[!ENDTABS]
