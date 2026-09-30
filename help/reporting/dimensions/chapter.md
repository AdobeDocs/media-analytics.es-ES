---
title: Capítulo
description: Informa de cada capítulo único reproducido, escrito con un ID de capítulo generado automáticamente.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 9%
---

# Capítulo

La dimensión **Capítulo** indica cada capítulo único reproducido, escrito con un ID de capítulo generado automáticamente. SDK o backend construye el ID a partir del ID de contenido, el índice de capítulos y la hora de inicio de capítulos, de modo que dos sesiones del mismo capítulo en el mismo contenido se acumulan en un solo elemento de línea. Utilice la dimensión como clave de unión para clasificaciones de nivel de capítulo como Nombre del capítulo, Longitud del capítulo, Desplazamiento del capítulo y Posición del capítulo.

## Cómo se rellena esta dimensión

El identificador de capítulo se genera automáticamente cuando se activa un evento [chapter start](/help/implementation/events/chapters/chapter-start.md). El valor no se establece directamente; se deriva de la posición del capítulo, el desplazamiento y el ID de contenido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.name` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `videochapter`, `post_videochapter` |
| Audience Manager | N/A |

## Elementos de dimensión

Cada elemento es un ID de capítulo único. El ID es opaco (normalmente un hash de ID de contenido + índice + desplazamiento) y resulta más útil como clave de agrupación. Emparejar con [nombre de capítulo](chapter-name.md) para obtener una etiqueta descriptiva.
