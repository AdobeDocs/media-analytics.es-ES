---
title: Transmisiones afectadas por silenciar
description: Cuenta las sesiones en las que el visualizador silenció el audio al menos una vez.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%
---

# Transmisiones afectadas por silenciar

>[!BEGINSHADEBOX]

*Esta página cubre las **transmisiones afectadas por la métrica de informes silenciar**. Consulte [Silenciar](/help/implementation/variables/player-state/mute.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

Las **transmisiones afectadas por la métrica silenciar** cuentan sesiones en las que el visor silenció el audio al menos una vez. La métrica es un booleano de nivel de sesión; varios silenciadores se conmutan dentro de la misma sesión y cuentan como un flujo afectado. Para el volumen silencioso total, use [Recuentos silenciosos](mute-count.md).

## Cálculo de esta métrica

El backend de medios establece este indicador la primera vez que se recibe un evento de inicio de estado silencioso durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.states.mute.set` cuando el [[!UICONTROL seguimiento de estado del reproductor]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada donde `name = "mute"`, campo `isSet` |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
