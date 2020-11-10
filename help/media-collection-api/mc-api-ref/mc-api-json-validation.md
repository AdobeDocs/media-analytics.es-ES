---
title: Esquemas de validación de JSON
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 9b2f8b14ddb5b814f57c752665b78409e31173e8
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 100%

---


# Esquemas de validación de JSON {#json-validation-schemas}

El back end de Media Analytics valida los parámetros de solicitud para cada tipo de evento con esquemas de validación JSON. Estos esquemas están disponibles para usted y sirven como autoridad actual en los tipos de parámetros utilizados en la API de MA.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Para obtener más información sobre el uso de los esquemas de validación de JSON, consulte [Validación de solicitudes de eventos.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
