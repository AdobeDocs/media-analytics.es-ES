---
title: Explicación de las claves de metadatos de Roku
description: Obtenga información sobre las claves de metadatos Roku disponibles y vea toda la lista de constantes de metadatos estándar.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 95%

---

# Claves de metadatos de Roku{#roku-metadata-keys}

Los metadatos de publicidad, audio y vídeo estándar se pueden establecer en objetos de información de publicidad y contenido multimedia, respectivamente. El uso de las claves constantes para los metadatos de vídeo/publicidad establece el diccionario con metadatos estándar en el objeto info antes de invocar las API de seguimiento. Consulte las siguientes tablas para ver la lista completa de constantes de metadatos estándar, con ejemplos.

## Constantes de metadatos de vídeo {#video-metadata-constants}

| Nombre de metadatos | Clave de datos de contexto | Nombre de la constante |
| --- | --- | --- |
| Show | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Temporada | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episodio | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Activo | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Género | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Fecha de la primera emisión | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Fecha de la primera emisión digital | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Clasificación | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Creador | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Red | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Tipo de programa | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Carga de publicidad | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Con autorización | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Parte del día | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Fuente | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Formato de la emisión | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Constantes de metadatos de audio {#audio-metadata-constants}

| Nombre de metadatos | Clave de datos de contexto | Nombre de la constante |
| --- | --- | --- |
| Artista | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Álbum | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Etiqueta | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Autor | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Emisora | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Editor | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Constantes de metadatos de publicidad {#ad-metadata-constants}

| Nombre de metadatos | Clave de datos de contexto | Nombre de la constante |
| --- | --- | --- |
| Anunciante | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| ID de campaña | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| ID del creativo | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| ID de colocación | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| ID del sitio | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| URL del anuncio | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Constantes {#constants}

Puede utilizar las siguientes constantes para hacer un seguimiento de eventos de contenido multimedia:

### Otras constantes

| Constante | Descripción   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Constante si el origen del error es el reproductor. |

### Constantes MediaObjectkey (utilizadas como claves en instancias de MediaObject)

| Constante | Descripción   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Constante para definir metadatos en `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Constante para establecer los metadatos de la publicidad en `EventData``trackEvent` |
| `MEDIA_RESUMED` | Constante para enviar un latido de reanudación de vídeo. Para reanudar el seguimiento de vídeos de contenido pausado, es necesario establecer la propiedad `MEDIA_RESUMED` en el objeto `mediaInfo` cuando se invoca `mediaTrackLoad`. (`MEDIA_RESUMED` no es un evento que se pueda rastrear con la API `mediaTrackEvent`). `MEDIA_RESUMED` se debe establecer como true cuando una aplicación desee seguir controlando contenido que un usuario haya pausado pero que ahora desea reanudar la visualización. <br/><br/>Por ejemplo, supongamos que un usuario ve el 30% del contenido y luego cierra la aplicación. Esto hará que finalice la sesión. Posteriormente, si el mismo usuario vuelve al contenido y la aplicación permite que lo reanude desde el mismo punto en el que lo dejó, la aplicación debería establecer `MEDIA_RESUMED` como “true” mientras invoca la API de `mediaTrackLoad`. El resultado es que estas dos sesiones de contenidos diferentes para el mismo contenido de vídeo se pueden vincular. A continuación se muestra un ejemplo de implementación: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>Esto creará una nueva sesión para el vídeo, pero también hace que el SDK envíe una solicitud de latido con el tipo de evento “continuar”, que se puede utilizar en los informes para vincular dos sesiones de contenidos diferentes. |

### Constantes de tipo de contenido

| Constante | Descripción   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Constante para tipo de emisión EN DIRECTO. |
| `MEDIA_STREAM_TYPE_VOD` | Constante para tipo de emisión de VOD. |

### Constantes de tipo de evento (utilizadas para la llamada trackEvent)

| Constante | Descripción   |
|---|---|
| `MEDIA_BUFFER_START` | Tipo de evento para inicio del almacenamiento en búfer. |
| `MEDIA_BUFFER_COMPLETE` | Tipo de evento para la finalización del almacenamiento en búfer. |
| `MEDIA_SEEK_START` | Tipo de evento para iniciar la llamada a otro punto del contenido. |
| `MEDIA_SEEK_COMPLETE` | Tipo de evento para la finalización de la llamada. |
| `MEDIA_BITRATE_CHANGE` | Tipo de evento para cambiar la velocidad de bits. |
| `MEDIA_CHAPTER_START` | Tipo de evento para el inicio de un capítulo. |
| `MEDIA_CHAPTER_COMPLETE` | Tipo de evento para la finalización del capítulo. |
| `MEDIA_CHAPTER_SKIP` | Tipo de evento para el inicio de publicidad. |
| `MEDIA_AD_BREAK_START` | Tipo de evento para el inicio de publicidad. |
| `MEDIA_AD_BREAK_COMPLETE` | Tipo de evento para la finalización de AdBreak. |
| `MEDIA_AD_BREAK_SKIP` | Tipo de evento para la omisión de AdBreak. |
| `MEDIA_AD_START` | Tipo de evento para el inicio de publicidad. |
| `MEDIA_AD_COMPLETE` | Tipo de evento para la finalización de publicidad. |
| `MEDIA_AD_SKIP` | Tipo de evento para la omisión de publicidad. |
