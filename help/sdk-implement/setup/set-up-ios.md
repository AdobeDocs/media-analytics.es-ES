---
title: Configuración de iOS
description: Configuración de la aplicación de Media SDK para la implementación en iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: be82be2eb58f89344f2125288599fef461db441e

---


# Configuración de iOS {#set-up-ios}

>[!IMPORTANT]
>
>A partir de octubre de 2020, Adobe dejará de ser compatible con los SDK para móviles de la versión 4 y los SDK independientes de Media Analytics para iOS. Puede seguir descargando y utilizando los SDK de la versión 4, pero el servicio de atención al cliente y el acceso a los foros finalizarán. Debe migrar a los SDK de Adobe Experience Platform (AEP) para iOS. El SDK de AEP Mobile (anteriormente denominado v5) solo admitirá las funciones y funciones de Adobe Experience Cloud. Para obtener más información sobre este cambio, consulte las preguntas más frecuentes sobre el fin de la compatibilidad con los SDK móviles de la [versión 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq). Le recomendamos que migre al nuevo SDK de AEP Mobile.
Después de migrar al SDK de AEP Mobile, debe implementar la extensión de inicio de Analytics y la extensión de inicio de Media Analytics para habilitar Adobe Analytics para audio y vídeo. Para obtener más información sobre la migración al nuevo SDK de AEP Mobile, consulte [Migración del SDK de medios independiente a Adobe Launch ](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)


## Requisitos previos

* **Obtenga parámetros de configuración válidos para Media SDK**: Estos parámetros se pueden obtener de un representante de Adobe una vez creada la cuenta de Analytics.
* **Implemente ADBMobile para iOS en su aplicación**: Para obtener más información sobre la documentación del SDK de Adobe Mobile, consulte [SDK 4.x de iOS para las soluciones de Experience Cloud.](https://docs.adobe.com/content/help/es-ES/mobile-services/ios/overview.html)

   >[!IMPORTANT]
   >
   >A partir de iOS 9, Apple introdujo una función denominada App Transport Security (ATS). Esta función tiene como objetivo mejorar la seguridad de la red asegurándose de que las aplicaciones utilicen únicamente los protocolos y los cifrados estándar del sector. Esta función está habilitada de forma predeterminada, pero tiene opciones de configuración que le permiten trabajar con ATS. Para obtener más información sobre ATS, consulte [Seguridad del transporte de aplicaciones.](https://docs.adobe.com/content/help/en/mobile-services/ios/config-ios/app-transport-security.html)

* **Proporcione las siguientes capacidades en su reproductor de contenidos**:

   * _Una API para suscribirse a eventos del reproductor_: El SDK de medios requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.
   * _Una API que proporciona información del reproductor_: Esta información incluye detalles como el nombre del medio y la posición del cabezal de reproducción.

## Implementación del SDK

1. Añada el Media SDK [descargado](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto.

   1. Compruebe que los siguientes componentes de software existan en el directorio `libs`:

      * `ADBMediaHeartbeat.h`: archivo del encabezado Objective-C que se utiliza para las API de seguimiento de Heartbeat para iOS.
      * `ADBMediaHeartbeatConfig.h`: archivo del encabezado Objective-C que se utiliza para la configuración del SDK.
      * `MediaSDK.a`: binario multiarquitectura habilitado para código de bits que contiene las compilaciones de biblioteca para los simuladores (i386 y x86_64) y dispositivos iOS (armv7, armv7s, arm64).

         Este binario se debe vincular cuando el destino se dirija a una aplicación iOS.

      * `MediaSDK_TV.a`: binario multiarquitectura habilitado para código de bits que contiene las compilaciones de biblioteca para el simulador (x86_64) y los dispositivos Apple TV (arm64) nuevos.

         Este binario se debe vincular cuando el destino se dirija a una aplicación Apple TV (tvOS).
   1. Añada la biblioteca al proyecto:

      1. Inicie el IDE de Xcode y abra la aplicación.
      1. In **[!UICONTROL Project Navigator]**, drag the `libs` directory and drop it under your project.

      1. Asegúrese de que la casilla de verificación **[!UICONTROL Copy Items if Needed]** está seleccionada, la casilla **[!UICONTROL Create Groups]** está seleccionada y ninguna de las casillas de verificación de **[!UICONTROL Add to Target]** .

         ![](assets/choose-options_ios.png)

      1. Haga clic en **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. Link the required frameworks and libraries in the **[!UICONTROL Linked Frameworks]** and **[!UICONTROL Libraries]** section on the **[!UICONTROL General]** tab.

         **Destinos de aplicaciones iOS:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Apple TV (tvOS) Targets:**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Confirme que la aplicación se compila sin errores.




1. Importe la biblioteca.

   ```
   #import "ADBMediaHeartbeat.h"
   #import "ADBMediaHeartbeatConfig.h"
   ```

1. Cree una instancia de `ADBMediaHeartbeatConfig`.

   Esta sección le ayudará a entender los parámetros de configuración de `MediaHeartbeat` y a seleccionar valores de configuración correctos en la instancia de `MediaHeartbeat` para conseguir un seguimiento preciso.

   Este es un ejemplo de una inicialización de `ADBMediaHeartbeatConfig`:

   ```
   // Media Heartbeat Initialization
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>;
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName     = <SAMPLE_PLAYER_NAME>;
   config.ssl            = <YES/NO>;
   config.debugLogging   = <YES/NO>;
   ```

1. Implemente el protocolo de `ADBMediaHeartbeatDelegate`.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate>
   
   @end
   
   @implementation VideoAnalyticsProvider
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values.
   - (ADBMediaObject *)getQoSObject {
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>];
   }
   
   // Return the current video player playhead position.
   // Replace <currentPlaybackTime> with the video player current playback time
   - (NSTimeInterval)getCurrentPlaybackTime {
       return <currentPlaybackTime>;
   }
   
   @end
   ```

1. Utilice `ADBMediaHeartBeatConfig` y `ADBMediaHeartBeatDelegate` para crear la instancia `ADBMediaHeartbeat`.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Asegúrese de que la instancia de `ADBMediaHeartbeat` es accesible y *no se desasigna hasta el final de la sesión*. Esta instancia se utilizará para todos los eventos de seguimiento posteriores.

## Migración de la versión 1.x a 2.x en iOS {#migrate-to-two-x}

En la versión 2.x, todos los métodos públicos se incluyen en la clase `ADBMediaHeartbeat` para facilitar el trabajo de los desarrolladores. Todas las configuraciones se incluyen en la clase `ADBMediaHeartbeatConfig`.

Para obtener información detallada sobre la migración de 1.x a 2.x, consulte [Migración de VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configurar una aplicación nativa para tvOS

Con el lanzamiento de Apple TV, ahora puede crear aplicaciones para ejecutarlas en el entorno nativo de tvOS. Puede crear una aplicación puramente nativa con cualquiera de los distintos marcos disponibles en iOS o puede crear la aplicación con plantillas XML y JavaScript. A partir de la versión 2.0 de MediaSDK, está disponible la compatibilidad con tvOS. Para obtener más información sobre tvOS, consulte el [Sitio para desarrolladores de tvOS.](https://developer.apple.com/tvos/)

Realice los siguientes pasos en su proyecto de Xcode. Esta guía se escribe suponiendo que el proyecto tiene un destinatario que es una aplicación de Apple TV dirigida a tvOS:

1. Arrastre el archivo de biblioteca `VideoHeartbeat_TV.a` a la carpeta `lib` de su proyecto.

1. In the **[!UICONTROL Build Phases]** tab of your tvOS app’s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
