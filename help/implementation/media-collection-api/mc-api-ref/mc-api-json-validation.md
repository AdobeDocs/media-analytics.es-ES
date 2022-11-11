---
title: Esquemas de validación de JSON de Streaming Media Analytics
description: Qué son los esquemas de validación JSON de medios de transmisión y cómo se utilizan para determinar los parámetros de cuerpo de solicitud correctos para cada tipo de evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 63%

---

# Esquemas de validación de JSON{#json-validation-schemas}

El back end de Media Analytics valida los parámetros de solicitud para cada tipo de evento con esquemas de validación JSON. Estos esquemas están disponibles para usted y sirven como autoridad actual en los tipos de parámetros utilizados en la API de MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Para obtener más información sobre el uso de los esquemas de validación de JSON, consulte [Validación de solicitudes de eventos.](../mc-api-impl/mc-api-validate-reqs.md)
