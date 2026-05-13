---
title: Transmisiones afectadas por pantalla completa
description: Cuenta las sesiones en las que el usuario accedió a pantalla completa al menos una vez.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# Transmisiones afectadas por pantalla completa

>[!BEGINSHADEBOX]

*Esta página cubre las **transmisiones afectadas por la métrica de informes de pantalla completa**. Consulte [Pantalla completa](/help/implementation/variables/player-state/full-screen.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

Las **transmisiones afectadas por la métrica de pantalla completa** cuentan sesiones en las que el visor entró a pantalla completa al menos una vez. La métrica es un booleano de nivel de sesión: varias entradas de pantalla completa dentro de la misma sesión cuentan como un flujo afectado. Para el volumen total de entradas a pantalla completa, usa [Recuentos de pantalla completa](full-screen-count.md).

## Cálculo de esta métrica

El servidor multimedia establece el marcador `isSet` en `mediaReporting.states[]` para la entrada `fullscreen` en `true` la primera vez que se recibe un evento `media.statesUpdate` con `fullscreen` en `statesStart`. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.fullscreen.set` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "fullscreen"`, campo `isSet` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
