---
title: Recuentos de Imagen en imagen
description: Informa del número de veces que el usuario ha introducido imagen en imagen durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 8%

---


# Recuentos de Imagen en imagen

>[!BEGINSHADEBOX]

*Esta página cubre los recuentos de **Imagen en imagen**&#x200B;de la métrica para informes. Consulte [Imagen en imagen](/help/implementation/variables/player-state/picture-in-picture.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Recuento de imagen en imagen** indica la cantidad de veces que el visor entró en la reproducción de imagen en imagen durante una sesión. Cada evento de inicio de estado imagen en imagen incrementa el recuento. Emparejar con [Transmisiones afectadas por imagen en imagen](picture-in-picture-streams-impacted.md) para obtener resúmenes booleanos de nivel de sesión y con [Duración total de imagen en imagen](picture-in-picture-total-duration.md) para el tiempo total en el estado.

## Cálculo de esta métrica

El servidor multimedia incrementa el campo `count` en la entrada `pictureInPicture` de `mediaReporting.states[]` en cada evento de inicio de estado de imagen en imagen. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.pictureinpicture.count` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "pictureInPicture"`, campo `count` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
