---
title: Migración de audiencias al nuevo tipo de datos de Adobe Analytics para medios de streaming
description: Obtenga información sobre cómo migrar audiencias al nuevo tipo de datos de Adobe Analytics para medios de streaming
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
source-git-commit: 61e5279e6d53b18955424e76d05d440b83dae07e
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 44%

---

# Asignación de parámetros de Media Analytics para Adobe Experience Platform y Customer Journey Analytics

Este documento proporciona una lista completa de todos los parámetros de Media Analytics utilizados en Adobe Experience Platform y Customer Journey Analytics. Está diseñado para admitir la integración de datos importados de Adobe Analytics a Platform mediante el [conector Source de Analytics](https://experienceleague.adobe.com/es/docs/experience-platform/sources/connectors/adobe-applications/analytics) o el [conector Source de Analytics para clasificaciones](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/classifications), y asignar cada parámetro a su ruta de campo XDM correspondiente.

## Variables reservadas de Media Analytics

Para todas las variables reservadas de Media Analytics, los datos ingeridos desde Adobe Analytics en AEP hasta mayo de 2025 (incluido) se pueden encontrar en la &quot;Ruta del campo XDM actual&quot; que se indica en las tablas siguientes.

Como los equipos de Media Analytics y ADC están trabajando actualmente para realizar la migración completa a la &quot;Ruta del campo XDM de creación de informes&quot;, se compartirá una comunicación oficial una vez que se complete esta migración y la &quot;Ruta del campo XDM de creación de informes&quot; esté disponible para su uso.

## Parámetros de Streaming Media

| Nombre de campo | Ruta del campo XDM actual (obsoleto) | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| Tipo de emisión | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | Dimensión | Tipo de emisión |                                                                       |
| ID de contenido | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | Dimensión | ID de contenido |                                                                       |
| Longitud del contenido | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | Dimensión | Longitud del contenido |                                                                       |
| Tipo de contenido | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | Dimensión | Tipo de contenido |                                                                       |
| ID de sesión de contenidos | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | Dimensión | ID de sesión de contenidos |                                                                       |
| Nombre del reproductor de contenido | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | Dimensión | Nombre del reproductor de contenido |                                                                       |
| Canal de contenido | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | Dimensión | Canal de contenido |                                                                       |
| Segmento de contenido | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | Dimensión | Segmento de contenido |                                                                       |
| Nombre del contenido | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | Dimensión | Nombre del contenido |                                                                       |
| Ruta de vídeo | *No se usa en AEP/CJA* |                                                   |           |                   | Propiedad específica de Adobe Analytics |
| Show | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | Dimensión | Show |                                                                       |
| Temporada | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | Dimensión | Temporada |                                                                       |
| Episodio | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | Dimensión | Episodio |                                                                       |
| Género | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | Dimensión | no admitido | Usar campo de mediaReporting |
| Red | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | Dimensión | Red |                                                                       |
| Tipo de programa | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | Dimensión | Tipo de programa |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | Dimensión | MVPD |                                                                       |
| Con autorización | No admitido | mediaReporting.sessionDetails.authorized | Dimensión | Con autorización |                                                                       |
| Parte del día | No admitido | mediaReporting.sessionDetails.dayPart | Dimensión | Parte del día |                                                                       |
| Tipo de fuente de contenidos | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | Dimensión | Tipo de fuente de contenidos |                                                                       |
| Artista | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | Dimensión | Artista |                                                                       |
| Álbum | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | Dimensión | Álbum |                                                                       |
| Etiqueta | No admitido | mediaReporting.sessionDetails.label | Dimensión | Etiqueta |                                                                       |
| Autor | No admitido | mediaReporting.sessionDetails.author | Dimensión | Autor |                                                                       |
| Emisora | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | Dimensión | Emisora |                                                                       |
| Editor | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | Dimensión | Editor |                                                                       |
| Inicios de contenidos | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | Métrica | Inicios de contenidos |                                                                       |
| Inicio de contenido | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | Métrica | Inicio de contenido |                                                                       |
| Contenido finalizado | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | Métrica | Contenido finalizado |                                                                       |
| Tiempo invertido en contenido | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | Métrica | Tiempo invertido en contenido |                                                                       |
| Tiempo invertido en contenido | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | Métrica | Tiempo invertido en contenido |                                                                       |
| Tiempo de reproducción única | No admitido | mediaReporting.sessionDetails.uniqueTimePlayed | Métrica | Tiempo de reproducción única |                                                                       |
| Marcador de progreso del 10% | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | Métrica | Marcador de progreso del 10% |                                                                       |
| Marcador de progreso del 25% | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | Métrica | Marcador de progreso del 25% |                                                                       |
| Marcador de progreso del 50 % | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | Métrica | Marcador de progreso del 50 % |                                                                       |
| Marcador de progreso del 75% | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | Métrica | Marcador de progreso del 75% |                                                                       |
| Marcador de progreso del 95% | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | Métrica | Marcador de progreso del 95% |                                                                       |
| Promedio de público por minuto | No admitido | mediaReporting.sessionDetails.averageMinuteAudience | Métrica | Promedio de público por minuto |                                                                  |
| Segundos desde la última llamada | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | Métrica | Segundos desde la última llamada |                                                              |
| Flujos afectados por la pausa | No admitido | mediaReporting.sessionDetails.hasPauseImpactedStreams | Métrica | Flujos afectados por la pausa | cubrimos mediaTimed calculando este valor de otros eventos |
| Pausar eventos | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | Métrica | Pausar eventos |                                                                       |
| Duración de la pausa | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | Métrica | Duración de la pausa |                                                                       |
| Reanudación de contenido | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | Métrica | Reanudación de contenido |                                                                       |
| Vistas de segmentos de contenido | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | Métrica | Vistas de segmentos de contenido |                                                                     |

{style="table-layout:auto"}

## Actualización de parámetros de estado del reproductor

| Nombre de campo | Ruta del campo XDM actual (obsoleto) | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| Transmisiones afectadas por estados de reproductor | No admitido | mediaReporting.states.isSet | Métrica | no admitido | usar campo mediaReporting |
| Recuentos de estados de reproductor | No admitido | mediaReporting.states.count | Métrica | no admitido | usar campo mediaReporting |
| Duración total de los estados del reproductor | No admitido | mediaReporting.states.time | Métrica | no admitido | usar campo mediaReporting |
| Nombre del estado del reproductor | No admitido | mediaReporting.states.name | Dimensión | no admitido | usar campo mediaReporting |

{style="table-layout:auto"}

## Parámetros de capítulo 

| Nombre de campo | Ruta del campo XDM actual (obsoleto) | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| Capítulo | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | Dimensión | Capítulo |           |
| Inicio del capítulo. | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | Métrica | Inicio del capítulo. |           |
| Capítulo completado | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | Métrica | Capítulo completado |          |
| Tiempo invertido en el capítulo | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | Métrica | Tiempo invertido en el capítulo |        |

{style="table-layout:auto"}

## Parámetros de anuncio 

| Nombre de campo | Ruta del campo XDM actual (obsoleto) | Ruta del campo XDM de creación de informes | Tipo de datos | Campo derivado | Notas |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| ID de anuncio | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | Dimensión | ID de anuncio |           |
| Posición del anuncio en la secuencia | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | Dimensión | Posición del anuncio en la secuencia |     |
| Duración del anuncio | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | Métrica | Duración del anuncio |           |
| Nombre del reproductor del anuncio | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | Dimensión | Nombre del reproductor del anuncio |           |
| ID de desglose de anuncios | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | Dimensión | ID de desglose de anuncios |           |
| Nombre de publicidad | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | Dimensión | Nombre de publicidad |           |
| Anunciante | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | Dimensión | Anunciante |           |
| ID de campaña | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | Dimensión | ID de campaña |           |
| Inicio del anuncio | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | Métrica | Inicio del anuncio |           |
| Publicidad completa | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | Métrica | Publicidad completa |           |
| Tiempo invertido en publicidad | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | Métrica | Tiempo invertido en publicidad |           |

{style="table-layout:auto"}

## Parámetros de calidad 

| Nombre de campo | Ruta del campo XDM actual (obsoleto) | Ruta del campo XDM de creación de informes | Tipo de datos | Campos derivados | Notas |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Velocidad de bits media | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Ambos | Velocidad de bits media |           |
| Tiempo para el inicio | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Ambos | Tiempo para el inicio |           |
| Fotogramas perdidos | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Ambos | Fotogramas perdidos |           |
| Eventos de búfer | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Ambos | Eventos de búfer |           |
| Duración total del búfer | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Ambos | Duración total del búfer |     |
| Cambios en la velocidad de bits | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Ambos | Cambios en la velocidad de bits |         |
| Errores/eventos de error | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Ambos | Errores/eventos de error |  |
| ID de error de SDK de reproductor | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | Dimensión | no admitido | usar campo mediaReporting |
| ID de error externo | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | Dimensión | no admitido | usar campo mediaReporting |
| Pérdidas antes del inicio | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | Métrica | Pérdidas antes del inicio |     |
| Flujos afectados por el búfer | No admitido | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | Métrica | Flujos afectados por el búfer | calculado a partir de otros eventos |
| Flujos afectados por el cambio en la velocidad de bits | No admitido | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | Métrica | Flujos afectados por el cambio en la velocidad de bits | calculado a partir de otros eventos |
| Flujos afectados por el error | No admitido | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | Métrica | Flujos afectados por el error | calculado a partir de otros eventos |
| Flujos afectados por la pérdida de cuadros | No admitido | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | Métrica | Flujos afectados por la pérdida de cuadros | calculado a partir de otros eventos |

{style="table-layout:auto"}

## Clasificaciones de Media Analytics

Las clasificaciones de Media Analytics se incorporan en AEP a través de un flujo independiente denominado ACDC. Cada grupo de clasificación enumerado en la tabla siguiente corresponde a un conjunto de datos único dentro de AEP. En CJA, es necesario establecer una conexión entre el conjunto de datos de evento de Media Analytics y cada uno de los conjuntos de datos de clasificación.

### Conexión de conjuntos de datos en Customer Journey Analytics

Para configurar la conexión en Customer Journey Analytics:

- Vaya a la pestaña **Conexiones** y seleccione **Crear nueva conexión**.
- En la interfaz Conexiones, elija **Agregar conjuntos de datos** y busque el conjunto de datos de evento de Media Analytics (utilizado para importar datos de medios a través de ADC), junto con los cuatro conjuntos de datos de clasificación relevantes.

### Detalles de configuración

Para cada conjunto de datos de búsqueda (conjunto de datos de clasificación), configure como se indica a continuación:

- **conjunto de datos de vídeo**:
   - Clave: `_sandbox.key`
   - Clave de coincidencia: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - Tipo de origen de datos: `Web Data`

- **conjunto de datos videoad**:
   - Clave: `_sandbox.key`
   - Clave de coincidencia: `Ad ID (advertising.adAssetReference._id)`
   - Tipo de origen de datos: `Web Data`

- **conjunto de datos de videoadpod**:
   - Clave: `_sandbox.key`
   - Clave de coincidencia: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - Tipo de origen de datos: `Web Data`

- **conjunto de datos de videochapter**:
   - Clave: `_sandbox.key`
   - Clave de coincidencia: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - Tipo de origen de datos: `Web Data`

### Consideraciones del informe

Cuando trabaje con los conjuntos de datos de clasificación durante la creación de informes, asegúrese de hacer referencia a las rutas de campo específicas de la clasificación (`ACDC XDM Path`) en lugar de a los campos XDM estándar de Media Analytics.

## Tabla de clasificaciones

| Nombre de clasificación (grupo) | Nombre de campo | Ruta de ACDC XDM |
|------------|----------|-------------|
| vídeo | ID de clave/recurso | `<_sandbox>.key` |
| vídeo | Duración del vídeo | `<_sandbox>.video_length` |
| vídeo | Nombre del vídeo | `<_sandbox>.video_name` |
| vídeo | ID del recurso | `<_sandbox>.asset_id` |
| vídeo | Fecha de la primera emisión | `<_sandbox>.first_air_date` |
| vídeo | Fecha de primera emisión digital | `<_sandbox>.first_digital_date` |
| vídeo | Clasificación del contenido | `<_sandbox>.content_rating` |
| vídeo | Creador | `<_sandbox>.originator` |
| videoad | Clave/ID de anuncio | `<_sandbox>.key` |
| videoad | Duración del anuncio | `<_sandbox>.ad_length` |
| videoad | Nombre de publicidad | `<_sandbox>.ad_name` |
| videoad | ID del creativo | `<_sandbox>.creative_id` |
| videoadpod | ID de clave/pod de anuncios | `<_sandbox>.key` |
| videoadpod | Posición en la secuencia | `<_sandbox>.pod_position` |
| videoadpod | Nombre de la secuencia | `<_sandbox>.pod_name` |
| videochapter | Clave/Capítulo | `<_sandbox>.key` |
| videochapter | Duración del capítulo | `<_sandbox>.chapter_length` |
| videochapter | Desplazamiento de capítulo | `<_sandbox>.chapter_offset` |
| videochapter | Posición del capítulo | `<_sandbox>.chapter_position` |
| videochapter | Nombre del capítulo | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Variables personalizadas de Media Analytics

En Adobe Analytics, las variables personalizadas se asignan a diferentes eventos o eVars según las reglas de implementación definidas dentro de cada grupo de informes. Como resultado, cuando estas variables personalizadas se importan en Adobe Experience Platform (AEP), se asignan a diferentes rutas XDM.

- Los eventos se almacenan en la ruta:

  `_experience.analytics.event<x>to<y>.event<number>.value`

- Las eVars se almacenan en la ruta:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

En ambos casos, `<number>` corresponde al evento específico o al número de eVar utilizado en la configuración original del grupo de informes de Adobe Analytics.

### Variables personalizadas

| Nombre de campo | Ruta de XDM | Tipo de datos |
|-------------|-------------|-----------|
| Indicador de descarga de contenidos | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Versión de SDK | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| Versión de VHL | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| Formato de la emisión | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| Fecha de la primera emisión | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| Fecha de primera emisión digital | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| Datos federados | `_experience.analytics.customDimensions.eVars.eVar<number>` y `_experience.analytics.event<x>to<y>.event<number>.value` | Ambos |
| Emisiones previstas | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Recuento de anuncios | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Recuento de capítulos | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| ID del creativo | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| ID del sitio | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| URL del anuncio | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| ID de colocación | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensión |
| Fotogramas por segundo | `_experience.analytics.customDimensions.eVars.eVar<number>` y `_experience.analytics.event<x>to<y>.event<number>.value` | Ambos |
| ID de error de Media SDK | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Flujos afectados por demoras | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Eventos de demora | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Duración total de demora | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |

{style="table-layout:auto"}
