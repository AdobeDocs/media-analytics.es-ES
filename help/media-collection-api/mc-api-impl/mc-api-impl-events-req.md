---
title: Implementación de una solicitud de eventos
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Implementación de una solicitud de eventos {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilice la [Solicitud de eventos](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) para las llamadas de seguimiento subsiguientes después de obtener un ID de sesión mediante la [Solicitud de sesiones.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Especifique la ubicación, la marca de tiempo y el tipo del evento junto con los parámetros opcionales que desee incluir en el cuerpo de la solicitud JSON.

El cuerpo de la solicitud JSON para la [solicitud de eventos](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) tiene la misma estructura que la de las sesiones. Sin embargo, compruebe los [esquemas de validación de JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para ver los requisitos y los tipos de parámetros.
