---
title: Reanudación de sesiones inactivas
description: Aprenda cómo reanudar una sesión inactiva.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 37%

---

# Reanudación de sesiones inactivas{#resuming-inactive-sessions}

## Pausas largas

Media SDK realiza automáticamente un seguimiento de la duración de la reproducción de los contenidos en uno de los siguientes estados inactivos:

* En pausa
* Buscando
* Estancado
* Almacenamiento en búfer

Si una sesión de seguimiento de contenidos permanece en estado inactivo durante más de 30 minutos, la sesión se cerrará automáticamente. Si el usuario reanuda una sesión de seguimiento de vídeos previamente inactiva (`trackPlay`), Media Heartbeat crea automáticamente una nueva sesión de vídeo utilizando la información de vídeo y los metadatos utilizados anteriormente, y envía un evento de reanudación de latidos.

## Entrega entre dispositivos con el indicador de reanudación

El mismo mecanismo de reanudación que gestiona la continuación de la sesión de una sola aplicación también se aplica cuando un visualizador transfiere la reproducción entre dispositivos, por ejemplo, convirtiendo un vídeo de un teléfono móvil a un receptor de TV o Chromecast. Dado que cada dispositivo ejecuta su propia instancia de Media SDK, el traspaso crea varias sesiones de forma predeterminada. Utilice el indicador de reanudación para unirlos a una continuación lógica, de modo que Analytics informe de la visualización combinada como una sola pieza de participación en lugar de inicios de medios independientes.

**Cómo implementar:**

1. En el **dispositivo de origen** (por ejemplo, el teléfono), llame a `trackSessionEnd` cuando el visor inicie la conversión. No llamar a `trackComplete`: el contenido no ha finalizado, se está moviendo a otro dispositivo.
2. En el **dispositivo de destino** (por ejemplo, el Chromecast), llame a `trackSessionStart` con el marcador de reanudación establecido en `true` y los mismos metadatos de contenido (nombre, ID, longitud) utilizados en el dispositivo de origen. Pase la posición del cabezal de reproducción donde el visualizador lo dejó en el dispositivo de origen.
3. Si más tarde el visor devuelve la reproducción al dispositivo de origen, repita el mismo patrón: `trackSessionEnd` en el destino y `trackSessionStart` con el indicador de reanudación en el origen.

Si se establece el indicador de reanudación, Adobe Analytics incrementará [las reanudaciones de contenido](/help/reporting/metrics/content-resumes.md) en lugar de [los inicios de contenido](/help/reporting/metrics/media-starts.md) para la segunda parte y las siguientes de la entrega. Dado que no hay ningún mecanismo integrado para compartir el ID de sesión entre instancias de SDK, el indicador de reanudación es una declaración del lado del cliente; se pasa en función de la lógica de la aplicación cuando se sabe que el visor continúa una sesión anterior.

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
