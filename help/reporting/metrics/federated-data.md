---
title: Datos federados
description: Cuenta las sesiones recibidas a través de un recurso compartido de datos federado en lugar de la implementación propia de un cliente.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 6%

---


# Datos federados

>[!AVAILABILITY]
>
>El servicio Federated Analytics solo está disponible cuando se utilizan funciones de medios de streaming con Adobe Analytics. Federated Analytics no está disponible en Customer Journey Analytics.

La métrica **Federated data** cuenta las sesiones que se recibieron a través de un recurso compartido de datos federado en lugar de hacerlo desde su propia implementación. Utilícelo para medir el volumen de sesiones compartidas por el socio y comparar la participación, la finalización o la calidad con las sesiones de origen.

Consulte el caso de uso [Federated Media](/help/use-cases/federated-media.md) para obtener más información.

>[!TIP]
>
>Si desea usar datos federados como dimensión, cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne la variable de datos de contexto `a.media.federated` a una eVar.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.sessionDetails.isFederated = true` cuando la sesión llega a través de un canal federado. La métrica aumenta una vez por sesión correspondiente y se comunica en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.federated` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
