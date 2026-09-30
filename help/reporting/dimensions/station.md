---
title: Emisora
description: Informa del nombre o ID de la emisora de radio para el contenido de difusión de audio.
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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.station` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Elementos de dimensión

Cada elemento es el nombre o ID literal de la estación registrado al inicio de la sesión. Utilice un único identificador canónico por estación para que la participación no se fragmente entre las variantes de signo de llamada.
