---
title: Notas de la versión de Adobe Analytics para medios de streaming
description: Ver las notas de la versión actuales de Adobe Analytics.
feature: Release Notes
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 355b3b079d53ae8e83822f61fc79e60e47f6d715
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 91%

---

# Notas de la versión de Adobe Analytics para medios de streaming (mayo de 2023)

**Última actualización:** 12 de mayo de 2023

## Medios relacionados

Para obtener información acerca de nuevas funciones, correcciones e información importante para los administradores, consulte los siguientes recursos.

* [Notas de la versión de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=es)
* [Notas de la versión de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=es)
* Las últimas actualizaciones de la versión para los [productos de Adobe Experience Cloud](https://business.adobe.com/es/products/adobe-experience-cloud-products.html)

* [Tutoriales de Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=es)

## *Notas de la versión actual*

## Funciones nuevas y actualizadas en Adobe Customer Journey Analytics para medios de streaming {#cja-features}

| Función | Descripción | Fecha objetivo |
| ----------- | ---------- | ------- |
| Recopilación de medios: integración con Experience Edge (API y SDK móvil) | Ahora puede utilizar la API de Experience Edge y el SDK móvil para implementar medios de streaming, lo que le permite crear campañas más personalizadas y proporcionar contenido más personalizado, lo que da como resultado más datos de seguimiento para informar sobre ellos.<p>Esta mejora proporciona un método de recopilación unificado en todas las soluciones de, como informes de Customer Journey Analytics, RT-CDP, AJO y reenvío de eventos.  [Más información](/help/implementation/implementation-edge.md) | 12 de mayo de 2023 |
| Panel de visualizadores simultáneos de medios | Comprenda dónde se produjo el pico de concurrencia o dónde se produjeron las disminuciones. Obtenga valiosos conocimientos de la calidad del contenido y de la participación del visualizador, y solucione problemas o planifique el volumen o la escala.  [Más información](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=es) | 9 de agosto de 2022 |
| Panel Tiempo invertido en la reproducción de medios | El Tiempo invertido en la reproducción de medios proporciona un valioso conocimiento sobre la participación de los espectadores y permite a las organizaciones de medios obtener una información más profunda y granular. Esto se realiza con la participación de los usuarios detallada minuto a minuto, por medio de un análisis avanzado del tiempo invertido con capacidades de partición del día. Puede observar la cantidad de tiempo que se dedica a ver sus flujos de contenido en un momento determinado. Puede dividir la duración de la reproducción por diferentes granularidades, incluyendo las nuevas granularidades de 5, 15 y 30 minutos. [Más información](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=es) | 9 de agosto de 2022 |
| Compartir anotaciones en cuadros de resultados móviles | Puede mostrar anotaciones creadas en Workspace en cuadros de resultados móviles. Esto le permite compartir matices de datos contextuales y perspectivas sobre su organización y campañas directamente en proyectos de cuadros de resultados móviles, visibles en la aplicación móvil de paneles de Analytics. [Más información](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=es) | 15 de junio de 2022 |
| Report Builder para actualizaciones de Customer Journey Analytics | Incluye funciones como programación y administrador de bloques de datos. [Más información](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=es) | 18 de mayo de 2022 |
| Anotaciones en Workspace | Las anotaciones en Workspace le permiten comunicar de forma eficaz los matices y perspectivas de datos contextuales a su organización. [Más información](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=es) | El despliegue gradual comienza el 23 de marzo de 2022 |
| Modo de vista previa del proyecto del cuadro de resultados móvil | Inicie una vista previa del aspecto que tendrá su cuadro de resultados móvil en la aplicación de paneles de Analytics, directamente desde el generador de cuadros de resultados. El modo de vista previa permite que los usuarios interactúen con filtros y gráficos del mismo modo que lo harían en la aplicación, lo que les permite obtener una vista previa de la experiencia antes de guardar y compartir el cuadro de resultados. Los usuarios también pueden utilizar el selector de dispositivos en el modo de vista previa para ver el aspecto que tendrá su cuadro de resultados en distintos dispositivos. [Más información](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=es#preview) | 16 de febrero de 2022 |


## Funciones nuevas y actualizadas en Adobe Analytics para medios de streaming {#sm-features}

| Función | Descripción | Fecha objetivo |
| ----------- | ---------- | ------- |
| Seguimiento de varios estados de reproductor | Utilice la API de recopilación de medios para implementar el seguimiento de varios estados de reproductor. [Más información](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=es) | Septiembre de 2022 |
| Se ha cambiado el nombre de los campos XDM | Se ha cambiado el nombre de los campos XDM por coherencia:<br>* Parámetros de audio y vídeo<br>* Parámetros de publicidad<br>* Parámetros de capítulo<br>* Parámetros de estado del reproductor<br>* Parámetros de calidad | Septiembre de 2022 |
| Referencia a la cooperación entre dispositivos | Se ha eliminado la referencia a la cooperación entre dispositivos de Adobe Experience Cloud y el requisito del servicio de ID de Experience Cloud. | Agosto de 2022 |
| Nombres de campo y rutas XDM actualizados para la recopilación y la creación de informes | Se ha actualizado lo siguiente:<br>* Parámetros de audio y vídeo<br>* Parámetros de publicidad<br>* Parámetros de capítulo<br>* Parámetros de estado del reproductor<br>* Parámetros de calidad | Agosto de 2022 |
| Promedio de audiencia por minuto | Los clientes de Media Analytics pueden usar el panel Audiencia media por minuto de medios para comprender mejor el consumo promedio de su contenido. <br>La audiencia media por minuto permite comparar la programación de cualquier género o duración. Además, los clientes pueden comparar o anexar esta audiencia de minuto promedio digital a métricas de minuto promedio de televisión lineales. Este panel proporciona más flexibilidad para medir la audiencia promedio en períodos de tiempo personalizados, así como cuando la clasificación de duración se ha actualizado. [Más información](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=es) | 16 de marzo de 2022 |
| Panel Tiempo invertido en la reproducción de medios | Descubra cómo el panel Tiempo invertido en la reproducción de medios permite a los usuarios de medios comprender su audiencia según el tiempo que han visto durante el día en una granularidad elegida. <br>[Panel Tiempo invertido en la reproducción de medios (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=es) | Enero de 2022 |


## *Notas de la versión anterior*

| Funcionalidad | Descripción | Fecha de objetivo o actualización |
| ----------- | ---------- | -------------- |
| Tiempo invertido en la reproducción de contenido | El Tiempo invertido en la reproducción de contenido de Adobe proporciona un valioso conocimiento sobre la participación de los espectadores y permite a las organizaciones de medios obtener una información más profunda y granular. Esto se realiza con la participación de los usuarios detallada minuto a minuto, a través de un análisis avanzado del tiempo invertido con capacidades de partición del día. Puede observar la cantidad de tiempo que se dedica a ver sus flujos de contenido en un momento determinado. Puede dividir la duración de la reproducción por diferentes granularidades, incluyendo las nuevas granularidades de 5, 15 y 30 minutos. [Más información...](/help/reporting/workspace/media-playback-time-spent.md) | Septiembre de 2021 |
| Panel de visualizador simultáneo de medios en Analytics Workspace | Comprenda dónde se produjo el pico de concurrencia o dónde se produjeron las disminuciones. Obtenga valiosos conocimientos de la calidad del contenido y de la participación del visualizador, y solucione problemas o planifique el volumen o la escala. [Más información…](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Panel de visualizadores simultáneos de medios en Analytics Workspace (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=es#analysis-workspace) | Septiembre de 2020 <br><br><br>enero de 2021 |
| Dispositivos y plataformas compatibles | Media Launch Extension con el SDK de AEP ahora admite los siguientes dispositivos OTT: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (sistema operativo Fire)</li><li>Android TV</li></ul></div> | Junio de 2020 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
