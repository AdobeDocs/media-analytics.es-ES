---
title: Descubra cómo rastrear la reproducción principal en iOS
description: Obtenga información sobre cómo implementar el seguimiento principal mediante Media SDK en iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 95%

---

# Seguimiento de reproducción principal en iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>Esta documentación abarca el seguimiento en la versión 2.x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identifique el momento en que el usuario desencadena la intención de reproducir (cuando hace clic en reproducir o la reproducción automática está activada) y cree una instancia de `MediaObject`.

   [API de createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nombre de variable | Descripción | Requerido |
   |---|---|---|
   | `name` | Nombre del vídeo | Sí |
   | `mediaid` | Identificador único de vídeo | Sí |
   | `length` | Duración del vídeo | Sí |
   | `streamType` | Tipo de flujo (consulte _Constantes de StreamType_ a continuación) | Sí |
   | `mediaType` | Tipo de contenido (consulte _Constantes de MediaType_ a continuación) | Sí |

   **`StreamType`Constantes de:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo de emisión de vídeo bajo demanda |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo de emisión de contenido en directo |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo de emisión del contenido lineal |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo de emisión de audio a la carta. |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo de emisión de audiolibro. |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo de emisión de podcast. |

   **`MediaType`Constantes de:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `ADBMediaTypeAudio` | Tipo de contenido para emisiones de audio. |
   | `ADBMediaTypeVideo` | Tipo de contenido para emisiones de vídeo. |

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

   Opcionalmente, se pueden adjuntar objetos de metadatos de vídeo estándar o personalizados a la sesión de seguimiento de vídeo mediante el uso de variables de datos de contexto.

   * **Metadatos de vídeo estándar**

      * [Implementación de metadatos estándar en iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Claves de metadatos de vídeo**

         [Claves de metadatos de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consulte la lista completa de metadatos de vídeo aquí: [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md).
      >[!NOTE]
      >
      >No es obligatorio adjuntar el objeto de metadatos de vídeo estándar al objeto de contenidos.

   * **Metadatos personalizados**

      Cree un objeto de variable para las variables personalizadas y rellénelo con los datos de este vídeo. Por ejemplo:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Realice un seguimiento de la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, invoque `trackSessionStart` en la instancia de Media Heartbeat.

   >[!TIP]
   >
   >El segundo valor es el nombre de objeto de metadatos de video personalizado que ha creado en el paso 2.

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
   >Si no utiliza metadatos de vídeo personalizados, envíe un objeto vacío para el argumento `data` en `trackSessionStart`, tal y como se muestra en la línea comentada del ejemplo para iOS anterior.

1. **Realizar un seguimiento del inicio real de la reproducción**

   Identifique el evento del reproductor de vídeo para el principio de la reproducción, cuando se renderice el primer fotograma del vídeo en la pantalla e invoque `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Realizar un seguimiento de la finalización de la reproducción**

   Identifique el evento del reproductor de vídeo para la finalización de la reproducción, cuando el usuario ha visto el contenido hasta el final e invoque `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Realizar un seguimiento del final de la sesión**

   Identifique el evento del reproductor de vídeo para la descarga o cierre de la reproducción, cuando el usuario cierra o completa la descarga e invoque `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento de vídeo. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Las demás llamadas de la API `track*` se pasan por alto después de `trackSessionEnd` (salvo `trackSessionStart` en una nueva sesión de seguimiento de vídeo).

1. **Rastrear todos los escenarios de pausa posibles**

   Identifique el evento del reproductor en el que se pause el vídeo e invoque `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Pausar escenarios**

   Identifique cualquier situación en la que se pausará el reproductor y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * El usuario hace una pausa explícita en la aplicación.
   * El reproductor se pone en estado de pausa.
   * (*Aplicaciones móviles*): El usuario pone la aplicación en segundo plano, pero desea que la aplicación mantenga abierta la sesión.
   * (*Aplicaciones móviles*): Se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se ponga en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el vídeo desde donde se produjo la interrupción.

1. Identifique el evento del reproductor en el que el vídeo se reproduzca o se reanude e invoque `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >Puede ser el mismo origen de evento empleado en el paso 4. Asegúrese de que cada llamada de API a `trackPause()` esté vinculada a continuación con una llamada de API a `trackPlay()` cuando se reanude la reproducción de vídeo.

Consulte lo siguiente para obtener más información sobre el seguimiento de la reproducción principal:

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para iOS para ver un ejemplo de seguimiento completo.
