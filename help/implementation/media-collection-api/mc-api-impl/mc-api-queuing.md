---
title: Poner eventos en cola cuando la respuesta de las sesiones es lenta
description: Aprenda qué hacer cuando el ID de sesión se devuelve después de que su reproductor dispare eventos.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 100%

---

# Poner eventos en cola cuando la respuesta de las sesiones es lenta{#queueing-events-when-sessions-response-is-slow}

La API de Media Collection es RESTful: es decir, el usuario realiza una solicitud HTTP y espera la respuesta. Esto solo es importante para cuando se realiza una [Solicitud de sesiones](../mc-api-ref/mc-api-sessions-req.md) para obtener un ID de sesión al principio de la reproducción de vídeo. Esto es importante porque el ID de sesión es necesario para todas las llamadas de seguimiento subsiguientes.

El reproductor puede desencadenar eventos _antes de recibir la respuesta de sesión_ (con el parámetro ID de sesión) del backend. En este caso, la aplicación debe poner en cola los eventos de seguimiento que lleguen entre la [Solicitud de sesiones](../mc-api-ref/mc-api-sessions-req.md) y su respuesta. Cuando llega la respuesta de sesiones, primero debe procesar los [eventos](../mc-api-ref/mc-api-events-req.md) en cola y, a continuación, iniciar el procesamiento de eventos _en directo_ con las llamadas de [eventos](../mc-api-ref/mc-api-events-req.md).

>[!NOTE]
>
>La [solicitud de eventos](../mc-api-ref/mc-api-events-req.md) no devuelve datos al cliente aparte de un código de respuesta HTTP.

Consulte el reproductor de referencia de su distribución para procesar eventos antes de recibir un ID de sesión. Por ejemplo:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**Procesa cualquier evento en cola:** el reproductor de referencia procesa los eventos en cola de la siguiente manera:

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

Continúe procesando los eventos de seguimiento a medida que ocurren.
