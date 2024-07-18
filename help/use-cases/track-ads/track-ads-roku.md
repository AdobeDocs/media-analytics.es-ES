---
title: Aprenda a rastrear anuncios en Roku
description: Implementar el seguimiento de anuncios en aplicaciones Roku usando Media SDK.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 100%

---

# Seguimiento de anuncios en Roku{#track-ads-on-roku}

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
   | `name` | Nombre de la pausa publicitaria: publicidad pre-roll, mid-roll y post-roll. | Sí |
   | `position` | La posición numérica de la pausa publicitaria, comenzando por 1. | Sí |
   | `startTime` | Valor del cabezal de reproducción al comienzo de la pausa publicitaria. | Sí |

   ```
   ‘ Create an adbreak info object
   adBreakInfo = adb_media_init_adbreakinfo()
   adBreakInfo.name = <ADBREAK_NAME>
   adBreakInfo.startTime = <START_TIME>
   adBreakInfo.position = <POSITION>
   ```

1. Invoque `trackEvent()` con `AdBreakStart` en la instancia de `MediaHeartbeat` para iniciar el seguimiento de la pausa publicitaria:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identifique cuándo se inicia el recurso publicitario y cree una instancia de `AdObject` con la información de la publicidad.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration)
   ```

1. Opcionalmente, se pueden adjuntar metadatos estándar o de anuncio a la sesión de seguimiento de contenido mediante el uso de variables de datos de contexto.

   * [Implementación de metadatos de publicidad estándar en Roku ](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Metadatos de anuncio personalizados**: para los metadatos personalizados, cree un objeto de variable para las variables de datos personalizadas y rellénelas con los datos del recurso publicitario actual:

     ```
     contextData = {}
     contextData["adinfo1"] = "adinfo2"
     contextData["adinfo2"] = "adinfo2"
     ```

1. Invoque `trackEvent()` con el evento `AdStart` de la instancia de `MediaHeartbeat` para iniciar el seguimiento de la reproducción de publicidad:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. Cuando la reproducción del recurso publicitario llega al final de la publicidad, invoque `trackEvent()` con el evento `AdComplete`.

   ```
   standardAdMetadata = {}
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Si la reproducción de la publicidad no ha finalizado porque el usuario ha elegido omitirla, realice un seguimiento del evento `AdSkip`

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. Si hay anuncios adicionales dentro del mismo `AdBreak`, repita los pasos del 3 al 7.
1. Cuando finalice la pausa publicitaria, utilice el evento `AdBreakComplete` para realizar el seguimiento:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Consulte la situación de seguimiento [Reproducción de VOD con anuncios previos a la emisión](/help/use-cases/tracking-scenarios/vod-preroll-ads.md) para obtener más información.
