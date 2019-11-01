---
title: Seguimiento de reproducción principal en Roku
description: En este tema se describe cómo implementar el seguimiento principal mediante el SDK de medios en Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Seguimiento de reproducción principal en Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Esta documentación cubre el seguimiento en la versión 2.x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`referencia:**

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del vídeo | Sí |
   | `mediaid` | Identificador único de vídeo | Sí |
   | `length` | Duración del vídeo | Sí |
   | `streamType` | Tipo de flujo (consulte _Constantes_ StreamType a continuación) | Sí |
   | `mediaType` | Tipo de medio (consulte _las constantes_ de MediaType más abajo) | Sí |

   **`StreamType`constantes:**

   | Nombre de la constante | Descripción   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `MEDIA_STREAM_TYPE_LIVE` | Tipo de emisión de contenido en directo. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Tipo de emisión del contenido lineal. |
   | `MEDIA_STREAM_TYPE_AOD` | Tipo de emisión de audio a la carta. |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Tipo de emisión de audiolibro. |
   | `MEDIA_STREAM_TYPE_PODCAST` | Tipo de emisión de podcast. |

   **`MediaType`constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Tipo de medio para emisiones de audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Tipo de medio para emisiones de vídeo. |

   **Cree un objeto de información multimedia para vídeo con contenido de VOD:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   O bien

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Cree un objeto de información multimedia para vídeo con contenido de AOD:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   O bien

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Adjuntar metadatos**

   Si lo desea, adjunte objetos de metadatos estándar o personalizados a la sesión de seguimiento mediante variables de datos de contexto.

   * **Metadatos estándar**

      [Implementación de metadatos estándar en JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >La asociación del objeto de metadatos estándar al objeto multimedia es opcional.

      * Referencia de API de claves de metadatos de medios: [Claves de metadatos estándar de JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadatos personalizados**

      Cree un objeto variable para las variables personalizadas y rellene con los datos de este medio. Por ejemplo:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Rastrear la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, llame `trackSessionStart` a la instancia de Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >El segundo valor es el nombre del objeto de metadatos multimedia personalizado que se creó en el paso 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos, y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Rastrear el inicio real de la reproducción**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Rastrear la finalización de la reproducción**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Rastrear el final de la sesión**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >A `trackSessionEnd` marks the end of a tracking session. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.  Método de seguimiento de reproducción de medios para hacer un seguimiento de la carga de medios y establecer la sesión actual como activa:

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **Adjuntar metadatos de vídeo**

   Si lo desea, adjunte objetos de metadatos de vídeo estándar o personalizados a la sesión de seguimiento de vídeo mediante variables de datos de contexto.

   * **Metadatos de vídeo estándar**

      [Implementación de metadatos estándar en Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >La asociación del objeto de metadatos de vídeo estándar al objeto multimedia es opcional.

   * **Metadatos personalizados**

      Cree un objeto variable para las variables personalizadas y rellene con los datos de este vídeo. Por ejemplo:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Rastrear la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, llame `trackSessionStart` a la instancia de Media Heartbeat:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >El segundo valor es el nombre del objeto de metadatos de vídeo personalizado que creó en el paso 2.

   >[!IMPORTANT]
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos del vídeo y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Rastrear el inicio real de la reproducción**

   Identifique el evento del reproductor de vídeo para el principio de la reproducción, cuando se renderice el primer fotograma del vídeo en la pantalla e invoque `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Rastrear la finalización de la reproducción**

   Identifique el evento del reproductor de vídeo para la finalización de la reproducción, cuando el usuario ha visto el contenido hasta el final e invoque `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Rastrear el final de la sesión**

   Identifique el evento del reproductor de vídeo para la descarga o cierre de la reproducción, cuando el usuario cierra o completa la descarga e invoque `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` marca el final de una sesión de seguimiento de video. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Rastrear todos los escenarios posibles de pausa**

   Identifique el evento del reproductor en el que se pause el vídeo e invoque `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausar escenarios**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * Cuando el usuario pausa explícitamente en la aplicación.
   * Cuando el reproductor se sitúa en el estado En pausa.
   * (*Aplicaciones móviles*): cuando el usuario coloca la aplicación en segundo plano, pero desea que la sesión continúe abierta.
   * (*Aplicaciones móviles*): cuando se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se quede en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el vídeo desde donde se produjo la interrupción.

1. Identifique el evento del reproductor en el que el vídeo se reproduzca o se reanude e invoque `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Puede ser la misma fuente de eventos que se utilizó en el paso 4. Asegúrese de que cada llamada de API a `trackPause()` esté vinculada a continuación con una llamada de API a `trackPlay()` cuando se reanude la reproducción de vídeo.

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para Roku para ver un ejemplo de seguimiento completo.

