---
title: Reanudación de sesiones inactivas
description: Aprenda cómo reanudar una sesión inactiva.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '158'
ht-degree: 100%

---

# Reanudación de sesiones inactivas{#resuming-inactive-sessions}

## Pausas largas

Media SDK realiza automáticamente un seguimiento de la duración de la reproducción de los contenidos en uno de los siguientes estados inactivos:

* En pausa
* Llamada a otro punto del contenido
* Atascado
* Almacenamiento en búfer

Si una sesión de seguimiento de contenidos permanece en estado inactivo durante más de 30 minutos, la sesión se cerrará automáticamente. Si el usuario reanuda una sesión de seguimiento de vídeos previamente inactiva (`trackPlay`), Media Heartbeat crea automáticamente una nueva sesión de vídeo utilizando la información de vídeo y los metadatos utilizados anteriormente, y envía un evento de reanudación de latidos. Para obtener más información, consulte: [Parámetros de audio y vídeo.](/help/implementation/variables/audio-video-parameters.md)


## Continuar una sesión cerrada previamente de forma manual

Media SDK solo reanudará automáticamente las sesiones si la aplicación no se ha cerrado. Si la aplicación almacena datos de usuario y tiene la capacidad de reanudar un contenido que se cerró, se puede desencadenar manualmente un evento de reanudación. Al iniciar la sesión de seguimiento de vídeo, establezca la propiedad opcional de reanudación de vídeo.

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
