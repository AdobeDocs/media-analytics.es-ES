---
title: Seguimiento de capítulos y segmentos
description: Implementar el seguimiento de capítulos y segmentos con Media SDK.
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 191
ht-degree: 39%

---


# Seguimiento de capítulos y segmentos

El seguimiento de capítulos y segmentos está disponible para capítulos o segmentos de contenido multimedia detallados. Algunos usos comunes del seguimiento de capítulos son definir los segmentos personalizados basados en el contenido del medio, tales como los innings de béisbol o definir segmentos de contenido entre las pausas publicitarias. El seguimiento de capítulos **no** es necesario para las implementaciones de seguimiento de contenidos principales.

El seguimiento de capítulos incluye el inicio del capítulo, su finalización y omisión. Utilice la API del reproductor de contenido con una lógica de segmentación personalizada para identificar eventos de capítulo y rellenar variables de capítulo.

## Eventos del reproductor

| Evento del reproductor | Acción |
| --- | --- |
| Inicio del capítulo | Crear objeto de capítulo; llamar a ChapterStart |
| Capítulo completado | Invocar a ChapterComplete |
| Omisión de capítulo | Llamar a ChapterSkip |

## Pasos de implementación

1. Identifique cuándo se produce el evento de inicio de capítulo y cree el objeto de capítulo. Consulte [Nombre de capítulo](/help/implementation/variables/chapters/chapter-name.md), [Posición de capítulo](/help/implementation/variables/chapters/chapter-position.md), [Longitud de capítulo](/help/implementation/variables/chapters/chapter-length.md) y [Desplazamiento de capítulo](/help/implementation/variables/chapters/chapter-offset.md) para ver las definiciones de los campos.
1. Si lo desea, puede crear variables de datos de contexto para metadatos de capítulo personalizados.
1. Llame a [Inicio del capítulo](/help/implementation/events/chapters/chapter-start.md) para iniciar el seguimiento del capítulo.
1. Cuando la reproducción llegue al final del capítulo, invoque [Capítulo completado](/help/implementation/events/chapters/chapter-complete.md).
1. Si el usuario omite el capítulo antes de completarlo, llame a [Chapter skip](/help/implementation/events/chapters/chapter-skip.md).
1. Para capítulos adicionales, repita los pasos del 1 al 5.
