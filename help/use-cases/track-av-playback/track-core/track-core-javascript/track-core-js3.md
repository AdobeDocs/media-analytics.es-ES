---
title: Aprenda a realizar un seguimiento de la reproducción del núcleo mediante JavaScript v3.x
description: Aprenda a implementar el seguimiento del núcleo mediante Media SDK en un explorador utilizando aplicaciones JavaScript 3.x.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 87%

---

# Seguimiento de reproducción principal con JavaScript 3.x{#track-core-playback-on-javascript}

Esta documentación abarca el seguimiento en la versión 3.x del SDK.

>[!IMPORTANT]
>
>Si va implementar cualquier versión anterior del SDK, puede descargar las guías del desarrollador aquí: [Descargar SDK](/help/getting-started/download-sdks.md)

1. **Configuración de seguimiento inicial**

   Identifique el momento en que el usuario desencadena la intención de reproducir (cuando hace clic en reproducir o la reproducción automática está activada) y cree una instancia de `MediaObject`.

   [API de createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nombre de variable | Tipo | Descripción |
   | --- | --- | --- |
   | `name` | string | Cadena no vacía que indica el nombre de los medios. |
   | `id` | string | Cadena no vacía que indica un identificador de medios único. |
   | `length` | number | Número positivo que indica la longitud de los medios en segundos. Utilice 0 si se desconoce la longitud. |
   | `streamType` | string |   |
   | `mediaType` | | Tipo de medios (audio o vídeo). |

   **`StreamType`Constantes:**

   | Nombre de la constante | Descripción   |
   |---|---|
   | `VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `AOD` | Tipo de emisión de audio a la carta. |

   **`MediaType`Constantes:**

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

   Opcionalmente, se pueden adjuntar metadatos estándar o personalizados a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos estándar**

     >[!NOTE]
     >
     >La adición de metadatos estándar es opcional.

      * Referencia de API de claves de metadatos de contenidos: [Claves de metadatos estándar de JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        Consulte el conjunto completo de metadatos disponibles aquí: [Parámetros de audio y vídeo](/help/implementation/variables/audio-video-parameters.md).

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
   >Si no utiliza contextData, envíe un objeto vacío para el argumento `data` en `trackSessionStart`.

1. **Realizar un seguimiento del inicio real de la reproducción**

   Identifique el evento del reproductor de contenido para el principio de la reproducción, cuando se renderice el primer fotograma del contenido en la pantalla, e invoque `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Actualización de valor del cabezal de reproducción**

   Cuando el cabezal de reproducción de contenido cambie, notifique a SDK llamando a la API `mediaUpdatePlayhead`. <br /> Para el vídeo bajo demanda (VOD), el valor se especifica segundos después del comienzo del elemento de medios. <br /> Para el streaming en vivo, si el reproductor no proporciona información acerca de la duración del contenido, el valor se puede especificar como el número de segundos desde la medianoche (UTC) de ese día.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Tenga en cuenta lo siguiente al llamar a la API `tracker.updatePlayhead`:
   >* Cuando se utilizan marcadores de progreso, la duración del contenido es obligatoria y el cabezal de reproducción debe actualizarse como número de segundos desde el principio del elemento de medios, empezando por 0.
   >* Al utilizar los SDK de medios, debe llamar a la API `tracker.updatePlayhead` al menos una vez por segundo.

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

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK de JavaScript para ver un ejemplo de seguimiento completo.
