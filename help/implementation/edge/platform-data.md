---
title: Asignación de datos de la API de Media Edge y validación de Platform
description: Descubra qué eventos de API de Media Edge generan eventos de experiencia en Adobe Experience Platform y cómo validar la implementación mediante el esquema XDM de creación de informes de medios.
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85eid: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 764
ht-degree: 4%

---


# Asignación de datos de la API de Media Edge y validación de Platform

Cuando envía eventos de seguimiento de contenido mediante la API de Media Edge o una SDK de Media Edge, el backend de Media Analytics procesa esos eventos y escribe eventos de experiencia calculados en conjuntos de datos de Adobe Experience Platform. Comprender qué eventos llegan a Platform y qué calcula el back-end por usted ayuda a validar la implementación y crear informes precisos en Customer Journey Analytics o Adobe Analytics.

Media Edge utiliza dos esquemas XDM distintos:

| Esquema | Área de nombres | Dirección | Finalidad |
|---|---|---|---|
| Colección de medios | `xdm.mediaCollection` | Cliente → Adobe | Lo que envía el reproductor para cada evento de seguimiento |
| Informes de medios | `xdm.mediaReporting` | Adobe → Platform | Lo que el servidor escribe en los conjuntos de datos después del procesamiento |

Los campos presentes en `mediaReporting` pero ausentes de la carga útil de `mediaCollection` son **calculados en el servidor**, derivados de la secuencia completa de eventos de una sesión. Estos campos nunca se envían; Adobe los genera.

## Eventos que escriben en conjuntos de datos de Platform

De los 12 tipos de eventos a los que se puede realizar un seguimiento, solo cinco generan escrituras de eventos de experiencia individuales en conjuntos de datos:

| Tipo de evento | Incluido en conjuntos de datos | Notas |
|---|---|---|
| [Inicio de sesión](/help/implementation/events/session/session-start.md) | Sí | Se escribe al inicializar la sesión |
| [Inicio del anuncio](/help/implementation/events/ads/ad-start.md) | Sí | Se escribe cuando comienza un anuncio individual |
| [Anuncio completado](/help/implementation/events/ads/ad-complete.md) | Sí | Se escribe cuando se reproduce un anuncio hasta su finalización |
| [Capítulo completado](/help/implementation/events/chapters/chapter-complete.md) | Sí | Se escribe cuando se reproduce un capítulo hasta su finalización |
| [Sesión completa](/help/implementation/events/session/session-complete.md) | Sí | Se escribe cuando finaliza la sesión; conjunto de campos calculados más completo |
| [Reproducir](/help/implementation/events/playback/play.md) | No | Se usó para calcular `timePlayed` |
| [Pausar inicio](/help/implementation/events/playback/pause-start.md) | No | Se usó para calcular `pauseCount` y `pauseTime` |
| [Ping](/help/implementation/events/playback/ping.md) | No | Heartbeat; se utiliza para detectar la inactividad de la sesión |
| [Inicio del búfer](/help/implementation/events/playback/buffer-start.md) | No | Se utiliza para calcular las métricas del búfer de QoE |
| [Cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md) | No | Se utiliza para calcular las métricas de velocidad de bits de QoE |
| [Inicio de estado](/help/implementation/events/player-state/state-start.md) | No | Se utiliza para calcular las métricas de estado del reproductor |
| [Error](/help/implementation/events/error.md) | No | Se usa para calcular `errorCount` en QoE |

## Campos calculados back-end

Los campos siguientes aparecen en `mediaReporting` cargas útiles, pero nunca forman parte de la carga útil de recopilación. El servidor los deriva de la secuencia de eventos completa.

**Nivel de sesión** (aparece en `sessionComplete`):

