---
title: Envío de eventos ping
description: Los eventos Ping son la base de Streaming Media Analytics. Aprenda a enviar un ping temporizado para el contenido principal o el seguimiento de anuncios.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e84864164adf056f47f24d65f0400c89d53d1630
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 70%

---

# Envío de eventos ping{#sending-ping-events}

**Debe activar eventos ping cada 10 segundos tras los 10 primeros segundos de reproducción, independientemente de los demás eventos de API que haya enviado. Esto se aplica tanto al contenido principal como al seguimiento de anuncios.**

Los eventos de ping representan literalmente el “latido” del corazón de Media Analytics. Los únicos parámetros requeridos para una llamada de ping son `eventType: ping` y el objeto `playerTime` (posición del cursor de encabezado y la marca de tiempo).

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
