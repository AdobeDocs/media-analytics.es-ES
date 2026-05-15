---
title: Transmisiones afectadas por imagen en imagen
description: Cuenta las sesiones en las que el usuario ha introducido imagen en imagen al menos una vez.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# Transmisiones afectadas por imagen en imagen

>[!BEGINSHADEBOX]

*Esta página cubre las **transmisiones afectadas por la métrica de informes Imagen en imagen**. Consulte [Imagen en imagen](/help/implementation/variables/player-state/picture-in-picture.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Transmisiones afectadas por imagen en imagen** cuenta las sesiones en las que el visor entró en la reproducción de imagen en imagen al menos una vez. La métrica es un booleano de nivel de sesión: varias entradas de imagen en imagen dentro de la misma sesión cuentan como un flujo afectado. Para el volumen total de la entrada imagen en imagen, use [Recuentos de imagen en imagen](picture-in-picture-count.md).

## Cálculo de esta métrica

El servidor multimedia establece el marcador `isSet` en `mediaReporting.states[]` para la entrada `pictureInPicture` en `true` la primera vez que se recibe un evento `media.statesUpdate` con `pictureInPicture` en `statesStart`. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.pictureinpicture.set` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "pictureInPicture"`, campo `isSet` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
