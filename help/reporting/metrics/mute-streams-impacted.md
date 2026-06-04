---
title: Transmisiones afectadas por silenciar
description: Cuenta las sesiones en las que el visualizador silenció el audio al menos una vez.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---


# Transmisiones afectadas por silenciar

>[!BEGINSHADEBOX]

*Esta página cubre las **transmisiones afectadas por la métrica de informes silenciar**. Consulte [Silenciar](/help/implementation/variables/player-state/mute.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

Las **transmisiones afectadas por la métrica silenciar** cuentan sesiones en las que el visor silenció el audio al menos una vez. La métrica es un booleano de nivel de sesión: varios toggles de silencio dentro del mismo recuento de sesiones como un flujo afectado. Para el volumen silencioso total, use [Recuentos silenciosos](mute-count.md).

## Cálculo de esta métrica

El backend de medios establece este indicador la primera vez que se recibe un evento de inicio de estado silencioso durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.mute.set` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "mute"`, campo `isSet` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
