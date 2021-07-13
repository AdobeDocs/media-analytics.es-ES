---
title: Detalles de la llamada de prueba
description: Explore las llamadas que debe realizar para validar la implementación.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 98%

---

# Detalles de la llamada de prueba{#test-call-details}

## Iniciar el reproductor de contenidos {#start-the-media-player}

### Llamada de inicio de Adobe Analytics (AppMeasurement)  {#aa-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Campos de metadatos personalizados**_ |
| _**`a.media.[value]`**_ | _**Campos de metadatos estándar**_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración de las emisiones lineales debe establecerse con la mejor estimación para el programa actual.

### Metadatos estándar en la llamada de inicio de Adobe Analytics (AppMeasurement)  {#std-metadata-aa}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Título episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de Adobe Analytics (AppMeasurement)  {#custom-metadata-aa}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `custom.metadataA` | valor |
| `custom.metadataB` | valor |

### Llamada de inicio de Media Analytics (latidos)  {#ma-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Título episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Campos de metadatos personalizados**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campos de metadatos estándar**_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La posición del cabezal de reproducción para las emisiones lineales al inicio del vídeo debe establecerse en los segundos transcurridos desde el inicio del programa actual, en lugar de 0.

### Metadatos estándar en la llamada de inicio de Media Analytics (latidos)  {#std-metadata-ma}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Título episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | desbloqueado |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de Media Analytics (latidos)  {#custom-metadata-ma}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:custom.metadata` | valor |
| `s:meta:custom.metadata` | valor |

### Llamada de inicio de Adobe Analytics (latidos) de Media Analytics {#ma-aa-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Título episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* Esta llamada indica que Media SDK ha solicitado que se envíe una llamada `pev2=ms_s` de Adobe Analytics al servidor de Adobe Analytics (AppMeasurement).
* La llamada no puede contener metadatos personalizados.

## Visualización de la reproducción de anuncio {#view-ad-playback}

### Llamada de inicio de anucio de Adobe Analytics (AppMeasurement)  {#aa-ad-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0,0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**Campos de metadatos**_ |
| _**`a.media.[value]`**_ | _**Campos de metadatos estándar**_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración del anuncio debe establecerse en -1 si no está disponible al inicio del anuncio.

### Metadatos estándar en la llamada de inicio de anuncio de Adobe Analytics (AppMeasurement)  {#std-metadata-aa-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `a.media.show` | Mostrar título |
| `a.media.season` | 6 |
| `a.media.episode` | Título episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 07-2016-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | desbloqueado |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de anuncio de Adobe Analytics (AppMeasurement)  {#custom-metadata-aa-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `custom.metadata` | valor |
| `custom.metadata` | valor |

### Llamada de inicio de anuncio de Media Analytics (latidos)  {#ma-ad-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Campos de metadatos personalizados**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campos de metadatos estándar**_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración del anuncio debe establecerse en -1 si no está disponible al inicio del anuncio.

### Metadatos estándar en la llamada de inicio de anuncio de Media Analytics (latidos)  {#std-metadata-ma-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Título episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 07-2018 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | desbloqueado |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de anuncio de Media Analytics (latidos)  {#custom-metadata-ma-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:custom.metadata` | valor |
| `s:meta:custom.metadata` | valor |

### Llamada de inicio de anuncio de Adobe Analytics (latidos) de Media Analytics {#ma-aa-ad-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Llamada de reproducción de anuncio de Media Analytics (latidos)  {#ma-ad-play-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Llamada de pausa de anuncio de Media Analytics (latidos)  {#ma-ad-pause-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Llamada de finalización de anuncio de Adobe Analytics (latidos) de Media Analytics {#ma-aa-ad-complete-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Reproducción del contenido principal {#play-main-content}

### Llamada de reproducción de Media Analytics (latidos)  {#ma-play-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Título episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* La posición del cabezal de reproducción debe aumentarse en 10 segundos con cada llamada de reproducción.
* El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

## Pausar contenido principal {#pause-main-content}

### Llamada de pausa de Media Analytics (latidos)  {#ma-pause-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Título episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
