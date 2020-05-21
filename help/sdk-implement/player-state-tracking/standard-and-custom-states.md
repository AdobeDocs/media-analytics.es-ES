---
title: Acerca de los estados estándar y personalizados
description: En este tema se describe la función de seguimiento del estado del reproductor, que incluye requisitos y directrices para la implementación y sistema de informes de estados de reproductor estándar y personalizados.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '251'
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

* Una sesión de vídeo está limitada a 10 estados de reproductor personalizados únicos.
* Si pasan varios estados de reproductor, solo se retienen los 10 primeros y se reenvían a través del flujo hacia abajo al componente de procesamiento VA(?video analytics).
* El máximo de 10 estados se aplica a todos los estados, independientemente de si están cerrados o no.
* El mismo estado se puede iniciar y finalizar cualquier número de veces y se cuenta como un solo estado.
* ¿Todos los estados que exceden el máximo permitido? estados (10) se descartan.

## Estados personalizados

Con la capacidad de crear estados personalizados, puede capturar acciones personalizadas y actualizar los metadatos personalizados durante una sesión de reproducción.

NECESITA más información sobre los estados personalizados
