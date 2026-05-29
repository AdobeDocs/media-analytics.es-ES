---
title: Duración total del estancamiento
description: Informa del tiempo de detención acumulado para sumas y promedios entre sesiones.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%

---


# Duración total del estancamiento

La métrica **Duración total de la demora** indica el tiempo de espera acumulado entre sesiones, adecuado para sumas, promedios y acumulaciones de percentil. Utilice la métrica para calcular el tiempo total que los visualizadores pasan esperando a que se detenga la reproducción en un período de informe.

En Customer Journey Analytics, `xdm.mediaReporting.qoeDataDetails.stallTime` se puede usar como métrica o como dimensión sin un componente de dimensión independiente.

## Cálculo de esta métrica

El back-end de medios suma la duración de cada intervalo de detención, detectado cuando no se registra ningún movimiento del cabezal de reproducción en el contenido principal durante al menos tres eventos consecutivos. La métrica se recoge en la llamada de cierre. Analysis Workspace muestra el valor como `HH:MM:SS`; fuentes de datos, Data Warehouse y API de informes muestran el valor en segundos.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.qoe.stallTime` a un evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (el evento personalizado al que la regla de procesamiento asigna `a.media.qoe.stallTime`; consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
