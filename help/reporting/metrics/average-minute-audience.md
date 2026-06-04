---
title: Público medio por minuto
description: Informa del número promedio de espectadores que ven el contenido en un minuto determinado durante el tiempo de ejecución del contenido.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%

---


# Público medio por minuto

La métrica **Audiencia media por minuto** indica la cantidad promedio de espectadores que vieron el contenido en un minuto dado durante el tiempo de ejecución del contenido. Es la medida estándar &quot;AMA&quot; que se utiliza para comparar el alcance de los medios en contenido de diferentes longitudes.

## Cálculo de esta métrica

El servidor multimedia calcula la audiencia media por minuto por sesión como `Content time spent / Content length`. Cuando se suma entre sesiones, el total representa el tamaño promedio de audiencia en cada minuto del contenido. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.averageMinuteAudience` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>La audiencia media por minuto requiere un [Contenido de longitud](/help/reporting/dimensions/content-length.md) distinto de cero. Si la longitud del contenido no está establecida o es cero, esta métrica no se produce para la sesión.
