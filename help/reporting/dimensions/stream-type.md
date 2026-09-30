---
title: Tipo de emisión
description: Registra si cada sesión multimedia fue contenido de audio o vídeo.
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
source-wordcount: '322'
ht-degree: 6%
---

# Tipo de emisión

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Tipo de emisión**. Consulte [Tipo de emisión](/help/implementation/variables/core/stream-type.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Tipo de emisión** registra si cada sesión multimedia era contenido de audio o vídeo. Está disponible en Adobe Analytics una vez que [Media Core está habilitado](/help/reporting/setup/analytics-reporting.md) para el grupo de informes y en Customer Journey Analytics para cualquier conjunto de datos que incluya datos de medios de streaming.

## Cómo se rellena esta dimensión

El reproductor establece el tipo de emisión al principio de la sesión y la transfiere a la llamada de cierre de la sesión. No se calcula ni se deriva. El valor notificado coincide exactamente con lo que se envió durante la recopilación.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.streamType` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
