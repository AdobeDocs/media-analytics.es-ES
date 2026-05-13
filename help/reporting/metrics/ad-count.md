---
title: Recuento de anuncios
description: Informa del número de anuncios que se iniciaron durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Recuento de anuncios

La métrica **Recuento de anuncios** indica la cantidad de anuncios que se iniciaron durante una sesión. Utilícelo para comprender la carga de anuncios por contenido, canal o tipo de flujo. Para los recuentos de inicios de publicidad pivotados por dimensiones de publicidad (anunciante, campaña, creativo), utilice la métrica de inicios de publicidad disponible cuando la categoría de variable de Anuncios esté habilitada.

## Cálculo de esta métrica

El servidor multimedia incrementa `mediaReporting.sessionDetails.adCount` en cada evento `media.adStart` recibido durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.adCount` a un evento personalizado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (el evento personalizado al que la regla de procesamiento asigna `a.media.adCount`; consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
