---
title: Show
description: Informa del nombre del programa o la serie del contenido de vídeo que forma parte de una serie.
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
source-wordcount: '158'
ht-degree: 10%
---

# Show

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Mostrar**. Consulte [Mostrar](/help/implementation/variables/standard-metadata/show.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Mostrar** indica el nombre del programa o serie. Los episodios de varias temporadas se acumulan en el mismo elemento de línea de programa, por lo que debe utilizarlo para comparar la participación a lo largo de toda la duración de una serie.

## Cómo se rellena esta dimensión

El reproductor establece el programa al principio de la sesión cuando el contenido forma parte de una serie.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.show` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Elementos de dimensión

Cada elemento es el nombre literal para mostrar indicado al inicio de la sesión (por ejemplo, `"Blinding Light"`). Utilice nombres diferentes y estables por programa para que los datos no se contraigan en programas no relacionados que compartan una palabra.
