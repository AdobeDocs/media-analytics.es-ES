---
title: Esquemas de validación de JSON de Streaming Media Services
description: Qué son los esquemas de validación JSON de Streaming Media y cómo se utilizan para determinar los parámetros correctos del cuerpo de la solicitud para cada tipo de evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ZWKv1LJKc8qLkZYpcNdDFEs8Er70toRCoufarMcgVKQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 84
ht-degree: 71%

---

# Esquemas de validación de JSON{#json-validation-schemas}

El back-end de recopilación de medios de streaming valida los parámetros de solicitud para cada tipo de evento con esquemas de validación JSON. Estos esquemas están disponibles para usted y sirven como autoridad actual en los tipos de parámetros utilizados en la API de MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Para obtener más información sobre el uso de los esquemas de validación de JSON, consulte [Validación de solicitudes de eventos.](../mc-api-impl/mc-api-validate-reqs.md)