| Campo | Descripción |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | Segundos totales de contenido principal reproducido, sin incluir los anuncios |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | Segundos totales transcurridos, incluidos los anuncios |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | Segundos deduplicados: los intervalos vistos más de una vez se cuentan solo una vez |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed` dividido por la longitud del contenido |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | Flujos simultáneos estimados |
| `xdm.mediaReporting.sessionDetails.adCount` | Número de anuncios que comenzaron |
| `xdm.mediaReporting.sessionDetails.chapterCount` | Número de capítulos que comenzaron |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | Frecuencia de pausa y duración total de la pausa |
| `xdm.mediaReporting.sessionDetails.hasProgress10`... `xdm.mediaReporting.sessionDetails.hasProgress95` | Indicadores de hitos de progreso (10 %, 25 %, 50 %, 75 %, 95 %) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | Si se vio al menos un marco de contenido |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | Indicadores de finalización e inicio |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | Tiempo entre el último ping y el cierre de sesión |
| `xdm.mediaReporting.sessionDetails.segment` | Corchete de segmento de contenido (por ejemplo, `[0-1]`) |

**Nivel de anuncio** (aparece en `adComplete`):

| Campo | Descripción |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | Segundos de contenido de publicidad reproducido |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | Si el anuncio se reprodujo hasta su finalización |

**Nivel de capítulo** (aparece en `chapterComplete`):

| Campo | Descripción |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | Segundos de contenido del capítulo reproducido |
| `xdm.mediaReporting.chapterDetails.isCompleted` | Si el capítulo se reprodujo hasta su finalización |
| `xdm.mediaReporting.chapterDetails.isStarted` | Si el capítulo comenzó |

**QoE** (agregado el `sessionComplete`):

| Campo | Descripción |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | Velocidad de bits media durante la sesión |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | Intervalo de velocidad de bits media agrupada |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | Número de cambios de velocidad de bits |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | Número de errores |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | Total de fotogramas perdidos |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | Matriz de códigos de error del reproductor |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | Si se produjo algún error |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | Si se produjeron fotogramas perdidos |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | Si se produjeron cambios en la velocidad de bits |

## Contenido descargado

Para las sesiones rastreadas con el [extremo descargado](/help/use-cases/track-downloaded-content.md), el backend establece automáticamente `xdm.mediaReporting.sessionDetails.isDownloaded` en `true` en el evento de informe `sessionStart`. Todos los demás eventos de informes de sesiones descargadas siguen el mismo esquema que las sesiones en directo. Utilice este campo en CJA o Adobe Analytics para filtrar o segmentar la reproducción descargada.

Consulte [Extremo descargado](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/) en la referencia de la API de Media Edge para obtener detalles de implementación de recopilación.

## Validar la implementación

Después de enviar eventos a través de la API de Media Edge, compruebe que los datos aterrizaron correctamente mediante uno de los siguientes métodos:

**Vista previa del conjunto de datos Adobe Experience Platform**

1. En [CX Enterprise](https://experience.adobe.com), vaya a **[!UICONTROL Conjuntos de datos]** y seleccione su conjunto de datos de medios de streaming.
2. Seleccione **[!UICONTROL Previsualizar conjunto de datos]** para ver los eventos de experiencia ingeridos más recientemente.
3. Confirme que los valores de `eventType`, como `media.sessionStart` y `media.sessionComplete`, aparezcan con los campos `mediaReporting` rellenados.

**Inspección del conjunto de datos de Customer Journey Analytics**

1. En CJA, abra la conexión asociada a su conjunto de datos de medios de streaming.
2. Seleccione **Agregar conjuntos de datos** e inspeccione el esquema para confirmar que los campos `mediaReporting` están asignados a las dimensiones y métricas esperadas.

**Reglas de procesamiento de Adobe Analytics (si se usa el destino de Analytics)**

Para los grupos de informes de Adobe Analytics que reciben datos mediante el conector de origen de Analytics, puede utilizar Reglas de procesamiento para asignar `mediaReporting` variables de datos de contexto a props o eVars personalizadas. El marcador `isDownloaded` está disponible como `a.media.downloaded`.

## Ejemplos de carga útil de XDM

Los siguientes ejemplos muestran la estructura XDM `mediaReporting` completa para cada evento de sistema de informes como se escribe en los conjuntos de datos de Platform. La propiedad `_{tenantName}` representa el espacio de nombres de inquilino de su organización para cualquier campo personalizado.

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart (contenido descargado)

Las sesiones rastreadas con el [extremo descargado](/help/use-cases/track-downloaded-content.md) siguen el mismo esquema de informes con una diferencia clave: `xdm.mediaReporting.sessionDetails.isDownloaded` se establece en `true` en el evento de informes `sessionStart`. Todos los demás tipos de eventos son idénticos a los ejemplos de contenido en directo anteriores.

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++
