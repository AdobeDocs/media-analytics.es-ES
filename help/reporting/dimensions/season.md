---
title: Temporada
description: Informa del número de temporada del contenido episódico.
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
source-wordcount: '140'
ht-degree: 11%
---

# Temporada

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Temporada**. Consulte [Temporada](/help/implementation/variables/standard-metadata/season.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Temporada** indica el número de temporada del contenido episódico. Úsalo junto con [Show](show.md) y [Episode](episode.md) para episodios completos.

## Cómo se rellena esta dimensión

La temporada la establece el reproductor al inicio de la sesión cuando el contenido forma parte de una serie.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.season` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Elementos de dimensión

Cada elemento es el valor de temporada literal notificado al inicio de la sesión (normalmente un entero de cadena como `"1"`, `"2"`). Sea coherente en todos los episodios dentro del mismo programa; la dimensión no normaliza `"1"` y `"01"` al mismo elemento de línea.
