---
title: Streaming Media Collection API ‐ Punto final de solicitud de eventos
description: ¿Qué son los parámetros y respuestas de solicitud de parámetros de extremo de eventos de API de recopilación de medios?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 70%

---

# Solicitud de eventos{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## Parámetro URI

`sid`: ID de sesión devuelto desde una [Solicitud de sesiones](mc-api-sessions-req.md).

## Cuerpo de la solicitud

El cuerpo de la solicitud debe ser JSON y tener la misma estructura que este cuerpo de solicitud de muestra:

```json
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

Para obtener una lista de tipos de eventos válidos y ejemplos de implementación por SDK, consulte [Información general sobre eventos](/help/implementation/events/overview.md).

>[!IMPORTANT]
>
>***Seguimiento de publicidad:** Solo puede rastrear las publicidades dentro de un`adBreak`*.
>
>En ausencia de los &quot;bookends&quot; `adBreakStart` y `adBreakComplete` alrededor de los anuncios, los eventos `adStart` y `adComplete` se omitirán simplemente, y la duración de la publicidad correspondiente se rastreará como la duración del contenido principal. Esto podría tener un impacto considerable en los datos agregados que estarán disponibles en Adobe Analytics.

## Respuesta

```text
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
| **204** | **Sin contenido.** La llamada a <br/><br/>Heartbeat se realizó correctamente. | N/D |
| **400** | **Solicitud incorrecta.** El formato de la solicitud <br/><br/> no es correcto. | Compruebe los [esquemas JSON de validación](mc-api-json-validation.md) para el tipo de solicitud. |
| **404** | **No encontrado.** <br/><br/>No se encontró el Id. de sesión para la sesión de contenido en el servicio back-end. | La aplicación del cliente debe utilizar la API de [solicitud de sesiones](mc-api-sessions-req.md) para crear otra sesión de medios y realizar el seguimiento de informes. |
| **410** | **Desaparecido.** <br/><br/>Se encontró la sesión de contenido en el servicio back-end, pero el cliente ya no puede informar de la actividad en ella. | La aplicación del cliente debe utilizar la API de [solicitud de sesiones](mc-api-sessions-req.md) para crear otra sesión de medios y realizar el seguimiento de informes. |
| **500** | **Error del servidor** | N/A |
