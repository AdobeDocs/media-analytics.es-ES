---
title: El anuncio finaliza
description: Cuenta todos los anuncios reproducidos hasta su finalización.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# El anuncio finaliza

La métrica **Anuncio completado** cuenta cada anuncio reproducido hasta su finalización. Emparejarlo con [Inicios de publicidad](ad-starts.md) para calcular la tasa de finalización del anuncio.

## Cálculo de esta métrica

El servidor multimedia establece este indicador cuando se recibe un evento [y completado](/help/implementation/events/ads/ad-complete.md). La métrica se recoge en la llamada de cierre del anuncio. Los anuncios omitidos o abandonados no se cuentan como finalizaciones.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.complete` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
