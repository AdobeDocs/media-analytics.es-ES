---
seo-title: Seguimiento de reproducción principal en Roku
title: Seguimiento de reproducción principal en Roku
uuid: a 8 aa 7 b 3 c -2 d 39-44 d 7-8 ebc-b 101 d 130101 f
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Seguimiento de reproducción principal en Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Esta documentación abarca el seguimiento en la versión 2. x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](../../../sdk-implement/download-sdks.md).

1. **Configuración inicial del seguimiento**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`reference:**

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del vídeo | Sí |
   | `mediaid` | Identificador único de vídeo | Sí |
   | `length` | Duración del vídeo | Sí |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sí |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sí |

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

   o

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Cree un objeto de información multimedia para vídeo con contenido AOD:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   o

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Adjuntar metadatos**

   De forma opcional, adjunte objetos de metadatos estándar o personalizados a la sesión de seguimiento a través de variables de datos de contexto.

   * **Metadatos estándar**

      [Implementación de metadatos estándar en JavaScript](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Incluir el objeto de metadatos estándar en el objeto multimedia es opcional.

      * Referencia de API de claves de metadatos de medios: [Claves de metadatos estándar de JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
   * **Metadatos personalizados**

      Cree un objeto variable para las variables personalizadas y rellene los datos de este medio. Por ejemplo:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Rastrear la intención de iniciar la reproducción**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >El segundo valor es el nombre de objeto de metadatos de medios personalizado que ha creado en el paso 2.

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

   De forma opcional, adjunte objetos de metadatos de vídeo estándar o/o personalizados a la sesión de seguimiento de vídeo a través de variables de datos de contexto.

   * **Metadatos de vídeo estándar**

      [Implementación de metadatos estándar en Roku](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Incluir el objeto de metadatos de vídeo estándar en el objeto multimedia es opcional.

   * **Metadatos personalizados**

      Cree un objeto variable para las variables personalizadas y rellene los datos de este vídeo. Por ejemplo:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Rastrear la intención de iniciar la reproducción**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >El segundo valor es el nombre de objeto de metadatos de vídeo personalizado que ha creado en el paso 2.

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
   >`trackSessionEnd` marca el final de una sesión de seguimiento de vídeo. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Rastrear todos los escenarios de pausa posibles**

   Identifique el evento del reproductor en el que se pause el vídeo e invoque `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Poner en pausa escenarios**

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
   >Puede ser el mismo origen de evento que se utilizó en el paso 4. Asegúrese de que cada llamada de API a `trackPause()` esté vinculada a continuación con una llamada de API a `trackPlay()` cuando se reanude la reproducción de vídeo.

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para Roku para ver un ejemplo de seguimiento completo.

