---
title: Con autorización
description: Cuenta las sesiones cuyo usuario ha sido autorizado a través de Adobe Pass.
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
source-wordcount: '137'
ht-degree: 12%
---

# Con autorización

>[!BEGINSHADEBOX]

*Esta página cubre la métrica para informes **Autorizado**. Consulte [Autorizado](/help/implementation/variables/standard-metadata/authorized.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Autorizado** cuenta las sesiones cuyo usuario ha sido autorizado a través de Adobe Pass o TV-Everywhere. Asociar con la dimensión [MVPD](/help/reporting/dimensions/mvpd.md) para dividir el volumen de autenticación por proveedor.

## Cálculo de esta métrica

El backend de medios aumenta el recuento cuando el reproductor marca la sesión como autorizada al inicio de la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.pass.auth` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
