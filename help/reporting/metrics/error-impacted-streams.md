---
title: Flujos afectados por error
description: Cuenta las sesiones en las que se produjo al menos un error.
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
source-wordcount: '143'
ht-degree: 10%
---

# Flujos afectados por error

La métrica **Flujos afectados por el error** cuenta sesiones en las que se produjo al menos un error (`trackError` se llamó o se activó un evento [error](/help/implementation/events/error.md)). La métrica es un booleano de nivel de sesión; varios errores dentro de la misma sesión cuentan como un flujo afectado. Para el volumen total de errores, use [Errores](/help/reporting/dimensions/errors.md).

## Cálculo de esta métrica

El servidor multimedia establece este indicador la primera vez que se recibe un evento de [error](/help/implementation/events/error.md) durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.error` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
