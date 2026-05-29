---
title: Recuentos de Silenciar
description: Notifica el número de veces que el visualizador silenció el audio durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%

---


# Recuentos de Silenciar

>[!BEGINSHADEBOX]

*Esta página cubre los **recuentos de Silenciar**de la métrica para informes. Consulte [Silenciar](/help/implementation/variables/player-state/mute.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Silenciar cuenta** indica la cantidad de veces que el visor silenció el audio durante una sesión. Cada evento de inicio de estado silencioso incrementa el recuento. Emparejar con [Transmisiones afectadas por mute](mute-streams-impacted.md) para resúmenes booleanos de nivel de sesión y con [Duración total de Silenciar](mute-total-duration.md) para el tiempo total en el estado.

## Cálculo de esta métrica

El backend de medios incrementa este recuento en cada evento de inicio de estado silencioso. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.mute.count` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "mute"`, campo `count` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
