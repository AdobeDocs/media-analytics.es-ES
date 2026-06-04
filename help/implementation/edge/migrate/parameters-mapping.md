---
title: Asignación de parámetros de Media Analytics para Adobe Experience Platform y Customer Journey Analytics
description: Asignación de ruta de campo XDM para parámetros de Media Analytics utilizados con el conector de Source de Analytics y Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 1331
ht-degree: 19%

---

# Asignación de parámetros de Media Analytics para Adobe Experience Platform y Customer Journey Analytics

Este documento proporciona una lista completa de todos los parámetros de Media Analytics utilizados en Adobe Experience Platform y Customer Journey Analytics. Está diseñado para admitir la integración de datos importados de Adobe Analytics a Platform mediante el [conector Source de Analytics](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/analytics) o el [conector Source de Analytics para clasificaciones](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/classifications), y asignar cada parámetro a su ruta de campo XDM correspondiente.

>[!NOTE]
>
>Esta referencia se aplica a las organizaciones que usan el [conector de origen de Analytics](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/analytics) para traer datos de medios de streaming de Adobe Analytics a Adobe Experience Platform para usarlos con los informes de Customer Journey Analytics u otros servicios de Platform. Estos cambios no afectan a Adobe Analytics como aplicación independiente, incluida la recopilación de datos, el procesamiento y la creación de informes.

## Variables reservadas de Media Analytics

A partir de octubre de 2025, la ruta de campo XDM `media.mediaTimed` utilizada por el conector de origen de Analytics está totalmente obsoleta y se ha reemplazado por `mediaReporting`. Los datos introducidos después de octubre de 2025 solo incluyen `mediaReporting` campos. Los datos anteriores permanecen disponibles en la ruta de campo heredada, tal y como se refleja en las tablas siguientes en **Campo XDM heredado**.

### Comportamiento de llamada de mantenimiento de conexión

Con el conector de origen de Analytics para los medios de streaming, las llamadas de conexión persistente de Adobe Analytics ahora se incorporan a Adobe Experience Platform. Esto puede afectar a los informes de Customer Journey Analytics:

* **Recuentos de sesiones**: Las llamadas de mantenimiento de conexión ayudan a mantener sesiones de usuarios activas incluso sin interacciones de medios directas. Estas llamadas se generan cada 20 minutos después del último evento por reproducción de contenido. Para garantizar un seguimiento óptimo de la sesión, configure la caducidad de la visita a 30 minutos en la vista de datos.

* **Recuentos de eventos**: Las llamadas de mantenimiento activas ahora se cuentan para la métrica Eventos de Customer Journey Analytics. Para excluirlos, cree un filtro que excluya los eventos del tipo de evento `media.keepalive`.

## Parámetros de Streaming Media

