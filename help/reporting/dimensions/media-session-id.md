---
title: ID de sesión de medios
description: Identifica exclusivamente cada sesión de reproducción.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# ID de sesión de medios

La dimensión **ID de sesión de contenido** identifica de forma exclusiva cada sesión de reproducción. Se genera mediante el servidor y se marca en cada evento de la sesión. Utilícela para aislar los eventos de una sola sesión para depurarla o para anular la duplicación de sesiones en análisis personalizados.

## Cómo se rellena esta dimensión

El ID de sesión se genera automáticamente cuando el backend recibe un evento [inicio de sesión](/help/implementation/events/session/session-start.md). Las implementaciones de Web SDK y Mobile SDK capturan y conservan el ID por usted; las implementaciones de API directas deben leer el ID de sesión de la respuesta `sessionStart` (el encabezado `Location` para la API de Media Collection o el identificador `media-analytics:new-session` para la API de Media Edge) e incluirlo en eventos posteriores.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.vsid` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## Elementos de dimensión

Cada elemento es un ID de sesión único generado por el backend (normalmente una cadena alfanumérica de 22 caracteres). Utilice el campo Filter o Search para buscar una sesión específica.
