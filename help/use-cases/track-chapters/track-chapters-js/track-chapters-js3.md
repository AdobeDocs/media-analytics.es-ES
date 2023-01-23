---
title: Aprenda a rastrear capítulos y segmentos usando JavaScript 3.x
description: Obtenga información sobre la implementación del seguimiento de capítulos y segmentos mediante el uso de Media SDK en aplicaciones de explorador (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '218'
ht-degree: 100%

---

# Seguimiento de capítulos y segmentos en JavaScript 3.x{#track-chapters-and-segments-on-javascript}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 3.x.

>[!IMPORTANT]
>
> Si está implementando alguna versión anterior del SDK, puede descargar la Guía del desarrollador aquí: [Descargar SDKs.](/help/getting-started/download-sdks.md)

1. Identifique cuándo se produce el evento de inicio de capítulo y cree la instancia de `ChapterObject` con la información del capítulo.

   Referencia de seguimiento de capítulos `ChapterObject`:

   >[!NOTE]
   >
   >Estas variables solo son necesarias si planea rastrear capítulos.

   | Nombre de variable | Tipo | Descripción |
   | --- | --- | --- |
   | `name` | string | Cadena no vacía que indica el nombre del capítulo. |
   | `position` | number | La posición del capítulo dentro del contenido, comenzando por 1. |
   | `length` | number | Número positivo que indica la longitud del capítulo. |
   | `startTime` | number | Valor del cabezal de reproducción al principio del capítulo. |

   Objeto de capítulo:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Si incluye metadatos personalizados para el capítulo, cree las variables de datos de contexto para los metadatos:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Para empezar a rastrear la reproducción del capítulo, invoque el evento `ChapterStart` en la instancia de `MediaHeartbeat`

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Cuando la reproducción llega al final del capítulo, como se define en el código personalizado, invoque el evento `ChapterComplete` en la instancia de `MediaHeartbeat`:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Si no se ha completado la reproducción del capítulo porque el usuario ha elegido omitirlo (por ejemplo, si el usuario hace clic en la línea de tiempo para saltar el capítulo), invoque el evento `ChapterSkip` en la instancia de MediaHeartbeat:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Si hay más capítulos, repita los pasos del 1 al 5.
