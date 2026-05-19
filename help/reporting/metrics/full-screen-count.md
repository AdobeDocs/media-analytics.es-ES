---
title: Recuento de pantalla completa
description: Informa del número de veces que el visualizador ha accedido a pantalla completa durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# Recuento de pantalla completa

>[!BEGINSHADEBOX]

*Esta página cubre la métrica para informes **Recuentos de pantalla completa**. Consulte [Pantalla completa](/help/implementation/variables/player-state/full-screen.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Recuentos de pantalla completa** indica la cantidad de veces que el visor ingresó a pantalla completa durante una sesión. Cada evento de inicio de estado de pantalla completa incrementa el recuento. Asociar con [Transmisiones afectadas por pantalla completa](full-screen-streams-impacted.md) para obtener resúmenes booleanos de nivel de sesión y con [Duración total de pantalla completa](full-screen-total-duration.md) para el tiempo total en el estado.

## Cálculo de esta métrica

El backend de medios incrementa este recuento en cada evento de inicio de estado de pantalla completa. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.fullscreen.count` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "fullscreen"`, campo `count` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
