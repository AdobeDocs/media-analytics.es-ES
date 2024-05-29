---
title: Envío de datos web a Edge con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos de medios de streaming de Adobe a Experience Platform Edge con el SDK web de Adobe Experience Platform.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ad40260d29bd5b739184cb551f084565d05e65a7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Envío de datos web a Edge con el SDK web de Adobe Experience Platform

A partir de la versión 2.20.0, la variable `streamingMedia` componente de Adobe Experience Platform [SDK web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) permite recopilar datos relacionados con las sesiones de contenido del sitio web. Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados.

Una vez recopilados los datos, puede enviarlos a Adobe Experience Platform o Adobe Analytics para generar informes. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

Para los clientes que utilizan el SDK de Media JS, el SDK web proporciona una ruta de migración para pasar de Media JS SDK a SDK web, a la vez que incluye compatibilidad con las funcionalidades de Media JS existentes, como la administración de eventos de medios.

## Requisitos previos {#prerequisites}

Para usar la variable `streamingMedia` del SDK web, debe cumplir los siguientes requisitos previos:

* Para poder enviar datos de Media Analytics a Edge, primero complete los pasos en [Instalación de Media Analytics con Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Asegúrese de que tiene acceso a Adobe Experience Platform o Adobe Analytics.
* Debe utilizar la versión 2.20.0 o posterior del SDK web. Consulte la [Información general sobre la instalación del SDK web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) para obtener información sobre cómo instalar la versión más reciente.
* Habilite la **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** para la secuencia de datos que está utilizando.
* Asegúrese de que el esquema utilizado por el conjunto de datos incluya los campos de esquema de recopilación de contenido.
* Configure la función Streaming Media en la configuración del SDK web, como se muestra en esta página, a través del [extensión de etiqueta](#tag-extension) o a través de [Biblioteca JavaScript](#library).

Siga los pasos descritos en esta página para migrar la implementación de Adobe Analytics para mídia de streaming de Media JS a SDK web.

### Paso 1: Instalación del SDK web de Experience Platform

Consulte la [documentación dedicada](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) para obtener información sobre cómo instalar el SDK web en las propiedades web.

### Paso 2: Configuración del SDK web `streamingMedia` componente.

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

En su lugar, debe configurar la variable `streamingMedia` en el SDK web como se muestra a continuación.

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

Consulte el SDK web `streamingMedia` componente [documentación](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) para obtener información detallada sobre cómo configurarla.

### Paso 3: Obtención de la instancia de rastreador de medios al migrar desde el SDK de Media JS

Para los clientes que utilizan el SDK de Media JS, el SDK web proporciona una ruta de migración para pasar de Media JS SDK a SDK web, a la vez que incluye compatibilidad con las funcionalidades de Media JS existentes, como la administración de eventos de medios.

[!DNL Web SDK] incluye un comando para recuperar un rastreador de Media Analytics. Puede utilizar este comando para crear una instancia de objeto y, a continuación, utilizando las mismas API que las proporcionadas por el [Biblioteca de Media JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), rastree eventos de medios.

Consulte la [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) para obtener información detallada sobre los métodos admitidos.

El siguiente fragmento muestra cómo recuperar la instancia de seguimiento de medios en Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

En su lugar, utilice el `getMediaAnalyticsTracker` en el SDK web para lograr el mismo resultado, como se muestra a continuación.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Todos los métodos de ayuda estarán disponibles en la `Media` objeto. Los métodos de seguimiento están disponibles en la instancia de seguimiento, como se muestra a continuación.

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
