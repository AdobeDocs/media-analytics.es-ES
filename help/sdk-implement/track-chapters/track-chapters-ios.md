---
title: Seguimiento de capítulos y segmentos en iOS
description: En este tema se describe la implementación del seguimiento de capítulos y segmentos mediante el SDK de medios en iOS.
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Seguimiento de capítulos y segmentos en iOS{#track-chapters-and-segments-on-ios}

>[!IMPORTANT]
>
>Las siguientes instrucciones proporcionan instrucciones para la implementación mediante SDK 2.x. Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

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

   Objeto de capítulo:

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                        position:[POSITION] 
                        length:[LENGTH] 
                        startTime:[START_TIME]];
   ```

1. Si incluye metadatos personalizados para el capítulo, cree las variables de datos de contexto para los metadatos:

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. Para empezar a rastrear la reproducción del capítulo, invoque el evento `ChapterStart` en la instancia de `MediaHeartbeat`

   ```
   - (void)onChapterStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary]; 
   }
   ```

1. Cuando la reproducción llega al final del capítulo, como se define en el código personalizado, invoque el evento `ChapterComplete` en la instancia de `MediaHeartbeat`:

   ```
   - (void)onChapterComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Si no se ha completado la reproducción del capítulo porque el usuario ha elegido omitirlo (por ejemplo, si el usuario hace clic en la línea de tiempo para saltar el capítulo), invoque el evento `ChapterSkip` en la instancia de MediaHeartbeat:

   ```
   - (void)onChapterSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Si hay más capítulos, repita los pasos del 1 al 5.

