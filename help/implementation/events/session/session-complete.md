---
title: Sesión completa
description: Indica que el visualizador ha llegado al final del contenido principal.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%
---

# Sesión completa

El evento de sesión completa indica que el visor ha llegado al final del contenido principal. No cierra inmediatamente la sesión; la sesión permanece abierta hasta que caduca de forma natural. Si desea cerrar inmediatamente la sesión, llame a [Fin de sesión](session-end.md) en su lugar.

* **Requisitos previos**: [Inicio de sesión](session-start.md)
* **Métrica asociada**: [[!UICONTROL El contenido finaliza]](/help/reporting/metrics/content-completes.md)

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Invoque `trackComplete` cuando el reproductor multimedia llegue al final del contenido.

```swift
tracker.trackComplete()
```

>[!TAB Android]

Invoque `trackComplete` cuando el reproductor multimedia llegue al final del contenido.

```kotlin
tracker.trackComplete()
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Invoque `trackComplete` cuando el reproductor multimedia llegue al final del contenido:

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

Invoque `trackComplete` cuando el reproductor multimedia llegue al final del contenido:

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

Invoque `mediaTrackComplete` cuando el reproductor multimedia llegue al final del contenido:

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB API de recopilación de medios]

Enviar un POST de `sessionComplete` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
