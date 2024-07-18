---
title: Seguimiento de la reproducción de contenido explicado
description: "Obtenga información sobre el seguimiento de la reproducción central, incluido el seguimiento de la carga, el inicio, la pausa y la finalización de medios. "
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0d53e62069a65b252e004e21943ecdbd011a3658
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 99%

---

# Información general de seguimiento{#tracking-overview}

Esta documentación abarca el seguimiento en la versión 2.x del SDK.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Eventos del reproductor

El seguimiento de la reproducción principal incluye el seguimiento de la carga, el inicio, la pausa y la finalización de los contenidos. Aunque no es obligatorio, el seguimiento del almacenamiento en búfer y la búsqueda también son componentes principales utilizados para rastrear la reproducción del contenido. En la API del reproductor de contenidos, identifique los eventos del reproductor correspondientes a las llamadas de seguimiento del Media SDK, y codifique los controladores de eventos para invocar las API de seguimiento y rellenar las variables necesarias y opcionales.

### Carga del contenido

* Crear el objeto de contenido.
* Rellenar metadatos
* Invocar `trackSessionStart`; Por ejemplo: `trackSessionStart(mediaObject, contextData)`

### Inicio del contenido

* La llamada `trackPlay`

### Pausa/Reanudación

* La llamada `trackPause`
* Invocar `trackPlay`   _cuando se reanude la reproducción_

### Finalización del contenido

* La llamada `trackComplete`

### Cancelación del contenido

* La llamada `trackSessionEnd`

### Inicio de arrastre de cabezal de reproducción

* La llamada `trackEvent(SeekStart)`

### Fin de arrastre de cabezal de reproducción

* Llamar a `trackEvent(SeekComplete)`
Cancelar cambios

### Inicio del almacenamiento en búfer

* La llamada `trackEvent(BufferStart);`

### Finalización del almacenamiento en búfer

* La llamada `trackEvent(BufferComplete);`


## Implementación {#implement}

1. **Configuración inicial del seguimiento**: identifique cuándo el usuario activa la reproducción (cuando hace clic en reproducción o reproducción automática) y cree una instancia de `MediaObject` con la información del contenido: nombre, ID y duración del contenido, así como el tipo de emisión.

   **`MediaObject`Referencia:**

   | Nombre de variable | Descripción | Requerido |
   |---|---|---|
   | `name` | Nombre de contenido | Sí |
   | `mediaid` | Identificador único de contenido | Sí |
   | `length` | Longitud de contenido | Sí |
   | `streamType` | Tipo de emisión | Sí |
   | `mediaType` | Tipo de contenido (contenido de audio o vídeo) | Sí |

   **`StreamType`Constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `VOD` | Tipo de emisión de vídeo bajo demanda. |
   | `LIVE` | Tipo de emisión de contenido en directo. |
   | `LINEAR` | Tipo de emisión de contenido lineal. |
   | `AOD` | Tipo de emisión de audio a la carta. |
   | `AUDIOBOOK` | Tipo de emisión de audiolibro. |
   | `PODCAST` | Tipo de emisión de podcast. |

   **`MediaType`Constantes:**

   | Nombre de la constante | Descripción |
   |---|---|
   | `Audio` | Tipo de contenido para emisiones de audio. |
   | `Video` | Tipo de contenido para emisiones de vídeo. |

   El formato general para crear `MediaObject` es `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Adjuntar metadatos**: Opcionalmente, se pueden adjuntar objetos de metadatos estándar o personalizados a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos estándar -**

     >[!NOTE]
     >
     >No es obligatorio adjuntar el objeto de metadatos estándar al objeto de contenidos.

     Cree una instancia de un objeto de metadatos estándar, rellene las variables deseadas y establezca el objeto de metadatos en el objeto de Media Heartbeat.

     Consulte la lista completa de metadatos aquí: [Parámetros de audio y vídeo.](../../implementation/variables/audio-video-parameters.md)

   * **Metadatos personalizados**: cree un objeto de variable para las variables personalizadas y rellénelo con los datos de este contenido.

1. **Seguimiento de la intención de inicio de reproducción**: para comenzar el seguimiento de una sesión, invoque `trackSessionStart` en la instancia de Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos, y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >Si no utiliza metadatos personalizados, envíe un objeto vacío para el argumento `data` en `trackSessionStart`.

1. **Seguimiento del inicio real de la reproducción**: identifique el evento del reproductor de contenidos para el comienzo de la reproducción (cuando el primer fotograma del contenido aparece en pantalla) e invoque `trackPlay`.

1. **Seguimiento de la finalización de la reproducción**: identifique el evento del reproductor de contenidos para la finalización de la reproducción (cuando el usuario ha visto el contenido hasta el final) e invoque `trackComplete`.

1. **Seguimiento del final de la sesión**: identifique el evento del reproductor de contenidos para la descarga/cierre de la reproducción (el usuario cierra el contenido, o este finalizó y se descargó) e invoque `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Las demás llamadas de la API `track*` se pasan por alto después de `trackSessionEnd` (salvo `trackSessionStart` en una nueva sesión de seguimiento).

