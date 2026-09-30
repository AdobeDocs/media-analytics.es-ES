---
title: El capítulo comienza
description: Cuenta todos los capítulos que comenzaron a reproducirse durante una sesión.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%
---

# El capítulo comienza

La métrica **Capítulos iniciados** cuenta cada capítulo que comenzó a reproducirse durante una sesión. Emparejarlo con [Capítulo completado](chapter-completes.md) para calcular la tasa de finalización del capítulo.

## Cálculo de esta métrica

El servidor multimedia establece este indicador cuando se recibe un evento [inicio de capítulo](/help/implementation/events/chapters/chapter-start.md). La métrica se recoge en la llamada de cierre del capítulo.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.view` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
