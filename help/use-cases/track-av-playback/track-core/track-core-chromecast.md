---
title: Cómo rastrear la reproducción principal en Chromecast
description: Aprenda a implementar el seguimiento principal mediante Media SDK en Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 100%

---

# Seguimiento de reproducción principal en Chromecast {#track-core-playback-on-chromecast}

Esta documentación abarca el seguimiento en la versión 2.x del SDK.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](/help/getting-started/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identifique el momento en que el usuario desencadena la intención de reproducir (cuando hace clic en reproducir o la reproducción automática está activada) y cree una instancia de `MediaObject`.

   **`MediaObject`Referencia de API:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>);
   ```

   Constantes de **`StreamType`:**

   [Medios de ADBMobile](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   Constantes de **`MediaType`:**

   [Medios de ADBMobile](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Adjuntar metadatos de vídeo**

   Opcionalmente, se pueden adjuntar objetos de metadatos de vídeo estándar o personalizados a la sesión de seguimiento de vídeo mediante el uso de variables de datos de contexto.

   * **Metadatos de vídeo estándar**

      [Implementación de metadatos estándar en Chromecast](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >No es obligatorio adjuntar el objeto de metadatos de vídeo estándar al objeto de contenidos.

   * **Metadatos personalizados**

      Cree un objeto de variable para las variables personalizadas y rellénelo con los datos de este vídeo. Por ejemplo:

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```

1. **Realice un seguimiento de la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión de contenidos, invoque a [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) en el objeto `media`.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos del vídeo y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >El segundo valor es el nombre de objeto de metadatos de video personalizado que ha creado en el paso 2. Si no utiliza metadatos de vídeo personalizados, envíe un objeto vacío para el argumento `data` en `trackSessionStart`, tal y como se muestra en la línea comentada del ejemplo para iOS anterior.

1. **Realizar un seguimiento del inicio real de la reproducción**

   Identifique el evento del reproductor de vídeo para el principio de la reproducción, cuando se renderice el primer fotograma del vídeo en la pantalla e invoque [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Actualización del valor del cabezal de reproducción**

   Actualice la posición de `mediaUpdatePlayhead` varias veces cuando cambia el cabezal de reproducción. <br /> Para el vídeo bajo demanda (VOD), el valor se especifica segundos después del comienzo del elemento de medios. <br /> Para el streaming en directo, si el reproductor no proporciona información acerca de la duración del contenido, el valor se puede especificar como el número de segundos desde la medianoche (UTC) de ese día. <br /> Nota: Cuando se utilizan marcadores de progreso, la duración del contenido es obligatoria, y el cabezal de reproducción debe actualizarse como número de segundos desde el principio del elemento de medios, empezando por 0.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **Realizar un seguimiento de la finalización de la reproducción**

   Identifique el evento del reproductor de vídeo para la finalización de la reproducción, cuando el usuario ha visto el contenido hasta el final e invoque [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Realizar un seguimiento del final de la sesión**

   Identifique el evento del reproductor de vídeo para la descarga o cierre de la reproducción, cuando el usuario cierra o completa la descarga e invoque [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento de vídeo. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Las demás llamadas de la API `track*` se pasan por alto después de `trackSessionEnd` (salvo `trackSessionStart` en una nueva sesión de seguimiento de vídeo).

1. **Rastrear todos los escenarios de pausa posibles**

   Identifique el evento del reproductor en el que se pause el vídeo e invoque [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausar escenarios**

   Identifique cualquier situación en la que se pausará el reproductor y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * El usuario hace una pausa explícita en la aplicación.
   * El reproductor se pone en estado de pausa.
   * (*Aplicaciones móviles*): El usuario pone la aplicación en segundo plano, pero desea que la aplicación mantenga abierta la sesión.
   * (*Aplicaciones móviles*): Se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se ponga en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el vídeo desde donde se produjo la interrupción.

1. Identifique el evento del reproductor en el que el vídeo se reproduzca o se reanude e invoque [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Puede ser el mismo origen de evento empleado en el paso 4. Asegúrese de que cada llamada de API a `trackPause()` esté vinculada a continuación con una llamada de API a `trackPlay()` cuando se reanude la reproducción de vídeo.

* Situaciones de seguimiento: [reproducción de VOD sin anuncios](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para Chromecast para ver un ejemplo de seguimiento completo.
