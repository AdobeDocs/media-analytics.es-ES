---
title: Tipo de contenido
description: Informa del formato de la emisión (VOD, Live, Lineal, podcast, canción, etc.).
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 9%

---


# Tipo de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Tipo de contenido**. Consulte [Tipo de contenido](/help/implementation/variables/core/content-type.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Tipo de contenido** indica el formato de la emisión (por ejemplo, VOD, Live o Lineal para vídeo y canción, podcast o audiolibro para audio).

## Cómo se rellena esta dimensión

El reproductor establece el tipo de contenido al inicio de la sesión y lo lleva a cabo en cada evento. No se deriva; el valor del informe coincide con el que se envió durante la recopilación.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.contentType` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

>[!IMPORTANT]
>
>Si el tipo de contenido no está establecido o está vacío, la dimensión informa de `missing_content_type` para la sesión. Utilice este valor para buscar implementaciones que deban corregirse.

## Elementos de dimensión

Los valores definidos por Adobe rellenan los segmentos e informes integrados. Se aceptan cadenas personalizadas, pero no coincidirán con los segmentos integrados.

| Tipo de emisión | Valores recomendados |
| --- | --- |
| Vídeo | `vod`, `live`, `linear`, `ugc`, `dvod` |
| Audio | `song`, `podcast`, `audiobook`, `radio` |

## Segmentos recomendados

| Segmento | Regla |
| --- | --- |
| [!UICONTROL Contenido de VOD] | Tipo de contenido = `vod` |
| [!UICONTROL Contenido en directo] | Tipo de contenido = `live` |
| [!UICONTROL Contenido lineal] | Tipo de contenido = `linear` |
