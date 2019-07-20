---
seo-title: Seguimiento de reproducción principal en JavaScript
title: Seguimiento de reproducción principal en JavaScript
uuid: 3 d 6 e 0 ab 1-899 a -43 c 3-b 632-8276 e 84345 ab
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Seguimiento de reproducción principal en JavaScript{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Esta documentación abarca el seguimiento en la versión 2. x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](../../../sdk-implement/download-sdks.md).

1. **Configuración inicial del seguimiento**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API de createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del medio | Sí |
   | `mediaid` | Identificador único del medio | Sí |
   | `length` | Duración del medio | Sí |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sí |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sí |

   **`StreamType`constantes:**

   | Nombre de la constante | Descripción   |
   |---|---|
   | `VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `LIVE` | Tipo de emisión de contenido en directo. |
   | `LINEAR` | Tipo de emisión del contenido lineal. |
   | `AOD` | Tipo de flujo para audio on Demand. |
   | `AUDIOBOOK` | Tipo de flujo del libro de audio. |
   | `PODCAST` | Tipo de flujo para Podcast. |

   **`MediaType`constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `Audio` | Tipo de medio para emisiones de audio. |
   | `Video` | Tipo de medio para emisiones de vídeo. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
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
   >`trackSessionEnd` marca el final de una sesión de seguimiento. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Rastrear todos los escenarios de pausa posibles**

   Identify the event from the media player for pause and call `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Poner en pausa escenarios**

   Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * Cuando el usuario pausa explícitamente en la aplicación.
   * Cuando el reproductor se sitúa en el estado En pausa.
   * (*Aplicaciones móviles*): cuando el usuario coloca la aplicación en segundo plano, pero desea que la sesión continúe abierta.
   * (*Aplicaciones móviles*): cuando se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se quede en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el medio desde donde se produjo la interrupción.

1. Identifique el evento del reproductor para la reproducción o reanudación después de la pausa e invoque `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Puede ser el mismo origen de evento que se utilizó en el paso 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para JavaScript para ver un ejemplo de seguimiento completo.

