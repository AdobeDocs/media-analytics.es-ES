---
title: Explicación de los segmentos de streaming de medios
description: “Obtenga información acerca de los segmentos de creación de informes asociados con el tipo de flujo de medios, incluidos el segmento, la descripción y la regla para el tipo de flujo de medios”.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: "Media Analytics, Segmentation"
role: User, Admin, Data Engineer
source-git-commit: b15a81dc8f08e94c9b80d66019f3d0fe95ef5a74
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 99%

---

# Segmentos de medios{#segments}

Los segmentos le permiten identificar subconjuntos de visitantes basándose en sus características o en las interacciones con el sitio web. Los segmentos de medios de streaming le permiten identificar el tipo de flujo del visitante, como emisiones de audio, en directo o pódcast. Para obtener información acerca de los segmentos de Adobe Analytics, consulte [Acerca de los segmentos y los contenedores](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=es) en la Guía de componentes de Adobe Analytics.

>[!NOTE]
>
>Los siguientes segmentos de informes asociados al tipo de emisión de contenido se introdujeron el 13 de septiembre de 2018 junto con el parámetro `streamType`.

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
