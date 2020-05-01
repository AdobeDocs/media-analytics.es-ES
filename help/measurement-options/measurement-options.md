---
title: Opciones de medición
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 47b4c7fe09da0d38c8faae1c3b4293ce48552bdc

---


# Opciones de medición

Puede activar el seguimiento de audio y vídeo mediante Adobe Launch con la extensión Adobe Media Analytics, el SDK de medios o la API de Media Collection.

## Adobe Launch con la extensión Adobe Media Analytics

Adobe Launch es la solución de administración de etiquetas de próxima generación de Adobe. Launch proporciona una manera sencilla de implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las experiencias relevantes de los clientes. Para crear y mantener sus propias integraciones con Launch, utilice extensiones. Una extensión es un paquete JavaScript, HTML y CSS que amplía la interfaz de usuario de Launch y la funcionalidad del cliente. Para obtener más información, consulte la Guía del usuario del [Experience Platform Launch](https://docs.adobe.com/content/help/es-ES/launch/using/overview.html)

La extensión Adobe Media Analytics (MA) agrega el SDK principal de medios JavaScript (SDK de Media 2.x) para audio y vídeo. Esta extensión proporciona la funcionalidad para agregar la instancia de seguimiento `MediaHeartbeat` a un sitio o proyecto de Launch.

Adobe Launch con la extensión Media Analytics requiere lo siguiente:
* Debe ser cliente de Adobe Experience Cloud.
* Debe implementar el código incrustado de Launch o DTM en las páginas web.
* [Extensión de Analytics](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Extensión de Experience Cloud ID](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

El SDK de medios se integra con los reproductores de medios más utilizados.

## API de recopilación de medios (API de RESTful)

Se integra con reproductores sin compatibilidad con SDK o cuando no se necesita integración con SDK.<br>A partir de la versión v2.2.0, los SDK de Video Heartbeat Library (VHL) pasan a denominarse SDK de Media Analytics para admitir el seguimiento de audio y vídeo. El SDK de Media 2.2.0 es totalmente compatible con la serie VHL 2.x del SDK. El cambio de nombre es simplemente un cambio en la convención de nombres y no representa cambios funcionales.
