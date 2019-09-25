---
seo-title: Seguimiento de reproducción principal en Chromecast
title: Seguimiento de reproducción principal en Chromecast
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de reproducción principal en Chromecast{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>Esta documentación cubre el seguimiento en la versión 2.x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`Referencia de API:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`constantes:**

   [Medios ADBMobile](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`constants:**

   [Medios ADBMobile](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Adjuntar metadatos de vídeo**

   Si lo desea, adjunte objetos de metadatos de vídeo estándar o personalizados a la sesión de seguimiento de vídeo mediante variables de datos de contexto.

   * **Metadatos de vídeo estándar**

      [Implementación de metadatos estándar en Chromecast](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >La asociación del objeto de metadatos de vídeo estándar al objeto multimedia es opcional.

   * **Metadatos personalizados**

      Cree un objeto variable para las variables personalizadas y rellene con los datos de este vídeo. Por ejemplo:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Rastrear la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión de medios, llame a [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) en el `media` objeto.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos del vídeo y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >El segundo valor es el nombre del objeto de metadatos de vídeo personalizado que creó en el paso 2. If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Track the actual start of playback**

   Identifique el evento del reproductor de vídeo para el principio de la reproducción, cuando se renderice el primer fotograma del vídeo en la pantalla e invoque [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Rastrear la finalización de la reproducción**

   Identifique el evento del reproductor de vídeo para la finalización de la reproducción, cuando el usuario ha visto el contenido hasta el final e invoque [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Rastrear el final de la sesión**

   Identifique el evento del reproductor de vídeo para la descarga o cierre de la reproducción, cuando el usuario cierra o completa la descarga e invoque [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a video tracking session. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Rastrear todos los escenarios posibles de pausa**

   Identifique el evento del reproductor en el que se pause el vídeo e invoque [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausar escenarios**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * Cuando el usuario pausa explícitamente en la aplicación.
   * Cuando el reproductor se sitúa en el estado En pausa.
   * (*Aplicaciones móviles*): cuando el usuario coloca la aplicación en segundo plano, pero desea que la sesión continúe abierta.
   * (*Aplicaciones móviles*): cuando se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se quede en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el vídeo desde donde se produjo la interrupción.

1. Identifique el evento del reproductor en el que el vídeo se reproduzca o se reanude e invoque [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Asegúrese de que cada llamada de API a `trackPause()` esté vinculada a continuación con una llamada de API a `trackPlay()` cuando se reanude la reproducción de vídeo.

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para Chromecast para ver un ejemplo de seguimiento completo.

