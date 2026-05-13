---
title: Actualización de varios estados de reproductor a la vez
description: En este tema se describe la funcionalidad de seguimiento de varios estados de reproductor.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
TQID: https://experienceleague.adobe.com/fKpr-TULVqDnK7j07e66gd-kiFLYzf7D2GmoGtP8Aqg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 186
ht-degree: 80%

---

# Seguimiento de varios estados de reproductor

A veces, dos estados de reproductor comienzan y finalizan al mismo tiempo, o el principio de uno es también el inicio de otro, como se muestra en la siguiente imagen:

![Varios estados de reproductor](assets/multiple-player-states.png)

La implementación actual permite ambas situaciones:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Sin embargo, esto requiere que emita varios eventos `stateStart` y `stateEnd` para indicar múltiples cambios de estado simultáneos. Entrada
para optimizar este comportamiento común, se ha implementado un nuevo tipo de evento `statesUpdate`, que finaliza una lista de estados
e inicia una lista de nuevos estados.

Con el nuevo evento `statesUpdate`, la lista anterior de eventos se convierte en lo siguiente:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

El número de llamadas de actualización de estado se ha reducido de seis a tres para el mismo comportamiento. El último evento
también podría haber sido un simple `stateEnd(fullScreen)`.

## Implementación de la API de Media Collection {#mpst-api}

Puede utilizar la API de recopilación de medios para implementar el seguimiento de varios estados de reproductor.

### Ejemplo

A continuación se muestra un ejemplo de implementación de la API de recopilación de medios para el seguimiento de varios estados de reproductor.

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Implementación de Media SDK

No hay ninguna implementación del SDK de medios.
