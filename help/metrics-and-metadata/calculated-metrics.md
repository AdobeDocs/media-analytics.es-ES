---
title: Métricas calculadas
description: Obtenga información sobre las métricas calculadas y fórmulas de métricas de medios de flujo continuo de Adobe.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 78%

---

# Métricas calculadas{#calculated-metrics}

>[!NOTE]
>
>Estas métricas calculadas se introdujeron el 13 de septiembre de 2018.

| Métrica | Descripción | Fórmula |
|---|---|---|
| Promedio de anuncios por flujo de medios | Inicios de publicidad por inicios de contenido | `Ad Starts / Media Starts` |
| Promedio de capítulos por flujo de medios | Inicios de capítulo por inicios de contenido | `Chapter Start / Media Starts` |
| Promedio de Tiempo invertido en contenido | Tiempo total empleado por inicios de contenido (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Promedio de Tiempo invertido en contenido | Tiempo invertido en contenido por contenido iniciado (HH:MM:SS) | `Content Time Spent / Content Start` |
| Promedio de Tiempo invertido en publicidad | Tiempo invertido en publicidad por anuncios iniciados (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Promedio de Tiempo invertido en el capítulo | Tiempo invertido en el capítulo por capítulos iniciados (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Índice de medios finalizados | Tasa de contenido completado frente a medio iniciado (%) | `Content Completes/ Media Starts` |
| Relación de contenido finalizado | Relación de contenido finalizado frente a contenido iniciado (%) | `Content Completes / Content Starts` |
| Relación de anuncios finalizados | Relación de anuncios finalizados frente a anuncios iniciados (%) | `Ad Completes / Ad Starts` |
| Relación de capítulos finalizados | Relación de capítulos finalizados frente a capítulos iniciados (%) | `Chapter Completes / Chapter Starts` |
| Tasa de pérdidas antes del inicio | Relación de pérdidas antes del inicio frente a medios iniciados (%) | `Drops before Starts / Media Starts` |
| Relación de duración de la pausa de contenido | Relación de la duración total de la pausa frente a tiempo invertido en contenido (%) | `Total Pause Duration / Content Time Spent` |
| Relación de la duración del búfer de contenido | Relación de la duración total del búfer frente al tiempo invertido en contenido (% ) | `Total Buffer Duration / Content Time Spent` |
| Relación de tiempo de inicio del contenido | Relación de tiempo para el inicio frente a tiempo invertido en contenido (%) | `Time to Start / Content Time Spent` |
| Relación de tiempo invertido en publicidad | Relación de tiempo invertido en publicidad frente a tiempo invertido en contenido (%) | `Ad Time Spent / Content Time Spent` |
