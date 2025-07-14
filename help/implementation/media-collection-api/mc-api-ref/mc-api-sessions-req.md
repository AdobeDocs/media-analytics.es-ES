---
title: 'API de recopilación de medios de transmisión: Punto final de solicitud de sesiones'
description: ¿Qué son los parámetros y respuestas de solicitud de extremo de sesiones de API de recopilación de medios?
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 90%

---

# Solicitud de sesiones{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## Parámetros de URI

Ninguna

## Cuerpo de la solicitud

El cuerpo de la solicitud debe ser JSON y tener la misma estructura que este cuerpo de solicitud de muestra:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (Obligatorio)
   * `playhead` - Si el contenido está activo, el cabezal de reproducción debe ser el segundo del día actual, 0 &lt;= cabezal de reproducción &lt; 86400. Si se registra el contenido, el cabezal de reproducción debe ser el segundo del contenido actual, 0 &lt;= cabezal de reproducción &lt; duración del contenido. El valor puede ser un número de coma flotante.
   * `ts` - Marca de tiempo; debe estar en milisegundos; Hora universal coordinada (UTC).
* `eventType` (Obligatorio)

  **Valor válido:** `sessionStart`
* `params` (Obligatorio)
* `customMetadata` (Opcional)
* `qoeData` (Opcional)

## Respuesta

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

Encabezado `Location:`: La parte `/api/v1/` proporciona la versión de API. La parte posterior a `[…]sessions/` es el ID de sesión.

## Códigos de respuesta

| Código de respuesta HTTP | Descripción |
|---|---|
| 201 | Sesión creada |
| 400 | Solicitud incorrecta |
| 500 | Error del servidor |
