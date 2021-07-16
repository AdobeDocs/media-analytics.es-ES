---
title: Obtenga información sobre cómo rastrear la reproducción principal en Android
description: Obtenga información sobre cómo implementar el seguimiento principal mediante Media SDK en Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 97%

---

# Seguimiento de reproducción principal en Android{#track-core-playback-on-android}

Esta documentación abarca el seguimiento en la versión 2.x del SDK.
>[!IMPORTANT]
>Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador de 1.x para Android aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identifique el momento en que el usuario desencadena la intención de reproducir (cuando hace clic en reproducir o la reproducción automática está activada) y cree una instancia de `MediaObject`.

   [API de createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del contenido | Sí |
   | `mediaId` | Identificador único del contenido | Sí |
   | `length` | Duración del contenido | Sí |
   | `streamType` | Tipo de flujo (consulte _Constantes de StreamType_ a continuación) | Sí |
   | `mediaType` | Tipo de contenido (consulte _Constantes de MediaType_ a continuación) | Sí |

   **`StreamType`Constantes de:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `LIVE` | Tipo de emisión de contenido en directo. |
   | `LINEAR` | Tipo de emisión de contenido lineal. |
   | `AOD` | Tipo de emisión de audio a la carta. |
   | `AUDIOBOOK` | Tipo de emisión de audiolibro. |
   | `PODCAST` | Tipo de emisión de podcast. |

   **`MediaType`Constantes de:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `Audio` | Tipo de contenido para emisiones de audio. |
   | `Video` | Tipo de contenido para emisiones de vídeo. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Adjuntar metadatos**

   Opcionalmente, se pueden adjuntar objetos de metadatos estándar o personalizados a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos estándar**

      [Implementación de metadatos estándar en Android](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >No es obligatorio adjuntar el objeto de metadatos estándar al objeto de contenidos.

      * Referencia de API de claves de metadatos de medios: [Claves de metadatos estándar de Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Consulte el conjunto completo de metadatos de vídeo disponibles aquí: [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md).
   * **Metadatos personalizados**

      Cree un diccionario para las variables personalizadas y rellénelo con los datos de estos contenidos. Por ejemplo:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>();
      mediaMetadata.put("isUserLoggedIn", "false");
      mediaMetadata.put("tvStation", "Sample TV Station");
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Realice un seguimiento de la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, invoque `trackSessionStart` en la instancia de Media Heartbeat. Por ejemplo:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
   }
   ```

   >[!TIP]
   >
   >El segundo valor es el nombre de objeto de metadatos de contenido personalizado que ha creado en el paso 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos del contenido y para calcular la métrica de QoS (tiempo entre `trackSessionStart` () y `trackPlay`).

   >[!NOTE]
   >
   >Si no utiliza metadatos de contenido personalizados, envíe un objeto vacío para el segundo argumento en `trackSessionStart`.

1. **Realizar un seguimiento del inicio real de la reproducción**

   Identifique el evento del reproductor de contenidos para el principio de la reproducción de contenido, cuando se renderice el primer fotograma del contenido en la pantalla, e invoque `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) {
       _heartbeat.trackPlay();
   }
   ```

1. **Realizar un seguimiento de la finalización de la reproducción**

   Identifique el evento del reproductor de contenidos para la finalización de la reproducción del contenido cuando el usuario ha visto el contenido hasta el final e invoque `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) {
       _heartbeat.trackComplete();
   }
   ```

1. **Realizar un seguimiento del final de la sesión**

   Identifique el evento del reproductor de contenidos para la carga o el cierre de la reproducción de contenido, cuando el usuario cierra o se completa la descarga, e invoque `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd();
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento de contenido. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Las demás llamadas de la API `track*` se ignoran después de `trackSessionEnd` (salvo `trackSessionStart` en una nueva sesión de seguimiento de contenido).

1. **Rastrear todos los escenarios de pausa posibles**

   Identifique el evento desde el reproductor de contenido para que los contenidos se detengan e invoque `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause();
   }
   ```

   **Pausar escenarios**

   Identifique cualquier situación en la que se pausará el reproductor y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * El usuario hace una pausa explícita en la aplicación.
   * El reproductor se pone en estado de pausa.
   * (*Aplicaciones móviles*): El usuario pone la aplicación en segundo plano, pero desea que la aplicación mantenga abierta la sesión.
   * (*Aplicaciones móviles*): Se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se ponga en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el contenido desde donde se produjo la interrupción.

1. Identifique el evento del reproductor para la reproducción o reanudación de contenido después de la pausa e invoque `trackPlay`.

   ```java
   // trackPlay()
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay();
   }
   ```

   >[!TIP]
   >
   >Puede ser el mismo origen de evento empleado en el paso 4. Asegúrese de que cada llamada de API `trackPause()` esté emparejada con una llamada posterior a la API `trackPlay()` cuando se reanude la reproducción del contenido.

Consulte lo siguiente para obtener más información sobre el seguimiento de la reproducción principal:

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para Android para ver un ejemplo de seguimiento completo.
