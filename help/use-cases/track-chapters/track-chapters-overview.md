---
title: Descubra cómo rastrear capítulos y segmentos explicados
description: Implementar el seguimiento de capítulos y segmentos con Media SDK.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 100%

---

# Información general{#overview}

Las siguientes instrucciones proporcionan directrices para la implementación mediante SDK de 2.x.

>[!IMPORTANT]
> 
> Si va a implementar una versión 1.x del SDK, puede descargar la guía del desarrollador aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

El seguimiento de capítulos y segmentos está disponible para capítulos o segmentos de contenido multimedia detallados. Algunos usos comunes del seguimiento de capítulos son definir los segmentos personalizados basados en el contenido del medio, tales como los innings de béisbol o definir segmentos de contenido entre las pausas publicitarias. El seguimiento de capítulos **no** es necesario para las implementaciones de seguimiento de contenidos principales.

El seguimiento de capítulos incluye el inicio del capítulo, su finalización y omisión. Puede utilizar la API del reproductor de contenidos con una lógica de segmentación personalizada para identificar eventos de capítulo y llenar las variables de capítulo opcionales y obligatorias.

## Eventos del reproductor

### Al inicio del capítulo

* Cree la instancia del objeto para el capítulo, `chapterObject`.
* Rellene los metadatos del capítulo, `chapterCustomMetadata`.
* La llamada `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Al completar el capítulo

* La llamada `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Omisión del capítulo

* La llamada `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementación del seguimiento de capítulos {#implement-chapter-tracking}

1. Identifique cuándo se produce el evento de inicio de capítulo y cree la instancia de `ChapterObject` con la información del capítulo.

   Esta es la referencia del seguimiento de capítulos de `ChapterObject`:

   >[!NOTE]
   >
   >Estas variables solo son necesarias si planea rastrear capítulos.

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

El siguiente código de ejemplo utiliza el SDK JavaScript 2.x para un reproductor de contenidos HTML5. Este código debe utilizarse con el código de reproducción de contenidos principal.

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
