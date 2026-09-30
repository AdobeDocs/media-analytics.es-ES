---
title: Cargas publicitarias
description: Informa del tipo de carga de publicidad utilizada para cada sesión de medios de streaming.
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
source-wordcount: '161'
ht-degree: 8%
---

# Cargas publicitarias

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Cargas del anuncio**. Consulte [Tipo de carga de anuncio](/help/implementation/variables/standard-metadata/ad-load-type.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Cargas de publicidad** indica el tipo de anuncio cargado al principio de cada sesión de medios de streaming. El valor está definido por el cliente, lo que permite a las organizaciones clasificar las sesiones según su mecanismo de envío de publicidad (por ejemplo, `"linear"`, `"dynamic"` o `"programmatic"`).

## Cómo se rellena esta dimensión

El reproductor establece el tipo de carga de anuncio al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.adLoad` cuando se configura [[!UICONTROL Streaming Media]](/help/reporting/setup/analytics-reporting.md). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## Elementos de dimensión

Cada elemento es el valor literal y la cadena de tipo de carga establecida al inicio de la sesión. Los valores no están restringidos a una enumeración estándar. Defina una taxonomía coherente en todas las implementaciones para que los valores se acumulen de forma predecible en los informes.
