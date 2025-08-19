---
title: Esquemas de validación de JSON de Streaming Media Services
description: Qué son los esquemas de validación JSON de Streaming Media y cómo se utilizan para determinar los parámetros correctos del cuerpo de la solicitud para cada tipo de evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 72%

---

# Esquemas de validación de JSON{#json-validation-schemas}

El back-end de recopilación de medios de streaming valida los parámetros de solicitud para cada tipo de evento con esquemas de validación JSON. Estos esquemas están disponibles para usted y sirven como autoridad actual en los tipos de parámetros utilizados en la API de MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Para obtener más información sobre el uso de los esquemas de validación de JSON, consulte [Validación de solicitudes de eventos.](../mc-api-impl/mc-api-validate-reqs.md)
