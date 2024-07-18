---
title: 'Información sobre las cronologías de seguimiento de medios: el usuario abandona la sesión'
description: Obtenga información sobre la cronología del cabezal de reproducción y la acción usuario correspondiente cuando se abandona una sesión de vídeo. Conozca los detalles de cada acción y solicitud.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4c68f5997a9d336e8c3545cdfb7b9cb955602b69
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 100%

---

# Cronología 2: El usuario abandona la sesión {#timeline--2-user-abandons-session}

## VOD, anuncios pre-roll, anuncios mid-roll, el usuario deja el contenido antes de terminarlo

Los siguientes diagramas ilustran la cronología del cabezal de reproducción y la cronología correspondiente de las acciones de un usuario. A continuación se presentan los detalles de cada acción y sus solicitudes correspondientes.

![Contenido de la API](assets/va_api_content_2.png)

![Acciones de API](assets/va_api_actions_2.png)

## Detalles de la acción

### Acción 1: inicio de la sesión {#Action-1}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Botón de reproducción o de reproducción automática pulsado | 0 | 0 | `/api/v1/sessions` |

Esta llamada indica _la intención del usuario de reproducir_ un vídeo. Devuelve un ID de sesión (`{sid}`) al cliente que se utiliza para identificar todas las llamadas de seguimiento subsiguientes dentro de la sesión. El estado del reproductor no es &quot;reproduciendo&quot;, sino &quot;comenzando&quot;.  Los parámetros de sesión obligatorios deben incluirse en el mapa de `params` en la solicitud.  En el servidor, esta llamada genera una llamada de inicio a Adobe Analytics. Para obtener información sobre las sesiones, consulte la documentación de la API de recopilación de medios.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "sessionStart",
    "params": {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Acción 2: inicio del temporizador de ping {#Action-2}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| La aplicación inicia el temporizador de eventos de ping | 0 | 0 | |

Inicie el temporizador de ping de su aplicación. El primer evento de ping debe activarse en el primer segundo si hay anuncios previos a la emisión y en los 10 primeros segundos en caso contrario.

### Acción 3: inicio de la pausa publicitaria {#Action-3}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Rastrear inicio de pausa del anuncio previo a la emisión | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Se debe hacer un seguimiento de los anuncios previos a la emisión. Los anuncios solo se pueden rastrear durante una pausa publicitaria.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Acción 4: inicio del anuncio {#Action-4}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Rastrear inicio del anuncio previo a la emisión n.º 1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Se inicia una publicidad de 12 segundos.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Acción 5: pings de anuncios {#Action-5}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

Mandar un ping al servidor cada segundo. (No se muestran los pings de anuncios posteriores en interés de la brevedad).

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Acción 6: anuncio completo {#Action-6}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Rastrear finalización del anuncio previo a la emisión n.º 1 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

El primer anuncio previo a la emisión ha finalizado.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Acción 7: pausa publicitaria completa {#Action-7}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Rastrear finalización de pausa del anuncio previo a la emisión | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Terminó la pausa publicitaria. Durante la pausa publicitaria, el reproductor ha permanecido en el estado de &quot;reproducción&quot;.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Acción 8: reproducir contenido {#Action-8}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Rastrear el evento de reproducción | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Cambie el reproductor al estado &quot;reproducir&quot;; comience a rastrear el inicio de la reproducción del contenido.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Acción 9: ping {#Action-9}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 20 | 8 | `/api/v1/sessions/{sid}/events` |

Mandar un ping al servidor cada 10 segundos.

```json
{
    "playerTime": {
        "playhead": 8,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Acción 10: ping {#Action-10}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 30 | 18 | `/api/v1/sessions/{sid}/events` |

Mandar un ping al servidor cada 10 segundos.

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Acción 11: error {#Action-11}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Se produce un error, la aplicación envía información de error. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 20,
        "ts": "<timestamp>"
    },
    "eventType": "error"
}
```

### Acción 12: reproducir contenido {#Action-12}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| La aplicación se recupera de un error, el usuario pulsa Reproducir | 37 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType":"play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Acción 13: ping {#Action-13}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| La aplicación envía eventos de ping | 40 | 28 | `/api/v1/sessions/{sid}/events` |

Mandar un ping al servidor cada 10 segundos.

```json
{
    "playerTime": {
        "playhead": 28,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Acción 14: inicio de la pausa publicitaria {#Action-14}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Rastrear inicio de pausa del anuncio durante la emisión | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Anuncio durante la emisión de 8 segundos: enviar `adBreakStart`.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Acción 15: inicio del anuncio {#Action-15}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| Rastrear inicio del anuncio durante la emisión n.º 1 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Seguimiento del anuncio durante la emisión.

```json
{
    "playerTime": { "playhead": 33, "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Acción 16: cerrar aplicación {#Action-16}

| Acción | Cronología de acción (segundos) | Posición del cabezal de reproducción (segundos) | Solicitud de cliente |
| --- | :---: | :---: | --- |
| El usuario cierra la aplicación. La aplicación determina que el usuario ha abandonado la visualización y no vuelve a esta sesión. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

Envíe `sessionEnd` al servidor de VA para indicar que la sesión debe cerrarse inmediatamente, sin procesar más.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType": "sessionEnd"
}
```
