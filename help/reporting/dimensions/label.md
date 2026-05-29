---
title: Etiqueta
description: Informa de la discográfica que publicó el contenido de audio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 10%

---


# Etiqueta

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Etiqueta**. Consulte [Etiqueta](/help/implementation/variables/standard-metadata/label.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Label** indica la etiqueta de registro que publicó el contenido de audio (por ejemplo, `"Capitol Records"`). Utilícelo para comparar la participación entre etiquetas en un catálogo de música o podcast.

## Cómo se rellena esta dimensión

El reproductor establece la etiqueta al inicio de la sesión para el contenido de audio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.label` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## Elementos de dimensión

Cada elemento es el nombre literal de la etiqueta que aparece al inicio de la sesión. Utilice un nombre canónico estable por etiqueta para que la participación no se fragmente entre las variantes ortográficas o de impresión.
