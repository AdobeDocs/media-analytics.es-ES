---
title: Notas de la versión de medios de streaming
description: Vea las notas de la versión de los servicios de medios de streaming.
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 720
ht-degree: 36%

---

# Notas de la versión de medios de streaming

**Última actualización**: 4 de junio de 2026

## 2026

| Función | Descripción | Fecha |
| --- | --- | --- |
| **Datos de programación de soporte** | Cargue datos programados del contenido en directo anterior para rastrear el número de espectadores por programa o segmento. Los tipos de contenido admitidos son:<ul><li>Plataformas FAST (Free Ad Supported TV)</li><li>Streams locales</li><li>Deportes en directo</li></ul>Consulte el caso de uso [Cargar datos de programación para rastrear contenido en directo](/help/use-cases/track-schedule-data.md) para obtener más información. | El despliegue comienza el 29 de octubre de 2025<p>Disponibilidad general: octubre de 2026</p> |

## 2025

| Función | Descripción | Fecha |
| --- | --- | --- |
| **`mediaTimed`desaprobación de campo XDM** | El objeto XDM `mediaTimed` está obsoleto en favor de `mediaReporting` rutas de campo. Los clientes que implementaron el conector de origen de Analytics antes del 9 de mayo de 2025 deben migrar sus configuraciones. Consulte las siguientes guías de migración para obtener más información:<ul><li>[Migrar audiencias a los nuevos campos de medios de transmisión](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[Migrar Customer Journey Analytics para usar los nuevos campos de medios de transmisión](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[Migrar preparación de datos para campos personalizados a los nuevos campos de medios de transmisión](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[Migrar perfiles a los nuevos campos de medios de transmisión](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | Octubre de 2025 |

## 2024

| Función | Descripción | Fecha |
| --- | --- | --- |
| **Compatibilidad con Web SDK** | Envíe datos web de medios de streaming a Adobe Experience Platform Edge Network mediante la extensión de etiquetas Web SDK o Web SDK, lo que permite un método de recopilación unificado en soluciones de Platform como Customer Journey Analytics, Real-time CDP, Journey Optimizer y reenvío de eventos. Consulte [Configurar Web SDK para medios de transmisión](/help/implementation/edge/web-sdk.md) o [Configurar la extensión de etiquetas Web SDK para medios de transmisión](/help/implementation/edge/web-sdk-tags.md) para obtener más información. | 29 de mayo de 2024 |
| **Compatibilidad con Roku** | Envíe datos de medios de streaming a Adobe Experience Platform mediante Roku SDK. Consulte [Configuración de Roku para medios de streaming](/help/implementation/edge/roku.md) para obtener más información. | 12 de abril de 2024 |

## 2023

| Función | Descripción | Fecha |
| --- | --- | --- |
| **Soporte de Experience Edge** | Implemente la recopilación de medios de streaming mediante la API de Media Edge o los SDK móviles para iOS y Android.<ul><li>[Configurar la API de Media Edge para los medios de transmisión](/help/implementation/edge/media-edge-api.md)</li><li>[Configurar iOS para medios de transmisión](/help/implementation/edge/ios.md) o [configurar iOS para medios de transmisión con etiquetas](/help/implementation/edge/ios-tags.md)</li><li>[Configurar Android para medios de transmisión](/help/implementation/edge/android.md) o [configurar Android para medios de transmisión con etiquetas](/help/implementation/edge/android-tags.md)</li></ul> | sábado, 12 de mayo de 2023 |

## 2022

| Función | Descripción | Fecha |
| --- | --- | --- |
| **Seguimiento de varios estados de reproductor** | Utilice la API de recopilación de medios para implementar varios [estados de seguimiento del reproductor](/help/implementation/events/player-state/overview.md). | Septiembre de 2022 |
| Se ha cambiado el nombre de los campos XDM | Se ha cambiado el nombre de los campos XDM por coherencia:<ul><li>Parámetros de audio y vídeo</li><li>Parámetros de anuncio</li><li>Parámetros de capítulo</li><li>Parámetros de estado del reproductor</li><li>Parámetros de calidad</li></ul> | Septiembre de 2022 |
| **Paneles agregados a Customer Journey Analytics** | Se agregaron el [panel de visores simultáneos de medios](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) y el [panel de tiempo invertido en la reproducción de medios](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent) a Customer Journey Analytics. | 9 de agosto de 2022 |
| **Promedio de público por minuto** | Puede usar el [panel Audiencia media por minuto](https://experienceleague.adobe.com/es/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel) para comprender mejor el consumo promedio de contenido. <br>El público medio por minuto permite comparar la programación de cualquier género o duración. Además, los clientes pueden comparar o anexar este público digital promedio por minuto a métricas promedio por minuto de televisión lineales. Este panel proporciona más flexibilidad para medir el público promedio en períodos de tiempo personalizados, así como cuando la clasificación de duración se ha actualizado. | 16 de marzo de 2022 |

## 2021

| Función | Descripción | Fecha |
| --- | --- | --- |
| **Tiempo invertido en la reproducción de medios** | El [panel Tiempo invertido en la reproducción](https://experienceleague.adobe.com/es/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent) proporciona un valioso insight en la participación de los espectadores y permite a las organizaciones de medios obtener una información más profunda y granular, con la participación de los usuarios detallada minuto a minuto, a través de un análisis avanzado del tiempo invertido con capacidades de partición del día. Puede observar la cantidad de tiempo que se dedica a ver sus flujos de contenido en un momento determinado. Puede dividir la duración de la reproducción por diferentes granularidades, incluidas las nuevas granularidades de 5, 15 y 30 minutos. | Septiembre de 2021 |

## 2020

| Función | Descripción | Fecha |
| --- | --- | --- |
| **Panel de visualizadores simultáneos de medios** | El [panel de visores simultáneos](https://experienceleague.adobe.com/es/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers) le ayuda a comprender dónde se produjo la concurrencia máxima o dónde se produjeron los descensos. Obtenga valiosos conocimientos de la calidad del contenido y de la participación del visualizador, y solucione problemas o planifique el volumen o la escala.<br><br>[Panel de visualizadores simultáneos de medios (tutorial)](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | Septiembre de 2020; enero de 2021 |
| **Dispositivos y plataformas compatibles** | Media Launch Extension con el SDK de AEP ahora admite los siguientes dispositivos OTT: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (sistema operativo Fire)</li><li>Android TV</li></ul></div> | Junio de 2020 |
