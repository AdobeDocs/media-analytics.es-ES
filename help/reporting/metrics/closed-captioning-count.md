---
title: Recuentos de subtítulos
description: Notifica la cantidad de veces que el visor ha habilitado subtítulos durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 7%

---


# Recuentos de subtítulos

>[!BEGINSHADEBOX]

*Esta página cubre los **recuentos de subtítulos**de la métrica para informes. Consulte [Subtítulos](/help/implementation/variables/player-state/closed-captioning.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Subtítulos** indica la cantidad de veces que el visor habilitó subtítulos durante una sesión. Cada evento de inicio de estado habilitado para subtítulos incrementa el recuento. Emparejar con [Transmisiones afectadas por los subtítulos opcionales](closed-captioning-streams-impacted.md) para resúmenes booleanos de nivel de sesión y con [Duración total de los subtítulos opcionales](closed-captioning-total-duration.md) para el tiempo total en el estado.

## Cálculo de esta métrica

El servidor multimedia incrementa el campo `count` en la entrada `closedCaptioning` de `mediaReporting.states[]` en cada evento de inicio de estado habilitado para subtítulos. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.closedcaptioning.count` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "closedCaptioning"`, campo `count` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
