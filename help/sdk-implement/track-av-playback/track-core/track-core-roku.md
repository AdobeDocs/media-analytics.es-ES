---
title: Aprenda a rastrear la reproducción principal en Roku
description: Obtenga información sobre cómo implementar el seguimiento principal mediante Media SDK en Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d7cb36c2dd6b35da4531ca975c7fc730e387b750
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 90%

---

# Seguimiento de reproducción principal en Roku{#track-core-playback-on-roku}

Esta documentación abarca el seguimiento en la versión 2.x del SDK.

>[!IMPORTANT]
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK](/help/sdk-implement/download-sdks.md).

1. **Configuración de seguimiento inicial**

   Identifique el momento en que el usuario desencadena la intención de reproducir (cuando hace clic en reproducir o la reproducción automática está activada) y cree una instancia de `MediaObject`.

   **`MediaObject`Referencia de:**

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del vídeo | Sí |
   | `mediaid` | Identificador único de vídeo | Sí |
   | `length` | Duración del vídeo | Sí |
   | `streamType` | Tipo de flujo (consulte _Constantes de StreamType_ a continuación) | Sí |
   | `mediaType` | Tipo de contenido (consulte _Constantes de MediaType_ a continuación) | Sí |

   **`StreamType`Constantes de:**

   | Nombre de la constante | Descripción   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `MEDIA_STREAM_TYPE_LIVE` | Tipo de emisión de contenido en directo. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Tipo de emisión de contenido lineal. |
   | `MEDIA_STREAM_TYPE_AOD` | Tipo de emisión de audio a la carta. |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Tipo de emisión de audiolibro. |
   | `MEDIA_STREAM_TYPE_PODCAST` | Tipo de emisión de podcast. |

   **`MediaType`Constantes de:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Tipo de contenido para emisiones de audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Tipo de contenido para emisiones de vídeo. |

   **Cree un objeto de información multimedia para vídeo con contenido de VOD:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   O bien

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Cree un objeto de información multimedia para vídeo con contenido de AOD:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>",
    "<MEDIA_ID>",
    600,
    ADBMobile().MEDIA_STREAM_TYPE_AOD,
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   O bien

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Adjuntar metadatos**

   Opcionalmente, se pueden adjuntar objetos de metadatos estándar o personalizados a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos estándar**

   [Implementación de metadatos estándar en Roku ](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >No es obligatorio adjuntar el objeto de metadatos de vídeo estándar al objeto de contenidos.

   * **Metadatos personalizados**

      Cree un objeto de variable para las variables personalizadas y rellénelo con los datos de este vídeo. Por ejemplo:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Realice un seguimiento de la intención de iniciar la reproducción**

   Para empezar a realizar el seguimiento de una sesión multimedia, invoque a `trackSessionStart` en la instancia de Media Heartbeat:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >El segundo valor es el nombre de objeto de metadatos de video personalizado que ha creado en el paso 2.

   >[!IMPORTANT]
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos del vídeo y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >Si no utiliza metadatos de vídeo personalizados, envíe un objeto vacío para el argumento `data` en `trackSessionStart`, tal y como se muestra en la línea comentada del ejemplo para iOS anterior.

1. **Realizar un seguimiento del inicio real de la reproducción**

   Identifique el evento del reproductor de vídeo para el principio de la reproducción, cuando se renderice el primer fotograma del vídeo en la pantalla e invoque `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Actualizar valor del cabezal de reproducción**

   Cuando el cabezal de reproducción de contenido cambie, notifique al SDK llamando a la API `mediaUpdatePlayhead` . En el caso de vídeo bajo demanda (VOD), el valor se especifica segundos después del comienzo del elemento multimedia. Para la transmisión en directo, el valor se especifica como el número de segundos desde la medianoche UTC de ese día.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **Realizar un seguimiento de la finalización de la reproducción**

   Identifique el evento del reproductor de vídeo para la finalización de la reproducción, cuando el usuario ha visto el contenido hasta el final e invoque `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Realizar un seguimiento del final de la sesión**

   Identifique el evento del reproductor de vídeo para la descarga o cierre de la reproducción, cuando el usuario cierra o completa la descarga e invoque `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` marca el final de una sesión de seguimiento de vídeo. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Las demás llamadas de la API `track*` se pasan por alto después de `trackSessionEnd` (salvo `trackSessionStart` en una nueva sesión de seguimiento de vídeo).

1. **Rastrear todos los escenarios de pausa posibles**

   Identifique el evento del reproductor en el que se pause el vídeo e invoque `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausar escenarios**

   Identifique cualquier situación en la que se pausará el reproductor y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * El usuario hace una pausa explícita en la aplicación.
   * El reproductor se pone en estado de pausa.
   * (*Aplicaciones móviles*): El usuario pone la aplicación en segundo plano, pero desea que la aplicación mantenga abierta la sesión.
   * (*Aplicaciones móviles*): Se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se ponga en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el vídeo desde donde se produjo la interrupción.

1. Identifique el evento del reproductor en el que el vídeo se reproduzca o se reanude e invoque `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Puede ser el mismo origen de evento empleado en el paso 4. Asegúrese de que cada llamada de API a `trackPause()` esté vinculada a continuación con una llamada de API a `trackPlay()` cuando se reanude la reproducción de vídeo.

* Situaciones de seguimiento: [Reproducción de VOD sin anuncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reproductor de muestra incluido con el SDK para Roku para ver un ejemplo de seguimiento completo.
