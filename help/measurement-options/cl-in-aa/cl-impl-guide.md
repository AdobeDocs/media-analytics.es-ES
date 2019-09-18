---
seo-title: Guía de implementación de vínculo personalizado
title: Guía de implementación de vínculo personalizado
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
translation-type: tm+mt
source-git-commit: f790d60c7c19dc203ea5dd48e1e55ec20a341900

---


# Custom Link Implementation Guide{#custom-link-implementation-guide}

Custom Video Tracking utilizes [manual link tracking using custom link code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) within Analytics `appMeasurement`. Con frecuencia, el seguimiento de enlace de vídeo personalizado se utiliza en las plataformas y los dispositivos en los que es necesaria una medición mínima del vídeo.

* En JavaScript: la `s.tl()` función
* En aplicaciones móviles: [trackAction() para Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html), [trackAction() para iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html) y [trackAction() para OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)

* In Data Insertion API: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Requisitos

* Acceso a datos y eventos de API del reproductor de vídeo
* Capacidad para añadir scripts con el uso de SDK de Analytics
* Capacidad para añadir señalizaciones de seguimiento (scripts personalizados o codificación) con el uso de Data Insertion API

## Metadatos

* Los metadatos se pueden añadir a cualquier llamada de seguimiento como parte de los datos de vínculos.
* Remember to update the `linkTrackVars` and `linkTrackEvents`

```javascript
/* Call on video complete */ 
 
if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15’; 
    s.linkTrackEvents = 'event3'; 
    s.prop10 = mediaName; 
    s.eVar10 = mediaName; 
    s.eVar12 = "video"; 
    s.eVar13 = document.title; 
    s.eVar15 = mediaPlayerName; 
    s.events = 'event3'; 
    s.tl(this,'o','Video Complete'); 
};
```

## Por qué usar el vínculo personalizado

* Se necesitan unos requisitos mínimos.
* Funciona en cualquier plataforma, incluso NoScript.
* Todos los cálculos, como el tiempo invertido o los cuartiles, se deben realizar con un script personalizado.
* Es muy sencillo, sin bibliotecas ni scripts ocultos.
* Proporciona un control total de todos los aspectos relacionados con los datos del vídeo.
* Se elimina el vínculo al reproductor de muestra.

## JavaScript de muestra para HTML5 Player

```javascript
<script type="text/javascript"> 
  myvideo = document.getElementById('movie'); 
  myvideo.addEventListener('play',myHandler,false); 
  myvideo.addEventListener('seeked',myHandler,false); 
  myvideo.addEventListener('seeking',myHandler,false); 
  myvideo.addEventListener('pause',myHandler,false); 
  myvideo.addEventListener('ended',myHandler,false); 
   
  function myHandler(e) { 
      var video = document.getElementsByTagName('video')[0]; 
      var mediaName="13502979:Sailing"; 
      var mediaLength = video.duration; 
      var mediaPlayerName = "HTML5 Player"; 
      /*Define video offset*/ 
      if (video.currentTime > 0) { 
          mediaOffset = Math.floor(video.currentTime); 
      } else { 
          mediaOffset = 0; 
      }; 
      /*Call on video start*/ 
      if (e.type == "play") { 
          if (mediaOffset == 0) { 
              console.log(mediaPlayerName + 
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime)); 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event2'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event2'; 
              s.tl(this,'o','Video Start'); 
          } 
      }; 
   
      /*Call on video pause*/ 
      if (e.type == "pause") { 
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime)); 
          if (video.currentTime != video.duration) { 
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15'; 
              s.linkTrackEvents='event7'; 
              s.prop10=mediaName; 
              s.eVar10=mediaName; 
              s.eVar12="video"; 
              s.eVar13=document.title; 
              s.eVar15=mediaPlayerName; 
              s.events='event7'; 
              s.tl(this,'o','Video Pause'); 
          } 
      }; 
   
      /*Call on video complete*/ 
      if (e.type == "ended") { 
          console.log(mediaPlayerName + 
            ' -> ended -> playhead: ' + 
            Math.floor(video.currentTime)); 
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15'; 
          s.linkTrackEvents = 'event3'; 
          s.prop10= m ediaName; 
          s.eVar10=mediaName; 
          s.eVar12="video"; 
          s.eVar13=document.title; 
          s.eVar15=mediaPlayerName; 
          s.events='event3'; 
          s.tl(this,'o','Video Complete'); 
      }; 
  }; 
</script>
```

