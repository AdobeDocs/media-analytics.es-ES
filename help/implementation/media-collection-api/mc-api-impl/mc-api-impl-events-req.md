---
title: Implementación de una solicitud de eventos
description: Obtenga información sobre cómo utilizar el punto final de solicitud de eventos para todas las llamadas de seguimiento subsiguientes después de obtener un ID de sesión
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/xJntEcDm5sCGoCeuCjl9x51EOaYcOO2FzFAtK8mbt38
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 99
ht-degree: 56%

---

# Implementación de una solicitud de eventos{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use la [Solicitud de eventos](../mc-api-ref/mc-api-events-req.md) para todas las llamadas de seguimiento subsiguientes después de obtener un identificador de sesión mediante la [Solicitud de sesiones.](../mc-api-ref/mc-api-sessions-req.md) Especifique la ubicación, la marca de tiempo y el tipo del evento junto con los parámetros opcionales que desee incluir en el cuerpo de la solicitud JSON.

El cuerpo de la solicitud JSON para la [solicitud de eventos](../mc-api-ref/mc-api-events-req.md) tiene la misma estructura que la de las sesiones. Sin embargo, compruebe los [esquemas de validación de JSON](../mc-api-ref/mc-api-json-validation.md) para ver los requisitos y los tipos de parámetros.
