---
title: Tipo de emisión
description: Registra si cada sesión multimedia fue contenido de audio o vídeo.
feature: Dimensions
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 6%

---


# Tipo de emisión

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Tipo de emisión**. Consulte [Tipo de emisión](/help/implementation/variables/core/stream-type.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Tipo de emisión** registra si cada sesión multimedia era contenido de audio o vídeo. Está disponible en Adobe Analytics una vez que [Media Core está habilitado](/help/implementation/media-sdk/setup/media-reports-enable.md) para el grupo de informes y en Customer Journey Analytics para cualquier conjunto de datos que incluya datos de medios de streaming.

## Cómo se rellena esta dimensión

El reproductor establece el tipo de emisión al principio de la sesión y la transfiere a la llamada de cierre de la sesión. No se calcula ni se deriva. El valor notificado coincide exactamente con lo que se envió durante la recopilación.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.streamType` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videostreamtype` |
| Audience Manager | `c_contextdata.a.media.streamType` |

>[!IMPORTANT]
>
>Si no se establece el tipo de flujo, la dimensión no se rellena para esa sesión. Estas sesiones se excluyen de los segmentos integrados de solo audio y vídeo, y el segmento Todos los medios de streaming se contará por debajo si se utiliza junto con los desgloses de tipo de flujo.

## Elementos de dimensión

| Valor | Descripción |
| --- | --- |
| `video` | La sesión era contenido de vídeo. |
| `audio` | La sesión era contenido de audio, como podcast, audiolibro o flujo de música. |

Las API de colección aceptan técnicamente los valores personalizados, pero no se recomiendan. No coincidirán con los segmentos integrados que se describen a continuación y pueden generar informes incoherentes entre implementaciones.

## Segmentos recomendados

El tipo de flujo es la base de los segmentos integrados de [!UICONTROL Tipo de flujo de medios] de Adobe Analytics. Utilice estos segmentos para definir el ámbito de cualquier informe de medios de streaming para un tipo de contenido específico:

| Segmento | Regla |
| --- | --- |
| [!UICONTROL Todos los medios de transmisión] | El contenido (ID) existe |
| [!UICONTROL Solo audio] | El contenido (ID) existe Y el tipo de emisión es = `audio` |
| [!UICONTROL Solo vídeo] | El contenido (ID) existe Y el tipo de emisión != `audio` |

>[!TIP]
>
>El segmento [!UICONTROL Solo vídeo] usa una regla `!=` en lugar de `= video` para capturar correctamente sesiones en las que el tipo de flujo puede haberse establecido en un valor personalizado que no es `audio`.
