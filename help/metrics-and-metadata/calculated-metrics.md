---
title: Métricas calculadas de medios de streaming
description: Obtenga información acerca de las métricas calculadas y fórmulas de métricas de medios de streaming de Adobe.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 100%

---

# Métricas calculadas {#calculated-metrics}

Las métricas calculadas para los medios de streaming son métricas personalizadas que le permiten obtener datos de medios de streaming orientados, como el tiempo promedio invertido en la publicidad o el promedio de anuncios por flujo de medios.

Para obtener información acerca de las métricas calculadas de Adobe Analytics, consulte [Métricas calculadas y calculadas avanzadas (derivadas)](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=es) en la Guía de componentes de Adobe Analytics.

>[!NOTE]
>
>Estas métricas calculadas se introdujeron el 13 de septiembre de 2018.

| Métrica | Descripción | Fórmula |
|---|---|---|
| Promedio de anuncios por flujo de medios | Inicios de publicidad por inicios de contenido | `Ad Starts / Media Starts` |
| Promedio de capítulos por flujo de medios | Inicios de capítulo por inicios de contenido | `Chapter Start / Media Starts` |
| Promedio de Tiempo invertido en contenido | Tiempo total empleado por inicios de medios (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Promedio de Tiempo invertido en contenido | Tiempo invertido en contenido por inicios de contenido (HH:MM:SS) | `Content Time Spent / Content Start` |
| Promedio de Tiempo invertido en publicidad | Tiempo invertido en publicidad por inicios de anuncios (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Promedio de Tiempo invertido en el capítulo | Tiempo invertido en el capítulo por inicios de capítulo (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Índice de medios finalizados | Tasa de contenido completado frente a medio iniciado (%) | `Content Completes/ Media Starts` |
| Relación de contenido finalizado | Relación de contenido finalizado frente a contenido iniciado (%) | `Content Completes / Content Starts` |
| Relación de anuncios finalizados | Relación de anuncios finalizados frente a anuncios iniciados (%) | `Ad Completes / Ad Starts` |
| Relación de capítulos finalizados | Relación de capítulos finalizados frente a capítulos iniciados (%) | `Chapter Completes / Chapter Starts` |
| Tasa de pérdidas antes del inicio | Relación de pérdidas antes del inicio frente a medios iniciados (%) | `Drops before Starts / Media Starts` |
| Relación de duración de la pausa de contenido | Relación de la duración total de la pausa frente a tiempo invertido en contenido (%) | `Total Pause Duration / Content Time Spent` |
| Relación de la duración del búfer de contenido | Relación de la duración total del búfer frente al tiempo invertido en contenido (% ) | `Total Buffer Duration / Content Time Spent` |
| Relación de tiempo de inicio del contenido | Relación de tiempo para el inicio frente a tiempo invertido en contenido (%) | `Time to Start / Content Time Spent` |
| Relación de tiempo invertido en publicidad | Relación de tiempo invertido en publicidad frente a tiempo invertido en contenido (%) | `Ad Time Spent / Content Time Spent` |
