---
seo-title: Seguimiento de capítulos y segmentos en Chromecast
title: Seguimiento de capítulos y segmentos en Chromecast
uuid: 5 ea 562 b 9-0 e 07-4 fbb -9 a 3 b -213 d 746304 f 5
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# Seguimiento de capítulos y segmentos en Chromecast{#track-chapters-and-segments-on-chromecast}

>[!IMPORTANT]
>
>Las instrucciones siguientes proporcionan consejos para la implementación mediante SDK 2. x. Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

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

   Objeto de capítulo:[ createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. Si incluye metadatos personalizados para el capítulo, cree las variables de datos de contexto para los metadatos:

   ```js
   var chapterContextData = { 
       segmentType: "Sample segment type" 
   };
   ```

1. Para empezar a rastrear la reproducción del capítulo, realice un seguimiento del evento `ChapterStart`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData); 
   ```

1. Cuando la reproducción llega al final del capítulo, como se define en el código personalizado, invoque el evento `ChapterComplete` en la instancia de `MediaHeartbeat`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. Si no se ha completado la reproducción del capítulo porque el usuario ha elegido omitirlo (por ejemplo, si el usuario hace clic en la línea de tiempo para saltar el capítulo), realice un seguimiento del evento `ChapterSkip`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip); 
   ```

1. Si hay más capítulos, repita los pasos del 1 al 5.

