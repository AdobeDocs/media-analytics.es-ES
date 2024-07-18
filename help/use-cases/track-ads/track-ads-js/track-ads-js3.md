---
title: Aprenda a rastrear anuncios con JavaScript 3.x
description: Implementar el seguimiento de anuncios en aplicaciones de explorador (JS) mediante Media SDK.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 88%

---

# Seguimiento de anuncios en JavaScript 3.x{#track-ads-on-javascript}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 3.x.

>[!IMPORTANT]
>
>Si va a implementar cualquier versión anterior del SDK, puede descargar las guías del desarrollador aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

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

   | Nombre de variable | Tipo | Descripción |
   | --- | --- | --- |
   | `name` | string | Cadena no vacía que indica el nombre de la pausa (pre-roll, mid-roll y post-roll). |
   | `position` | number | La posición numérica de la pausa publicitaria, comenzando por 1. |
   | `startTime` | number | Valor del cabezal de reproducción al comienzo de la pausa publicitaria. |

   Creación de objeto de pausa publicitaria:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Invoque `trackEvent()` con `AdBreakStart` en la instancia de `MediaHeartbeat` para iniciar el seguimiento de la pausa publicitaria:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Identifique cuándo se inicia el anuncio y cree una instancia de `AdObject` con la información de la publicidad.

   Referencia de `AdObject`:

   | Nombre de variable | Tipo | Descripción |
   | --- | --- | --- |
   | `name` | string | Cadena no vacía que indica el nombre del anuncio. |
   | `adId` | string | Cadena no vacía que denota el identificador del anuncio. |
   | `position` | number | La posición numérica del anuncio dentro del adbreak, empezando por 1. |
   | `length` | number | Número positivo que indica la longitud del anuncio. |

   Creación de objeto de anuncio:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. (Opcional) Adjunte metadatos estándar o de publicidad a la sesión de seguimiento de contenido mediante el uso de variables de datos de contexto.

   * [Implementación de metadatos de publicidad estándar en JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Metadatos de anuncio personalizados**: para los metadatos personalizados, cree un objeto de variable para las variables de datos personalizadas y rellénelas con los datos del anuncio actual:

     ```js
     /* Set context data */
     // Standard metadata keys provided by adobe.
     adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
     adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
     
     // Custom metadata keys
     adMetadata["affiliate"] = "Sample affiliate";
     adMetadata["campaign"] = "Sample ad campaign";
     adMetadata["creative"] = "Sample creative";
     ```

1. Invoque `trackEvent()` con el evento `AdStart` de la instancia de `MediaHeartbeat` para iniciar el seguimiento de la reproducción de publicidad.

   Incluya una referencia a la variable de metadatos personalizada (o un objeto vacío) como tercer parámetro de la llamada de evento:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Cuando la reproducción del anuncio llega al final, invoque `trackEvent()` con el evento `AdComplete`:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Si la reproducción de la publicidad no ha finalizado porque el usuario ha elegido omitirla, realice un seguimiento del evento `AdSkip`

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Si hay anuncios adicionales dentro del mismo `AdBreak`, repita los pasos del 3 al 7.
1. Cuando finalice la pausa publicitaria, utilice el evento `AdBreakComplete` para realizar el seguimiento:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Consulte la situación de seguimiento [Reproducción de VOD con anuncios previos a la emisión](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) para obtener más información.

## Seguimiento de anuncios granular

El intervalo de ping de anuncio predeterminado es `10 seconds`.

Puede configurar el seguimiento de anuncios granular para habilitar el seguimiento de anuncios de `1 second`.

>[!IMPORTANT]
>
>Esta información debe proporcionarse al iniciar una sesión de seguimiento.



**Sintaxis**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**Ejemplo**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```
