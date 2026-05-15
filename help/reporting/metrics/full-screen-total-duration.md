---
title: Duración total de pantalla completa
description: Informa de los segundos acumulados que el visualizador ha invertido en pantalla completa durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Duración total de pantalla completa

>[!BEGINSHADEBOX]

*Esta página cubre la métrica para informes **Duración total de pantalla completa**. Consulte [Pantalla completa](/help/implementation/variables/player-state/full-screen.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Duración total de pantalla completa** indica el tiempo acumulado, en segundos, que el usuario pasó en pantalla completa durante una sesión. El backend suma cada intervalo entre un inicio de estado de pantalla completa y el evento de fin de estado coincidente.

## Cálculo de esta métrica

El back-end de medios suma el tiempo transcurrido en todos los intervalos de pantalla completa durante la sesión. La métrica se recoge en la llamada de cierre. Analysis Workspace muestra el valor como `HH:MM:SS`; fuentes de datos, Data Warehouse y API de informes muestran el valor en segundos.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.fullscreen.time` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "fullscreen"`, campo `time` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.time` |
