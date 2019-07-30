---
seo-title: Información general
title: Información general
uuid: 3 fe 32425-5 e 2 a -4886-8 fea-d 91 d 15671 bb 0
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Información general{#overview}

>[!IMPORTANT]
>
>Las instrucciones siguientes proporcionan consejos para la implementación mediante SDK 2. x. Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

El seguimiento de capítulo y segmento está disponible para capítulos o capítulos de medios personalizados. Algunos usos comunes del seguimiento de capítulos son definir segmentos personalizados basados en contenido multimedia (como entradas de béisbol) o definir segmentos de contenido entre pausas publicitarias. **No** es necesario rastrear capítulo para implementaciones de seguimiento de medios principales.

El seguimiento de capítulos incluye el inicio del capítulo, su finalización y omisión. Puede utilizar la API de reproductor de medios con lógica de segmentación personalizada para identificar eventos de capítulo y rellenar las variables de capítulo opcionales y requeridas.

## Eventos del reproductor

### Al inicio del capítulo

* Cree la instancia del objeto para el capítulo, `chapterObject`.
* Populate the chapter metadata, `chapterCustomMetadata`
* La llamada `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Al completar el capítulo

* La llamada `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Omisión del capítulo

* La llamada `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Identifique cuándo se produce el evento de inicio de capítulo y cree la instancia de `ChapterObject` con la información del capítulo.

   Esta es la referencia del seguimiento de capítulos de `ChapterObject`:

   >[!NOTE]
   >
   >Estas variables solo se requieren si planea rastrear capítulos.

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

El siguiente código de ejemplo utiliza el SDK 2. x de JavaScript para un reproductor de medios HTML 5. Debe utilizar este código con el código de reproducción multimedia principal.

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

## Validación {#section_07EC2811BE3249249494596BFE9BF869}

### Inicio del capítulo.

Al iniciar una reproducción de capítulo individual, se envía una llamada clave:

* Inicio del capítulo de Heartbeat (Esta llamada contiene variables adicionales de metadatos de capítulo).

### Capítulo completado

Al terminar un capítulo, se enviará una llamada de capítulo completado.

### Omisión del capítulo

Cuando se omita un capítulo, se enviará una llamada de omisión de capítulo.
