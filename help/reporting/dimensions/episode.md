---
title: Episodio
description: Informa del número del episodio dentro de una temporada.
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
source-wordcount: '132'
ht-degree: 12%
---

# Episodio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Episodio**. Consulte [Episodio](/help/implementation/variables/standard-metadata/episode.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Episodio** indica el número de episodio dentro de una temporada. Utilícelo junto con [Show](show.md) y [Season](season.md) para lograr participación a nivel de episodio individual.

## Cómo se rellena esta dimensión

El reproductor establece el episodio al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.episode` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## Elementos de dimensión

Cada elemento es el valor literal del episodio notificado al inicio de la sesión (normalmente un entero de cadena como `"13"`). Los números de episodio por sí solos no son únicos en todas las temporadas; combine con Season para obtener desgloses inequívocos.
