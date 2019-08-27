---
seo-title: Detalles de la llamada de prueba
title: Detalles de la llamada de prueba
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: d694ced982140c1f8020c0be304492aee0495cdc

---


# Detalles de la llamada de prueba{#test-call-details}

## Iniciar el reproductor de medios {#start-the-media-player}

### Llamada de inicio de Adobe Analytics (appmeasurement) {#aa-start-call}

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

### Metadatos estándar en la llamada de inicio de Adobe Analytics (appmeasurement) {#std-metadata-aa}

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
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de Adobe Analytics (appmeasurement) {#custom-metadata-aa}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Llamada de inicio de Media Analytics (latidos) {#ma-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Campos de metadatos personalizados**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campos de metadatos estándar**_ |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La posición del cabezal de reproducción para las emisiones lineales al inicio del vídeo debe establecerse en los segundos transcurridos desde el inicio del programa actual, en lugar de 0.

### Metadatos estándar en la llamada de inicio de Media Analytics (latidos) {#std-metadata-ma}

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
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de Media Analytics (latidos) {#custom-metadata-ma}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Llamada de inicio de Media Analytics (latidos) de Adobe Analytics {#ma-aa-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* Esta llamada indica que el SDK de Media ha solicitado que se envíe una `pev2=ms_s` llamada de Adobe Analytics al servidor de Adobe Analytics (appmeasurement).
* La llamada no puede contener metadatos personalizados.

## Visualización de la reproducción de anuncio {#view-ad-playback}

### Llamada de inicio de anuncio de Adobe Analytics (appmeasurement) {#aa-ad-start-call}

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

### Standard metadata in Adobe Analytics (AppMeasurement) Ad Start call {#std-metadata-aa-ad-start}

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
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de anuncio de Adobe Analytics (appmeasurement) {#custom-metadata-aa-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Llamada de inicio de publicidad de Media Analytics (latidos) {#ma-ad-start-call}

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

### Standard metadata in Media Analytics (heartbeats) Ad Start call {#std-metadata-ma-ad-start}

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
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadatos personalizados en la llamada de inicio de anuncio de Media Analytics (latidos) {#custom-metadata-ma-ad-start}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Llamada de inicio de anuncio de Media Analytics (latidos) de Adobe Analytics {#ma-aa-ad-start-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Llamada de reproducción de publicidad de Media Analytics (latidos) {#ma-ad-play-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**reproducir**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Llamada de pausa de medios (latidos) Llamada de pausa publicitaria {#ma-ad-pause-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Llamada de finalización de publicidad de Media Analytics (latidos) de Adobe Analytics {#ma-aa-ad-complete-call}

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

### Llamada de reproducción de Media Analytics (latidos) {#ma-play-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* La posición del cursor de reproducción debe incrementarse en 10 segundos con cada llamada de reproducción.
* El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

## Poner en pausa el contenido principal {#pause-main-content}

### Llamada de pausa de Media Analytics (latidos) {#ma-pause-call}

| Parámetro |  Valor (ejemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |


