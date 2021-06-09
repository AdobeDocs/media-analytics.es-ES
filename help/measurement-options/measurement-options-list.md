---
title: 'Opciones de medición '
description: null
uuid: null
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 93%

---


# Opciones de medición {#measurement-options}

Puede activar el seguimiento de audio y vídeo mediante Adobe Launch con la extensión de Adobe Media Analytics, Media SDK o la API de Media Collection.

## Adobe Launch con la extensión de Adobe Media Analytics

Adobe Launch es la función de administración de etiquetas de próxima generación de Adobe. Launch ofrece una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Para crear y mantener sus propias integraciones con Launch, utiliza extensiones. Una extensión es un paquete de JavaScript, HTML y CSS que amplía la funcionalidad del cliente y la interfaz de usuario de Launch. Para obtener más información, consulte la [Guía del usuario de Experience Platform Launch](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html)

La extensión de Adobe Media Analytics (MA) agrega el SDK principal de JavaScript Media (Media SDK 2.x) para audio y vídeo. Esta extensión proporciona la funcionalidad para agregar la instancia de seguimiento `MediaHeartbeat` a un sitio o proyecto de Launch.

Adobe Launch con la extensión Media Analytics requiere lo siguiente:
* Debe ser cliente de Adobe Experience Cloud.
* Debe implementar el código incrustado de Launch o DTM en las páginas web.
* [Extensión de Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Extensión de Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK se integra con los reproductores de contenidos más habituales.

## API de Media Collection (API RESTful)

Se integra con reproductores sin compatibilidad con SDK o cuando no se necesita integración con SDK.<br>Desde la versión v2.2.0, los SDK de Video Heartbeat Library (VHL) pasan a denominarse Media SDK Analytics para admitir el seguimiento de audio y vídeo. El SDK Media 2.2.0 es totalmente compatible con la serie SDK VHL 2.X. El cambio de nombre es simplemente un cambio en las normas de asignación de nombres y no representa cambios funcionales.
