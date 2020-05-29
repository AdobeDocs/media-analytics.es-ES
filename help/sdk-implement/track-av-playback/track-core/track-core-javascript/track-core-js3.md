---
title: Rastree la reproducción principal mediante JavaScript v3.x
description: En este tema se describe cómo implementar el seguimiento principal mediante el SDK de medios en un navegador mediante aplicaciones JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 40d75ef32596e915ac07c173b4595bb78db3688d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 81%

---


# Rastree la reproducción principal mediante JavaScript 3.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Esta documentación abarca el seguimiento en la versión 3.x del SDK. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs](/help/sdk-implement/download-sdks.md)

1. **Configuración de seguimiento inicial**

   Identifique el momento en que el usuario desencadena la intención de reproducir (cuando hace clic en reproducir o la reproducción automática está activada) y cree una instancia de `MediaObject`.

   [API de createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nombre de variable | Tipo | Descripción |
   | --- | --- | --- |
   | `name` | string | Cadena no vacía que indica el nombre del medio. |
   | `id` | string | Cadena no vacía que denota identificador de medios único. |
   | `length` | entero | Número positivo que indica la longitud del medio en segundos. Utilice 0 si se desconoce la longitud. |
   | `streamType` | string |  |
   | `mediaType` |  | Tipo de medio (audio o vídeo). |

   **`StreamType`Constantes de:**

   | Nombre de la constante | Descripción   |
   |---|---|
   | `VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `AOD` | Tipo de emisión de audio a la carta. |

   **`MediaType`Constantes de:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `Audio` | Tipo de contenido para emisiones de audio. |
   | `Video` | Tipo de contenido para emisiones de vídeo. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Adjuntar metadatos**

   Si lo desea, adjunte metadatos estándar o personalizados a la sesión de seguimiento mediante variables de datos de contexto.

   * **Metadatos estándar**

      >[!NOTE]
      >
      >La adición de metadatos estándar es opcional.

      * Referencia de API de claves de metadatos de contenidos: [Claves de metadatos estándar de JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consulte el conjunto completo de metadatos disponibles aquí: [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md).
   * **Metadatos personalizados**

      Cree un objeto de variable para las variables personalizadas y rellénelo con los datos de estos contenidos. Por ejemplo:

      ```js
      /* Set context data */
       var contextData = {};
      
       //Standard metadata
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
      
       //Custom metadata
       contextData["isUserLoggedIn"] = "false";
       contextData["tvStation"] = "Sample TV Station";
      ```


1. **Realice un seguimiento de la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, invoque a `trackSessionStart` en la instancia de Media Heartbeat:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos, y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >If you are not using contextData, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Realizar un seguimiento del inicio real de la reproducción**

   Identifique el evento del reproductor de contenido para el principio de la reproducción, cuando se renderice el primer fotograma del contenido en la pantalla, e invoque `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Realizar un seguimiento de la finalización de la reproducción**

   Identifique el evento del reproductor de contenido para la finalización de la reproducción cuando el usuario ha visto el contenido hasta el final e invoque `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Realizar un seguimiento del final de la sesión**

   Identifique el evento del reproductor de contenido para la carga o el cierre de la reproducción, cuando el usuario cierra o se completa la descarga, e invoque `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Las demás llamadas de la API `track*` se pasan por alto después de `trackSessionEnd` (salvo `trackSessionStart` en una nueva sesión de seguimiento).

1. **Rastrear todos los escenarios de pausa posibles**

   Identifique el evento desde el reproductor de contenidos para pausar e invocar `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Pausar escenarios**

   Identifique cualquier situación en la que se pausará el reproductor de contenido y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * El usuario hace una pausa explícita en la aplicación.
   * El reproductor se pone en estado de pausa.
   * (*Aplicaciones móviles*): El usuario pone la aplicación en segundo plano, pero desea que la aplicación mantenga abierta la sesión.
   * (*Aplicaciones móviles*): Se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se ponga en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el contenido desde donde se produjo la interrupción.

1. Identifique el evento del reproductor para la reproducción o reanudación después de la pausa e invoque `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Puede ser el mismo origen de evento empleado en el paso 4. Asegúrese de que cada llamada de API `trackPause()` esté emparejada con una llamada posterior a la API `trackPlay()` cuando se reanude la reproducción.

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK de JavaScript para ver un ejemplo de seguimiento completo.
