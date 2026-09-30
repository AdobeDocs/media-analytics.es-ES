---
title: Canal de contenido
description: Informa de la estación de distribución, red o propiedad donde se reprodujo cada sesión.
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
source-wordcount: '163'
ht-degree: 8%
---

# Canal de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Canal de contenido**. Consulte [Canal de contenido](/help/implementation/variables/core/content-channel.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Canal de contenido** indica la estación de distribución, red o propiedad donde se reprodujo cada sesión. Utilícela para dividir la reproducción por red o sección de una propiedad.

## Cómo se rellena esta dimensión

El reproductor establece el canal al inicio de la sesión y persiste durante la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.channel` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Si no se establece el canal, la dimensión no se rellena para esa sesión.

## Elementos de dimensión

Cada elemento es la cadena literal establecida al inicio de la sesión. Se acepta cualquier cadena. Los valores habituales son un nombre de red, una parte de una ruta de sitio o un identificador de propiedad interno.
