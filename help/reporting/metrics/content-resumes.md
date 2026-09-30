---
title: Currículos de contenido
description: Cuenta las sesiones que reanudaron una reproducción interrumpida previamente.
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
source-wordcount: '171'
ht-degree: 9%
---

# Currículos de contenido

>[!BEGINSHADEBOX]

*Esta página cubre las **reanudaciones de contenido**&#x200B;métricas de informes. Consulte [Reanudación de contenido](/help/implementation/variables/core/content-resumes.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Reanudación de contenido** cuenta las sesiones que reanudaron una reproducción interrumpida anteriormente. Se incrementa cuando el reproductor marca una sesión como reanudada en `sessionStart` (por ejemplo, después de que un búfer, una pausa o una detención hayan superado los 30 minutos). Utilícelo para separar las sesiones nuevas genuinas de las sesiones de continuación para el mismo visualizador y recurso.

## Cálculo de esta métrica

El servidor multimedia establece este indicador cuando `xdm.mediaCollection.sessionDetails.hasResume` es `true` en el evento [inicio de sesión](/help/implementation/events/session/session-start.md). El reproductor debe marcar explícitamente la sesión como reanudación. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.resume` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/A |
