---
title: Métricas calculadas
description: Métricas calculadas personalizadas para la creación de informes de medios de streaming en Adobe Analytics y Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: ea740a32bbd5e640cd437cd8c5c4f48071a0d02c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---


# Métricas calculadas

Las métricas calculadas para los servicios de medios de streaming de Adobe son métricas personalizadas creadas a partir de las métricas de medios de streaming estándar, lo que le permite derivar proporciones como el tiempo promedio invertido en la publicidad o la tasa de finalización de medios sin cambiar la implementación.

Para crear estas métricas calculadas en Analysis Workspace, consulta la descripción general de las métricas calculadas correspondientes en [Adobe Analytics](https://experienceleague.adobe.com/es/docs/analytics/components/calculated-metrics/cm-overview) o [Customer Journey Analytics](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Métrica calculada | Descripción | Fórmula |
| --- | --- | --- |
| Promedio de anuncios por flujo de medios | Inicios de publicidad por inicios de contenido | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Promedio de capítulos por flujo de medios | Inicios de capítulo por inicios de contenido | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Promedio de tiempo invertido en contenido | Tiempo total empleado por inicios de medios (`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Promedio de tiempo invertido en contenido | Tiempo invertido en contenido por inicios de contenido (`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Promedio de tiempo invertido en publicidad | Tiempo invertido en publicidad por inicios de publicidad (`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Promedio de tiempo dedicado al capítulo | Tiempo invertido en el capítulo por capítulo iniciado (`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Tasa de finalización de medios | Relación de contenido finalizado frente a medios iniciados | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Tasa de finalización de contenido | Relación de contenido completado frente a inicios de contenido | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Tasa de finalización de publicidad | Relación de anuncios finalizados frente a anuncios iniciados | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Tasa de finalización del capítulo | Relación de capítulos completados frente a capítulos iniciados | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Tasa de caída antes del inicio | Relación de caídas antes del inicio frente a medios iniciados | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Tasa de duración de pausa de contenido | Relación de la duración total de la pausa frente al tiempo invertido en contenido | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Velocidad de duración del búfer de contenido | Relación de la duración total del búfer frente al tiempo invertido en contenido | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Tasa de tiempo de inicio del contenido | Relación de tiempo para el inicio frente a tiempo invertido en contenido | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Tasa de tiempo invertido en publicidad | Relación de tiempo invertido en publicidad frente a tiempo invertido en contenido | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
