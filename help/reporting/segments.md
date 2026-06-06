---
title: Explicación de los segmentos de streaming de medios
description: Obtenga información acerca de los segmentos de creación de informes asociados con el tipo de flujo de medios, incluidos el segmento, la descripción y la regla para el tipo de flujo de medios.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: cb3770abd06eb8debe4ff92641835f04f62471f7
workflow-type: tm+mt
source-wordcount: 189
ht-degree: 75%

---

# Segmentos de medios de streaming

Los segmentos le permiten identificar subconjuntos de visitantes basándose en sus características o en las interacciones con el sitio web. Los segmentos de medios de streaming le permiten identificar el tipo de flujo del visitante, como emisiones de audio, en directo o pódcast. Para obtener información sobre los segmentos de Adobe Analytics, consulte [Acerca de los segmentos](https://experienceleague.adobe.com/en/docs/analytics/components/segmentation/seg-overview) en la Guía de componentes de Adobe Analytics.

| Segmento | Descripción | Regla |
|---|---|---|
| Tipo de flujo de medios: todos | Segmentar todos los datos de flujo de *medios* | “Content (ID) exists” |
| Tipo de flujo de medios: audio | Segmentar todos los datos del flujo de *audio* | “El contenido (ID) existe” Y “Tipo de emisión de medio = `audio`” |
| Tipo de flujo de medios: vídeo | Segmentar todos los datos de flujo de *vídeo* | “El contenido (ID) existe” Y “Tipo de emisión de medio != `audio`” |
| Tipo de contenido de medios: VoD | Segmentar todo el contenido de VoD | “Tipo de contenido = `vod`” |
| Tipo de contenido de medios: activo | Segmentar todo el contenido activo | “Tipo de contenido = `live`” |
| Tipo de contenido de medios: lineal | Segmentar todo el contenido lineal | “Tipo de contenido = `linear`” |
| Tipo de contenido de medios: podcast | Segmentar todo el contenido del podcast | “Tipo de contenido = `podcast`” |
| Tipo de contenido de medios: audiolibro | Segmentar todo el contenido de Audiobook | “Tipo de contenido = `audiobook`” |
| Tipo de contenido de medios: AoD | Segmentar todo el contenido de AoD | “Tipo de contenido = `aod`” |
