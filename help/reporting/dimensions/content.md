---
title: Contenido
description: Informa de cada fragmento único de contenido reproducido, marcado por el ID de contenido.
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
source-wordcount: '251'
ht-degree: 7%
---

# Contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Contenido**. Consulte [ID. de contenido](/help/implementation/variables/core/content-id.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Contenido** indica cada fragmento único de contenido reproducido, marcado por el ID de contenido establecido al inicio de la sesión. Es el desglose principal para los informes de medios de streaming y la clave de unión para las dimensiones de clasificación como Nombre del vídeo, Duración del vídeo, ID del recurso, Fecha de primera publicación y Clasificación del contenido.

## Cómo se rellena esta dimensión

El reproductor establece el contenido al inicio de la sesión como un identificador estable para el recurso. Se informa del mismo ID de contenido en cada evento subsiguiente de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.name` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. Persiste durante la visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>Se requiere el ID de contenido. Si no está configurada o está vacía, la sesión se eliminará de los informes de medios de transmisión y no aparecerá en ningún informe de medios ni en el segmento [!UICONTROL Todos los medios de transmisión].

## Elementos de dimensión

Cada elemento es un ID de contenido único que se registra al inicio de la sesión. Utilice un identificador estable (por ejemplo, un CMS ID interno, un ID del sector como EIDR, TMS/Gracenote o un slug persistente) para que las sesiones del mismo recurso se acumulen en un solo elemento de línea a lo largo del tiempo.

## Segmentos recomendados

| Segmento | Regla |
| --- | --- |
| [!UICONTROL Todos los medios de transmisión] | El contenido (ID) existe |
