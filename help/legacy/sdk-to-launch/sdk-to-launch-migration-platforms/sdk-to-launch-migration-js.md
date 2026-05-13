---
title: 'Migración de Media SDK independiente a Adobe Launch: Web (JS)'
description: Obtenga información acerca de cómo migrar del SDK de medios a Launch para JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/N4Fcbg3R9tT9cjUcaw-kcUm6h-QT8TYwatdCe1IdsaM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c069c44e-5426-4c1a-accc-8028662f2fdeid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 77%

---

# Migración del SDK de medios independiente a Adobe Launch: Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=es) para obtener una referencia consolidada de los cambios terminológicos.

## Diferencias de características

* *Launch*: Launch proporciona una interfaz de usuario que le guiará a través de la instalación, configuración e implementación de sus soluciones de seguimiento de medios basadas en la web. Launch supone una mejora respecto a Dynamic Tag Management (DTM).
* *SDK de medios*: El SDK de medios incluye bibliotecas de seguimiento de medios diseñadas para plataformas específicas (por ejemplo: Android, iOS, etc.). Adobe recomienda usar el SDK de medios para rastrear el uso de medios en sus aplicaciones móviles.

## Configuración

### SDK de medios independiente

En Media SDK independiente se establece la configuración de seguimiento en la aplicación
y pasarlo al SDK cuando cree el rastreador.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Además de la configuración de `MediaHeartbeat`, la página debe configurar y pasar
la instancia `AppMeasurement` y la instancia `VisitorAPI` para el seguimiento de medios en orden
para funcionar correctamente.

### Extensión de Launch

1. En Experience Platform Launch, haga clic en la ficha [!UICONTROL Extensiones] para su
propiedad web.
1. En la ficha [!UICONTROL Catálogo], busque Adobe Media Analytics para audio y vídeo
Extensión de vídeo y haga clic en [!UICONTROL Instalar].
1. En la página de configuración de la extensión, configure los parámetros de seguimiento.
La extensión de medios utilizará los parámetros configurados para el seguimiento.

   ![](assets/launch_config_js.png)

[Guía del usuario de Launch: Instalar y configurar la extensión de medios](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=es#install-and-configure-the-ma-extension)

## Diferencias en la creación del rastreador

### Media SDK

1. Añadir la biblioteca de Media Analytics al proyecto de desarrollo.
1. Crear un objeto config (`MediaHeartbeatConfig`).
1. Implementar el protocolo delegado, con las funciones `getQoSObject()` y `getCurrentPlaybackTime()`.
1. Crear una instancia de Media Heartbeat (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### Launch

Launch ofrece dos métodos para crear la infraestructura de seguimiento. Ambos métodos utilizan la extensión de Launch de Media Analytics:

1. Utilice las API de seguimiento de medios de una página web.

   En este escenario, la extensión de Media Analytics exporta las API de seguimiento de medios a una variable configurada en el objeto de ventana global:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilice las API de seguimiento de medios de otra extensión de Launch.

   En este escenario, se utilizan las API de seguimiento de medios expuestas por los módulos compartidos `get-instance` y `media-heartbeat`.

   >[!NOTE]
   >
   >Los módulos compartidos no están disponibles para su uso en páginas web. Solo puede usar módulos compartidos desde otra extensión.

   Cree una instancia `MediaHeartbeat` con el módulo compartido `get-instance`.
Pase un objeto delegado a `get-instance` que exponga las funciones `getQoSObject()` y `getCurrentPlaybackTime()`.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Acceda a las constantes de `MediaHeartbeat` a través del módulo compartido `media-heartbeat`.

## Documentación relacionada

### Media SDK

* [Configuración de JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [API de JS de Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Información general de Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
* [Extensión de Media Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=es)
