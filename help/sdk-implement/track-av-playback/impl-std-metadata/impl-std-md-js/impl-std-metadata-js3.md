---
title: Aprenda a implementar metadatos estándar con JavaScript 3.x
description: Obtenga información sobre cómo configurar metadatos de anuncios y vídeos estándar para que se envíen con llamadas de seguimiento en aplicaciones de navegador (JS 3.x).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 10%

---

# Implementación de metadatos estándar con JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementación

Cree una instancia de un objeto de datos de contexto y rellene las variables de metadatos estándar que desee. Por ejemplo:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
