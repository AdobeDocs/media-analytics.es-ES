---
title: Duración total de pantalla completa
description: Informa de los segundos acumulados que el visualizador ha invertido en pantalla completa durante una sesión.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.fullscreen.time` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "fullscreen"`, campo `time` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.time` |