1. **Seguimiento de todas las situaciones de pausa posibles**: identifique el evento del reproductor de contenidos para la pausa e invoque `trackPause`.

   **Situaciones de pausa**: identifique todas las situaciones en las que puede pausarse el reproductor y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * El usuario hace una pausa explícita en la aplicación.
   * El reproductor se pone en estado de pausa.
   * (*Aplicaciones móviles*): El usuario pone la aplicación en segundo plano, pero desea que la aplicación mantenga abierta la sesión.
   * (*Aplicaciones móviles*): Se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se ponga en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el contenido desde donde se produjo la interrupción.

1. Identifique el evento del reproductor para la reproducción o reanudación después de la pausa e invoque `trackPlay`.

   >[!TIP]
   >
   >Puede ser el mismo origen de evento empleado en el paso 4. Asegúrese de que cada llamada de API `trackPause()` esté emparejada con una llamada posterior a la API `trackPlay()` cuando se reanude la reproducción.

1. Escuche los eventos de llamada a otro punto de la reproducción del reproductor de contenidos. En la notificación del evento de inicio de la llamada a otro punto del contenido, utilice el evento `SeekStart` para realizar el seguimiento.
1. En la notificación de finalización de llamada a otro punto del contenido del reproductor, realice un seguimiento del final de la llamada a otro punto del contenido utilizando el evento `SeekComplete`.
1. Escuche los eventos de almacenamiento en búfer de reproducción procedentes del reproductor de contenidos y, cuando reciba la notificación del evento Inicio de almacenamiento en búfer, rastree el almacenamiento en búfer mediante el evento `BufferStart`.
1. En la notificación de Finalización de almacenamiento en búfer procedente del reproductor de contenidos, rastree el final del almacenamiento en búfer con el evento `BufferComplete`.

Consulte ejemplos de cada paso en los siguientes temas específicos de la plataforma y observe los reproductores de muestra incluidos en los SDK.

Para ver un ejemplo sencillo de seguimiento de reproducción, consulte este uso del SDK de JavaScript 2.x en un reproductor HTML5:

```js
/* Call on media start */
if (e.type == "play") {

    // Check for start of media
    if (!sessionStarted) {
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>,
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/
        var mediaInfo = MediaHeartbeat.createMediaObject(
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration,
          MediaHeartbeat.StreamType.VOD);

        /* Set custom context data */
        var customVideoMetadata = {
            isUserLoggedIn: "false",
            tvStation: "Sample TV station",
            programmer: "Sample programmer"
        };

        /* Set standard video metadata */     
        var standardVideoMetadata = {};
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     

        // Start Session
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    

        // Track play
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     

    } else {
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    }
};

/* Call on video complete */
if (e.type == "ended") {
    console.log("video ended");
    this.mediaHeartbeat.trackComplete();
    this.mediaHeartbeat.trackSessionEnd();
    sessionStarted = false;     
};

/* Call on pause */
if (e.type == "pause") {
    this.mediaHeartbeat.trackPause();
};

/* Call on scrub start */
if (e.type == "seeking") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};

/* Call on scrub stop */
if (e.type == "seeked") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};

/* Call on buffer start */
if (e.type == "buffering") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == "buffered") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## Validación {#validate}

Para obtener información sobre la validación de su implementación de *legado*, consulte [Validación de legado.](/help/legacy/validation/validation-overview.md)
