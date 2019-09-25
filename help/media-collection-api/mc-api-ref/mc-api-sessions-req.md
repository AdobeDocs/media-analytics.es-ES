---
seo-title: Solicitud de sesiones
title: Solicitud de sesiones
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
translation-type: tm+mt
source-git-commit: f1c9f5f4cbcd4c043e1c7b4a5037c134b2bdd380

---


# Solicitud de sesiones{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## Parámetros de URI

Ninguna

## Cuerpo de la solicitud

The request body must be JSON, and must have the same structure as this sample request body:

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
   * `playhead`: debe estar en segundos, pero puede ser float.
   * `ts`: marca de tiempo; debe estar en milisegundos.
* `eventType` (Obligatorio)

   **Valor válido:**`sessionStart`
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

`Location:` header - The `/api/v1/` part provides the API version. La parte posterior `[…]sessions/` es el ID de sesión.

## Códigos de respuesta

| Código de respuesta HTTP | Descripción |
|---|---|
| 201 | Sesión creada |
| 400 | Solicitud incorrecta |
| 500 | Error del servidor |

