---
title: Recuentos de Enfocado
description: Indica la cantidad de veces que el reproductor ganó Focus durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# Recuentos de Enfocado

>[!BEGINSHADEBOX]

*Esta página cubre la métrica de informes **Recuentos de enfoque**. Consulte [Enfocado](/help/implementation/variables/player-state/in-focus.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **En el enfoque cuenta** indica la cantidad de veces que el reproductor se enfocó durante una sesión. Cada evento de inicio de estado de enfoque incrementa el recuento. Emparejar con [Transmisiones afectadas por en el enfoque](in-focus-streams-impacted.md) para resúmenes booleanos de nivel de sesión y con [Duración total del enfoque](in-focus-total-duration.md) para el tiempo total en el estado.

## Cálculo de esta métrica

El backend de medios incrementa este recuento en cada evento de inicio de estado de enfoque. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.infocus.count` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "inFocus"`, campo `count` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
