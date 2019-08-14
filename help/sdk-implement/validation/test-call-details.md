---
seo-title: Detalles de la llamada de prueba
title: Detalles de la llamada de prueba
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Detalles de la llamada de prueba{#test-call-details}

## Iniciar el reproductor de vídeo {#section_qts_xff_f2b}

### Llamada de inicio de Media Analytics

| Parámetro | Valor (ejemplo)   |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | true |
| `a.contentType` | vod |
| `custom.[value]` | Campos de metadatos personalizados |
| `a.media.[value]` | Campos de metadatos estándar |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración de las emisiones lineales debe establecerse con la mejor estimación para el programa actual.

### Metadatos estándar en la llamada de inicio de Media Analytics

| Parámetro | Valor (ejemplo)   |
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

### Llamada inicial de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | Campos de metadatos personalizados |
| `s:meta:a.media.[value]` | Campos de metadatos estándar |

### Metadatos de medios en la llamada de inicio de Media Analytics

| Parámetro | Valor (ejemplo)   |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La posición del cabezal de reproducción para las emisiones lineales al inicio del vídeo debe establecerse en los segundos transcurridos desde el inicio del programa actual, en lugar de 0.

### Llamada inicial del análisis de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

### Metadatos de medios en la llamada de inicio de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Metadatos estándar de la llamada inicial de Heartbeat

| Parámetro | Valor (ejemplo)   |
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

**Notas:**

* Esta llamada indica que la biblioteca de Heartbeat ha solicitado el envío de una llamada pev2=ms_s de análisis al servidor de análisis.
* La llamada no puede contener metadatos personalizados.

## Visualización de la reproducción de anuncio {#section_wz3_yff_f2b}

### Llamada de inicio de anuncio de Media Analytics

| Parámetro | Valor (ejemplo)   |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0,0 |
| `a.media.ad.view` | True |
| `custom.[value]` | Campos de metadatos |
| `a.media.[value]` | Campos de metadatos estándar |

**Nota:** Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.

### Llamada inicial de anuncio de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | Campos de metadatos personalizados |
| `s:meta:a.media.[value]` | Campos de metadatos estándar |

### Metadatos de medios en la llamada de inicio de anuncio de Media Analytics

| Parámetro | Valor (ejemplo)   |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Metadatos estándar en la llamada de inicio de anuncio de Media Analytics

| Parámetro | Valor (ejemplo)   |
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

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración del anuncio debe establecerse en -1 si no está disponible al inicio del anuncio.

### Llamada inicial de anuncio de análisis de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Metadatos de medios en la llamada de inicio de anuncio de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Metadatos estándar de la llamada inicial de anuncio de Heartbeat

| Parámetro | Valor (ejemplo)   |
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

**Notas:**

* Las variables de datos de contexto adicionales deben estar presentes y contener metadatos. Consulte los detalles de metadatos a continuación.
* La duración del anuncio debe establecerse en -1 si no está disponible al inicio del anuncio.

### Llamada de finalización de anuncio de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:event:type` | complete |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Llamada de reproducción de anuncio de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

## Reproducción del contenido principal {#section_u1l_1gf_f2b}

### Llamada de reproducción de Heartbeat

| Parámetro | Valor (ejemplo)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* La posición del cabezal de reproducción debe aumentarse en 10 unidades con cada llamada de reproducción.
* El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

