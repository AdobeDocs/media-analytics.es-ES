---
title: Seguimiento de reproducción principal con JavaScript 2.x
description: En este tema se describe cómo implementar el seguimiento principal mediante el SDK de medios en un explorador con aplicaciones JavaScript 2.x.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
translation-type: ht
source-git-commit: 815965d1cd41e73e50666a89f4a7c450af5022da
workflow-type: ht
source-wordcount: '688'
ht-degree: 100%

---


# Seguimiento de reproducción principal con JavaScript 2.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Esta documentación abarca el seguimiento en la versión 2.x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identifique el momento en que el usuario desencadena la intención de reproducir (cuando hace clic en reproducir o la reproducción automática está activada) y cree una instancia de `MediaObject`.

   [API de createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del contenido | Sí |
   | `mediaid` | Identificador único del contenido | Sí |
   | `length` | Duración del contenido | Sí |
   | `streamType` | Tipo de flujo (consulte _Constantes de StreamType_ a continuación) | Sí |
   | `mediaType` | Tipo de contenido (consulte _Constantes de MediaType_ a continuación) | Sí |

   **`StreamType`Constantes de:**

   | Nombre de la constante | Descripción   |
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
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Adjuntar metadatos**

   Opcionalmente, se pueden adjuntar objetos de metadatos estándar o personalizados a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos estándar**

      [Implementación de metadatos estándar en JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >No es obligatorio adjuntar el objeto de metadatos estándar al objeto de contenidos.

      * Referencia de API de claves de metadatos de contenidos: [Claves de metadatos estándar de JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consulte el conjunto completo de metadatos disponibles aquí: [Parámetros de audio y vídeo](/help/metrics-and-metadata/audio-video-parameters.md).
   * **Metadatos personalizados**

      Cree un objeto de variable para las variables personalizadas y rellénelo con los datos de estos contenidos. Por ejemplo:

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```


1. **Realice un seguimiento de la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, invoque a `trackSessionStart` en la instancia de Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >El segundo valor es el nombre de objeto de metadatos de contenido personalizado que ha creado en el paso 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos, y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >Si no utiliza metadatos personalizados, envíe un objeto vacío para el argumento `data` en `trackSessionStart`, tal y como se muestra en la línea comentada del ejemplo para iOS anterior.

1. **Realizar un seguimiento del inicio real de la reproducción**

   Identifique el evento del reproductor de contenido para el principio de la reproducción, cuando se renderice el primer fotograma del contenido en la pantalla, e invoque `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Realizar un seguimiento de la finalización de la reproducción**

   Identifique el evento del reproductor de contenido para la finalización de la reproducción cuando el usuario ha visto el contenido hasta el final e invoque `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Realizar un seguimiento del final de la sesión**

   Identifique el evento del reproductor de contenido para la carga o el cierre de la reproducción, cuando el usuario cierra o se completa la descarga, e invoque `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Las demás llamadas de la API `track*` se pasan por alto después de `trackSessionEnd` (salvo `trackSessionStart` en una nueva sesión de seguimiento).

1. **Rastrear todos los escenarios de pausa posibles**

   Identifique el evento desde el reproductor de contenidos para pausar e invocar `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pausar escenarios**

   Identifique cualquier situación en la que se pausará el reproductor de contenido y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * El usuario hace una pausa explícita en la aplicación.
   * El reproductor se pone en estado de pausa.
   * (*Aplicaciones móviles*): El usuario pone la aplicación en segundo plano, pero desea que la aplicación mantenga abierta la sesión.
   * (*Aplicaciones móviles*): Se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se ponga en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el contenido desde donde se produjo la interrupción.

1. Identifique el evento del reproductor para la reproducción o reanudación después de la pausa e invoque `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Puede ser el mismo origen de evento empleado en el paso 4. Asegúrese de que cada llamada de API `trackPause()` esté emparejada con una llamada posterior a la API `trackPlay()` cuando se reanude la reproducción.

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK de JavaScript para ver un ejemplo de seguimiento completo.
