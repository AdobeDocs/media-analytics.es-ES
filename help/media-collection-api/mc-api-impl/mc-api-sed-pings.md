---
title: Envío de eventos ping
description: null
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Envío de eventos ping {#sending-ping-events}

**Para el contenido principal, debe activar los eventos ping cada 10 segundos tras los 10 primeros segundos de reproducción, independientemente de los otros eventos de API que haya enviado. Para el seguimiento de anuncios, debe activar eventos de ping cada segundo.**

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

