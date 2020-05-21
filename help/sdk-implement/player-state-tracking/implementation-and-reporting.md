---
title: Implementación y Sistema de informes
description: En este tema se describe cómo implementar la función de seguimiento de estado del reproductor, incluyendo .
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Implementación y sistema de informes

Durante una sesión de reproducción, se debe realizar un seguimiento individual de cada incidencia de estado (inicio a extremo). El SDK de medios y la API de recopilación de medios proporcionan nuevos métodos de seguimiento para esta capacidad.

El SDK de medios incluye dos nuevos métodos para el seguimiento de estado personalizado:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


La API de Media Collection incluye dos nuevos eventos que tienen &quot;media.stateName&quot; como parámetro requerido:

`stateStart` y `stateEnd`

## Implementación de SDK de medios

Inicios de estado del reproductor

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

El estado del reproductor finaliza

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Implementación de la API de Media Collection

Inicios de estado del reproductor

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

El estado del reproductor finaliza

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## Métricas de estado

Las métricas proporcionadas para cada estado individual se calculan y transfieren a Adobe Analytics como parámetros de datos de contexto y se almacenan con fines de sistema de informes. Hay tres métricas disponibles para cada estado:

* `a.media.states.(media.state.name).set = true` — Se establece en true si el estado se estableció al menos una vez por cada reproducción específica de un flujo.
* `a.media.states.(media.state.name).count = 4` — Identifica el número de ocurrencias de un estado durante cada reproducción individual de un flujo
* `a.media.states.(media.state.name).time = 240` — Identifica la duración total del estado en segundos por cada reproducción individual de un flujo

## Creación de informes

Todas las métricas de estado se pueden utilizar para cualquier visualización de sistema de informes o componente (segmento, métricas calculadas).
TBD - compruebe la fuente/wiki para obtener información actualizada - para captura de pantalla de AW

## Importación de métricas declaradas por el reproductor a Adobe Experience Platform

Los datos almacenados en Analytics se pueden usar para cualquier fin y las métricas del estado del reproductor se pueden importar en la plataforma de Adobe Experience Platform mediante XDM y se pueden usar con el análisis de viajes del cliente. Las propiedades de estado estándar tienen propiedades específicas, mientras que los estados personalizados son propiedades disponibles mediante las eventos personalizadas. Para obtener más información, consulte la lista de propiedades de identidades XDM en ?LINK TO METRIC LISTA?.
