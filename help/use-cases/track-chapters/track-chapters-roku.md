---
title: Aprenda a rastrear capítulos y segmentos en Roku
description: Obtenga información acerca de la implementación del seguimiento de capítulos y segmentos mediante Media SDK en Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '199'
ht-degree: 100%

---

# Seguimiento de capítulos y segmentos en Roku{#track-chapters-and-segments-on-roku}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 2.x.

>[!IMPORTANT]
>
> Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Implemente los metadatos de publicidad estándar

1. Identifique cuándo se produce el evento de inicio de capítulo y cree la instancia de `ChapterObject` con la información del capítulo.

   Referencia de seguimiento de capítulos `ChapterObject`:

   >[!NOTE]
   >
   >Estas variables solo son necesarias si planea rastrear capítulos.

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
