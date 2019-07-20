---
seo-title: Envío de eventos ping
title: Envío de eventos ping
uuid: c 92 c 1 a 92-3 af 6-4474-9 e 42-ffb 8 f 6 c 94 b 33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Envío de eventos ping{#sending-ping-events}

**Para el contenido principal, debe activar los eventos ping cada 10 segundos tras los 10 primeros segundos de reproducción, independientemente de los otros eventos de API que haya enviado. For Ad tracking, you must fire ping events every 1 second.**

Los eventos ping son literalmente el "latido" de Media Analytics. Los únicos parámetros requeridos para una llamada de ping son `eventType: ping` y el objeto `playerTime` (posición del cursor de encabezado y la marca de tiempo).

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

