---
seo-title: Implementación de una solicitud de eventos
title: Implementación de una solicitud de eventos
uuid: 3 bfa 313 c-ff 74-4 e 2 e-bbde -6 f 4 a 6221 d 85 b
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Implementación de una solicitud de eventos{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) Especifique la ubicación y la marca de fecha y hora del cursor de reproducción, el tipo de evento y los parámetros opcionales que desee incluir en el cuerpo JSON de la solicitud.

The JSON request body for the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the Sessions request, however check the [JSON validation schemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) for parameter requirements and types.
