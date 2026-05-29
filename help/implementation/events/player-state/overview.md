---
title: Seguimiento de estados del reproductor
description: Obtenga información acerca de los eventos de estado del reproductor y cómo rastrear los estados de pantalla completa, silencio, subtítulos opcionales, imagen en imagen y enfoque.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 12%

---


# Seguimiento de estados del reproductor

Los eventos de estado del reproductor rastrean cómo los visualizadores interactúan con los controles del reproductor a lo largo de una sesión. Son opcionales y no son necesarios para las implementaciones de seguimiento de medios principales. Los cinco estados a los que se puede realizar el seguimiento son: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` y `inFocus`.

Los eventos de estado del reproductor son útiles para comprender el uso de las funciones de accesibilidad, como la frecuencia con la que los visualizadores habilitan los subtítulos o el silencio. También revelan patrones de comportamiento de visualización como la pantalla completa frente a la visualización en línea y la multitarea de imagen en imagen.

## Eventos del reproductor

| Evento del reproductor | Acción |
| --- | --- |
| El reproductor entra en un estado | Inicio del estado de llamada |
| El reproductor sale de un estado | Fin de estado de llamada |

## Estados estándar y personalizados

Hay cinco estados de reproductor estándar disponibles y puede agregar sus propios estados personalizados.

| Nombre de estado estándar | Constante de Media SDK | Nombre de la API de Media Collection |
|----|----|----|
| Pantalla completa | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Subtítulos opcionales | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Silenciar | `ADB.Media.PlayerState.Mute` | `mute` |
| Imagen en imagen | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| En el centro | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Consulte [Variables de estado del reproductor](/help/implementation/variables/player-state/) para obtener la referencia de variable completa, incluidas las rutas XDM y las definiciones de métricas.

**Estados personalizados:** Puede crear estados personalizados para capturar comportamientos de reproductor adicionales específicos de su aplicación. Consulte la [Referencia de API de medios: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/) para obtener detalles sobre cómo crear objetos de estado personalizados.

## Pasos de implementación

1. **Invocar al [inicio de estado](state-start.md)** cuando el reproductor entre en cualquiera de los cinco estados rastreables. Se pueden activar varios estados al mismo tiempo y se pueden iniciar varios estados en la misma llamada de evento.
1. **Invocar a [State end](state-end.md)** cuando el reproductor salga de un estado. Se pueden finalizar varios estados en la misma llamada de evento, y los estados se pueden iniciar y finalizar juntos en una sola llamada.

## Directrices

* Una sesión de vídeo está limitada a 10 estados de reproductor.
* Se permite cualquier combinación de estados.
* Si se pasan varios estados de reproductor, solo se retienen los 10 primeros y se reenvían a través del flujo hacia abajo al servidor de contenido.
* El máximo de 10 estados se aplica a todos los estados, independientemente de si están abiertos o cerrados.
* Un estado se puede iniciar y finalizar varias veces y se cuenta como un solo estado. Por ejemplo, `closedCaptioning` se puede iniciar y detener cinco veces, pero cuenta como un estado.
* El estado del reproductor se calcula en todos los estados de reproducción (sin división).
* Los estados del reproductor se capturan para cada sesión de reproducción individual. El estado del reproductor no se calcula entre reproducciones.
* El conocimiento del estado de la aplicación no se mantiene una vez que se detiene un estado. Una vez finalizado el estado, este debe volver a iniciarse para continuar con el seguimiento.

## Actualización de varios estados simultáneamente

En plataformas basadas en XDM, se pueden agrupar varios cambios de estado en una sola llamada de `statesUpdate` mediante matrices en `statesStart` y `statesEnd`. En los SDK móviles, cada cambio de estado requiere una llamada independiente.

Los siguientes ejemplos inician el silencio y la imagen en imagen juntos y, a continuación, la transición a pantalla completa.

## Tipos de implementación recomendados

>[!BEGINTABS]

>[!TAB SDK web ]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Mobile SDK no admite el agrupamiento: envíe una llamada independiente para cada cambio de estado.

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

Mobile SDK no admite el agrupamiento: envíe una llamada independiente para cada cambio de estado.

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB API de Media Edge]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipos de implementación heredados (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Si hay varios cambios de estado, es necesario realizar llamadas independientes.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

Si hay varios cambios de estado, es necesario realizar llamadas independientes.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB API de recopilación de medios]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## Pausa larga

Cuando una sesión de vídeo tiene una duración de pausa superior a 30 minutos, la API requiere una nueva sesión. Genere un nuevo ID de sesión y conserve todos los estados activos para que se puedan restaurar con `stateStart` eventos justo después de la nueva llamada de `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Una vez enviado `sessionEnd`, inicie una nueva sesión y vuelva a enviar inmediatamente los estados activos:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## Métricas de estado

Se calculan tres métricas para cada estado rastreado y se envían a Adobe Analytics en la llamada de cierre de medios:

| Métrica | Clave de datos de contexto | Descripción |
| --- | --- | --- |
| Estado establecido | `a.media.states.[state.name].set = true` | `true` si el estado se estableció al menos una vez durante la reproducción |
| Recuento de estados | `a.media.states.[state.name].count = 4` | Número de veces que se produjo el estado durante la reproducción |
| Hora del estado | `a.media.states.[state.name].time = 240` | Tiempo total (segundos) invertido en el estado durante la reproducción |
