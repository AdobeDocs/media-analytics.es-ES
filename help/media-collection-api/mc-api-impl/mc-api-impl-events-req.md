---
title: Implementación de una solicitud de eventos
description: Obtenga información sobre cómo utilizar el extremo de solicitud de eventos para todas las llamadas de seguimiento subsiguientes después de obtener un ID de sesión
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 81%

---

# Implementación de una solicitud de eventos{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilice la [Solicitud de eventos](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) para las llamadas de seguimiento subsiguientes después de obtener un ID de sesión mediante la [Solicitud de sesiones.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Especifique la ubicación, la marca de tiempo y el tipo del evento junto con los parámetros opcionales que desee incluir en el cuerpo de la solicitud JSON.

El cuerpo de la solicitud JSON para la [solicitud de eventos](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) tiene la misma estructura que la de las sesiones. Sin embargo, compruebe los [esquemas de validación de JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para ver los requisitos y los tipos de parámetros.
