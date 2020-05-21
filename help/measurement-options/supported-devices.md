---
title: Dispositivos y plataformas admitidos
description: Adobe Analytics para audio y vídeo garantiza que cada flujo de medios se recopile y se notifique en todos los dispositivos.
translation-type: tm+mt
source-git-commit: a8fec1747e688473af7a5eabbc4f9968772b5db3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 15%

---


# Dispositivos y plataformas admitidos {#devices-supported}

>[!IMPORTANT]
>
>Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejará de ofrecer compatibilidad con el SDK de Media Analytics para iOS y Android.  Para obtener más información, consulte Preguntas más frecuentes sobre el fin de la asistencia técnica del SDK de [Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics para audio y vídeo admite todos los dispositivos principales, incluidos:

* Smartphones y tabletas iOS y Android
* Dispositivos OTT para ROKU, AppleTV, FireTV y Android TV
* Navegador JavaScript para equipos de escritorio y portátiles

Los SDK de medios se actualizan de forma rutinaria cuando se lanzan nuevas versiones de dispositivos y puede utilizar el SDK para integrarse con los reproductores de medios más grandes de hoy, incluidos Brightcove y Ooyala.

En el caso de dispositivos o plataformas que actualmente no son compatibles con SDK o en situaciones en las que no desea utilizar un SDK, puede implementar la API de Media Collection. La API de Media Collection le permite realizar llamadas a la API de RESTful directamente desde un dispositivo o plataforma al servidor de Media Analytics.

La siguiente tabla lista los dispositivos y plataformas compatibles actualmente. Para descargar la versión más actualizada del SDK, consulte [Descarga de SDK](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). Si un dispositivo no aparece en la lista, póngase en contacto con el servicio de atención al cliente o con el consultor de soluciones para conocer el estado de dicho dispositivo.

| Plataformas y dispositivos de flujo continuo |  | Media Launch Extension con SDK de AEP | Media SDK | API de Media Collection |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Web móvil |  |  |  |  |
|  | Exploradores JavaScript | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Aplicación móvil |  |  |  |  |
|  | Dispositivos iOS | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos Android | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos Windows |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | Planeado para 2020 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(nativo) |
|  | Fire TV (Fire OS) | Planeado para 2020 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | Planeado para 2020 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Consolas de juegos (por ejemplo, Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Definir los cuadros superiores (por ejemplo, xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Televisores inteligentes (por ejemplo, Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(basado en web)    | ![](/help/assets/icon-blue-check.png) |
| Otro |  |  |  |  |
|  | Nuevos dispositivos conectados |  |  | ![](/help/assets/icon-blue-check.png) |

1. La compatibilidad con estos SDK finaliza el 31 de agosto de 2021. Para obtener más información, consulte Preguntas más frecuentes sobre el fin de la asistencia técnica del SDK de [Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Para obtener información adicional sobre las versiones de plataforma mínimas admitidas para cada SDK, consulte Compatibilidad con versiones de plataforma [mínima](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)
