---
title: Capítulo
description: Informa de cada capítulo único reproducido, escrito con un ID de capítulo generado automáticamente.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 8%

---


# Capítulo

La dimensión **Capítulo** indica cada capítulo único reproducido, escrito con un ID de capítulo generado automáticamente. SDK o backend construye el ID a partir del ID de contenido, el índice de capítulos y la hora de inicio de capítulos, de modo que dos sesiones del mismo capítulo en el mismo contenido se acumulan en un solo elemento de línea. Utilice la dimensión como clave de unión para clasificaciones de nivel de capítulo como Nombre del capítulo, Longitud del capítulo, Desplazamiento del capítulo y Posición del capítulo.

## Cómo se rellena esta dimensión

El identificador de capítulo se genera automáticamente cuando se activa un evento [chapter start](/help/implementation/events/chapters/chapter-start.md). El valor no se establece directamente; se deriva de la posición del capítulo, el desplazamiento y el ID de contenido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.name` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `videochapter`, `post_videochapter` |
| Audience Manager | N/A |

## Elementos de dimensión

Cada elemento es un ID de capítulo único. El ID es opaco (normalmente un hash de ID de contenido + índice + desplazamiento) y resulta más útil como clave de agrupación. Emparejar con [nombre de capítulo](chapter-name.md) para obtener una etiqueta descriptiva.
