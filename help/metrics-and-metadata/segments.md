---
title: Segmentos
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Segmentos {#segments}

>[!NOTE]
>
>Los siguientes segmentos de informes asociados al tipo de emisión de contenido se introdujeron el 13 de septiembre de 2018 junto con el parámetro `streamType`.

| Segmento | Descripción | Regla |
|---|---|---|
| Tipo de flujo de medios: todos | Segmentar todos los datos de flujo de *medios* | &quot;Content (ID) exists&quot; |
| Tipo de flujo de medios: audio | Segmentar todos los datos del flujo de *audio* | “El contenido (ID) existe” AND “Tipo de emisión de medio = `audio`” |
| Tipo de flujo de medios: vídeo | Segmentar todos los datos de flujo de *vídeo* | &quot;Content (ID) exists&quot; AND &quot;Media Stream Type != `audio`&quot; |
| Tipo de contenido de medios: VoD | Segmentar todo el contenido de VoD | &quot;Tipo de contenido = `vod`&quot; |
| Tipo de contenido de medios: activo | Segmentar todo el contenido activo | &quot;Tipo de contenido = `live`&quot; |
| Tipo de contenido de medios: lineal | Segmentar todo el contenido lineal | &quot;Tipo de contenido = `linear`&quot; |
| Tipo de contenido de medios: podcast | Segmentar todo el contenido del podcast | &quot;Tipo de contenido = `podcast`&quot; |
| Tipo de contenido de medios: audiolibro | Segmentar todo el contenido de Audiobook | &quot;Tipo de contenido = `audiobook`&quot; |
| Tipo de contenido de medios: AoD | Segmentar todo el contenido de AoD | &quot;Tipo de contenido = `aod`&quot; |

