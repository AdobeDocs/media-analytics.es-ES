---
title: Implementación de vínculo personalizado explicada
description: Obtenga información sobre cómo implementar el seguimiento de vínculos personalizados en Streaming Media Analytics.
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 92%

---

# Guía de implementación de Vínculo personalizado {#custom-link-implementation-guide}

El seguimiento de vídeo personalizado utiliza el seguimiento de vínculo manual mediante el código de vínculo personalizado con `appMeasurement` de Analytics.
Con frecuencia, el seguimiento de enlace de vídeo personalizado se utiliza en las plataformas y los dispositivos en los que es necesaria una medición mínima del vídeo.

* En JavaScript: la función `s.tl()`
* En aplicaciones móviles: [trackAction() para Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=es), [trackAction() para iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=es) y [trackAction() para OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* En la API de inserción de datos: [etiqueta linktype](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Requisitos

* Acceso a eventos y datos de API de reproductor de vídeo
* Posibilidad de agregar secuencias de comandos si se utiliza el SDK de Analytics
* Posibilidad de agregar señalizaciones de seguimiento (secuencia de comandos personalizada o código duro) si se utiliza la API de inserción de datos

## Metadatos

* Los metadatos se pueden añadir a cualquier llamada de seguimiento como parte de los datos de vínculos.
* Recuerde actualizar los valores `linkTrackVars` y `linkTrackEvents`.

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
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

## Por qué utilizar Vínculo personalizado:

* Se necesitan requisitos previos mínimos
* Funciona en cualquier plataforma, incluso sin script
* Cualquier cálculo, como el tiempo empleado o los cuartiles, debe calcularse en una secuencia de comandos personalizada
* Muy directo y sin bibliotecas ni secuencias de comandos ocultas
* Control total de cada aspecto de los datos de vídeo

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
