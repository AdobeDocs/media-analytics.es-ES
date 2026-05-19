---
title: Contenido principal en directo
description: Vea un ejemplo de cómo rastrear contenido en directo mediante Media SDK.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oOshJZEQmXqgNh5l10-qhLMO8dmph6Tz9mpH0a4FePU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 77%

---

# Contenido principal en directo{#live-main-content}

## Escenario {#scenario}

En este escenario, hay un recurso activo sin anuncios reproducidos durante 40 segundos tras unirse a la emisión en directo.

| Activador | Método de Heartbeat | Llamadas de red | Notas   |
|---|---|---|---|
| El usuario hace clic en **[!UICONTROL Reproducir]**. | `trackSessionStart` | Inicio del contenido de Analytics, inicio del contenido de Heartbeat | Puede ser porque el usuario hace clic en **[!UICONTROL Reproducir]** o por un evento de reproducción automática. |
| Se reproduce el primer fotograma del contenido. | `trackPlay` | Reproducción del contenido de Heartbeat | Este método activa el temporizador. Los latidos se envían cada 10 segundos mientras dure la reproducción. |
| Se reproduce el contenido. |  | Latidos de contenido |  |
| La sesión finaliza. | `trackSessionEnd` |  | `SessionEnd` significa el final de una sesión de visualización. Hay que invocar a esta API aunque el usuario no vea el contenido completo. |

## Parámetros {#parameters}

Muchos de los valores que existen en las llamadas de inicio de contenido de Adobe Analytics están presentes en las llamadas de inicio de contenido de Heartbeat. También verá muchos otros parámetros que Adobe utiliza para rellenar los distintos informes de contenido en Adobe Analytics. Aquí no vamos a detallar todos, solo los más importantes.

### Inicio del contenido de Heartbeat

| Parámetro | Valor | Notas |
|---|---|---|
| `s:sc:rsid` | &lt;El ID de su grupo de informes de Adobe> |  |
| `s:sc:tracking_serve` | &lt;La URL de servidor de seguimiento de Analytics> |  |
| `s:user:mid` | `s:user:mid` | Debe coincidir con el valor medio de la llamada de inicio de contenido de Adobe Analytics |
| `s:event:type` | &quot;start&quot; |  |
| `s:asset:type` | &quot;main&quot; |  |
| `s:asset:mediao_id` | &lt;Nombre de su contenido> |  |
| `s:stream:type` | live |  |
| `s:meta:*` | opcional | Metadatos personalizados definidos en el contenido |

## Latidos de contenido {#content-heartbeats}

Durante la reproducción del contenido, hay un temporizador que enviará uno o más latidos (o pings) cada 10 segundos para el contenido principal y cada segundo para los anuncios. Estos latidos tendrán información sobre la reproducción, los anuncios, el almacenamiento en búfer y muchas otras cosas. El contenido exacto de cada latido está fuera del ámbito de este documento. Lo más importante para validar es que los latidos se activan de forma coherente durante la reproducción.

En los latidos de contenido, busque algunas cosas específicas:

| Parámetro | Valor | Notas |
|---|---|---|
| `s:event:type` | &quot;play&quot; |  |
| `l:event:playhead` | &lt;posición del cabezal de reproducción> p. ej., 50, 60, 70 | Esto debería indicar la posición actual del cabezal de reproducción. |

## Finalización de contenido de Heartbeat {#heartbeat-content-complete}

No habrá una llamada de finalización en este caso, ya que la emisión en directo nunca llegó a completarse.

## Configuración del valor del cabezal de reproducción

Para los flujos en directo, debe establecer el valor del cabezal de reproducción como el número de segundos desde la medianoche (UTC) de ese día, de modo que en los informes, los analistas puedan determinar en qué momento se unen los usuarios y abandonan el flujo en directo en una vista de 24 horas.

### Al comienzo

En el caso de los medios en directo, cuando un usuario comienza a reproducir el flujo, debe establecer `l:event:playhead` a la cantidad de segundos desde la medianoche UTC en ese día. Esto es lo contrario a VOD, donde establecería el cursor de reproducción en “0”. Nota: Cuando se utilizan marcadores de progreso, la duración del contenido es obligatoria y el cabezal de reproducción debe actualizarse como número de segundos desde el principio del elemento de medios, empezando por 0.

Por ejemplo, supongamos que un evento de transmisión en vivo comienza a medianoche y se ejecuta durante 24 horas (`a.media.length=86400`; `l:asset:length=86400`). Entonces, digamos que un usuario comienza a reproducir ese flujo en vivo a las 12:00pm. En esta situación, debe configurar `l:event:playhead` a 43 200 (12 horas desde la medianoche UTC de ese día en segundos).

### Al pausar

La misma lógica de “cabezal de lectura en directo” aplicada al inicio de la reproducción debe aplicarse cuando un usuario pone en pausa la reproducción. Cuando el usuario vuelve a reproducir el flujo en directo, debe establecer el valor `l:event:playhead` según el nuevo número de segundos desde la medianoche (UTC), _no_ en el punto en el que el usuario detuvo el flujo en directo.

## Seguimiento de cambios de programas en una emisión en directo {#live-program-changes}

Cuando un flujo en directo pasa de un programa o programa a otro (un patrón común para las propiedades de difusión y cable), cada programa debe seguirse como una sesión separada. Esto le permite informar sobre la participación y el tiempo empleado por título individual en lugar de atribuir todas las visualizaciones a un único flujo continuo.

**Enfoque recomendado:**

1. Cuando finalice el programa actual (o cuando el reproductor indique un evento de cambio de programa), llame a `trackSessionEnd` para cerrar la sesión actual.
2. Cuando comience el nuevo programa, llame a `trackSessionStart` con los metadatos del nuevo programa (nombre, ID, tipo de contenido, etc.).

El seguimiento de cada programa como su propia sesión mantiene [Tiempo invertido en contenido](/help/reporting/metrics/content-time-spent.md), [Marcadores de progreso](/help/reporting/metrics/progress-markers.md) y las métricas de finalización enfocadas en el programa individual, y permite generar informes de audiencia precisos por título. Use `trackSessionEnd` en lugar de `trackComplete` para la transición: `trackComplete` indica que el visor ha visto intencionadamente el final de un contenido discreto, mientras que `trackSessionEnd` es correcto porque el flujo continúa con una programación diferente en lugar de finalizarse.

## Código de muestra {#sample-code}

![](assets/live-content-playback.png)

### Android

Este es el orden esperado de las llamadas de API:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS

Este es el orden esperado de las llamadas de API:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

Este es el orden esperado de las llamadas de API:

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```
