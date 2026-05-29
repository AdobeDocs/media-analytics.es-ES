---
title: Métricas calculadas
description: Métricas calculadas personalizadas para la creación de informes de medios de streaming en Adobe Analytics y Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# Métricas calculadas

Las métricas calculadas para los servicios de medios de streaming de Adobe son métricas personalizadas creadas a partir de las métricas de medios de streaming estándar, lo que le permite derivar proporciones como el tiempo promedio invertido en la publicidad o la tasa de finalización de medios sin cambiar la implementación.

Para crear estas métricas calculadas en Analysis Workspace, consulta la descripción general de las métricas calculadas correspondientes en [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) o [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Métrica calculada | Descripción | Fórmula |
| --- | --- | --- |
| Promedio de anuncios por flujo de medios | [[!UICONTROL Inicios de publicidad]](/help/reporting/metrics/ad-starts.md) por [[!UICONTROL inicios de medios]](/help/reporting/metrics/media-starts.md) | `[Ad starts] / [Media starts]` |
| Promedio de capítulos por flujo de medios | [[!UICONTROL Capítulos iniciados]](/help/reporting/metrics/chapter-starts.md) por [[!UICONTROL Inicio de contenido]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| Promedio de tiempo invertido en contenido | [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/media-time-spent.md) por [[!UICONTROL inicios de contenido]](/help/reporting/metrics/media-starts.md) (`HH:MM:SS`) | `[Media time spent] / [Media starts]` |
| Promedio de tiempo invertido en contenido | [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md) por [[!UICONTROL inicios de contenido]](/help/reporting/metrics/content-starts.md) (`HH:MM:SS`) | `[Content time spent] / [Content starts]` |
| Promedio de tiempo invertido en publicidad | [[!UICONTROL Tiempo invertido en publicidad]](/help/reporting/metrics/ad-time-spent.md) por [[!UICONTROL inicios de publicidad]](/help/reporting/metrics/ad-starts.md) (`HH:MM:SS`) | `[Ad time spent] / [Ad starts]` |
| Promedio de tiempo dedicado al capítulo | [[!UICONTROL Tiempo invertido en el capítulo]](/help/reporting/metrics/chapter-time-spent.md) por [[!UICONTROL inicios de capítulo]](/help/reporting/metrics/chapter-starts.md) (`HH:MM:SS`) | `[Chapter time spent] / [Chapter starts]` |
| Tasa de finalización de medios | Relación de [[!UICONTROL contenido finalizado]](/help/reporting/metrics/content-completes.md) frente a [[!UICONTROL inicios de medios]](/help/reporting/metrics/media-starts.md) | `[Content completes] / [Media starts]` |
| Tasa de finalización de contenido | Relación de [[!UICONTROL contenido finalizado]](/help/reporting/metrics/content-completes.md) frente a [[!UICONTROL contenido iniciado]](/help/reporting/metrics/content-starts.md) | `[Content completes] / [Content starts]` |
| Tasa de finalización de publicidad | Relación de [[!UICONTROL anuncios finalizados]](/help/reporting/metrics/ad-completes.md) frente a [[!UICONTROL anuncios iniciados]](/help/reporting/metrics/ad-starts.md) | `[Ad completes] / [Ad starts]` |
| Tasa de finalización del capítulo | Tasa de [[!UICONTROL capítulos completados]](/help/reporting/metrics/chapter-completes.md) frente a [[!UICONTROL capítulos iniciados]](/help/reporting/metrics/chapter-starts.md) | `[Chapter completes] / [Chapter starts]` |
| Tasa de caída antes del inicio | Tasa de [[!UICONTROL caídas antes del inicio]](/help/reporting/metrics/drops-before-start.md) frente a [[!UICONTROL inicios de medios]](/help/reporting/metrics/media-starts.md) | `[Drops before start] / [Media starts]` |
| Tasa de duración de pausa de contenido | Relación de [[!UICONTROL duración total de la pausa]](/help/reporting/metrics/total-pause-duration.md) frente a [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md) | `[Total pause duration] / [Content time spent]` |
| Velocidad de duración del búfer de contenido | Relación de [[!UICONTROL duración total del búfer]](/help/reporting/metrics/total-buffer-duration.md) frente a [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md) | `[Total buffer duration] / [Content time spent]` |
| Tasa de tiempo de inicio del contenido | Relación de [[!UICONTROL tiempo para el inicio]](/help/reporting/metrics/time-to-start.md) frente a [[!UICONTROL tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md) | `[Time to start] / [Content time spent]` |
| Tasa de tiempo invertido en publicidad | Relación de [[!UICONTROL tiempo invertido en publicidad]](/help/reporting/metrics/ad-time-spent.md) frente a [[!UICONTROL tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md) | `[Ad time spent] / [Content time spent]` |

