---
title: Dispositivos admitidos
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 3a237ee31412784f708e772cc3a58047630e2184

---


# Dispositivos admitidos {#devices-supported}

Adobe Analytics para audio y vídeo garantiza que cada flujo de medios se recopile y se notifique en todos los dispositivos.

Adobe Analytics para audio y vídeo admite todos los dispositivos principales, incluidos:

* Smartphones y tabletas iOS y Android
* Dispositivos OTT para ROKU, AppleTV, FireTV y Android TV
* Navegador JavaScript para equipos de escritorio y portátiles

El SDK de medios se actualiza de forma rutinaria cuando se lanzan nuevas versiones de dispositivos y puede utilizarlo para integrarlo con los reproductores de medios más grandes de la actualidad, incluidos Brightcove y Ooyala.

En el caso de dispositivos o plataformas que actualmente no son compatibles con SDK o en situaciones en las que no desea utilizar un SDK, puede implementar la API de Media Collection. La API de Media Collection le permite realizar llamadas a la API de RESTful directamente desde un dispositivo o plataforma al servidor de Media Analytics.

La tabla siguiente lista los dispositivos admitidos actualmente. Para descargar la versión más actualizada del SDK, consulte [Descarga de SDK](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). Si un dispositivo no aparece en la lista, póngase en contacto con el servicio de atención al cliente o con el consultor de soluciones para conocer el estado de dicho dispositivo.


| Dispositivo/plataforma de flujo continuo |  | Media Launch Extension con SDK de AEP | Media SDK | API de Media Collection |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| Web/Web móvil |  |  |  |  |
|  | Exploradores JavaScript | X | X | X |
| Aplicación móvil |  |  |  |  |
|  | Dispositivos iOS | X | X | X |
|  | Dispositivos Android | X | X | X |
|  | Dispositivos Windows |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV (heredado, TVOS) |  | X | X |
|  | ROKU |  | X<br>(BrightScript) | X<br>(nativo) |
|  | Fire TV (Fire OS) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | Consolas de juegos (por ejemplo, Xbox ONE, Sony PS3/PS4) |  |  | X |
|  | Definir los cuadros superiores (por ejemplo, xfinity X1) |  |  | X |
|  | Televisores inteligentes (por ejemplo, Samsung, LG, Sony, Vizio) |  | X<br>(basado en Web) | X |
| Otro |  |  |  |  |
|  | Nuevos dispositivos conectados |  |  | X |


Para Media SDK, consulte [Compatibilidad con versiones de plataforma mínima](/help/sdk-implement/setup/setup-overview.md#minimum-platform-version)
