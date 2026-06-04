---
title: Género
description: Género de contenido de informes. El contenido de varios géneros se divide en elementos de línea, cada uno de los cuales recibe el mismo peso de métrica.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---


# Género

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Género**. Consulte [Género](/help/implementation/variables/standard-metadata/genre.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Género** indica el género de contenido. El género se recopila como una cadena delimitada por comas y se almacena como una dimensión de lista. El contenido de varios géneros se divide en elementos de línea independientes, cada uno de los cuales recibe el mismo peso de métrica. Utilícelo para comparar la participación entre géneros sin contar dos veces el tiempo empleado en un único recurso de varios géneros.

## Cómo se rellena esta dimensión

El reproductor establece el género al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.genre` (almacenados como una variable de lista) cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) o [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) (heredado) |
| Fuentes de datos | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Elementos de dimensión

Cada elemento es un valor de género. Las sesiones de varios géneros (por ejemplo, `"Drama,Action"`) aparecen como dos elementos de línea independientes (`Drama` y `Action`), y cada elemento recibe el crédito total de la sesión.
