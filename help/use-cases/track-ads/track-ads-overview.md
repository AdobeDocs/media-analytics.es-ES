---
title: Seguimiento de anuncios explicados
description: Información general sobre la implementación del seguimiento de anuncios con Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 100%

---

# Información general{#overview}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

La reproducción de publicidad incluye el seguimiento de las pausas publicitarias y el inicio, finalización y omisión de un anuncio. Utilice la API del reproductor de contenido para identificar eventos clave del reproductor y rellenar las variables de publicidad opcionales y obligatorias. Consulte la lista completa de metadatos aquí: [Parámetros de publicidad.](../../implementation/variables/ad-parameters.md)

## Eventos del reproductor {#player-events}


### Al iniciar la pausa publicitaria

>[!NOTE]
>Incluido el anuncio previo a la emisión

* Cree una instancia de objeto `adBreak` para la pausa publicitaria. Por ejemplo, `adBreakObject`.

* Invoque `trackEvent` para el inicio de la pausa publicitaria con `adBreakObject`.

### En cada inicio de recurso de publicidad

* Cree una instancia de objeto de anuncio para el recurso de publicidad. Por ejemplo, `adObject`.
* Rellenar metadatos de publicidad, `adCustomMetadata`.
* Invoque `trackEvent` para el inicio del anuncio.

### En cada anuncio finalizado

* Invoque `trackEvent` para la finalización del anuncio.

### Al omitir publicidad

* Invoque `trackEvent` para la omisión del anuncio.

### Al finalizar la pausa publicitaria

* Invoque `trackEvent` para la finalización de la pausa publicitaria.

## Implementación del seguimiento de anuncios {#implement-ad-tracking}

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

   Referencia de `AdBreakObject`:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre de la pausa publicitaria: publicidad pre-roll, mid-roll y post-roll. | Sí |
   | `position` | La posición numérica de la pausa publicitaria del contenido, comenzando por 1. | Sí |
   | `startTime` | Valor del cabezal de reproducción al comienzo de la pausa publicitaria. | Sí |

1. Invoque `trackEvent()` con `AdBreakStart` en la instancia de `MediaHeartbeat` para iniciar el seguimiento de la pausa publicitaria.

1. Identifique cuándo se inicia el anuncio y cree una instancia de `AdObject` con la información de la publicidad.

   Referencia de `AdObject`:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre descriptivo del anuncio. | Sí |
   | `adId` | Identificador único del anuncio. | Sí |
   | `position` | Posición numérica del anuncio en la pausa publicitaria, comenzando por 1. | Sí |
   | `length` | Duración del anuncio | Sí |

1. Opcionalmente, se pueden adjuntar metadatos estándar o de anuncio a la sesión de seguimiento mediante el uso de variables de datos de contexto.

   * **Metadatos de publicidad estándar**: para los metadatos de publicidad estándar, cree un diccionario de conexiones de clave/valor de metadatos de publicidad estándar con el uso de las claves correspondientes a su plataforma.
   * **Metadatos de anuncio personalizados**: para los metadatos personalizados, cree un objeto de variable para las variables de datos personalizadas y rellénelas con los datos del anuncio actual.

1. Invoque `trackEvent()` con el evento `AdStart` de la instancia de `MediaHeartbeat` para iniciar el seguimiento de la reproducción de publicidad.

   Incluya una referencia a la variable de metadatos personalizada (o un objeto vacío) como tercer parámetro de la llamada de evento.

1. Cuando la reproducción del anuncio llega al final, invoque `trackEvent()` con el evento `AdComplete`.

1. Si la reproducción de la publicidad no ha finalizado porque el usuario ha elegido omitirla, realice un seguimiento del evento `AdSkip`.
1. Si hay anuncios adicionales dentro del mismo `AdBreak`, repita los pasos del 3 al 7.
1. Cuando finalice la pausa publicitaria, utilice el evento `AdBreakComplete` para realizar el seguimiento.

>[!IMPORTANT]
>
>Asegúrese de NO aumentar el cabezal de reproducción (`l:event:playhead`) del reproductor de contenido durante la reproducción del anuncio (`s:asset:type=ad`). Si lo hace, las métricas de Tiempo empleado en el contenido se verán afectadas negativamente.

El siguiente código de ejemplo utiliza el SDK JavaScript 2.x para un reproductor de contenido HTML5.

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
