---
title: Con autorización
description: Cuenta las sesiones cuyo usuario ha sido autorizado a través de Adobe Pass.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
