---
title: Referencia de la API de Media SDK de JavaScript 3.x
description: Referencia de API para Media SDK JavaScript 3.x (clases ADB.Media y ADB.MediaConfig).
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# Referencia de la API de Media SDK de JavaScript 3.x

>[!BEGINSHADEBOX]

Esta página cubre SDK 3.x de JavaScript solo de Analytics. Para la implementación recomendada, consulte [Implementar medios de transmisión mediante Edge Network](/help/implementation/edge/edge-web-sdk.md).

>[!ENDSHADEBOX]

## ADB.Media

### Métodos estáticos

+++configurar

Configura MediaSDK para el seguimiento. Se debe llamar a este método una vez antes de crear instancias de seguimiento en una página.

**Sintaxis**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| Nombre de variable | Tipo | Descripción |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | Configuración de medios válida |
| `appMeasurement` | objeto | Instancia de AppMeasurement |

**Ejemplo**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

Crea una instancia del contenido para realizar un seguimiento de la sesión de reproducción. Devuelve `null` si se llama antes de configurar los medios.

**Sintaxis**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| Nombre de variable | Tipo | Requerido | Descripción |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | Configuración del rastreador | No | Objeto de configuración del rastreador. |

**Ejemplo**

```javascript
var tracker = ADB.Media.getInstance();
```

Para anular `channel` o `playerName` por instancia de seguimiento, pase los valores de anulación en el objeto de configuración del rastreador.

**Ejemplo con la configuración del rastreador**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

Crea un objeto que contiene información multimedia. Devuelve un objeto vacío si se pasan parámetros no válidos.

**Sintaxis**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| Nombre de variable | Tipo | Descripción |
| :--- | :--- | :--- |
| `name` | string | Cadena no vacía que indica el nombre de los medios |
| `id` | string | Cadena no vacía que indica un identificador de medios único |
| `length` | number | Número positivo que indica la longitud de los medios en segundos. Utilice `0` si se desconoce la longitud. |
| `streamType` | string | Tipo de emisión o cadena no vacía para indicar el tipo de emisión de contenido. |
| `mediaType` | Tipo de medio | Tipo de medios (audio o vídeo) |

**Ejemplo**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

Crea un objeto que contiene información de un salto. Devuelve un objeto vacío si se pasan parámetros no válidos.

**Sintaxis**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| Nombre de variable | Tipo | Descripción |
| :--- | :--- | :--- |
| `name` | string | Cadena no vacía que indica el nombre de un salto de página (anuncio previo a la emisión, anuncio durante la emisión y anuncio posterior a la emisión) |
| `position` | number | La posición numérica de la pausa publicitaria dentro del contenido, empezando por 1 |
| `startTime` | number | Valor del cabezal de reproducción al comienzo de la pausa publicitaria. |

**Ejemplo**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

Crea un objeto que contiene información de publicidad. Devuelve un objeto vacío si se pasan parámetros no válidos.

**Sintaxis**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| Nombre de variable | Tipo | Descripción |
| :--- | :--- | :--- |
| `name` | string | Cadena no vacía que indica el nombre del anuncio |
| `id` | string | Cadena no vacía que indica un ID de anuncio |
| `position` | number | La posición numérica del anuncio dentro del salto de página, empezando por 1 |
| `length` | number | Número positivo que indica la duración del anuncio |

**Ejemplo**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

Crea un objeto que contiene información del capítulo. Devuelve un objeto vacío si se pasan parámetros no válidos.

**Sintaxis**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| Nombre de variable | Tipo | Descripción |
| :--- | :--- | :--- |
| `name` | string | Cadena no vacía que indica el nombre del capítulo |
| `position` | number | La posición del capítulo dentro del contenido, empezando por 1 |
| `length` | number | Número positivo que indica la longitud del capítulo |
| `startTime` | number | Valor del cabezal de reproducción al principio del capítulo |

**Ejemplo**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

Crea un objeto que contiene información de estado. Devuelve un objeto vacío si se pasan parámetros no válidos.

**Sintaxis**

```javascript
ADB.Media.createStateObject(name)
```

| Nombre de variable | Tipo | Descripción |
| :--- | :--- | :--- |
| `name` | string | Estado del reproductor o cadena no vacía que indica el nombre del estado |

**Ejemplo**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

Crea un objeto que contiene información de QoE. Devuelve un objeto vacío si se pasan parámetros no válidos.

**Sintaxis**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| Nombre de variable | Tipo | Descripción |
| :--- | :--- | :--- |
| `bitrate` | número | Número positivo que indica la velocidad de bits actual (0 si se desconoce) |
| `startupTime` | number | Número positivo que indica la hora de inicio (0 si se desconoce) |
| `fps` | number | Número positivo que indica el fps actual (0 si se desconoce) |
| `droppedFrames` | number | Número positivo que indica el número de fotogramas perdidos (0 si se desconoce) |

**Ejemplo**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

Devuelve la versión de MediaSDK.

**Sintaxis**

```javascript
ADB.Media.version
```

**Ejemplo**

```javascript
console.log(ADB.Media.version);
```

+++

### Métodos de instancia

+++trackSessionStart

Realice un seguimiento de la intención de iniciar la reproducción. Esto inicia una sesión de seguimiento en la instancia de seguimiento de medios. Consulte también Reanudación de contenido.

**Sintaxis**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| Nombre de variable | Descripción | Requerido |
| :--- | :--- | :---: |
| `mediaObject` | Información multimedia creada con el método `createMediaObject`. | Sí |
| `contextData` | Datos de contexto de medios opcionales. Para las claves de metadatos estándar, utilice constantes de vídeo estándar o constantes de audio estándar. | No |

