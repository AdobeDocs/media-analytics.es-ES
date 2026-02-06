---
title: Aprenda a rastrear anuncios con JavaScript 2.x
description: Implementar el seguimiento de anuncios en aplicaciones de explorador (JS) mediante Media SDK.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
exl-id: 4404d3a6-ab98-40f0-9573-ee32f480f650
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 91%

---

# Seguimiento de anuncios en JavaScript 2.x{#track-ads-on-javascript}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Constantes de seguimiento de anuncio

| Nombre de la constante | Descripción   |
|---|---|
| `AdBreakStart` | Constante para rastrear el evento de inicio de AdBreak |
| `AdBreakComplete` | Constante para rastrear el evento de finalización de AdBreak |
| `AdStart` | Constante para rastrear el evento de Inicio de Ad |
| `AdComplete` | Constante para rastrear el evento de Finalización de Ad |
| `AdSkip` | Constante para rastrear el evento Omitir Ad |

## Pasos de implementación

1. Identifique cuándo comienza la zona de salto de anuncio, incluido el anuncio previo a la emisión, y cree un `AdBreakObject` utilizando la información de la pausa publicitaria.

   Referencia de `AdBreakObject`:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre de la pausa publicitaria, como anuncio previo a la emisión, anuncio durante la emisión y anuncio posterior a la emisión. | Sí |
   | `position` | La posición numérica de la pausa publicitaria, comenzando por 1. | Sí |
   | `startTime` | Valor del cabezal de reproducción al comienzo de la pausa publicitaria. | Sí |

   Creación de objeto de pausa publicitaria:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Invoque `trackEvent()` con `AdBreakStart` en la instancia de `MediaHeartbeat` para iniciar el seguimiento de la pausa publicitaria:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Identifique cuándo se inicia el anuncio y cree una instancia de `AdObject` con la información de la publicidad.

   Referencia de `AdObject`:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre descriptivo del anuncio. | Sí |
   | `adId` | Identificador único del anuncio. | Sí |
   | `position` | La posición numérica del anuncio dentro de la pausa publicitaria, empezando por 1. | Sí |
   | `length` | Duración del anuncio | Sí |

   Creación de objeto de anuncio:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Opcionalmente, se pueden adjuntar metadatos estándar o de anuncio a la sesión de seguimiento de contenido mediante el uso de variables de datos de contexto.

   * [Implementación de metadatos de publicidad estándar en JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **Metadatos de anuncio personalizados**: para los metadatos personalizados, cree un objeto de variable para las variables de datos personalizadas y rellénelas con los datos del anuncio actual:

     ```js
     /* Set custom context data */
     var adCustomMetadata = {
         affiliate: "Sample affiliate",
         campaign: "Sample ad campaign",
         creative: "Sample creative"
     };
     ```

1. Invoque `trackEvent()` con el evento `AdStart` de la instancia de `MediaHeartbeat` para iniciar el seguimiento de la reproducción de publicidad.

   Incluya una referencia a la variable de metadatos personalizada (o un objeto vacío) como tercer parámetro de la llamada de evento:

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. Cuando la reproducción del anuncio llega al final, invoque `trackEvent()` con el evento `AdComplete`:

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. Si la reproducción de la publicidad no ha finalizado porque el usuario ha elegido omitirla, realice un seguimiento del evento `AdSkip`

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. Si hay anuncios adicionales dentro del mismo `AdBreak`, repita los pasos del 3 al 7.
1. Cuando finalice la pausa publicitaria, utilice el evento `AdBreakComplete` para realizar el seguimiento:

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

Consulte la situación de seguimiento [Reproducción de VOD con anuncios previos a la emisión](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) para obtener más información.
