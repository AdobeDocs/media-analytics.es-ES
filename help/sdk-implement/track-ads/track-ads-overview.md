---
seo-title: Información general
title: Información general
uuid: 1607798 b-c 6 ef -4 d 60-8 e 40-e 958 c 345 b 09 c
translation-type: tm+mt
source-git-commit: 56e8716ea37049b95a59a82144bbad0e882c16b4

---


# Información general{#overview}

>[!IMPORTANT]
>
>Las instrucciones siguientes proporcionan indicaciones para la implementación con los SDK 2. x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

La reproducción de publicidad incluye el seguimiento de las pausas publicitarias y el inicio, finalización y omisión de un anuncio. Use la API del reproductor de medios para identificar eventos de reproductor clave y rellenar las variables de publicidad opcionales y requeridas. See the comprehensive list of metadata here: [Ad parameters.](../../metrics-and-metadata/ad-parameters.md)

## Player events {#player-events}


### Al iniciar la pausa publicitaria

>[!NOTE]
>Incluido el previo

* Cree una instancia de objeto `adBreak` para la pausa publicitaria. Por ejemplo, `adBreakObject`.

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### En cada inicio de recurso de publicidad

* Cree una instancia de objeto de anuncio para el recurso de publicidad. Por ejemplo, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Invoque `trackEvent` para el inicio del anuncio.

### En cada anuncio finalizado

* Invoque `trackEvent` para la finalización del anuncio.

### Al omitir publicidad

* Invoque `trackEvent` para la omisión del anuncio.

### Al finalizar la pausa publicitaria

* Invoque `trackEvent` para la finalización de la pausa publicitaria.

## Implement ad tracking {#section_83E0F9406A7743E3B57405D4CDA66F68}

### Constantes de seguimiento de anuncio

| Nombre de la constante | Descripción   |
|---|---|
| `AdBreakStart` | Constante para rastrear el evento de inicio de AdBreak |
| `AdBreakComplete` | Constante para rastrear el evento de finalización de AdBreak |
| `AdStart` | Constante para rastrear el evento de Inicio de Ad |
| `AdComplete` | Constante para rastrear el evento de Finalización de Ad |
| `AdSkip` | Constante para rastrear el evento Omitir Ad |

### Pasos de implementación

1. Identifique cuándo comienza la zona de salto de anuncio, incluido el anuncio previo a la emisión, y cree un `AdBreakObject` utilizando la información de la pausa publicitaria.

   `AdBreakObject` reference:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre de la pausa publicitaria: publicidad pre-roll, mid-roll y post-roll. | Sí |
   | `position` | La posición numérica de la pausa publicitaria del contenido, comenzando por 1. | Sí |
   | `startTime` | Valor del cabezal de reproducción al comienzo de la pausa publicitaria. | Sí |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. Identifique cuándo se inicia el anuncio y cree una instancia de `AdObject` con la información de la publicidad.

   `AdObject` reference:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre descriptivo del anuncio. | Sí |
   | `adId` | Identificador único del anuncio. | Sí |
   | `position` | Posición numérica del anuncio en la pausa publicitaria, comenzando por 1. | Sí |
   | `length` | Duración del anuncio | Sí |

1. Opcionalmente, se pueden adjuntar metadatos estándar o de anuncio a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos de publicidad estándar**: para los metadatos de publicidad estándar, cree un diccionario de conexiones de clave/valor de metadatos de publicidad estándar con el uso de las claves correspondientes a su plataforma.
   * **Metadatos de anuncio personalizados**: para los metadatos personalizados, cree un objeto de variable para las variables de datos personalizadas y rellénelas con los datos del anuncio actual.

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Incluya una referencia a la variable de metadatos personalizada (o un objeto vacío) como tercer parámetro de la llamada de evento.

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. Si la reproducción de la publicidad no ha finalizado porque el usuario ha elegido omitirla, realice un seguimiento del evento `AdSkip`.
1. Si hay anuncios adicionales dentro del mismo `AdBreak`, repita los pasos del 3 al 7.
1. Cuando finalice la pausa publicitaria, utilice el evento `AdBreakComplete` para realizar el seguimiento.

>[!IMPORTANT]
>
>Make sure you do NOT increment the content player playhead (`l:event:playhead`) during ad playback (`s:asset:type=ad`). Si lo hace, las métricas Tiempo empleado se verán afectadas negativamente.

El siguiente código de ejemplo utiliza el SDK 2. x de JavaScript para un reproductor de medios HTML 5.

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```

## Validación {#section_5F1783F5FE2644F1B94B0101F73D57EB}

### Inicio de publicidad

Al comienzo de una reproducción de publicidad individual, se envían tres llamadas clave en el siguiente orden:

1. Inicio de análisis de publicidad de vídeo
1. Inicio de publicidad de Heartbeat
1. Inicio del análisis de Heartbeat

Las llamadas 1 y 2 contienen variables de metadatos adicionales para las funciones estándar y personalizadas.

### Reproducción de publicidad

Durante la reproducción de publicidad, las llamadas de reproducción de publicidad de Heartbeat se envían al servidor de Heartbeat cada segundo.

### Publicidad completa

Al 100 % de la reproducción de la publicidad, se enviará una llamada de finalización de anuncio de Heartbeat.

### Omisión de publicidad

Cuando se omite un anuncio no se envía ningún evento, por lo que las llamadas de seguimiento no incluirán la información de la publicidad.

>[!TIP]
>
>No se envían llamadas únicas al inicio de pausa publicitaria y a la finalización de la pausa publicitaria.

