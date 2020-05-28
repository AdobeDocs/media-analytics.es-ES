---
title: Acerca de los estados estándar y personalizados
description: En este tema se describe la función de seguimiento del estado del reproductor, que incluye requisitos y directrices para la implementación y sistema de informes de estados de reproductor estándar y personalizados.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# Acerca de los estados estándar y personalizados

Hay cinco estados de reproductor estándar disponibles y puede agregar sus propios estados personalizados.

| Nombre de estado estándar | Constante de SDK de medios | Nombre de la API de Media Collection |
|-----------------------|------------------------------------------|-----------------------------|
| Pantalla completa | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Subtítulos opcionales | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Silenciar | `ADB.Media.PlayerState.Mute` | `mute` |
| Imagen en imagen | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| En Enfoque | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Los datos se calculan del mismo modo para los estados estándar y personalizados, pero los datos se almacenan de forma diferente para Analytics sistema de informes.

**Para estados** estándar: cuando se habilita el seguimiento del estado del reproductor desde la consola de Media Management en Analytics sistema de informes (administrador), hay 15 variables de solución disponibles para las exportaciones de sistema de informes y datos.

**Para los estados** personalizados: puede crear sus propias reglas de procesamiento para almacenar los valores calculados en eventos personalizados y, a continuación, utilizar esas reglas para las exportaciones de sistemas de informes y datos.

## Directrices

* Una sesión de vídeo está limitada a 10 estados de reproductor.
* Se permite cualquier combinación de estados.
* Si pasan varios estados del reproductor, solo se retienen los 10 primeros y se reenvían a la fase posterior al componente de procesamiento de VA.
* El máximo de 10 estados se aplica a todos los estados, independientemente de si están cerrados o no.
* Un estado puede inicio y finalizar varias veces y se cuenta como un solo estado. Por ejemplo, `closedCapationing` se puede iniciar y detener cinco veces, pero se contará como un solo estado.
* Se descartan todos los estados que superen el máximo de 10 estados permitidos.

## Estados personalizados

Con la capacidad de crear estados personalizados, puede capturar acciones personalizadas y actualizar los metadatos personalizados durante una sesión de reproducción.

Para obtener información sobre la creación de estados personalizados, consulte la Guía de referencia de API de [medios: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
