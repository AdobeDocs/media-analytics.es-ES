---
title: Fin de sesión
description: Cierre inmediatamente una sesión multimedia cuando el usuario abandone el contenido.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 4%

---


# Fin de sesión

El evento de fin de sesión cierra de forma inmediata e irreversible una sesión de seguimiento de contenido. El final de la sesión es un cierre estricto; una vez enviada, la sesión finaliza y no se pueden rastrear más eventos debajo de ella. Utilice Finalizar sesión únicamente cuando esté seguro de que no se producirán eventos adicionales, como cuando se destruya el reproductor o se descargue la página. En la mayoría de los casos, es más seguro permitir que la sesión caduque de forma natural, en lugar de arriesgarse a interrumpir eventos que podrían llegar. Si el visor termina el contenido, llama a [Sesión completa](session-complete.md) en su lugar.

Sin un final de sesión explícito, una sesión se cierra automáticamente tras 10 minutos sin eventos o 30 minutos sin movimiento del cabezal de reproducción.

>[!NOTE]
>
>Puede llamar al final de la sesión más de una vez de forma segura para la misma sesión. El servidor cierra la sesión en el primer evento y cierra en silencio todos los eventos subsiguientes para ese ID de sesión, incluido un segundo fin de sesión. No es necesario protegerse contra llamadas duplicadas en condiciones de carrera, como un tiempo de espera de 30 minutos que caduca en el mismo momento en que el visualizador cierra el reproductor.

* **Requisitos previos**: [Inicio de sesión](session-start.md)
* **Métrica asociada**: ninguna

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

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

>[!TAB iOS]

Invoque `trackSessionEnd` cuando el visor cierre el reproductor o salga del mismo.

```swift
tracker.trackSessionEnd()
```

>[!TAB Android]

Invoque `trackSessionEnd` cuando el visor cierre el reproductor o salga del mismo.

```kotlin
tracker.trackSessionEnd()
```

>[!TAB Roku Edge]

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

>[!TAB API de Media Edge]

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

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Invoque `trackSessionEnd` cuando el visor cierre el reproductor o salga:

```javascript
tracker.trackSessionEnd();
```

>[!TAB Chromecast]

Invoque `trackSessionEnd` cuando el visor cierre el reproductor o salga:

```javascript
ADBMobile.media.trackSessionEnd();
```

>[!TAB Roku 2.x]

Invoque `mediaTrackSessionEnd` cuando el visor cierre el reproductor o salga:

```brightscript
ADBMobile().mediaTrackSessionEnd()
```

>[!TAB API de recopilación de medios]

Enviar un POST de `sessionEnd` al [extremo de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```

>[!ENDTABS]
