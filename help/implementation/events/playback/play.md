---
title: Play
description: Indica que el reproductor multimedia ha entrado en el estado de reproducción.
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
source-wordcount: '187'
ht-degree: 9%
---

# Play

El evento de reproducción indica que el reproductor de contenido ha cambiado de estado a reproducción. Enviarlo al inicio del contenido, en la reproducción automática y siempre que el reproductor se reanude tras una pausa o almacenamiento en búfer. No hay un evento de reanudación independiente; un evento de reproducción después de [Pausar inicio](pause-start.md) o [Inicio del búfer](buffer-start.md) sirve como reanudación.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: [[!UICONTROL El contenido comienza]](/help/reporting/metrics/content-starts.md)

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.play"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Invoque `trackPlay` cuando el reproductor de contenido comience o reanude la reproducción.

```swift
tracker.trackPlay()
```

>[!TAB Android]

Invoque `trackPlay` cuando el reproductor de contenido comience o reanude la reproducción.

```kotlin
tracker.trackPlay()
```

>[!TAB Roku Edge]

Llamar a `sendMediaEvent` con `eventType: "media.play"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

Llamar al extremo [play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
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

Invoque `trackPlay` cuando el reproductor de contenido comience o reanude la reproducción:

```javascript
tracker.trackPlay();
```

>[!TAB Chromecast]

Invoque `trackPlay` cuando el reproductor de contenido comience o reanude la reproducción:

```javascript
ADBMobile.media.trackPlay();
```

>[!TAB Roku 2.x]

Invoque `mediaTrackPlay` cuando el reproductor de contenido comience o reanude la reproducción:

```brightscript
ADBMobile().mediaTrackPlay()
```

>[!TAB API de recopilación de medios]

Enviar un POST de `play` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
