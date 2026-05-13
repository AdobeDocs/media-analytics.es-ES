---
title: Mostrar tipo
description: Informa del formato del contenido (episodio completo, vista previa, clip u otro).
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

---


# Mostrar tipo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Mostrar tipo**. Consulte [Mostrar tipo](/help/implementation/variables/standard-metadata/show-type.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Mostrar tipo** informa del formato de contenido mediante un código entero de cadena. Utilícelo para separar la visualización de programa completo del contenido corto, como remolques y clips, al medir la participación.

## Cómo se rellena esta dimensión

El tipo de programa lo establece el reproductor al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.type` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoshowtype, post_videoshowtype` |

## Elementos de dimensión

| Valor | Descripción |
| --- | --- |
| `0` | Episodio completo |
| `1` | Vista previa o tráiler |
| `2` | Clip |
| `3` | Otro |

Los valores se registran como cadenas. Se aceptan valores personalizados, pero no se acumulan en los cuatro contenedores integrados.
