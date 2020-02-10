---
title: 'Línea de tiempo 3: Capítulos'
description: null
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
translation-type: ht
source-git-commit: 5107de22c2388e8ac5b15b8d28fa974e97363fdf

---


# Línea de tiempo 3: Capítulos {#timeline-3-chapters}

## VOD, anuncios pre-roll, pausar, almacenar en búfer, ver contenido hasta el final


Los siguientes diagramas ilustran la cronología del cabezal de reproducción y la cronología correspondiente de las acciones de un usuario. A continuación se presentan los detalles de cada acción y sus solicitudes correspondientes.


![](assets/va_api_content_3.png)


![](assets/va_api_actions_3.png)


## Detalles de la acción


### Acción 1 - Iniciar sesión {#Action-1}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| El botón Reproducción automática o Reproducir se ha presionado, el vídeo empieza a cargarse. | 0 | 0 | `/api/v1/sessions` |

**Detalles de implementación**

Esta llamada indica _la intención del usuario de reproducir_ un vídeo. Devuelve un ID de sesión (`{sid}`) al cliente que se utiliza para identificar todas las llamadas de seguimiento subsiguientes dentro de la sesión. El estado del reproductor no es &quot;reproduciendo&quot;, sino &quot;comenzando&quot;.  [Los parámetros de sesión obligatorios](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) deben incluirse en el mapa de `params` en la solicitud.  En el servidor, esta llamada genera una llamada de inicio a Adobe Analytics.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Acción 2: Se inicia el temporizador de ping {#Action-2}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación inicia el temporizador del evento de ping | 0 | 0 |  |

**Detalles de implementación**

Inicie el temporizador de ping. El primer evento de ping debe activarse en el primer segundo si hay anuncios previos a la emisión y en los 10 primeros segundos en caso contrario.

### Acción 3 - Inicio de la pausa publicitaria {#Action-3}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Seguimiento del comienzo de la pausa publicitaria pre-roll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Los anuncios solo se pueden rastrear durante una pausa publicitaria.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### Acción 4 - Inicio del anuncio {#Action-4}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Seguimiento del comienzo del primer anuncio pre-roll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Comience a rastrear el primer anuncio pre-roll, que dura 15 segundos. Incluir metadatos personalizados con `adStart` .

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### Acción 5 - Agrupaciones de anuncios {#Action-5}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 10 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada segundo. (Los pings de anuncios posteriores no se muestran en interés de la brevedad).

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 6 - Finalización del anuncio {#Action-6}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Se ha completado el seguimiento del primer anuncio pre-roll | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Rastrear el final del primer anuncio pre-roll.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Acción 7 - Inicio del anuncio {#Action-7}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Seguimiento del comienzo del segundo anuncio pre-roll | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Realice un seguimiento del inicio del segundo anuncio pre-roll, que dura 7 segundos.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Acción 8 - Agrupaciones de anuncios {#Action-8}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 16 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada segundo. (Los pings de anuncios posteriores no se muestran en interés de la brevedad).

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 9 - Finalización del anuncio {#Action-9}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Se ha completado el seguimiento del segundo anuncio pre-roll | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Rastrear el final del segundo anuncio pre-roll.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Acción 10 - Se completó la pausa publicitaria {#Action-10}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Rastrear la pausa publicitaria pre-roll | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

La pausa publicitaria ha finalizado. Durante la pausa publicitaria, el estado de reproducción será “reproduciendo”.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Acción 11 - Reproducir contenido {#Action-11}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Rastrear el evento de Reproducción | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Tras el evento `adBreakComplete`, ponga el reproductor en el estado “reproduciendo” utilizando el evento `play`.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Acción 12 - Inicio del capítulo {#Action-12}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Rastrear el evento Inicio del capítulo | 23 | 1 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Tras el evento Reproducir, realice un seguimiento del principio del primer capítulo.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### Acción 13 - Ping {#Action-13}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada 10 segundos.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 14 - Inicio del búfer {#Action-14}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Se produce el evento de Inicio del almacenamiento en búfer. | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Rastree el movimiento al estado “almacenamiento en búfer”.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:bufferStart
}
```

### Acción 15 - Fin del búfer (reproducción) {#Action-15}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| El almacenamiento en búfer finalizó, la aplicación hace un seguimiento de la reanudación del contenido. | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

El almacenamiento en búfer finaliza después de 3 segundos, por lo que el reproductor vuelve al estado &quot;reproduciendo&quot;. Debe enviar otro evento de seguimiento de reproducción cuando termine el almacenamiento en búfer.  **La llamada`play`después de`bufferStart`infiere una llamada “bufferEnd” al back end**, por lo que no es necesario un evento `bufferEnd`.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Acción 16 - Ping {#Action-16}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada 10 segundos.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 17 - Fin del capítulo {#Action-17}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación rastrea el final del capítulo | 45 | 20 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

El primer capítulo termina justo antes de la segunda pausa publicitaria.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### Acción 18 - Inicio de la pausa publicitaria {#Action-18}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Seguimiento del comienzo del anuncio mid-roll | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Anuncio mid-roll de 8 segundos: enviar `adBreakStart` .

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### Acción 19 - Inicio del anuncio {#Action-19}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Seguimiento del tercer anuncio mid-roll | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Seguimiento del anuncio mid-roll.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Acción 20 - Anuncios {#Action-20}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 47 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada segundo. (Los pings de anuncios posteriores no se muestran en interés de la brevedad).

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 21 - Finalización del anuncio {#Action-21}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Se ha completado el seguimiento del primer anuncio mid-roll | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

El anuncio mid-roll ha finalizado.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Acción 22 - Se completó la pausa publicitaria {#Action-22}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Seguimiento de la pausa publicitaria mid-roll completado | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Se ha completado la pausa publicitaria.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Acción 23 - Inicio del capítulo {#Action-23}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Rastrear el inicio del capítulo 2 | 55 | 22 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**



**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 22,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### Acción 24 - Ping {#Action-24}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada 10 segundos.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 25 - Pausa {#Action-25}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| El usuario ha hecho clic en Pausa | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

La acción del usuario cambia el estado de reproducción a “en pausa”.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Acción 26 - Ping {#Action-26}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada 10 segundos. El reproductor sigue en estado &quot;almacenamiento en búfer&quot;; el usuario se queda en los 20 primeros segundos de contenido. Trabajando...

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 27 - Reproducir contenido {#Action-27}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| El usuario ha presionado Reproducir para reanudar el contenido principal | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Cambie el estado de reproducción a &quot;reproduciendo&quot;.  **La llamada`play`después de`pauseStart`ya infiere una llamada &quot;continuar&quot; al final**, por lo que no hay necesidad de un evento `resume`.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:play
}
```

### Acción 28 - Ping {#Action-28}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Mandar un ping al servidor cada 10 segundos.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Acción 29 - Fin del capítulo {#Action-29}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| Fin del capítulo 2 | 87 | 44 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Rastrear el final del segundo y último capítulo.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterComplete
}
```

### Acción 30 - Sesión completa {#Action-30}

| Acción | Línea de tiempo de acción (segundos) | Posición del cabezal de reproducción (en segundos) | Solicitud del cliente |
| --- | :---: | :---: | --- |
| El usuario termina de ver el contenido hasta el final. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Detalles de implementación**

Envíe `sessionComplete` al servidor para indicar que el usuario ha terminado de ver todo el contenido.

**Cuerpo de la solicitud de muestra**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    },
    eventType:sessionComplete
}
```


>[!NOTE]
>
>**¿No hay eventos de búsqueda? -** No hay compatibilidad explícita en la API de Media Collection para eventos `seekStart` o `seekComplete`. Esto se debe a que algunos reproductores generan un número muy grande de eventos cuando el usuario final arrastra el cabezal de reproducción, y varios cientos de usuarios podrían atascar fácilmente el ancho de banda de red de un servidor. Adobe busca la compatibilidad explícita con los eventos de llamada con el cabezal de reproducción, computando la duración del latido en función de la marca de tiempo del dispositivo en lugar de la posición del cabezal.

