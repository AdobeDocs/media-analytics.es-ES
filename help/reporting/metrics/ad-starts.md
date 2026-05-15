---
title: El anuncio comienza
description: Cuenta todos los anuncios que comenzaron a reproducirse durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---


# El anuncio comienza

La métrica **Inicios de publicidad** cuenta todos los anuncios que comenzaron a reproducirse durante una sesión. Emparejarlo con [Finalizaciones de publicidad](ad-completes.md) para calcular la tasa de finalización del anuncio y con [Recuento de anuncios](/help/reporting/metrics/ad-count.md) para el resumen equivalente de nivel de sesión.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.advertisingDetails.isStarted = true` cuando se recibe un evento [inicio de publicidad](/help/implementation/events/ads/ad-start.md). La métrica se recoge en la llamada de inicio del anuncio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.view` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
