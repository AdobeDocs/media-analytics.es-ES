---
title: Solicitud de eventos
description: null
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Solicitud de eventos{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Parámetro URI

`sid`:: ID de sesión devuelto desde una solicitud de [sesiones.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Cuerpo de la solicitud

El cuerpo de la solicitud debe ser JSON y tener la misma estructura que este cuerpo de solicitud de muestra:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Obligatorio)
   * `playhead`: debe estar en segundos, pero puede ser float.
   * `ts`: marca de tiempo; debe estar en milisegundos.
* `eventType` (Obligatorio)
* `params` (Opcional)
* `customMetadata` (Opcional; enviar solo con `adStart` y `chapterStart` tipos de eventos)
* `qoeData` (Opcional)

Para obtener una lista de tipos de eventos válidos para esta versión, consulte [Tipos de eventos y descripciones.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Seguimiento de publicidad:**solo puede rastrear publicidades dentro de un`adBreak`*.
>
>En ausencia de los "bookends" `adBreakStart` y `adBreakComplete` alrededor de los anuncios, los eventos `adStart` y `adComplete` se omitirán simplemente, y la duración de la publicidad correspondiente se rastreará como la duración del contenido principal. Esto podría tener un impacto considerable en los datos agregados que estarán disponibles en Adobe Analytics.

## Respuesta

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## Códigos de respuesta HTTP

| Código de respuesta HTTP | Descripción | Elementos de acción de cliente |
|---|---|---|
| **204** | **Sin contenido.** <br/><br/>La llamada de Heartbeat se ha realizado correctamente. | N/D |
| **400** | **Solicitud incorrecta.** <br/><br/>El formato de la solicitud es incorrecto. | Compruebe los [esquemas de validación de JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para el tipo de solicitud. |
| **404** | **No encontrado.** No se encontró <br/><br/>el ID de sesión de la sesión de medios en el servicio back-end. | La aplicación cliente debe utilizar la API de [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para crear otra sesión de medios e informar de su seguimiento. |
| **410** | **No existe.** <br/><br/>La sesión de medios se encontró en el servicio back-end pero el cliente ya no puede informar de la actividad en él. | La aplicación cliente debe utilizar la API de [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para crear otra sesión de medios e informar de su seguimiento. |
| **500** | **Error del servidor** | N/D |

