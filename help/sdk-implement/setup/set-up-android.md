---
seo-title: Configuración de Android
title: Configuración de Android
uuid: 3 ffe 3276-a 104-4182-9220-038729 e 9 f 3 d 5
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Configuración de Android{#set-up-android}

## Requisitos previos

* **Obtenga parámetros de configuración válidos para el SDK**
de medios Estos parámetros pueden obtenerse de un representante de Adobe después de configurar su cuenta de Analytics.
* **Implementar adbmobile para Android en su aplicación**
Para obtener más información sobre la documentación del SDK de Adobe Mobile, consulte [SDK 4. x de Android para Soluciones de Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **Proporcione las siguientes capacidades en su reproductor de medios**:
   * *Una API para suscribirse a eventos del reproductor*: el Media SDK requiere que se invoquen varias API sencillas cuando se producen eventos en el reproductor.
   * *Una API que proporcione información del reproductor*: esta información incluye detalles como el nombre del contenido y la posición del cabezal de reproducción.

## Implementación del SDK

1. Añada el Media SDK [descargado](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) al proyecto.

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. Añada la biblioteca al proyecto.

      **IntelliJ IDEA:**

      1. Haga clic con el botón secundario en el proyecto desde el panel **[!UICONTROL Navegación del proyecto]**.
      1. Seleccione **[!UICONTROL Abrir configuración del módulo]**.
      1. En **[!UICONTROL Configuración del proyecto]**, seleccione **[!UICONTROL Bibliotecas]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Seleccione **[!UICONTROL Java]** y busque el archivo `MediaSDK.jar`.

      1. Seleccione los módulos en los que va a utilizar la biblioteca móvil.
      1. Haga clic en **[!UICONTROL Aplicar]** y, a continuación, en **[!UICONTROL Aceptar]** para cerrar la ventana Configuración del módulo.
      **Eclipse:**

      1. En Eclipse IDE, haga clic con el botón secundario en el nombre del proyecto.
      1. Click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. Select `MediaSDK.jar`.
      1. Haga clic en **[!UICONTROL Abrir]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. Haga clic en las pestañas **[!UICONTROL Ordenar]** y **[!UICONTROL Exportar]**.

      1. Asegúrese de que el archivo `MediaSDK.jar` está seleccionado.


1. Importe la biblioteca.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

   Este es un ejemplo de una inicialización de `MediaHeartbeatConfig`:

   ```java
   // Media Heartbeat Initialization 
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_; 
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName = <SAMPLE_PLAYER_NAME>; 
   config.ssl = <true/false>; 
   config.debugLogging = <true/false>; 
   ```

1. Implement the `MediaHeartbeatDelegate` interface.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override 
   public MediaObject getQoSObject() { 
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>); 
   } 
   
   //Replace <currentPlaybackTime> with the video player current playback time 
   @Override 
   public Double getCurrentPlaybackTime() { 
       return <currentPlaybackTime>; 
   }
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Esta instancia se utilizará para todos los eventos de seguimiento posteriores.

**Adición de permisos de aplicación**

La aplicación que utiliza el Media SDK requiere los permisos siguientes para enviar datos en llamadas de seguimiento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Para agregar estos permisos, agregue las siguientes líneas al archivo `AndroidManifest.xml` en el directorio del proyecto de la aplicación:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migración de la versión 1.x a 2.x en Android**

En las versiones 2.x, todos los métodos públicos se incluyen en la clase `com.adobe.primetime.va.simple.MediaHeartbeat` para facilitar el trabajo de los desarrolladores. Asimismo, todas las configuraciones están consolidadas en la clase `com.adobe.primetime.va.simple.MediaHeartbeatConfig`. 

For detailed information about migrating from 1.x to 2.x, see [mig-1x-2x-overview.md.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
