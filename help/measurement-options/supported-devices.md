---
title: Dispositivos y plataformas compatibles
description: Adobe Analytics para audio y vídeo garantiza que cada flujo de medios se recopile y se informe en todos los dispositivos.
translation-type: tm+mt
source-git-commit: 4db4e4281ba9c7af078c18d03f73b6e1e007a0e8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 100%

---


# Dispositivos y plataformas compatibles {#devices-supported}

>[!IMPORTANT]
>
>Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejará de ofrecer compatibilidad con el SDK de Media Analytics para iOS y Android.  Para obtener más información, consulte [Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics para audio y vídeo admite todos los dispositivos principales, incluidos:

* Smartphones y tabletas iOS y Android
* Dispositivos OTT para ROKU, AppleTV, FireTV y Android TV
* Navegador JavaScript para equipos de escritorio y portátiles

Los Media SDK se actualizan normalmente cuando salen al mercado nuevas versiones de estos dispositivos, y se puede utilizar integrándolo con los grandes reproductores de contenidos actuales, incluidos Brightcove y Ooyala.

En el caso de dispositivos o plataformas que actualmente no son compatibles con SDK, o en situaciones en que no desea utilizar un SDK, puede implementar la API de Media Collection. La API de Media Collection le permite hacer llamadas a la API de RESTful directamente de un dispositivo o plataforma al servidor de Media Analytics.

En la tabla siguiente, se detallan los dispositivos y las plataformas actualmente compatibles. Para descargar la versión más actualizada del SDK, consulte [Descarga de SDK](https://docs.adobe.com/content/help/es-ES/media-analytics/using/sdk-implement/download-sdks.html). Si un dispositivo no aparece en la lista, póngase en contacto con el servicio de atención al cliente o con el consultor de soluciones para conocer el estado de dicho dispositivo.

| Plataformas y dispositivos de transmisión |  | Extensión de Media Launch con SDK de AEP | Media SDK | API de Media Collection |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Web móvil |  |  |  |  |
|  | Exploradores con JavaScript | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Aplicación móvil |  |  |  |  |
|  | Dispositivos iOS | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos Android | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos con Windows |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript) | ![](/help/assets/icon-blue-check.png)<br>(nativo) |
|  | Fire TV (sistema operativo Fire) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Consolas de juegos (por ejemplo, Xbox ONE, Sony PS3/PS4) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Definir los cuadros superiores (por ejemplo, xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Televisores inteligentes (por ejemplo, Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(basado en la Web) | ![](/help/assets/icon-blue-check.png) |
| Otro |  |  |  |  |
|  | Nuevos dispositivos conectados |  |  | ![](/help/assets/icon-blue-check.png) |

1. La compatibilidad con estos SDK finaliza el 31 de agosto de 2021. Para obtener más información, consulte [Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Para obtener información adicional sobre las versiones de plataforma mínimas admitidas para cada SDK, consulte [Compatibilidad con versiones de plataforma mínima](https://docs.adobe.com/content/help/es-ES/media-analytics/using/sdk-implement/setup/setup-overview.html)
