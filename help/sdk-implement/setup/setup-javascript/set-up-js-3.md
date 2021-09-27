---
title: Configuración de Media SDK mediante JavaScript 3.x
description: Siga estos pasos para configurar la aplicación de Media SDK en JavaScript 3.x.
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e10f705e135cc6b9c630059596994d12fc787866
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 92%

---

# Configuración de JavaScript 3.x{#set-up-javascript}

## Requisitos previos

* **Obtenga parámetros de configuración válidos**: Estos parámetros se pueden obtener de un representante de Adobe una vez creada la cuenta de Analytics.
* **Implementación de `AppMeasurement` y `Experience Cloud Identity Service` para JavaScript en la aplicación de medios**
Para obtener más información, consulte [Implementación de Analytics con JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=es) e [Implementación del servicio de identidad de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html).

* **Proporcione las siguientes capacidades en su reproductor de contenidos**:

   * *Una API para suscribirse a eventos del reproductor*: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.
   * *Una API que proporciona información sobre el reproductor*: incluye información sobre medios, anuncios y capítulos que se están reproduciendo.

1. Añada la biblioteca [descargada](/help/sdk-implement/download-sdks.md#download-3x-sdks) al proyecto. Cree referencias locales a las clases para mayor comodidad.

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
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
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
