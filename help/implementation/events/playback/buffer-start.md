---
title: Inicio del búfer
description: Indica que el reproductor de contenidos ha entrado en un estado de almacenamiento en búfer.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 7%
---

# Inicio del búfer

El evento de inicio de almacenamiento en búfer indica que el reproductor de medios ha entrado en un estado de almacenamiento en búfer.

* **Requisitos previos**: [Inicio de sesión](../session/session-start.md)
* **Métrica asociada**: [[!UICONTROL Eventos de búfer]](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**API basadas en XDM (Web SDK, Roku, API de Media Edge, API de Media Collection):** No hay ningún tipo de evento de reanudación de búfer; el fin de búfer se infiere al enviar un evento [`play`](play.md) después de `bufferStart`.
>
>**SDK móvil:** Llama a `trackEvent(BufferComplete)` cuando el reproductor salga del almacenamiento en búfer y, a continuación, llama a `trackPlay()` para reanudar la reproducción.

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.bufferStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

Llame a `trackEvent` con `BufferStart` cuando el reproductor entre en un estado de almacenamiento en búfer y a `BufferComplete` cuando salga.

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Llame a `trackEvent` con `BufferStart` cuando el reproductor entre en un estado de almacenamiento en búfer y a `BufferComplete` cuando salga.

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

>[!TAB Roku Edge]

Llamar a `sendMediaEvent` con `eventType: "media.bufferStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
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

Llamar a `trackEvent` con el tipo de evento `BufferStart`:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

>[!TAB Chromecast]

Llamar a `trackEvent` con `BufferStart` cuando el reproductor entra en estado de almacenamiento en búfer y a `BufferComplete` cuando sale:

```javascript
// Buffer starts
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);

// Buffer ends
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
```

>[!TAB Roku 2.x]

Llamar a `mediaTrackEvent` con `MEDIA_BUFFER_START` cuando el reproductor entra en estado de almacenamiento en búfer y a `MEDIA_BUFFER_COMPLETE` cuando sale:

```brightscript
adb = ADBMobile()

' Buffer starts
adb.mediaTrackEvent(adb.MEDIA_BUFFER_START)

' Buffer ends
adb.mediaTrackEvent(adb.MEDIA_BUFFER_COMPLETE)
```

>[!TAB API de recopilación de medios]

Enviar un POST de `bufferStart` al [extremo de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
