---
title: Marcadores de progreso
description: Contar sesiones cuyo cabezal de reproducción superó cada uno de los cinco umbrales fijos (10 %, 25 %, 50 %, 75 % y 95 %).
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 9%

---


# Marcadores de progreso

Los **marcadores de progreso** son cinco métricas independientes que cuentan las sesiones cuyo cabezal de reproducción superó cada uno de los cinco umbrales fijos (10 %, 25 %, 50 %, 75 % y 95 % de la duración del contenido). Utilícelos para trazar la lista desplegable durante el tiempo de ejecución del contenido; emparéjelos con [Inicios de contenido](content-starts.md) para calcular la proporción de sesiones iniciadas que alcanzaron cada hito.

Cada marcador se activa una vez por sesión y no se vuelve a activar en la recuperación. Los marcadores omitidos al buscar hacia delante no se cuentan (por ejemplo, un visor que salta de un 5 % a un 60 % déclencheur los marcadores de 10 %, 25 % y 50 % a la vez).

## Cálculo de cada marcador

El servidor multimedia evalúa el cabezal de reproducción del informe con [Longitud del contenido](../dimensions/content-length.md) después de cada evento. Cuando el cabezal de reproducción cruza por primera vez un umbral, el indicador correspondiente se establece para el resto de la sesión. Los cinco marcadores se registran en la llamada de cierre. Las sesiones que nunca producen un evento de reproducción en el contenido principal (como [Pérdidas antes del inicio](/help/reporting/metrics/drops-before-start.md)) nunca hacen avanzar el cabezal de reproducción más allá de ningún umbral, por lo que no se establece ningún marcador.

>[!IMPORTANT]
>
>Los marcadores de progreso requieren un [Contenido de longitud](/help/reporting/dimensions/content-length.md) distinto de cero e informes precisos del cabezal de reproducción. Si la longitud del contenido no está establecida, es cero o es incorrecta, los marcadores pueden activarse en el momento incorrecto o no activarse.

### Marcador de progreso al 10 % {#progress-10}

Se activa cuando el cabezal de reproducción alcanza por primera vez el 10 % de la longitud del contenido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.progress10` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress10` |

### Marcador de progreso del 25 % {#progress-25}

Se activa cuando el cabezal de reproducción alcanza por primera vez el 25 % de la longitud del contenido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.progress25` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress25` |

### Marcador de progreso al 50 % {#progress-50}

Se activa cuando el cabezal de reproducción alcanza por primera vez el 50 % de la longitud del contenido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.progress50` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress50` |

### Marcador de progreso al 75 % {#progress-75}

Se activa cuando el cabezal de reproducción alcanza por primera vez el 75 % de la longitud del contenido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.progress75` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress75` |

### Marcador de progreso al 95 % {#progress-95}

Se activa cuando el cabezal de reproducción alcanza por primera vez el 95 % de la longitud del contenido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.progress95` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress95` |
