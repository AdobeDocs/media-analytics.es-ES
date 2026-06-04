---
title: El contenido finaliza
description: Cuenta las sesiones cuyo cabezal de reproducción llegó al final del contenido.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.complete` |
