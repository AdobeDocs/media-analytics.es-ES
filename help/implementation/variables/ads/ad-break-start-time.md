---
title: Hora de inicio de la pausa publicitaria
description: Establezca el tiempo de inicio (desplazamiento) de la pausa publicitaria dentro del contenido, en segundos.
feature: Streaming Media
role: Developer
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 6%
---

# Hora de inicio de la pausa publicitaria

>[!BEGINSHADEBOX]

*Esta página cubre la recopilación de datos para la variable **Hora de inicio de las pausas publicitarias**. Ver [Posición de la secuencia](/help/reporting/dimensions/pod-position.md) para la dimensión de informe correspondiente.*

>[!ENDSHADEBOX]

La variable de tiempo de inicio de la pausa publicitaria es el desplazamiento de la pausa publicitaria dentro del contenido, medido en segundos. Para una emisión previa el valor es `0`; para una emisión intermedia, el valor es la posición del cabezal de reproducción en la que comienza la pausa.

| Propiedad | Valor |
| --- | --- |
| **Variable de datos de contexto** | `a.media.ad.podSecond` |
| **Campo de colección XDM** | [`xdm.mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **rasgo de Audience Manager** | `c_contextdata.a.media.ad.podSecond` |
| **Requerido** | Sí |
| **Enviado con** | [Inicio de la pausa publicitaria](/help/implementation/events/ads/ad-break-start.md), cierre del anuncio |

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

Establecer `offset` dentro de `xdm.mediaCollection.advertisingPodDetails` al llamar a [`sendEvent`](https://experienceleague.adobe.com/es/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Pase el tiempo de inicio en segundos como tercer argumento a `createAdBreakObject`.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Pase el tiempo de inicio en segundos como tercer argumento a `createAdBreakObject`.

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

Establecer `offset` dentro de `xdm.mediaCollection.advertisingPodDetails` al llamar a `sendMediaEvent` para `media.adBreakStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

>[!TAB API de Media Edge]

Llame al extremo [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) con `offset` dentro de `xdm.mediaCollection.advertisingPodDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Pasar la hora de inicio como tercer argumento a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

Pasar el tiempo de inicio en segundos como tercer argumento a `ADBMobile.media.createAdBreakObject`:

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

Pase el tiempo de inicio en segundos como segundo argumento a `adb_media_init_adbreakinfo`. Observe el orden del parámetro Roku: `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("mid-roll-1", 90.0, 2)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB API de recopilación de medios]

Incluir `media.ad.podSecond` en el objeto `params` de su solicitud POST de `adBreakStart`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

Consulte la [referencia de eventos de API de Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events) para obtener la estructura de solicitudes completa.

>[!ENDTABS]
