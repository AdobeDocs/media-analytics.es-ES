---
title: Mostrar tipo
description: Informa del formato del contenido (episodio completo, vista previa, clip u otro).
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
source-wordcount: '145'
ht-degree: 11%
---

# Mostrar tipo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Mostrar tipo**. Consulte [Mostrar tipo](/help/implementation/variables/standard-metadata/show-type.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Mostrar tipo** informa del formato de contenido mediante un código entero de cadena. Utilícelo para separar la visualización de programa completo del contenido corto, como remolques y clips, al medir la participación.

## Cómo se rellena esta dimensión

El tipo de programa lo establece el reproductor al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.type` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## Elementos de dimensión

| Valor | Descripción |
| --- | --- |
| `0` | Episodio completo |
| `1` | Vista previa o tráiler |
| `2` | Clip |
| `3` | Otro |

Los valores se registran como cadenas. Se aceptan valores personalizados, pero no se acumulan en los cuatro contenedores integrados.
