---
title: Envío de datos web a Edge con Adobe Experience Platform Web SDK
description: Aprenda a enviar datos de medios de streaming de Adobe a Experience Platform Edge con Adobe Experience Platform Web SDK.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Envío de datos web a Edge con Adobe Experience Platform Web SDK

A partir de la versión 2.20.0, el componente `streamingMedia` de Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) le permite recopilar datos relacionados con las sesiones de contenido en su sitio web. Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados.

Una vez recopilados los datos, puede enviarlos a Adobe Experience Platform o Adobe Analytics para generar informes. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

Para los clientes que utilizan Media JS SDK, Web SDK proporciona una ruta de migración para pasar de Media JS SDK a Web SDK, a la vez que incluye compatibilidad con las funcionalidades de Media JS existentes, como la administración de eventos de medios.

## Requisitos previos {#prerequisites}

Para utilizar el componente `streamingMedia` de Web SDK, debe cumplir los siguientes requisitos previos:

* Antes de poder enviar datos de medios de transmisión a Edge, primero complete los pasos en [Implementar los servicios de medios de transmisión de Adobe mediante Edge Network](/help/implementation/edge/implementation-edge.md).
* Asegúrese de que tiene acceso a Adobe Experience Platform o Adobe Analytics.
* Debe utilizar Web SDK versión 2.20.0 o posterior. Consulte la [descripción general de la instalación de Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/install/overview) para obtener información sobre cómo instalar la versión más reciente.
* Habilite la opción **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure)** para el conjunto de datos que está usando.
* Asegúrese de que el esquema utilizado por el conjunto de datos incluya los campos de esquema de recopilación de contenido.
* Configure los servicios de medios de streaming en la configuración de Web SDK, como se muestra en esta página, ya sea mediante la [extensión de etiquetas](#tag-extension) o a través de la [biblioteca de JavaScript](#library).

Siga los pasos descritos en esta página para migrar la implementación de los servicios de medios de streaming de Media JS a Web SDK.

### Paso 1: Instalar Experience Platform Web SDK

Consulte la [documentación específica](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/install/overview) para obtener información sobre cómo instalar Web SDK en sus propiedades web.

### Paso 2: Configuración del componente `streamingMedia` de Web SDK.

**Ejemplo**

El siguiente fragmento muestra cómo configurar la recopilación de medios en Media JS.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

En su lugar, debe configurar el componente `streamingMedia` en Web SDK, como se muestra a continuación.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Consulte la `streamingMedia`documentación[&#x200B; del componente &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) de Web SDK para obtener información detallada sobre cómo configurarlo.

### Paso 3: Obtención de la instancia de rastreador de medios al migrar desde Media JS SDK

Para los clientes que utilizan Media JS SDK, Web SDK proporciona una ruta de migración para pasar de Media JS SDK a Web SDK, a la vez que incluye compatibilidad con las funcionalidades de Media JS existentes, como la administración de eventos de medios.

[!DNL Web SDK] incluye un comando para recuperar un rastreador de Media Analytics. Puede utilizar este comando para crear una instancia de objeto y, a continuación, utilizar las mismas API que las proporcionadas por la [biblioteca Media JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), realizar un seguimiento de los eventos de medios.

Consulte la documentación de [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) para obtener información detallada sobre los métodos admitidos.

El siguiente fragmento muestra cómo recuperar la instancia de seguimiento de medios en Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

En su lugar, utilice el comando `getMediaAnalyticsTracker` en Web SDK para lograr el mismo resultado, como se muestra a continuación.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Todos los métodos de ayuda estarán disponibles en el objeto `Media`. Los métodos de seguimiento están disponibles en la instancia de seguimiento, como se muestra a continuación.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
