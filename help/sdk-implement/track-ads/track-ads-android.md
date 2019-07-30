---
seo-title: Seguimiento de anuncios en Android
title: Seguimiento de anuncios en Android
uuid: 4 a 4249 fb-dc 39-4947-a 14 d-a 51 d 972 f 32 d 4
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de anuncios en Android{#track-ads-on-android}

>[!IMPORTANT]
>
>Las instrucciones siguientes proporcionan indicaciones para la implementación con los SDK 2. x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de seguimiento de anuncio

| Nombre de la constante | Descripción |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Constante para rastrear el evento de inicio de AdBreak |
| `MediaHeartbeat.Event.AdBreakComplete` | Constante para rastrear el evento de finalización de AdBreak |
| `MediaHeartbeat.Event.AdStart` | Constante para rastrear el evento de Inicio de Ad |
| `MediaHeartbeat.Event.AdComplete` | Constante para rastrear el evento de Finalización de Ad |
| `MediaHeartbeat.Event.AdSkip` | Constante para rastrear el evento Omitir Ad |

## Pasos de implementación

1. Identifique cuándo comienza la zona de salto de anuncio, incluido el anuncio previo a la emisión, y cree un `AdBreakObject` utilizando la información de la pausa publicitaria.

   `AdBreakObject` reference:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre de la pausa publicitaria: publicidad pre-roll, mid-roll y post-roll. | Sí |
   | `position` | La posición numérica de la pausa publicitaria del contenido, comenzando por 1. | Sí |
   | `startTime` | Valor del cabezal de reproducción al comienzo de la pausa publicitaria. | Sí |

   Creación de objeto de pausa publicitaria:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
   ```

1. Identifique cuándo se inicia el anuncio y cree una instancia de `AdObject` con la información de la publicidad.

   `AdObject` reference:

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre descriptivo del anuncio. | Sí |
   | `adId` | Identificador único del anuncio. | Sí |
   | `position` | Posición numérica del anuncio en la pausa publicitaria, comenzando por 1. | Sí |
   | `length` | Duración del anuncio | Sí |

   Creación de objeto de anuncio:

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. De forma opcional, adjunte metadatos estándar o de anuncio a la sesión de seguimiento de medios a través de variables de datos de contexto.

   * [Implementación de metadatos de publicidad estándar en Android](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **Metadatos de anuncio personalizados**: para los metadatos personalizados, cree un objeto de variable para las variables de datos personalizadas y rellénelas con los datos del anuncio actual:

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Incluya una referencia a la variable de metadatos personalizada (o un objeto vacío) como tercer parámetro de la llamada de evento:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. Si la reproducción de la publicidad no ha finalizado porque el usuario ha elegido omitirla, realice un seguimiento del evento `AdSkip`

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. Si hay anuncios adicionales dentro del mismo `AdBreak`, repita los pasos del 3 al 7.
1. Cuando finalice la pausa publicitaria, utilice el evento `AdBreakComplete` para realizar el seguimiento:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

Consulte la situación de seguimiento [Reproducción de VOD con anuncios previos a la emisión](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) para obtener más información.
