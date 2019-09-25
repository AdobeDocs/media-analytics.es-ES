---
seo-title: Seguimiento de capítulos y segmentos en Chromecast
title: Seguimiento de capítulos y segmentos en Chromecast
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de capítulos y segmentos en Chromecast{#track-chapters-and-segments-on-chromecast}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using 2.x SDKs. Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

1. Identifique cuándo se produce el evento de inicio de capítulo y cree la instancia de `ChapterObject` con la información del capítulo.

   `ChapterObject` referencia de seguimiento de capítulos:

   >[!NOTE]
   >
   >Estas variables solo son necesarias si planea realizar un seguimiento de los capítulos.

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