| Nombre de campo | Campo XDM heredado | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Tipo de emisión]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | Dimensión | [[!UICONTROL Tipo de emisión]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL ID de contenido]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | Dimensión | [[!UICONTROL ID de contenido]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL Longitud del contenido]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | Dimensión | [[!UICONTROL Longitud del contenido]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL Tipo de contenido]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | Dimensión | [[!UICONTROL Tipo de contenido]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL ID de sesión de medios]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | Dimensión | [[!UICONTROL ID de sesión de medios]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL Nombre del reproductor de contenido]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | Dimensión | [[!UICONTROL Nombre del reproductor de contenido]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL Canal de contenido]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | Dimensión | [[!UICONTROL Canal de contenido]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL Segmento de contenido]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | Dimensión | [[!UICONTROL Segmento de contenido]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL Nombre de contenido]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | Dimensión | [[!UICONTROL Nombre de contenido]](/help/reporting/dimensions/content-name.md) | |
| Ruta de vídeo | *No se usa en AEP/CJA* | | | | Propiedad específica de Adobe Analytics |
| [[!UICONTROL Mostrar]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | Dimensión | [[!UICONTROL Mostrar]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL Temporada]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | Dimensión | [[!UICONTROL Temporada]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL Episodio]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | Dimensión | [[!UICONTROL Episodio]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL Género]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | Dimensión | no admitido | Usar campo `mediaReporting` |
| [[!UICONTROL Red]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | Dimensión | [[!UICONTROL Red]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL Tipo de programa]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | Dimensión | [[!UICONTROL Tipo de programa]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | Dimensión | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL Autorizado]](/help/reporting/metrics/authorized.md) | No admitido | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | Dimensión | [[!UICONTROL Autorizado]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL Parte del día]](/help/reporting/dimensions/day-part.md) | No admitido | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | Dimensión | [[!UICONTROL Parte del día]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL Tipo de fuente de medios]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | Dimensión | [[!UICONTROL Tipo de fuente de medios]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL Artista]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | Dimensión | [[!UICONTROL Artista]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL Álbum]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | Dimensión | [[!UICONTROL Álbum]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL Etiqueta]](/help/reporting/dimensions/label.md) | No admitido | `xdm.mediaReporting.`<br>`sessionDetails.label` | Dimensión | [[!UICONTROL Etiqueta]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL Autor]](/help/reporting/dimensions/author.md) | No admitido | `xdm.mediaReporting.`<br>`sessionDetails.author` | Dimensión | [[!UICONTROL Autor]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL Estación]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | Dimensión | [[!UICONTROL Estación]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL Editor]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | Dimensión | [[!UICONTROL Editor]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL Comienzos de medios]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | Métrica | [[!UICONTROL Comienzos de medios]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL El contenido comienza]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | Métrica | [[!UICONTROL El contenido comienza]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL Contenido completado]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | Métrica | [[!UICONTROL Contenido completado]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | Métrica | [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | Métrica | [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL Tiempo único reproducido]](/help/reporting/metrics/unique-time-played.md) | No admitido | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | Métrica | [[!UICONTROL Tiempo único reproducido]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL Marcador de progreso del 10 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | Métrica | [[!UICONTROL Marcador de progreso del 10 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progreso del 25 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | Métrica | [[!UICONTROL Marcador de progreso del 25 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progreso del 50 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | Métrica | [[!UICONTROL Marcador de progreso del 50 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progreso al 75 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | Métrica | [[!UICONTROL Marcador de progreso al 75 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progreso al 95 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | Métrica | [[!UICONTROL Marcador de progreso al 95 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Promedio de público por minuto]](/help/reporting/metrics/average-minute-audience.md) | No admitido | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | Métrica | [[!UICONTROL Promedio de público por minuto]](/help/reporting/metrics/average-minute-audience.md) | |
| Segundos desde la última llamada | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | Métrica | Segundos desde la última llamada | |
| [[!UICONTROL Flujos afectados por la pausa]](/help/reporting/metrics/paused-impacted-streams.md) | No admitido | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | Métrica | [[!UICONTROL Flujos afectados por la pausa]](/help/reporting/metrics/paused-impacted-streams.md) | cubrimos mediaTimed calculando este valor de otros eventos |
| [[!UICONTROL Pausar eventos]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | Métrica | [[!UICONTROL Pausar eventos]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL Duración total de la pausa]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | Métrica | [[!UICONTROL Duración total de la pausa]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL Reanudación de contenido]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | Métrica | [[!UICONTROL Reanudación de contenido]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL Vistas de segmentos de contenido]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | Métrica | [[!UICONTROL Vistas de segmentos de contenido]](/help/reporting/metrics/content-segment-views.md) | |

## Actualización de parámetros de estado del reproductor

| Nombre de campo | Campo XDM heredado | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| Transmisiones afectadas por estados de reproductor | No admitido | `xdm.mediaReporting.`<br>`states.isSet` | Métrica | no admitido | usar campo `mediaReporting` |
| Recuentos de estados de reproductor | No admitido | `xdm.mediaReporting.`<br>`states.count` | Métrica | no admitido | usar campo `mediaReporting` |
| Duración total de los estados del reproductor | No admitido | `xdm.mediaReporting.`<br>`states.time` | Métrica | no admitido | usar campo `mediaReporting` |
| Nombre del estado del reproductor | No admitido | `xdm.mediaReporting.`<br>`states.name` | Dimensión | no admitido | usar campo `mediaReporting` |

## Parámetros de capítulo

| Nombre de campo | Campo XDM heredado | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Capítulo]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | Dimensión | [[!UICONTROL Capítulo]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL Inicio del capítulo]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | Métrica | [[!UICONTROL Inicio del capítulo]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL Capítulo completado]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | Métrica | [[!UICONTROL Capítulo completado]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL Tiempo invertido en el capítulo]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | Métrica | [[!UICONTROL Tiempo invertido en el capítulo]](/help/reporting/metrics/chapter-time-spent.md) | |

## Parámetros de anuncio

| Nombre de campo | Campo XDM heredado | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL ID de anuncio]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | Dimensión | [[!UICONTROL ID de anuncio]](/help/reporting/dimensions/ad.md) | |
| [[!UICONTROL Posición del anuncio en la secuencia]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | Dimensión | [[!UICONTROL Posición del anuncio en la secuencia]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL Duración del anuncio]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | Métrica | [[!UICONTROL Duración del anuncio]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL Nombre del reproductor del anuncio]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | Dimensión | [[!UICONTROL Nombre del reproductor del anuncio]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL ID de desglose de anuncios]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | Dimensión | [[!UICONTROL ID de desglose de anuncios]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL Nombre del anuncio]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | Dimensión | [[!UICONTROL Nombre del anuncio]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL Anunciante]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | Dimensión | [[!UICONTROL Anunciante]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL ID de campaña]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | Dimensión | [[!UICONTROL ID de campaña]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL Inicio de publicidad]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | Métrica | [[!UICONTROL Inicio de publicidad]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL Finalización de publicidad]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | Métrica | [[!UICONTROL Finalización de publicidad]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL Tiempo invertido en publicidad]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | Métrica | [[!UICONTROL Tiempo invertido en publicidad]](/help/reporting/metrics/ad-time-spent.md) | |

## Parámetros de calidad

| Nombre de campo | Campo XDM heredado | Ruta del campo XDM de creación de informes | Tipo de datos | Campos derivados | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Velocidad de bits media]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | Ambos | [[!UICONTROL Velocidad de bits media]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL Tiempo Para El Inicio]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | Ambos | [[!UICONTROL Tiempo Para El Inicio]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL Fotogramas perdidos]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | Ambos | [[!UICONTROL Fotogramas perdidos]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL Eventos de búfer]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | Ambos | [[!UICONTROL Eventos de búfer]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL Duración total del búfer]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | Ambos | [[!UICONTROL Duración total del búfer]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL Cambios de velocidad de bits]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | Ambos | [[!UICONTROL Cambios de velocidad de bits]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL Errores / Eventos de error]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | Ambos | [[!UICONTROL Errores / Eventos de error]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL ID de error del reproductor SDK]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | Dimensión | no admitido | usar campo `mediaReporting` |
| [[!UICONTROL Id. de error externo]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | Dimensión | no admitido | usar campo `mediaReporting` |
| [[!UICONTROL Pérdidas antes del inicio]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | Métrica | [[!UICONTROL Pérdidas antes del inicio]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL Transmisiones afectadas por búfer]](/help/reporting/metrics/buffer-impacted-streams.md) | No admitido | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | Métrica | [[!UICONTROL Transmisiones afectadas por búfer]](/help/reporting/metrics/buffer-impacted-streams.md) | calculado a partir de otros eventos |
| [[!UICONTROL Flujos afectados por el cambio de velocidad de bits]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | No admitido | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | Métrica | [[!UICONTROL Flujos afectados por el cambio de velocidad de bits]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | calculado a partir de otros eventos |
| [[!UICONTROL Transmisiones afectadas por el error]](/help/reporting/metrics/error-impacted-streams.md) | No admitido | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | Métrica | [[!UICONTROL Transmisiones afectadas por el error]](/help/reporting/metrics/error-impacted-streams.md) | calculado a partir de otros eventos |
| [[!UICONTROL Flujos afectados por la pérdida de fotogramas]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | No admitido | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | Métrica | [[!UICONTROL Flujos afectados por la pérdida de fotogramas]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | calculado a partir de otros eventos |

## Clasificaciones de Media Analytics

Las clasificaciones de Media Analytics se incorporan en AEP a través de un flujo independiente denominado ACDC. Cada grupo de clasificación enumerado en la tabla siguiente corresponde a un conjunto de datos único dentro de AEP. En CJA, es necesario establecer una conexión entre el conjunto de datos de evento de Media Analytics y cada uno de los conjuntos de datos de clasificación.

### Conexión de conjuntos de datos en Customer Journey Analytics

Para configurar la conexión en Customer Journey Analytics:

* Vaya a la pestaña **Conexiones** y seleccione **Crear nueva conexión**.
* En la interfaz Conexiones, elija **Agregar conjuntos de datos** y busque el conjunto de datos de evento de Media Analytics (utilizado para importar datos de medios a través de ADC), junto con los cuatro conjuntos de datos de clasificación relevantes.

### Detalles de configuración

Para cada conjunto de datos de búsqueda (conjunto de datos de clasificación), configure como se indica a continuación:

* **conjunto de datos de vídeo**:
   * Clave: `_sandbox.key`
   * Clave de coincidencia: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * Tipo de origen de datos: `Web Data`

* **conjunto de datos videoad**:
   * Clave: `_sandbox.key`
   * Clave de coincidencia: `Ad ID (advertising.adAssetReference._id)`
   * Tipo de origen de datos: `Web Data`

* **conjunto de datos de videoadpod**:
   * Clave: `_sandbox.key`
   * Clave de coincidencia: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * Tipo de origen de datos: `Web Data`

* **conjunto de datos de videochapter**:
   * Clave: `_sandbox.key`
   * Clave de coincidencia: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * Tipo de origen de datos: `Web Data`

### Consideraciones del informe

Cuando trabaje con los conjuntos de datos de clasificación durante la creación de informes, asegúrese de hacer referencia a las rutas de campo específicas de la clasificación (`ACDC XDM Path`) en lugar de a los campos XDM estándar de Media Analytics.

## Tabla de clasificaciones

| Nombre de clasificación (grupo) | Nombre de campo | Ruta de ACDC XDM |
| --- | --- | --- |
| vídeo | ID de clave/recurso | `xdm.<_sandbox>.key` |
| vídeo | Duración del vídeo | `xdm.<_sandbox>.video_length` |
| vídeo | Nombre del vídeo | `xdm.<_sandbox>.video_name` |
| vídeo | [[!UICONTROL ID de recurso]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| vídeo | [[!UICONTROL Fecha de la primera publicación]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| vídeo | [[!UICONTROL Fecha del primer uso digital]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| vídeo | [[!UICONTROL Clasificación del contenido]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| vídeo | [[!UICONTROL Creador]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | Clave/ID de anuncio | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL Duración del anuncio]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL Nombre del anuncio]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL ID. DE Creative]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | ID de clave/pod de anuncios | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL Posición de la secuencia]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL Nombre de secuencia]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | Clave/Capítulo | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL Longitud del capítulo]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL Desplazamiento de capítulo]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL Posición del capítulo]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL Nombre de capítulo]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Variables personalizadas de Media Analytics

En Adobe Analytics, las variables personalizadas se asignan a diferentes eventos o eVars según las reglas de implementación definidas dentro de cada grupo de informes. Como resultado, cuando estas variables personalizadas se importan en Adobe Experience Platform (AEP), se asignan a diferentes rutas XDM.

* Los eventos se almacenan en la ruta:

  `_experience.analytics.event<x>to<y>.event<number>.value`

* Las eVars se almacenan en la ruta:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

En ambos casos, `<number>` corresponde al evento específico o al número de eVar utilizado en la configuración original del grupo de informes de Adobe Analytics.

### Variables personalizadas

| Nombre de campo | Ruta de XDM | Tipo de datos |
| --- | --- | --- |
| [[!UICONTROL Indicador de medios descargados]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| Versión de SDK | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| Versión de biblioteca de medios | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| [[!UICONTROL Formato de emisión]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| [[!UICONTROL Fecha de la primera publicación]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| [[!UICONTROL Fecha del primer uso digital]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| [[!UICONTROL Datos federados]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>y<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Ambos |
| [[!UICONTROL Transmisiones estimadas]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Recuento de anuncios]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Recuento de capítulos]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL ID. DE Creative]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| [[!UICONTROL ID del sitio]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| [[!UICONTROL URL DE Creative]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| [[!UICONTROL ID. de ubicación]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensión |
| Fotogramas por segundo | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>y<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Ambos |
| ID de error de Media SDK | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Flujos afectados por estancamiento]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Eventos de demora]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Duración total de demora]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
