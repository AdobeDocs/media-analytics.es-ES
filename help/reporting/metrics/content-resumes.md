---
title: Currículos de contenido
description: Cuenta las sesiones que reanudaron una reproducción interrumpida previamente.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 7%

---


# Currículos de contenido

>[!BEGINSHADEBOX]

*Esta página cubre las **reanudaciones de contenido**&#x200B;métricas de informes. Consulte [Reanudación de contenido](/help/implementation/variables/core/content-resumes.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Reanudación de contenido** cuenta las sesiones que reanudaron una reproducción interrumpida anteriormente. Se incrementa cuando el reproductor marca una sesión como reanudada en `sessionStart` (por ejemplo, después de que un búfer, una pausa o una detención hayan superado los 30 minutos). Utilícelo para separar las sesiones nuevas genuinas de las sesiones de continuación para el mismo visualizador y recurso.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.sessionDetails.hasResume = true` cuando `mediaCollection.sessionDetails.hasResume` es `true` en el evento `media.sessionStart`. El reproductor debe marcar explícitamente la sesión como reanudación. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.resume` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
