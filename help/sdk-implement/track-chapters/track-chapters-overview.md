---
seo-title: Información general
title: Información general
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Información general{#overview}

>[!IMPORTANT]
>
>Las siguientes instrucciones proporcionan instrucciones para la implementación mediante SDK 2.x. Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

El seguimiento de capítulos y segmentos está disponible para capítulos o segmentos de medios definidos de forma personalizada. Algunos usos comunes para el seguimiento de capítulos son definir segmentos personalizados en función del contenido de los medios (como entradas de béisbol) o definir segmentos de contenido entre pausas publicitarias. Chapter tracking is **not** required for core media tracking implementations.

El seguimiento de capítulos incluye el inicio del capítulo, su finalización y omisión. You can use the media player API with customized segmentation logic to identify chapter events and to populate the required and optional chapter variables.

## Eventos del reproductor

### Al inicio del capítulo

* Cree la instancia del objeto para el capítulo, `chapterObject`.
* Populate the chapter metadata, `chapterCustomMetadata`
* La llamada `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Al completar el capítulo

* La llamada `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Omisión del capítulo

* La llamada `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementación del seguimiento de capítulos {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Identifique cuándo se produce el evento de inicio de capítulo y cree la instancia de `ChapterObject` con la información del capítulo.

   Esta es la referencia del seguimiento de capítulos de `ChapterObject`:

   >[!NOTE]
   >
   >Estas variables solo son necesarias si planea realizar un seguimiento de los capítulos.

   | Nombre de variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `name` | Nombre del capítulo | Sí |
   | `position` | Posición del capítulo | Sí |
   | `length` | Duración del capítulo | Sí |
   | `startTime` | Hora de inicio del capítulo | Sí |

1. Si incluye metadatos personalizados para el capítulo, cree las variables de datos de contexto para los metadatos.
1. Para empezar a rastrear la reproducción del capítulo, invoque el evento `ChapterStart` en la instancia de `MediaHeartbeat`.
1. Cuando la reproducción llega al final del capítulo, como se define en el código personalizado, invoque el evento `ChapterComplete` en la instancia de `MediaHeartbeat`.
1. Si no se ha completado la reproducción del capítulo porque el usuario ha elegido omitirlo (por ejemplo, si el usuario hace clic en la línea de tiempo para saltar el capítulo), invoque el evento `ChapterSkip` en la instancia de MediaHeartbeat.
1. Si hay más capítulos, repita los pasos del 1 al 5.

The following sample code uses the JavaScript 2.x SDK for an HTML5 media player. Debe utilizar este código con el código de reproducción de medios principal.

```js
/* Call on chapter start */ 
if (e.type == "chapter start") { 
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
    /* Set custom context data*/ 
    var chapterCustomMetadata = { 
        segmentType:"Baseball Innings", 
        segmentName:"Inning 5", 
        segmentInfo:"Game Six" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
}; 
```

