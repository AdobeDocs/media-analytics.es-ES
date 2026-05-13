---
title: El anuncio comienza
description: Cuenta todos los anuncios que comenzaron a reproducirse durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---


# El anuncio comienza

La métrica **Inicios de publicidad** cuenta todos los anuncios que comenzaron a reproducirse durante una sesión. Emparejarlo con [Finalizaciones de publicidad](ad-completes.md) para calcular la tasa de finalización del anuncio y con [Recuento de anuncios](/help/reporting/metrics/ad-count.md) para el resumen equivalente de nivel de sesión.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.advertisingDetails.isStarted = true` cuando se recibe un evento `media.adStart`. La métrica se recoge en la llamada de inicio del anuncio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.view` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
