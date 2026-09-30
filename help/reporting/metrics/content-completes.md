---
title: El contenido finaliza
description: Cuenta las sesiones cuyo cabezal de reproducción llegó al final del contenido.
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
source-wordcount: '142'
ht-degree: 10%
---

# El contenido finaliza

La métrica **Contenido completado** cuenta sesiones cuyo cabezal de reproducción llegó al final del contenido. Emparejarlo con [inicios de contenido](content-starts.md) para calcular la tasa de finalización; emparejarlo con [inicios de medios](media-starts.md) para calcular la tasa de visualización de extremo a extremo.

## Cálculo de esta métrica

El servidor multimedia establece este indicador cuando se recibe un evento [sesión completa](/help/implementation/events/session/session-complete.md). La métrica se recoge en la llamada de cierre. Una sesión que agota el tiempo de espera sin un `sessionComplete` explícito no se cuenta como una finalización.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.complete` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.complete` |
