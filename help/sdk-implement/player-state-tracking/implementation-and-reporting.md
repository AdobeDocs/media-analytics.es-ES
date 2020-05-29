---
title: Implementación y Sistema de informes
description: En este tema se describe cómo implementar la función de seguimiento de estado del reproductor, incluyendo .
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Implementación y sistema de informes

Durante una sesión de reproducción, se debe realizar un seguimiento individual de cada incidencia de estado (inicio a extremo). El SDK de medios y la API de recopilación de medios proporcionan nuevos métodos de seguimiento para esta capacidad.

El SDK de medios incluye dos nuevos métodos para el seguimiento de estado personalizado:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


La API de Media Collection incluye dos nuevos eventos que `media.stateName` tienen como parámetro requerido:

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

* `a.media.states.[state.name].set = true` — Se establece en true si el estado se estableció al menos una vez por cada reproducción específica de un flujo.
* `a.media.states.[state.name].count = 4` — Identifica el número de ocurrencias de un estado durante cada reproducción individual de un flujo
* `a.media.states.[state.name].time = 240` — Identifica la duración total del estado en segundos por cada reproducción individual de un flujo

## Creación de informes

Todas las métricas de estado del reproductor se pueden utilizar para cualquier visualización de sistema de informes disponible en el área de trabajo de Análisis o en un componente (segmento, métricas calculadas) una vez que un grupo de informes esté habilitado para el seguimiento de estado del reproductor. Las nuevas métricas podrían habilitarse desde la Consola de administración para cada informe individual mediante la Configuración de Media Sistema de informes (Editar configuración > Administración de medios > Media Sistema de informes).

![](assets/report-setup.png)

En Espacio de trabajo de Analytics, todas las propiedades nuevas se encuentran en el panel Métricas. Por ejemplo, puede buscar por `full screen` para vista los datos de pantalla completa en el panel de métricas.

![](assets/full-screen-report.png)

## Importación de métricas declaradas por el reproductor a Adobe Experience Platform

Los datos almacenados en Analytics se pueden usar para cualquier fin y las métricas del estado del reproductor se pueden importar en la plataforma de Adobe Experience Platform mediante XDM y se pueden usar con el análisis de viajes del cliente. Las propiedades de estado estándar tienen propiedades específicas, mientras que los estados personalizados son propiedades disponibles mediante las eventos personalizadas.
