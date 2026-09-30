---
title: Formato de flujo
description: Informa del nivel de calidad de cada sesión (normalmente HD o SD).
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%
---

# Formato de flujo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Formato de emisión**. Consulte [Formato de emisión](/help/implementation/variables/standard-metadata/stream-format.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Formato de emisión** indica el nivel de calidad de cada sesión (normalmente `"HD"` o `"SD"`, pero se acepta cualquier cadena). Utilícelo para comparar la participación, la finalización y la calidad en todos los niveles de calidad de entrega.

## Cómo se rellena esta dimensión

El reproductor establece el formato de la emisión al principio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.format` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.format`) |
| Audience Manager | `c_contextdata.a.media.format` |

## Elementos de dimensión

Cada elemento es el valor de formato literal registrado al inicio de la sesión. Use un conjunto estable de valores (`HD`, `SD`, `4K`, `UHD`) para que los elementos de línea no se dividan entre las variaciones ortográficas.
