---
seo-title: Configuración de iOS
title: Configuración de iOS
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: a3a81609046ab5e3c84fe4bf99c92c3dabc58247

---


# Configuración de iOS{#set-up-ios}

## Requisitos previos

* **Obtenga parámetros de configuración válidos para el SDK** de mediosEstos parámetros se pueden obtener de un representante de Adobe después de configurar la cuenta de análisis.
* **Implementación de ADBMobile para iOS en la aplicación** Para obtener más información sobre la documentación del SDK de Adobe Mobile, consulte SDK 4.x de [iOS para soluciones de Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >A partir de iOS 9, Apple introdujo una función denominada App Transport Security (ATS). Esta función es útil para mejorar la seguridad de la red al garantizar que las aplicaciones solo utilizan protocolos y codificadores estándar del sector. Esta función está activada de forma predeterminada, pero tiene opciones de configuración que le permiten trabajar con ATS de diferentes formas. Para obtener más información sobre ATS, consulte Seguridad del transporte de [aplicaciones.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **Proporcione las siguientes capacidades en su reproductor de medios**:

   * _Una API para suscribirse a eventos del reproductor_: el Media SDK requiere que se invoquen varias API sencillas cuando se producen eventos en el reproductor.
   * _Una API que proporcione información del reproductor_: esta información incluye detalles como el nombre del contenido y la posición del cabezal de reproducción.

## Implementación del SDK

1. Añada el Media SDK [descargado](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto.

   1. Compruebe que los siguientes componentes de software existan en el directorio `libs`:

      * `ADBMediaHeartbeat.h`: archivo del encabezado Objective-C que se utiliza para las API de seguimiento de Heartbeat para iOS.
      * `ADBMediaHeartbeatConfig.h`: archivo del encabezado Objective-C que se utiliza para la configuración del SDK.
      * `MediaSDK.a`: binario multiarquitectura habilitado para código de bits que contiene las compilaciones de biblioteca para los simuladores (i386 y x86_64) y dispositivos iOS (armv7, armv7s, arm_64).

         Este binario se debe vincular cuando el destino se dirija a una aplicación iOS.

      * `MediaSDK_TV.a`: binario multiarquitectura habilitado para código de bits que contiene las compilaciones de biblioteca para el simulador (x86_64) y los dispositivos Apple TV (arm_64) nuevos.

         Este binario se debe vincular cuando el destino se dirija a una aplicación Apple TV (tvOS).
   1. Añada la biblioteca al proyecto:

      1. Inicie el IDE de Xcode y abra la aplicación.
      1. En **[!UICONTROL Navegador de proyectos]**, arrastre el directorio `libs` y suéltelo debajo de su proyecto.

      1. Asegúrese de que la casilla de verificación **[!UICONTROL Copiar elementos si es necesario]** esté activada, que la opción **[!UICONTROL Crear grupos]esté seleccionada y que ninguna de las casillas de verificación de** Agregar a destino] esté activada.**[!UICONTROL **

         ![](assets/choose-options_ios.png)

      1. Haga clic en **[!UICONTROL Finalizar]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. Vincule los marcos y bibliotecas requeridos de la sección **[!UICONTROL Marcos vinculados]** y **[!UICONTROL Bibliotecas]** en la pestaña **[!UICONTROL General]**.

         **Destinos de aplicaciones iOS:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Destinos de Apple TV (tvOS):**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Compruebe que la aplicación se compile sin errores.




1. Importe la biblioteca.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a `ADBMediaHeartbeatConfig` instance.

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

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

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

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Esta instancia se utilizará para todos los eventos de seguimiento posteriores.

## Migración de la versión 1.x a 2.x en iOS {#migrate-to-two-x}

En la versión 2.x, todos los métodos públicos se incluyen en la clase `ADBMediaHeartbeat` para facilitar el trabajo de los desarrolladores. Todas las configuraciones se incluyen en la clase `ADBMediaHeartbeatConfig`.

Para obtener información detallada sobre la migración de 1.x a 2.x, consulte [Migración de VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configurar una aplicación nativa para tvOS

Ahora, gracias al lanzamiento del nuevo Apple TV, puede crear aplicaciones para utilizarlas en el entorno nativo de tvOS. Puede crear una aplicación original con varios marcos de trabajo disponibles en iOS o crear la aplicación utilizando plantillas XML y JavaScript. MediaSDK es compatible con tvOS a partir de la versión 2.0. Para obtener más información sobre tvOS, consulte el [Sitio para desarrolladores de tvOS.](https://developer.apple.com/tvos/)

Complete los siguientes pasos en su proyecto Xcode. En esta guía se presupone que el proyecto está dirigido a una aplicación de Apple TV para tvOS:

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. En la pestaña **[!UICONTROL Fases de compilación]** del destino de su aplicación de tvOS, expanda la sección **[!UICONTROL Vincular binario con bibliotecas]** y añada las bibliotecas siguientes:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

