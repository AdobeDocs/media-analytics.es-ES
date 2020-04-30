---
title: Reproducción de VOD sin anuncios
description: Ejemplo de seguimiento de la reproducción de VOD que no contenga anuncios.
uuid: ee2a1b79-2c2f-42e1-8e81-b62bbdd0d8cb
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Reproducción de VOD sin anuncios {#vod-playback-with-no-ads}

## Situación {#scenario}

Este escenario tiene un recurso de VOD, sin anuncios, que se reproduce una vez de principio a fin.

| Activador | Método de Heartbeat | Llamadas de red | Notas   |
|---|---|---|---|
| El usuario hace clic en **[!UICONTROL Reproducir]**. | `trackSessionStart` | Inicio del contenido de Analytics, inicio del contenido de Heartbeat | Puede ser porque el usuario hace clic en Reproducir o por un evento de reproducción automática. |
| Primer fotograma del contenido | `trackPlay` | Reproducción del contenido de Heartbeat | Este método desencadena el temporizador y, a partir de este momento, se envían latidos cada 10 segundos durante la reproducción. |
| Se reproduce el contenido |  | Latidos de contenido |  |
| El contenido termina de reproducirse. | `trackComplete` | Finalización de contenido de Heartbeat | *Complete* significa que el cabezal de reproducción ha llegado al final del contenido. |

## Parámetros {#parameters}

Muchos de los valores que existen en las llamadas de inicio de contenido de Heartbeat están presentes en las llamadas de `Content Start` de Adobe Analytics. Adobe usa muchos parámetros para rellenar los distintos informes de contenido, pero en la siguiente tabla solo se recogen los más importantes:

### Inicio del contenido de Heartbeat

| Parámetro | Valor | Notas   |
|---|---|---|
| `s:sc:rsid` | &lt;El ID de su grupo de informes de Adobe> |  |
| `s:sc:tracking_server` | &lt;La URL de servidor de seguimiento de Analytics> |  |
| `s:user:mid` | se debe definir | Debe coincidir con el valor medio de la llamada `Adobe Analytics Content Start`. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Nombre de su contenido> |  |
| `s:meta:*` | opcional | Metadatos personalizados que se definen en el contenido. |

## Reproducción del contenido de Heartbeat {#heartbeat-content-play}

Estos parámetros deberían ser casi idénticos a la llamada de `Heartbeat Content Start`, pero la diferencia clave es el parámetro `s:event:type`. Todos los demás parámetros deben seguir existiendo.

| Parámetro | Valor | Notas   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Latidos de contenido {#content-heartbeats}

Durante la reproducción de contenido, un temporizador envía al menos un latido cada 10 segundos. Estos latidos contienen información sobre reproducción, anuncios, almacenamiento en búfer, etc. El contenido exacto de cada latido está fuera del ámbito de este documento, pero el componente fundamental es que los latidos se activen de forma consistente mientras dura la reproducción.

En los latidos de contenido, busque los parámetros siguientes:

| Parámetros | Valor | Notas   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;posición del cabezal de reproducción> p.ej., 50,60,70 | Este parámetro indica la posición actual del cabezal de reproducción. |

## Finalización de contenido de Heartbeat {#heartbeat-content-complete}

Cuando termina la reproducción de contenido, lo que significa que se ha llegado al final del cabezal de reproducción, se envía una llamada de `Heartbeat Content Complete`. Esta llamada se parece a otras llamadas de Heartbeat, pero contiene algunos parámetros específicos:

| Parámetros | Valor | Notas   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Código de muestra {#sample-code}

En este escenario, el contenido dura 40 segundos. Se reproduce hasta el final sin interrupciones.

![](assets/main-content-regular-playback.png)

### Android

```java
// Set up  mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay  
//    is used, i.e., there's an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts,  
//    i.e., the first frame of media is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
//    i.e., when the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not watch  
//    the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS

```
when the user clicks Play 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 

NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there's an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 

// 2. Call trackPlay when the playback actually starts, i.e., when the  
//    first frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end, i.e.,  
//    when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 

// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME, Configuration.MEDIA_ID,  
Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the main content starts, i.e.,  
//    the first frame of the media content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
    i.e., the media completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not  
//    watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........
```

