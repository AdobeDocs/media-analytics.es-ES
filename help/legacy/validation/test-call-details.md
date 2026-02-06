---
title: Detalles de la llamada de prueba
description: Explore las llamadas que debe realizar para validar su implementación.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 80%

---

# Detalles de la llamada de prueba{#test-call-details}

## Iniciar el reproductor de medios {#start-the-media-player}

### Llamada de inicio de Adobe Analytics (AppMeasurement)  {#aa-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _&#x200B;**`a.media.name`**&#x200B;_ | _&#x200B;**123456**&#x200B;_ |
| _&#x200B;**`a.media.length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `a.media.playerName` | HTML5 |
| _&#x200B;**`a.media.view`**&#x200B;_ | _&#x200B;**true**&#x200B;_ |
| `a.contentType` | vod |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos personalizados**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos estándar**&#x200B;_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La longitud de los flujos lineales debe ajustarse a la mejor estimación para el programa actual.

### Metadatos estándar en la llamada de inicio de Adobe Analytics (AppMeasurement)  {#std-metadata-aa}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | Red |
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
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**0**&#x200B;_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos personalizados**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos estándar**&#x200B;_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La posición del cabezal de reproducción de los flujos lineales al iniciar el vídeo debe establecerse en los segundos transcurridos desde el inicio del programa actual, no en 0.

### Metadatos estándar en la llamada de inicio de Media Analytics (latidos)  {#std-metadata-ma}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | Red |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
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
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* Esta llamada indica que Media SDK ha solicitado que se envíe una llamada `pev2=ms_s` de Adobe Analytics al servidor de Adobe Analytics (AppMeasurement).
* La llamada no puede contener metadatos personalizados.

## Visualización de la reproducción de anuncio {#view-ad-playback}

### Llamada de inicio de anuncio de Adobe Analytics (AppMeasurement)  {#aa-ad-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _&#x200B;**`pev2`**&#x200B;_ | _&#x200B;**msa_s**&#x200B;_ |
| `a.media.name` | 123456 |
| _&#x200B;**`a.media.ad.name`**&#x200B;_ | _&#x200B;**9378**&#x200B;_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _&#x200B;**`a.media.ad.length`**&#x200B;_ | _&#x200B;**15**&#x200B;_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0,0 |
| _&#x200B;**`a.media.ad.view`**&#x200B;_ | _&#x200B;**True**&#x200B;_ |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos estándar**&#x200B;_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración del anuncio puede establecerse en -1 si no está disponible al inicio del anuncio.

### Metadatos estándar en la llamada de inicio de anuncio de Adobe Analytics (AppMeasurement)  {#std-metadata-aa-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | Red |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
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
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _&#x200B;**`l:asset:length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidad**&#x200B;_ |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos personalizados**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadatos estándar**&#x200B;_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración del anuncio puede establecerse en -1 si no está disponible al inicio del anuncio.

### Metadatos estándar en la llamada de inicio de anuncio de Media Analytics (latidos)  {#std-metadata-ma-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:a.media.show` | Show |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | Red |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
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
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_ad_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | Publicidad |

### Llamada de reproducción de anuncio de Media Analytics (latidos)  {#ma-ad-play-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**play**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidad**&#x200B;_ |

### Llamada de pausa de anuncio de Media Analytics (latidos)  {#ma-ad-pause-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidad**&#x200B;_ |

### Llamada de finalización de anuncio de Adobe Analytics (latidos) de Media Analytics {#ma-aa-ad-complete-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**complete**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidad**&#x200B;_ |

## Reproducción del contenido principal {#play-main-content}

### Llamada de reproducción de Media Analytics (latidos)  {#ma-play-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:event:type` | play |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| _&#x200B;**`l:event:duration`**&#x200B;_ | _&#x200B;**10189**&#x200B;_ |
| `s:asset:name` | Episode Title |
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
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
