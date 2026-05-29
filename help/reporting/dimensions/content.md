---
title: Contenido
description: Informa de cada fragmento único de contenido reproducido, marcado por el ID de contenido.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.name` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. Persiste durante la visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
