---
seo-title: Seguimiento de reproducción principal en iOS
title: Seguimiento de reproducción principal en iOS
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de reproducción principal en iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>Esta documentación cubre el seguimiento en la versión 2.x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API de createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nombre de variable | Descripción | Requerido |
   |---|---|---|
   | `name` | Nombre del vídeo | Sí |
   | `mediaid` | Identificador único de vídeo | Sí |
   | `length` | Duración del vídeo | Sí |
   | `streamType` | Tipo de flujo (consulte _Constantes_ StreamType a continuación) | Sí |
   | `mediaType` | Tipo de medio (consulte _las constantes_ de MediaType más abajo) | Sí |

   **`StreamType`constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo de emisión de vídeo bajo demanda |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo de emisión de contenido en directo |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo de emisión del contenido lineal |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo de emisión de audio a la carta. |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo de emisión de audiolibro. |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo de emisión de podcast. |

   **`MediaType`constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `ADBMediaTypeAudio` | Tipo de medio para emisiones de audio. |
   | `ADBMediaTypeVideo` | Tipo de medio para emisiones de vídeo. |

   Formato general para crear el objeto `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Adjuntar metadatos de vídeo**

   Optionally attach standard and/or custom video metadata objects to the video tracking session through context data variables.

   * **Metadatos de vídeo estándar**

      * [Implementación de metadatos estándar en iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Teclas de metadatos de vídeo**
         [Claves de metadatos de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consulte la lista completa de metadatos de vídeo aquí: [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md).
      >[!NOTE]
      >
      >La asociación del objeto de metadatos de vídeo estándar al objeto multimedia es opcional.

   * **Metadatos personalizados**

      Create a variable object for the custom variables and populate with the data for this video. Por ejemplo:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Rastrear la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, llame `trackSessionStart` a la instancia de Media Heartbeat.

   >[!TIP]
   >
   >El segundo valor es el nombre del objeto de metadatos de vídeo personalizado que creó en el paso 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos del vídeo y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Rastrear el inicio real de la reproducción**

   Identifique el evento del reproductor de vídeo para el principio de la reproducción, cuando se renderice el primer fotograma del vídeo en la pantalla e invoque `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Rastrear la finalización de la reproducción**

   Identifique el evento del reproductor de vídeo para la finalización de la reproducción, cuando el usuario ha visto el contenido hasta el final e invoque `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Rastrear el final de la sesión**

   Identifique el evento del reproductor de vídeo para la descarga o cierre de la reproducción, cuando el usuario cierra o completa la descarga e invoque `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento de video. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Rastrear todos los escenarios posibles de pausa**

   Identifique el evento del reproductor en el que se pause el vídeo e invoque `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Pausar escenarios**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * Cuando el usuario pausa explícitamente en la aplicación.
   * Cuando el reproductor se sitúa en el estado En pausa.
   * (*Aplicaciones móviles*): cuando el usuario coloca la aplicación en segundo plano, pero desea que la sesión continúe abierta.
   * (*Aplicaciones móviles*): cuando se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se quede en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el vídeo desde donde se produjo la interrupción.

1. Identifique el evento del reproductor en el que el vídeo se reproduzca o se reanude e invoque `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. Asegúrese de que cada llamada de API a `trackPause()` esté vinculada a continuación con una llamada de API a `trackPlay()` cuando se reanude la reproducción de vídeo.

Consulte lo siguiente para obtener más información sobre el seguimiento de la reproducción principal:

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para iOS para ver un ejemplo de seguimiento completo.

