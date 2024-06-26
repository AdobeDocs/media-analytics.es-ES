---
title: Esquemas de validación de JSON del complemento de recopilación de medios de streaming
description: Qué son los esquemas de validación JSON de Streaming Media y cómo se utilizan para determinar los parámetros correctos del cuerpo de la solicitud para cada tipo de evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 70%

---

# Esquemas de validación de JSON{#json-validation-schemas}

El back-end del complemento Streaming Media Collection valida los parámetros de solicitud para cada tipo de evento con esquemas de validación JSON. Estos esquemas están disponibles para usted y sirven como autoridad actual en los tipos de parámetros utilizados en la API de MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Para obtener más información sobre el uso de los esquemas de validación de JSON, consulte [Validación de solicitudes de eventos.](../mc-api-impl/mc-api-validate-reqs.md)
