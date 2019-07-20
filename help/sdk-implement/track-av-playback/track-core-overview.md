---
seo-title: Información general de seguimiento
title: Información general de seguimiento
uuid: 7 b 8 e 2 f 76-bc 4 e -4721-8933-3 e 4453 b 01788
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Tracking Overview{#tracking-overview}

>[!IMPORTANT]
>
>Esta documentación abarca el seguimiento en la versión 2. x del SDK. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

## Eventos del reproductor

El seguimiento de la reproducción principal incluye el seguimiento de la carga, el inicio, la pausa y la finalización de los medios. Aunque no es obligatorio, el seguimiento del almacenamiento en búfer y de la llamada a otro punto del contenido también son componentes básicos utilizados para el seguimiento de la reproducción de contenido. En la API del reproductor de medios, identifique los eventos del reproductor correspondientes a las llamadas de seguimiento del Media SDK, y codifique los controladores de eventos para invocar las API de seguimiento y rellenar las variables necesarias y opcionales.

### Carga del medio

* Crear el objeto de medio.
* Rellenar los metadatos.
* Call `trackSessionStart`; For example: `trackSessionStart(mediaObject, contextData)`

### Inicio del medio

* La llamada `trackPlay`

### Pausa/Reanudación

* La llamada `trackPause`
* Call `trackPlay`   _when playback resumes_

### Finalización del medio

* La llamada `trackComplete`

### Cancelación del medio

* La llamada `trackSessionEnd`

### Inicio de arrastre de cabezal de reproducción

* La llamada `trackEvent(SeekStart)`

### Fin de arrastre de cabezal de reproducción

* La llamada `trackEvent(SeekComplete)`

### Cuando comienza el almacenamiento en búfer

* La llamada `trackEvent(BufferStart);`

### Cuando finaliza el almacenamiento en búfer

* La llamada `trackEvent(BufferComplete);`

>[!TIP]
>
>La posición del cursor de reproducción se establece como parte del código de configuración y configuración. For more information about `getCurrentPlayheadTime`, see [Overview: General Implementation Guidelines.](../../sdk-implement/setup/setup-overview.md#section_965A3B699A8248DDB9B2B3EA3CC20E41)

## Implementación {#section_BB217BE6585D4EDEB34C198559575004}

1. **Configuración inicial del seguimiento**: identifique cuándo el usuario activa la reproducción (cuando hace clic en reproducción o reproducción automática) y cree una instancia de `MediaObject` con la información del medio: nombre, ID y duración del contenido, así como el tipo de emisión.

   **`MediaObject`reference:**

   | Nombre de variable | Descripción | Requerido |
   |---|---|---|
   | `name` | Nombre del contenido | Sí |
   | `mediaid` | Identificador único del contenido | Sí |
   | `length` | Duración del contenido | Sí |
   | `streamType` | Tipo de emisión | Sí |
   | `mediaType` | Tipo de medio (contenido de audio o vídeo) | Sí |

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

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Adjuntar metadatos**: opcionalmente, se pueden adjuntar objetos de metadatos estándar o personalizados a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos estándar**

      >[!NOTE]
      >
      >Incluir el objeto de metadatos estándar en el objeto multimedia es opcional.

      Cree una instancia de un objeto de metadatos estándar, rellene las variables deseadas y establezca el objeto de metadatos en el objeto de Media Heartbeat.

      See the comprehensive list of metadata here: [Audio and video parameters.](../../metrics-and-metadata/audio-video-parameters.md)

   * **Metadatos personalizados**: cree un objeto de variable para las variables personalizadas y rellénelo con los datos de este contenido.

1. **Seguimiento de la intención de inicio de reproducción**: para comenzar el seguimiento de una sesión, invoque `trackSessionStart` en la instancia de Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastrea la intención de reproducción, no el comienzo de la reproducción. Esta API se utiliza para cargar los datos y los metadatos, y para calcular la métrica de QoS (tiempo entre `trackSessionStart` y `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Seguimiento del inicio real de la reproducción**: identifique el evento del reproductor de medios para el comienzo de la reproducción (cuando el primer fotograma del contenido aparece en pantalla) e invoque `trackPlay`.

1. **Seguimiento de la finalización de la reproducción**: identifique el evento del reproductor de medios para la finalización de la reproducción (cuando el usuario ha visto el contenido hasta el final) e invoque `trackComplete`.

1. **Seguimiento del final de la sesión**: identifique el evento del reproductor de medios para la descarga/cierre de la reproducción (el usuario cierra el contenido, o este finalizó y se descargó) e invoque `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca el final de una sesión de seguimiento. Si la sesión se ha visto por completo correctamente, es decir, el usuario ha visto el contenido hasta el final, asegúrese de invocar `trackComplete` antes que `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Seguimiento de todas las situaciones de pausa posibles**: identifique el evento del reproductor de medios para la pausa e invoque `trackPause`.

   **Situaciones de pausa**: identifique todas las situaciones en las que puede pausarse el reproductor y compruebe que se ha invocado `trackPause` correctamente. Las siguientes situaciones requieren que la aplicación invoque `trackPause()`:

   * Cuando el usuario pausa explícitamente en la aplicación.
   * Cuando el reproductor se sitúa en el estado En pausa.
   * (*Aplicaciones móviles*): cuando el usuario coloca la aplicación en segundo plano, pero desea que la sesión continúe abierta.
   * (*Aplicaciones móviles*): cuando se produce cualquier tipo de interrupción del sistema que provoca que una aplicación se quede en segundo plano. Por ejemplo, si el usuario recibe una llamada o aparece una ventana emergente de otra aplicación, pero desea que la aplicación mantenga la sesión activa para que el usuario pueda reanudar el contenido desde donde se produjo la interrupción.

1. Identifique el evento del reproductor para la reproducción o reanudación después de la pausa e invoque `trackPlay`.

   >[!TIP]
   >
   >Puede ser el mismo origen de evento que se utilizó en el paso 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. Escuche los eventos de llamada a otro punto de la reproducción del reproductor de medios. En la notificación del evento de inicio de la llamada a otro punto del contenido, utilice el evento `SeekStart` para realizar el seguimiento.
1. En la notificación de finalización de llamada a otro punto del contenido del reproductor, realice un seguimiento del final de la llamada a otro punto del contenido utilizando el evento `SeekComplete`.
1. Escuche los eventos de almacenamiento en búfer de reproducción procedentes del reproductor de medios y, cuando reciba la notificación del evento Inicio de almacenamiento en búfer, rastree el almacenamiento en búfer mediante el evento `BufferStart`.
1. En la notificación de Finalización de almacenamiento en búfer procedente del reproductor de medios, rastree el final del almacenamiento en búfer con el evento `BufferComplete`.

Consulte ejemplos de cada paso en los siguientes temas específicos para cada plataforma, y examine los reproductores de muestra incluidos con los SDK.

Para ver un sencillo ejemplo del seguimiento de la reproducción, consulte este uso del SDK de JavaScript 2.x en un HTML5 Player:

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
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## Validación {#section_ABCFB92C587B4CAABDACF93452EFA78F}

### Inicio del contenido

Al inicio de la reproducción de un medio, estas llamadas clave se envían en el siguiente orden:

1. Inicio de análisis de medios
1. Inicio de Heartbeat
1. Inicio del análisis de Heartbeat

Las llamadas 1 y 2 contienen variables de metadatos adicionales para las funciones estándar y personalizadas.

### Reproducción de contenido

Durante la reproducción de contenido principal normal, las llamadas de Heartbeat se envían al servidor cada diez segundos.

### Contenido finalizado

En el 100 % de la reproducción de contenido o en un límite de pantalla en una emisión lineal, se enviará una llamada completa de Heartbeat.

### Pausa del contenido

Cuando se detenga el reproductor, se enviarán las llamadas de evento de pausa de reproductor cada diez segundos. Después de la pausa, los eventos de reproducción deben reanudarse.

### Arrastrar el cabezal de reproducción/Llamada a otro punto del vídeo

Al arrastrar el cabezal de reproducción, no se envían llamadas de seguimiento especiales. Sin embargo, cuando se reanuda la reproducción tras el desplazamiento, el valor del cabezal debe reflejar la nueva posición en el contenido principal.

### Búfer de contenido

Cuando el reproductor de medios realiza el almacenamiento en búfer, se envían llamadas de evento de búfer del reproductor cada 10 segundos. Cuando termine el almacenamiento en búfer, los eventos de reproducción deben reanudarse.
