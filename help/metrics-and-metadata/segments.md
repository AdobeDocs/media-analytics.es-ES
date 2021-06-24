---
title: Segmentos de flujo de medios explicados
description: '"Obtenga información sobre los segmentos de informes asociados con el tipo de flujo de medios, incluidos el segmento, la descripción y la regla para el tipo de flujo de medios".'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics, Segmentación"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: 2d9d4352b0fd71710a9952ba4a77f6796ea9f5cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 66%

---

# Segmentos{#segments}

Los segmentos le permiten identificar subconjuntos de visitantes basándose en sus características o en las interacciones con el sitio web. Los segmentos de medios de transmisión le permiten identificar el tipo de flujo del visitante, como emisiones de audio, en directo o podcast. Para obtener información sobre los segmentos de Adobe Analytics, consulte [Acerca de los segmentos y contenedores](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=en) en la Guía de componentes de Adobe Analytics.

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
