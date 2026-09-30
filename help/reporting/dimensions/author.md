---
title: Autor
description: Informa sobre el autor del contenido. Se utiliza principalmente para audiolibros.
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
source-wordcount: '119'
ht-degree: 11%
---

# Autor

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Autor**. Consulte [Autor](/help/implementation/variables/standard-metadata/author.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Autor** informa sobre el autor del contenido (por ejemplo, `"Eleanor Clementine"`). Se utiliza principalmente para audiolibros, pero también es válido para podcasts cuyo host o productor es la atribución relevante.

## Cómo se rellena esta dimensión

El reproductor establece el autor al inicio de la sesión para el contenido de audio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.author` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Elementos de dimensión

Cada elemento es el nombre literal del autor registrado al inicio de la sesión.
