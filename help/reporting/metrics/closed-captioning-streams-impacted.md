---
title: Transmisiones afectadas por los subtítulos
description: Cuenta las sesiones en las que el visor habilitó subtítulos al menos una vez.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# Transmisiones afectadas por los subtítulos

>[!BEGINSHADEBOX]

*Esta página cubre las **transmisiones afectadas por los subtítulos**&#x200B;de la métrica para informes. Consulte [Subtítulos](/help/implementation/variables/player-state/closed-captioning.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

Las **transmisiones afectadas por los subtítulos opcionales** cuentan sesiones en las que el visor habilitó subtítulos al menos una vez. La métrica es un booleano de nivel de sesión: varios subtítulos se alternan dentro del mismo recuento de sesiones como un flujo afectado. Para el volumen total de subtítulos habilitados, use [Recuentos de subtítulos](closed-captioning-count.md).

## Cálculo de esta métrica

El backend de medios establece este indicador la primera vez que se recibe un evento de inicio de estado para habilitar subtítulos durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.closedcaptioning.set` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "closedCaptioning"`, campo `isSet` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.set` |
