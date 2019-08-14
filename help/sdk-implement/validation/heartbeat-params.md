---
seo-title: Descripciones de parámetros de Heartbeat
title: Descripciones de parámetros de Heartbeat
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Descripciones de parámetros de Media Analytics (Heartbeat){#heartbeat-parameter-descriptions}

Lista de parámetros de Media Analytics que Adobe recopila y procesa en el servidor de latidos:

## Todos los eventos

| Nombre | Requerido/opcional | Fuente de datos | Descripción   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | Media SDK | Tipo de evento que se rastrea. Tipos de eventos: <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | Media SDK | Marca de fecha del último evento del mismo tipo en esta sesión. El valor es `-1` |
| `l:event:ts` | R | Media SDK | Marca de tiempo del evento. |
| `l:event:duration` | R | Media SDK | Este valor se establece internamente (en milisegundos) por la biblioteca VHL, no por el reproductor. Se utiliza para calcular las métricas de tiempo invertido en el servidor. For example `a.media.totalTimePlayed` `type=play` Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., `type=complete` `type=chapter_complete` `type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | El objeto playhead estaba dentro del recurso activo (principal o anuncio), cuando se registró el evento. |
| `s:event:sid` | R | Media SDK | El ID de sesión (cadena generada aleatoriamente). Todos los eventos de una sesión determinada (vídeo + anuncios) deben ser los mismos. |
| `l:asset:duration / l:asset:length` (Se ha cambiado el nombre de `length``duration` | R | `VideoInfo` | La duración del recurso de vídeo del recurso principal. |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | El editor del recurso. |
| `s:asset:video_id` | R | `VideoInfo` | ID que identifica de forma exclusiva el vídeo en el catálogo del editor. |
| `s:asset:type` | R | Media SDK | Tipo de recurso (principal o anuncio). |
| `s:stream:type` | R | `VideoInfo` | Tipo de emisión. Puede ser uno de los siguientes: <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>. |
| `s:user:id` | O | Objeto Configuration para dispositivos móviles, medición de aplicaciones VisitorID | El usuario definió específicamente el ID de visitante. |
| `s:user:aid` | O | Org. de Experience Cloud | El valor de ID de visitante de análisis del usuario. |
| `s:user:mid` | R | Org. de Experience Cloud | El valor de identificación de visitantes de la nube de experiencia del usuario. |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | Todos los ID de usuario de cliente definidos en Audience Manager. |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | ID (o identificadores) del grupo de informes | RSID de Adobe Analytics donde se deben enviar los informes. |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | Servidor de seguimiento de Adobe Analytics. |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | Indica si el tráfico se envía por HTTPS (si se configura en 1) o por HTTP (si se configura en 0). |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | Establézcalo en "primetime" para reproductores de Primetime o en el OVP real para otros reproductores. |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | La cadena de versión de OVP. |
| `s:sp:player_name` | R | `VideoInfo` | Nombre del reproductor de vídeo (el software de reproducción usado para identificar el reproductor). |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | Canal donde el usuario ve el contenido. En aplicaciones móviles, el nombre de la aplicación. En sitios web, el nombre del dominio. |
| `s:sp:hb_version` | R | Media SDK | Número de versión de VideoHeartbeat Library que efectúa la llamada. |
| `l:stream:bitrate` | R | `QoSInfo` | Valor real de la velocidad de bits de la emisión (en bps). |

## Eventos de error

| Nombre | Requerido/opcional | Fuente de datos | Descripción   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | Media SDK | Origen del error, ya sea que esté en el reproductor o en la aplicación. |
| `s:event:id` | R | Media SDK | ID de error, identifica el error de manera exclusiva. |

## Eventos de anuncio

| Nombre | Requerido/opcional | Fuente de datos | Descripción   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | Nombre del anuncio. |
| `s:asset:ad_sid` | R | Media SDK | Identificador único generado por el Media SDK, anexado a todos los pings relacionados con anuncios. |
| `s:asset:pod_id` | R | Media SDK | ID de la secuencia dentro del vídeo. Este valor se calcula automáticamente en función de la siguiente fórmula: `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | Índice del anuncio dentro de la secuencia (el primer anuncio tiene el índice 0, el segundo tiene el índice 1, etc.). |
| `s:asset:resolver` | R | `AdBreakInfo` | El solucionador de anuncios. |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | Los metadatos de anuncios personalizados. |

## Eventos de capítulo

| Nombre | Requerido/opcional | Fuente de datos | Descripción   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | Media SDK | Identificador exclusivo asociado a la instancia de reproducción del capítulo.  Nota: Un capítulo se puede reproducir varias veces debido a las operaciones seek-back realizadas por el usuario. |
| `s:stream:chapter_name` | O | `ChapterInfo` | El nombre descriptivo del capítulo (por ejemplo, que sea comprensible). |
| `s:stream:chapter_id` | R | Media SDK | ID exclusivo del capítulo. Este valor se calcula automáticamente en función de la siguiente fórmula: `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | Índice del capítulo en la lista de capítulos (a partir del 1). |
| `l:stream:chapter_offset` | R | `ChapterInfo` | El desplazamiento del capítulo (expresado en segundos) dentro del contenido principal, sin incluir los anuncios. |
| `l:stream:chapter_length` | R | `ChapterInfo` | La duración del capítulo (expresada en segundos). |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | Metadatos del capítulo personalizado. |

## Evento Fin de la sesión

| Nombre | Requerido/opcional | Fuente de datos | Descripción   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | Media SDK | El `end` `close` |

