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
| Tipo de emisión de medio: all | Segmenta todos los datos de emisión de *medios*. | “El contenido (ID) existe” |
| Tipo de emisión de medio: audio | Segmenta todos los datos de emisión de *audio*. | “El contenido (ID) existe” AND “Tipo de emisión de medio = `audio`” |
| Tipo de emisión de medio: video | Segmenta todos los datos de emisión de *vídeo*. | “El contenido (ID) existe” AND “Tipo de emisión de medio != `audio`" |
| Tipo de contenido de medio: vod | Segmenta todo el contenido VoD. | "Tipo de contenido = `vod`" |
| Tipo de contenido de medio: live | Segmenta todo el contenido en directo. | "Tipo de contenido = `live`" |
| Tipo de contenido de medio: linear | Segmenta todo el contenido lineal. | "Tipo de contenido = `linear`" |
| Tipo de contenido de medio: podcast | Segmenta todo el contenido de podcast. | "Tipo de contenido = `podcast`" |
| Tipo de contenido de medio: audiobook | Segmenta todo el contenido de audiolibro. | "Tipo de contenido = `audiobook`" |
| Tipo de contenido de medio: AoD | Segmenta todo el contenido AoD. | "Tipo de contenido = `aod`" |

