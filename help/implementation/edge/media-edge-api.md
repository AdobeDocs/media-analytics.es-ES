---
title: Configuración de la API de Media Edge para los medios de streaming
description: Envíe datos de medios de streaming directamente a Edge Network mediante la API de Media Edge.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Configuración de la API de Media Edge para los medios de streaming

Si no puede utilizar Web SDK, Mobile SDK o Roku Edge SDK (por ejemplo, en un tiempo de ejecución personalizado o no admitido), puede enviar datos de medios de streaming directamente a Edge Network con la API de Media Edge. La API de utiliza llamadas HTTP RESTful y es totalmente personalizable.

* **Requisitos previos**: complete la [descripción general de la implementación de Edge](overview.md) (esquema, conjunto de datos, secuencia de datos con [!UICONTROL Media Analytics] habilitado).

## Envío de eventos de medios a Edge Network

Los eventos multimedia se envían a los extremos `/ee/va/v1/`, incrustados en la secuencia de datos por el parámetro de consulta `configId`. Por ejemplo, una sesión inicia con un POST en `sessionStart`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

La respuesta devuelve el ID de sesión que deben incluir todos los eventos subsiguientes. Para obtener el conjunto de extremos completo, los formatos de solicitud/respuesta y la especificación de OpenAPI, consulte la [referencia de la API de Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

## Seguimiento de eventos de medios

Consulte la pestaña **API de Media Edge** en cada [evento](/help/implementation/events/overview.md) y página de [variable](/help/implementation/variables/overview.md) para ver las cargas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones de Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Referencia de la API de Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
