---
title: Envío de eventos ping
description: Los eventos ping son el latido del corazón de los servicios de medios de streaming de Adobe. Aprenda a enviar un ping temporizado para el contenido principal o el seguimiento de anuncios.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 50%

---

# Envío de eventos ping{#sending-ping-events}

**Debe activar eventos ping cada 10 segundos tras los 10 primeros segundos de reproducción, independientemente de los demás eventos de API que haya enviado. Esto se aplica tanto al contenido principal como al seguimiento de anuncios.**

Los eventos de ping son el &quot;latido&quot; de los servicios de medios de streaming de Adobe. Los únicos parámetros requeridos para una llamada de ping son `eventType: ping` y el objeto `playerTime` (posición del cursor de encabezado y la marca de tiempo).

El siguiente fragmento de código muestra una forma de implementar un mecanismo de ping para el contenido principal (con un intervalo de 10 segundos):

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
