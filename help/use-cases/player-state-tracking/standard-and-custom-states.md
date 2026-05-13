---
title: Acerca de los estados estándar y personalizados
description: Obtenga más información sobre la función de seguimiento del estado de los jugadores, incluidos los requisitos y las directrices para implementar e informar sobre los estados de los jugadores estándar y personalizados.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/QdUkyWt6cTcdmQXpj6Qe6-s3aYkGfro-G7DYegOVKvA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 96%

---

# Acerca de los estados estándar y personalizados

Hay cinco estados de reproductor estándar disponibles y puede agregar sus propios estados personalizados.

| Nombre de estado estándar | Constante de Media SDK | Nombre de la API de Media Collection |
|-----------------------|------------------------------------------|-----------------------------|
| Pantalla completa | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Subtítulos | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Silenciar | `ADB.Media.PlayerState.Mute` | `mute` |
| Imagen en imagen | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Enfocado | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Los datos se calculan del mismo modo para los estados estándar y personalizados, pero los datos se almacenan de forma diferente para el sistema de informes de Analytics.

**Para estados estándar**: cuando se habilita el seguimiento del estado del reproductor desde la consola de Media Management en el sistema de informes de Analytics (administrador), hay 15 variables de solución disponibles para las exportaciones de datos y sistemas de informes.

**Para los estados personalizados**: puede crear sus propias reglas de procesamiento para almacenar los valores calculados en eventos personalizados y, a continuación, utilizar esas reglas para las exportaciones de datos y sistemas de informes.

## Directrices

* Una sesión de vídeo está limitada a 10 estados de reproductor.
* Se permite cualquier combinación de estados.
* Si pasan varios estados de reproductor, solo se retienen los 10 primeros y se reenvían a través del flujo hacia abajo al componente de procesamiento VA.
* El máximo de 10 estados se aplica a todos los estados, independientemente de si están cerrados o no.
* Un estado se puede iniciar y finalizar varias veces y se cuenta como un solo estado. Por ejemplo, `closedCapationing` se puede iniciar y detener cinco veces, pero se contará como un solo estado.
* Se descartan todos los estados que superen el máximo de 10 estados permitidos.

## Estados personalizados

Con la capacidad de crear estados personalizados, puede capturar acciones personalizadas y actualizar los metadatos personalizados durante una sesión de reproducción.

Para obtener información sobre la creación de estados personalizados, consulte la [Guía de referencia de API de medios: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)
