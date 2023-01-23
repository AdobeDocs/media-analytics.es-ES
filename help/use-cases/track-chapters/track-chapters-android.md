---
title: Descubra cómo rastrear capítulos y segmentos en Android
description: Obtenga información acerca de la implementación del seguimiento de capítulos y segmentos mediante Media SDK en Android.
uuid: 013815d7-4d9e-48f4-a2b9-3b70cb1149d3
exl-id: ada2e2a7-1383-471c-9ce6-c82ea93fa79d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '198'
ht-degree: 100%

---

# Seguimiento de capítulos y segmentos en Android{#track-chapters-and-segments-on-android}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Implementación del seguimiento de capítulos

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

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Si incluye metadatos personalizados para el capítulo, cree las variables de datos de contexto para los metadatos:

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>();
   chapterMetadata.put("segmentType", "Sample Segment Type");
   chapterMetadata.put("segmentName", "Sample Segment Name");
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. Para empezar a rastrear la reproducción del capítulo, invoque el evento `ChapterStart` en la instancia de `MediaHeartbeat`

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata);
   }
   ```

1. Cuando la reproducción llega al final del capítulo, como se define en el código personalizado, invoque el evento `ChapterComplete` en la instancia de `MediaHeartbeat`:

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null);
   }
   ```

1. Si no se ha completado la reproducción del capítulo porque el usuario ha elegido omitirlo (por ejemplo, si el usuario hace clic en la línea de tiempo para saltar el capítulo), invoque el evento `ChapterSkip` en la instancia de MediaHeartbeat:

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null);
   }
   ```

1. Si hay más capítulos, repita los pasos del 1 al 5.
