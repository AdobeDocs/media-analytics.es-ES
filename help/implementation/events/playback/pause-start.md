---
title: Pausar inicio
description: Indicación de que el usuario ha pausado la reproducción de contenido.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 10%

---


# Pausar inicio

El evento de inicio de pausa indica que el usuario pausó la reproducción. No hay un evento de reanudación independiente; envíe un evento [Play](play.md) cuando se reanude la reproducción.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: [[!UICONTROL Pausar eventos]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>No hay ningún tipo de evento de reanudación. La reanudación se infiere al enviar un evento [`play`](play.md) después de `pauseStart`.

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.pauseStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

>[!TAB iOS]

Invoque `trackPause` cuando el usuario detenga la reproducción.

```swift
tracker.trackPause()
```

>[!TAB Android]

Invoque `trackPause` cuando el usuario detenga la reproducción.

```kotlin
tracker.trackPause()
```

>[!TAB Roku]

Llamar a `sendMediaEvent` con `eventType: "media.pauseStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
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

Invoque `trackPause` cuando el usuario ponga en pausa la reproducción:

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

Invoque `trackPause` cuando el usuario ponga en pausa la reproducción:

```javascript
ADBMobile.media.trackPause();
```

>[!TAB API de recopilación de medios]

Enviar un POST de `pauseStart` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
