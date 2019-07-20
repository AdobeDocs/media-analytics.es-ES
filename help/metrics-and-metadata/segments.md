---
seo-title: Segmentos
title: Segmentos
uuid: 61906 b 8 c -3362-4463-82 be-fe 0 e 741 a 5 eb 3
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Segmentos{#segments}

>[!NOTE]
>
>These reporting segments associated with Media Stream Type were introduced on 9/13/18 along with the `streamType` parameter.

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

