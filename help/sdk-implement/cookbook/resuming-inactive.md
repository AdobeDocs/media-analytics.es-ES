---
seo-title: Reanudación de sesiones inactivas
title: Reanudación de sesiones inactivas
uuid: 3 ff 1205 d -7 bbe -4016-9 bd 7-6 e 34 b 7862 c 4 c
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Reanudar sesiones inactivas{#resuming-inactive-sessions}

## Pausas largas

El SDK de medios rastrea automáticamente el tiempo que la reproducción de medios está en uno de los siguientes estados inactivos:

* En pausa
* Llamada a otro punto del contenido
* Atascado
* Almacenamiento en búfer

Si una sesión de seguimiento de medios permanece en estado inactivo durante más de 30 minutos, la sesión se cerrará automáticamente. Si el usuario reanuda una sesión de seguimiento de vídeos previamente inactiva (`trackPlay`), Media Heartbeat crea automáticamente una nueva sesión de vídeo utilizando la información de vídeo y los metadatos utilizados anteriormente, y envía un evento de reanudación de latidos. Para obtener más información, consulte: [Parámetros de audio y vídeo.](../../metrics-and-metadata/audio-video-parameters.md)

## Reanudar manualmente sesión cerrada anteriormente

El SDK de medios solo reanudará automáticamente las sesiones si la aplicación no se cerró. Si la aplicación almacena datos de usuario y tiene la capacidad de reanudar un medio cerrado anteriormente, es posible desencadenar manualmente un evento de reanudación. Al iniciar la sesión de seguimiento de vídeo, establezca la propiedad opcional de reanudación de vídeo.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true 
public void onmediaLoad(Observable observable, Object data) { 

  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Set to true if this is a resume playback scenario 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);
   
  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification { 
  //Replace <MEDIA_NAME> with the media name. 
  //Replace <MEDIA_ID> with a media unique identifier. 
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                       mediaId:<MEDIA_ID> 
                       length:<MEDIA_LENGTH> 
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 

  //Set to YES if this user is resuming a previously closed media session 
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata]; 
} 
```

### JavaScript

```js
_onmediaLoad = function () { 
  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session 
  mediaObject.setValue(MediaObjectKey.mediaResumed, true); 
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

