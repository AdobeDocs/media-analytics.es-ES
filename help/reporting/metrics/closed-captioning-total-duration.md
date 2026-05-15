---
title: Duración total de los subtítulos
description: Informa de los segundos acumulados en los que se activaron los subtítulos durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%

---


# Duración total de los subtítulos

>[!BEGINSHADEBOX]

*Esta página cubre la métrica para informes **Duración total de los subtítulos**. Consulte [Subtítulos](/help/implementation/variables/player-state/closed-captioning.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Duración total de los subtítulos** indica el tiempo acumulado, en segundos, que se habilitaron los subtítulos durante una sesión. El servidor suma cada intervalo entre un inicio de estado habilitado para subtítulos y el evento de fin de estado coincidente.

## Cálculo de esta métrica

El backend de medios suma el tiempo transcurrido en todos los intervalos habilitados para subtítulos durante la sesión. La métrica se recoge en la llamada de cierre. Analysis Workspace muestra el valor como `HH:MM:SS`; fuentes de datos, Data Warehouse y API de informes muestran el valor en segundos.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.closedcaptioning.time` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "closedCaptioning"`, campo `time` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.time` |