**Ejemplo**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

Rastrear la reproducción o reanudación de contenido después de una pausa previa.

**Sintaxis**

```javascript
ADB.Media.trackPlay();
```

**Ejemplo**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

Rastrear pausa de medios.

**Sintaxis**

```javascript
ADB.Media.trackPause();
```

**Ejemplo**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

Seguimiento de contenido completado. Llame a este método solo cuando el medio se haya visto por completo.

**Sintaxis**

```javascript
ADB.Media.trackComplete();
```

**Ejemplo**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

Rastrear el final de una sesión de visualización. Llame a este método aunque el usuario no vea el contenido completo.

**Sintaxis**

```javascript
ADB.Media.trackSessionEnd();
```

**Ejemplo**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

Realizar un seguimiento de un error en la reproducción de contenido.

**Sintaxis**

```javascript
ADB.Media.trackError(errorId);
```

| Nombre de variable | Descripción | Requerido |
| :--- | :--- | :---: |
| `errorId` | Cadena no vacía que contiene información de error | Sí |

**Ejemplo**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

Método para realizar un seguimiento de eventos de contenidos.

| Nombre de variable | Descripción |
| :--- | :--- |
| `event` | Evento de medios |
| `info` | Para el evento `AdBreakStart`, la información de adbreak se crea mediante el método `createAdBreakObject`. Para el evento `AdStart`, la información de la publicidad se crea mediante el método `createAdObject`. Para el evento `ChapterStart`, la información del capítulo se crea mediante el método `createChapterObject`. Para los eventos `StateStart` y `StateEnd`, la información de estado se crea mediante el método `createStateObject`. Esto no es necesario para otros eventos. |
| `contextData` | Se pueden proporcionar datos de contexto opcionales para los eventos `AdStart` y `ChapterStart`. Esto no es necesario para otros eventos. |

**Sintaxis**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**Ejemplos**

**Rastrear AdBreaks**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**Anuncios de seguimiento**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**Seguimiento de capítulos**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**Estados de seguimiento**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**Seguimiento de eventos de reproducción**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**Cambios de velocidad de bits de seguimiento**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

Proporcione el cabezal de reproducción de medios actual al rastreador de medios. Para obtener un seguimiento preciso, invoque este método siempre que el cabezal de reproducción cambie durante la reproducción.

**Sintaxis**

```javascript
ADB.Media.updatePlayhead(time);
```

| Nombre de variable | Descripción |
| :--- | :--- |
| `time` | Cabezal de reproducción actual en segundos. Para vídeo bajo demanda (VOD), el valor se especifica segundos después del comienzo del elemento de medios. Para el streaming en directo, si el reproductor no proporciona información acerca de la duración del contenido, el valor se puede especificar como el número de segundos desde la medianoche (UTC) de ese día. Nota: Cuando se utilizan marcadores de progreso, la duración del contenido es obligatoria y el cabezal de reproducción debe actualizarse como número de segundos desde el principio del elemento de medios, empezando por 0. |

**Ejemplo**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

Proporciona información actual de QoE al rastreador de medios. Para obtener un seguimiento preciso, llame a este método varias veces cuando el reproductor de contenido proporcione la información de QoE actualizada.

**Sintaxis**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| Nombre de variable | Descripción |
| :--- | :--- |
| `qoeObject` | Información actual de QoE creada con el método `createQoEObject`. |

**Ejemplo**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++destruir

Destruye la instancia de seguimiento.

**Sintaxis**

```javascript
ADB.Media.destroy();
```

**Ejemplo**

```javascript
tracker.destroy();
```

+++

### Constantes

+++Configuración del rastreador

Define las claves de configuración que se pueden establecer por cada instancia de seguimiento.

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++Tipo de medio

Define el tipo de medio que se está rastreando actualmente.

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++Tipo de emisión

Define el tipo de flujo del contenido que se rastrea actualmente.

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++Claves de metadatos estándar

`ADB.Media.VideoMetadataKeys`, `ADB.Media.AudioMetadataKeys` y `ADB.Media.AdMetadataKeys` proporcionan las cadenas de clave de datos de contexto para los metadatos estándar. Para obtener la lista completa de claves y sus variables de informes correspondientes, consulte [Referencia de variable de metadatos estándar](/help/implementation/variables/standard-metadata/show.md).

+++

+++Eventos de medios

Define el tipo de un evento de seguimiento.

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++Estados del reproductor

Define valores estándar para rastrear el estado del reproductor.

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++Media resume

Constante para indicar que la sesión de seguimiento actual está reanudando una sesión previamente cerrada. Esta información debe proporcionarse al iniciar una sesión de seguimiento.

**Sintaxis**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**Ejemplo**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| Clave | Requerido | Descripción |
| :--- | :--- | :--- |
| `trackingServer` | Sí | Escriba el nombre del servidor de API de recopilación de medios al que se deben enviar los datos de seguimiento de medios descargados. Póngase en contacto con el representante de su cuenta de Adobe para recibir esta información. |
| `channel` | No | Propiedad del nombre del canal |
| `playerName` | No | Nombre del reproductor de medios en uso |
| `appVersion` | No | Escriba la versión de la aplicación del reproductor de contenidos/SDK |
| `debugLogging` | No | Habilita o deshabilita los registros de Media SDK (valor predeterminado: `false`) |
| `ssl` | No | Envía pings a través de SSL (valor predeterminado: `true`) |
