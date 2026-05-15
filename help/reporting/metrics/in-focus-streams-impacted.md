---
title: Transmisiones afectadas por el enfoque
description: Cuenta las sesiones en las que el reproductor estaba enfocado al menos una vez.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Transmisiones afectadas por el enfoque

>[!BEGINSHADEBOX]

*Esta página cubre las **transmisiones afectadas por la métrica de informes en el enfoque**. Consulte [Enfocado](/help/implementation/variables/player-state/in-focus.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

Las **transmisiones afectadas por la métrica en el enfoque** cuentan sesiones en las que el reproductor estaba enfocado al menos una vez. La métrica es un booleano de nivel de sesión: varios eventos de enfoque dentro de la misma sesión cuentan como un flujo afectado. Para el volumen total del evento de enfoque, use [Recuentos de enfoque](in-focus-count.md).

## Cálculo de esta métrica

El servidor multimedia establece el marcador `isSet` en `mediaReporting.states[]` para la entrada `inFocus` en `true` la primera vez que se recibe un evento `media.statesUpdate` con `inFocus` en `statesStart`. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.infocus.set` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "inFocus"`, campo `isSet` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.set` |
