---
title: Esquemas de validación de JSON
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Esquemas de validación de JSON{#json-validation-schemas}

El back-end de Media Analytics valida los parámetros de solicitud para cada tipo de evento mediante esquemas de validación JSON. Estos esquemas están disponibles para usted y sirven como la autoridad actual en los tipos de parámetros utilizados en la API de MA.

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

Para obtener más información sobre el uso de los esquemas de validación de JSON, consulte [Validación de solicitudes de eventos.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
