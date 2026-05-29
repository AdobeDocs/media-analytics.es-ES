---
title: Emisora
description: Informa del nombre o ID de la emisora de radio para el contenido de difusión de audio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# Emisora

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Estación**. Consulte [Estación](/help/implementation/variables/standard-metadata/station.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Estación** indica el nombre o ID de la emisora de radio que difunde el contenido de audio (por ejemplo, `"NPR"` o `"WXYZ-FM"`). Utilícelo para comparar la participación entre emisoras de una red sindicada.

## Cómo se rellena esta dimensión

El reproductor establece la emisora al inicio de la sesión para el contenido de audio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.station` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Elementos de dimensión

Cada elemento es el nombre o ID literal de la estación registrado al inicio de la sesión. Utilice un único identificador canónico por estación para que la participación no se fragmente entre las variantes de signo de llamada.
