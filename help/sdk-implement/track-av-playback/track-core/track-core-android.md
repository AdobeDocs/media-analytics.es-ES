---
seo-title: Seguimiento de reproducción principal en Android
title: Seguimiento de reproducción principal en Android
uuid: ab 5 fab 95-76 ed -4 ae 6-aedb -2 e 66 eece 7607
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de reproducción principal en Android{#track-core-playback-on-android}

>[!IMPORTANT]
>Esta documentación abarca el seguimiento en la versión 2. x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador de 1.x para Android aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración inicial del seguimiento**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API de createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del medio | Sí |
   | `mediaId` | Identificador único del medio | Sí |
   | `length` | Duración del medio | Sí |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sí |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sí |

   **`StreamType`constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `LIVE` | Tipo de emisión de contenido en directo. |
   | `LINEAR` | Tipo de emisión de contenido lineal. |
   | `AOD` | Tipo de emisión de audio a la carta. |
   | `AUDIOBOOK` | Tipo de emisión de audiolibro. |
   | `PODCAST` | Tipo de emisión de podcast. |

   **`MediaType`constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `Audio` | Tipo de medio para emisiones de audio. |
   | `Video` | Tipo de medio para emisiones de vídeo. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Adjuntar metadatos**

   De forma opcional, adjunte objetos de metadatos estándar o personalizados a la sesión de seguimiento a través de variables de datos de contexto.

   * **Metadatos estándar**

      [Implementación de metadatos estándar en Android](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >Incluir el objeto de metadatos estándar en el objeto multimedia es opcional.

      * Referencia de API de claves de metadatos de medios: [Claves de metadatos estándar de Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Consulte el conjunto completo de metadatos de vídeo disponibles aquí: [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md).
   * **Metadatos personalizados**

      Cree un diccionario para las variables personalizadas y rellene los datos de este medio. Por ejemplo:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Rastrear la intención de iniciar la reproducción**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance. Por ejemplo:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >El segundo valor es el nombre de objeto de metadatos de medios personalizado que ha creado en el paso 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos del medio y para calcular la métrica de QoS (tiempo entre `trackSessionStart` () y `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **Rastrear el inicio real de la reproducción**

   Identify the event from the media player for the beginning of the media playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Rastrear la finalización de la reproducción**

   Identify the event from the media player for the completion of the media playback, where the user has watched the content until the end, and call `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Rastrear el final de la sesión**

   Identify the event from the media player for the unloading/closing of the media playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento de medios. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **Rastrear todos los escenarios de pausa posibles**

   Identify the event from the media player for media pause and call `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Poner en pausa escenarios**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * Cuando el usuario pausa explícitamente en la aplicación.
   * Cuando el reproductor se sitúa en el estado En pausa.
   * (*Aplicaciones móviles*): cuando el usuario coloca la aplicación en segundo plano, pero desea que la sesión continúe abierta.
   * (*Aplicaciones móviles*): cuando se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se quede en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el medio desde donde se produjo la interrupción.

1. Identifique el evento del reproductor para la reproducción o reanudación de medio después de la pausa e invoque `trackPlay`.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Puede ser el mismo origen de evento que se utilizó en el paso 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

Consulte lo siguiente para obtener más información sobre el seguimiento de la reproducción principal:

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para Android para ver un ejemplo de seguimiento completo.

