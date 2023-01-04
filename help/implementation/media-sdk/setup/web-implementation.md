---
title: Configuración de una implementación web para Analytics para medios de streaming
description: Aprenda a implementar medios de transmisión de Adobe para aplicaciones web.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: d1e7a74a03c68e08987f03a295edc69989d9a4c6
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 68%

---

# Instalación de Analytics mediante JavaScript {#install-web-sdks}

La información de esta página describe cómo instalar el SDK independiente web y configurar JavaScript.

Como alternativa, puede utilizar la extensión de Adobe Medium Analytics para implementar Analytics, tal como se describe en [Implementar Analytics con la extensión Media Analytics](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Requisitos previos  {#prerequesites}

* **Obtener parámetros de configuración válidos**

   Estos parámetros se pueden obtener de un representante de Adobes una vez creada la cuenta de Analytics.

* **Implementación `AppMeasurement` y `Experience Cloud Identity Service` para JavaScript en la aplicación multimedia**

   Para obtener más información, consulte [Implementación de Analytics con JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=es) y [Implementación del servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html).

* **Incluya las siguientes API en su reproductor de medios**

   * *Una API para suscribirse a eventos del reproductor*: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.
   * *Una API que proporcione información del reproductor* : incluye información sobre medios, anuncios y capítulos que se están reproduciendo.

## Configuración de JavaScript 3.x {#set-up-javascript}

1. Añada la biblioteca [descargada](/help/getting-started/download-sdks.md) al proyecto. Cree referencias locales a las clases para mayor comodidad.

   1. Expanda el archivo `MediaSDK-js-v3*.zip` que descargó.
   1. Compruebe si el archivo `MediaSDK.js` existe en el directorio `libs`.

   1. Aloje el archivo `MediaSDK.js`.

      Este archivo JavaScript principal debe alojarse en un servidor web al que se pueda acceder desde todas las páginas del sitio. Necesita la ruta a estos archivos para el siguiente paso.

   1. Haga referencia a `MediaSDK.js` en todas las páginas del sitio.

      Incluya `MediaSDK` para JavaScript agregando la línea de código siguiente en la etiqueta `<head>` o `<body>` de cada página. Por ejemplo:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Para verificar rápidamente que la biblioteca se ha importado correctamente, compruebe que `ADB.Media` se ha exportado en el objeto Window.

      >[!NOTE]
      >
      >El SDK de JavaScript es compatible con las especificaciones del módulo AMD y CommonJS, y `MediaSDK.js` también se puede utilizar con módulos de carga compatibles.

1. Cree una instancia de `AppMeasurement` y configure `visitor`.

   La configuración del SDK de medios requiere una instancia de `AppMeasurement` con `visitor` configurado.

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. Configuración del SDK de medios

   El SDK de medios debe configurarse una vez por página web y la configuración se aplica a todas las instancias del rastreador creadas.

   >[!IMPORTANT]
   >
   > El SDK de medios (3.x) utiliza la API de recopilación de medios para el seguimiento de medios, que es diferente del extremo HB utilizado en los SDK 2.x. Póngase en contacto con su representante de Adobe para obtener más información.

   Este es un ejemplo de una inicialización de `MediaConfig`:

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. Cree la instancia de `MediaTracker`.

   Después de configurar el SDK de medios, se pueden crear instancias de rastreador para el seguimiento de contenido de medios mediante `getInstance` de API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Asegúrese de que la instancia de `tracker` es accesible y no se desasigna hasta el final de la sesión de contenido. Esta instancia se utilizará para el seguimiento de los siguientes eventos para esa sesión.

## Migrar de JavaScript 2.x a 3.x

Para obtener información detallada sobre la migración de 2.x a 3.x, consulte [Migración de 2.x a 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

Para ver el contenido heredado, consulte [Implementaciones heredadas](/help/legacy/media-sdk/setup/setup-overview.md)
