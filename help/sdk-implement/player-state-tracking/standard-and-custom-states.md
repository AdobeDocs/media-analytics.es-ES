---
title: Acerca de los estados estándar y personalizados
description: Obtenga información sobre la función de seguimiento del estado del reproductor, que incluye requisitos y directrices para la implementación y creación de informes de estados de reproductor estándar y personalizados.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 92%

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

Para obtener información sobre la creación de estados personalizados, consulte la [Guía de referencia de API de medios: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
