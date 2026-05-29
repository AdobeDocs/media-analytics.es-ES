---
title: Error
description: Indica que el reproductor de contenidos ha encontrado un error.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 10%

---


# Error

El evento de error indica que el reproductor de contenido ha encontrado un error. El seguimiento de un error no cierra la sesión. Si el error impide que continúe la reproducción, llame a [Session end](session/session-end.md) después del evento de error.

* **Requisitos previos**: [Inicio de sesión](session/session-start.md)
* **Métrica asociada**: [[!UICONTROL Flujos afectados por el error]](/help/reporting/metrics/error-impacted-streams.md)

La propiedad `errorDetails.source` solo acepta dos valores: `player` (errores que se originan en el reproductor de medios) y `external` (errores de un origen externo como una CDN o una red).

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.error"` y el `errorDetails` requerido:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

Llamar a `trackError` con una cadena de identificador de error.

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

Llamar a `trackError` con una cadena de identificador de error.

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Roku]

Llamar a `sendMediaEvent` con `eventType: "media.error"` y el `errorDetails` requerido:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) con el elemento `errorDetails` requerido:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
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

Llamar a `trackError` con una cadena de identificador de error:

```javascript
tracker.trackError("media-error-001");
```

>[!TAB Chromecast]

Llamar a `trackError` con una cadena de identificador de error:

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB API de recopilación de medios]

Enviar un POST de `error` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```

>[!ENDTABS]
