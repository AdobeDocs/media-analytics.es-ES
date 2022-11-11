---
title: Obtenga información sobre cómo rastrear anuncios en Android
description: Implementar el seguimiento de anuncios en aplicaciones de Android mediante Media SDK.
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 96%

---

# Seguimiento de anuncios en Android{#track-ads-on-android}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Constantes de seguimiento de anuncio

| Nombre de la constante | Descripción |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Constante para rastrear el evento de inicio de AdBreak |
| `MediaHeartbeat.Event.AdBreakComplete` | Constante para rastrear el evento de finalización de AdBreak |
| `MediaHeartbeat.Event.AdStart` | Constante para rastrear el evento de Inicio de Ad |
| `MediaHeartbeat.Event.AdComplete` | Constante para rastrear el evento de Finalización de Ad |
| `MediaHeartbeat.Event.AdSkip` | Constante para rastrear el evento Omitir Ad |

## Pasos de implementación

1. Identifique cuándo comienza la zona de salto de anuncio, incluido el anuncio previo a la emisión, y cree un `AdBreakObject` utilizando la información de la pausa publicitaria.

   Referencia de `AdBreakObject`:

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

1. Invoque `trackEvent()` con `AdBreakStart` en la instancia de `MediaHeartbeat` para iniciar el seguimiento de la pausa publicitaria:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null);
   }
   ```

1. Identifique cuándo se inicia el anuncio y cree una instancia de `AdObject` con la información de la publicidad.

   Referencia de `AdObject`:

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

1. Opcionalmente, se pueden adjuntar metadatos estándar o de anuncio a la sesión de seguimiento de contenido mediante el uso de variables de datos de contexto.

   * [Implementación de metadatos de publicidad estándar en Android ](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)

   help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md

   * **Metadatos de anuncio personalizados**: para los metadatos personalizados, cree un objeto de variable para las variables de datos personalizadas y rellénelas con los datos del anuncio actual:

      ```java
      // Setting Ad Metadata
      HashMap<String, String> adMetadata = new HashMap<String, String>();
      adMetadata.put("affiliate", "Sample affiliate");
      adMetadata.put("campaign", "Sample ad campaign");
      ```


1. Invoque `trackEvent()` con el evento `AdStart` de la instancia de `MediaHeartbeat` para iniciar el seguimiento de la reproducción de publicidad.

   Incluya una referencia a la variable de metadatos personalizada (o un objeto vacío) como tercer parámetro de la llamada de evento:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata);
   }
   ```

1. Cuando la reproducción del anuncio llega al final, invoque `trackEvent()` con el evento `AdComplete`:

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

Consulte la situación de seguimiento [Reproducción de VOD con anuncios previos a la emisión](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) para obtener más información.
