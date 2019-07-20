---
seo-title: Seguimiento de capítulos y segmentos en Roku
title: Seguimiento de capítulos y segmentos en Roku
uuid: 15 c 07131-77 d 7-4 a 97-92 c 6-0 a 190 c 6 b 08 d 3
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# Seguimiento de capítulos y segmentos en Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>Las instrucciones siguientes proporcionan consejos para la implementación mediante SDK 2. x. Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

## Metadatos de anuncios estándar de implementación

1. Identifique cuándo se produce el evento de inicio de capítulo y cree la instancia de `ChapterObject` con la información del capítulo.

   `ChapterObject` referencia de seguimiento de capítulo:

   >[!NOTE]
   >
   >Estas variables solo se requieren si planea rastrear capítulos.

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del capítulo | Sí |
   | `position` | Posición del capítulo | Sí |
   | `length` | Duración del capítulo | Sí |
   | `startTime` | Hora de inicio del capítulo | Sí |

   Objeto de capítulo:

   ```
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Si incluye metadatos personalizados para el capítulo, cree las variables de datos de contexto para los metadatos:

   ```
   chapterContextData = {} 
   chapterContextData["seg_type"] = "seg_type" 
   chapterContextData["seg_name"] = "seg_name" 
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Para empezar a rastrear la reproducción del capítulo, invoque el evento `ChapterStart` en la instancia de `MediaHeartbeat`

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Cuando la reproducción llega al final del capítulo, como se define en el código personalizado, invoque el evento `ChapterComplete` en la instancia de `MediaHeartbeat`.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Si no se ha completado la reproducción del capítulo porque el usuario ha elegido omitirlo (por ejemplo, si el usuario hace clic en la línea de tiempo para saltar el capítulo), invoque el evento `ChapterSkip` en la instancia de MediaHeartbeat.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Si hay más capítulos, repita los pasos del 1 al 5.

