---
title: Configuración de JavaScript para medios de streaming
description: Instale y configure Media SDK for JavaScript (3.x) para implementaciones de medios de streaming solo de Analytics.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%

---

# Configuración de JavaScript para medios de streaming

Media SDK para JavaScript (3.x) envía datos de medios de streaming directamente a Adobe Analytics. Esta página cubre la instalación manual de JavaScript. Para implementar SDK mediante etiquetas en su lugar, consulte [Configurar la extensión de etiquetas de Media Analytics](javascript-tags.md). Para nuevas implementaciones, considere la posibilidad de usar [Web SDK](/help/implementation/edge/web-sdk.md) para enviar datos a Adobe Analytics a través de una secuencia de datos de Edge Network.

* **Requisitos previos**:
   * Complete la [descripción general de la implementación solo de Analytics](overview.md).
   * Implemente [AppMeasurement](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview?lang=es) y el [servicio de ID de visitante](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement).
   * [Descargar Media SDK para JavaScript](/help/getting-started/download-sdks.md).

## Instalación y configuración de SDK

1. Aloje `MediaSDK.js` (del directorio `libs` descargado) en un servidor web accesible para todas las páginas y haga referencia a él en cada página:

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. Configure Media SDK una vez por página, pasando la instancia `appMeasurement` que configuró como requisito previo:

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >La variable `mediaConfig.trackingServer` es su **servidor de recopilación de medios** (por ejemplo, `[namespace].hb-api.omtrdc.net`). Este servidor de recopilación es distinto del servidor de seguimiento de Analytics configurado en la instancia de AppMeasurement.

1. Crear una instancia de seguimiento con `getInstance`. Mantenga la instancia accesible para toda la sesión de medios:

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## Seguimiento de eventos de medios

Con el rastreador creado, rastree cada evento de medios mediante su método de rastreador. Consulte la pestaña **Media SDK JS 3.x** en cada página de [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Referencia de la API de Media SDK para JavaScript 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [Migrar de JS SDK 2.x a 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [Configurar la extensión de etiquetas de Media Analytics](javascript-tags.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
