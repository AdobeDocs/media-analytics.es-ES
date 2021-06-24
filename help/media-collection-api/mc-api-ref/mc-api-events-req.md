---
title: Punto final de solicitud de eventos � API de recopilación de medios de transmisión
description: '"¿Qué son los parámetros y respuestas de extremo de solicitud de eventos de API de recopilación de medios?"'
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 92%

---

# Solicitud de eventos{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Parámetro URI

`sid`: ID de sesión devuelto desde una [Solicitud de sesiones.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

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
* `customMetadata` (Opcional; enviar solo con tipos de eventos `adStart` y `chapterStart`)
* `qoeData` (Opcional)

Para obtener una lista de tipos de eventos válidos para esta versión, consulte [Tipos de eventos y descripciones.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Seguimiento de publicidad:** Solo puede rastrear las publicidades dentro de un`adBreak`*.
>
>En ausencia de los &quot;bookends&quot; `adBreakStart` y `adBreakComplete` alrededor de los anuncios, los eventos `adStart` y `adComplete` se omitirán simplemente, y la duración de la publicidad correspondiente se rastreará como la duración del contenido principal. Esto podría tener un impacto considerable en los datos agregados que estarán disponibles en Adobe Analytics.

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

| Código de respuesta HTTP | Descripción | Elementos de acción del cliente |
|---|---|---|
| **204** | **Sin contenido.** <br/><br/>La llamada de Heartbeat se ha realizado correctamente. | N/D |
| **400** | **Solicitud incorrecta.** <br/><br/>El formato de la solicitud es incorrecto. | Compruebe los [esquemas JSON de validación](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para el tipo de solicitud. |
| **404** | **No encontrado.** <br/><br/>No se ha encontrado el ID de la sesión de contenido en el servicio back-end. | La aplicación del cliente debe utilizar la API de [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para crear otra sesión de medios y realizar el seguimiento de informes. |
| **410** | **Se ha marchado.** <br/><br/>Se ha encontrado la sesión de contenido en el servicio back-end, pero el cliente ya no puede informar de la actividad en ella. | La aplicación del cliente debe utilizar la API de [solicitud de sesiones](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para crear otra sesión de medios y realizar el seguimiento de informes. |
| **500** | **Error del servidor** | N/D |
