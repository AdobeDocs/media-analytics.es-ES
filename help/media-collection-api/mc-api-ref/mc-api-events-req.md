---
seo-title: Solicitud de eventos
title: Solicitud de eventos
uuid: b 237 f 0 a 0-dc 29-418 b -89 ee -04 c 596 a 27 f 39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Solicitud de eventos{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Parámetro de URI

`sid`: El ID de sesión devuelto desde una [solicitud de Sesiones.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Cuerpo de la solicitud

El cuerpo de la solicitud debe ser JSON y debe tener la misma estructura que este cuerpo de solicitud de muestra:

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
* `customMetadata` (Opcional; enviar solo con `adStart` tipos `chapterStart` de eventos)
* `qoeData` (Opcional)

Para obtener una lista de tipos de eventos válidos para esta versión, consulte [Tipos de eventos y descripciones.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Seguimiento de anuncios:**solo puede rastrear publicidades dentro de`adBreak`* un.
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
| **404** | **No encontrado.**<br/><br/>No se encontró el ID de sesión de la sesión de medios en el servicio back-end. | La aplicación cliente debe utilizar la API de [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para crear otra sesión de medios e informar de su seguimiento. |
| **410** | **No existe.**<br/><br/>La sesión de medios se encuentra en el servicio back-end pero el cliente ya no puede informar sobre ella. | La aplicación cliente debe utilizar la API de [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para crear otra sesión de medios e informar de su seguimiento. |
| **500** | **Error del servidor** | N/D |

