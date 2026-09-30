---
title: Recuento de capítulos
description: Informa del número de capítulos que comenzaron durante una sesión.
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
source-wordcount: '172'
ht-degree: 9%
---

# Recuento de capítulos

La métrica **Recuento de capítulos** indica el número de capítulos que comenzaron durante una sesión. Utilícelo para comparar el consumo de capítulos en el contenido. Para los recuentos de inicios de capítulo pivotados por dimensiones de capítulo (nombre de capítulo, posición), utilice la métrica de inicios de capítulo disponible cuando la categoría de variables de capítulo está habilitada.

## Cálculo de esta métrica

El backend de medios incrementa este recuento en cada evento de [inicio de capítulo](/help/implementation/events/chapters/chapter-start.md) recibido durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapterCount` a un evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (el evento personalizado al que la regla de procesamiento asigna `a.media.chapterCount`; consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/A |
