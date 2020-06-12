---
title: Configuración de Android
description: Configuración de la aplicación de Media SDK para la implementación en Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: ht
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: ht
source-wordcount: '427'
ht-degree: 100%

---


# Configuración de Android {#set-up-android}

>[!IMPORTANT]
>
>Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejará de ofrecer compatibilidad con el SDK de Media Analytics para iOS y Android.  Para obtener más información, consulte [Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics](/help/sdk-implement/end-of-support-faqs.md).


## Requisitos previos

* **Obtenga parámetros de configuración válidos para Media SDK**: Estos parámetros se pueden obtener de un representante de Adobe una vez creada la cuenta de Analytics.
* **Implemente ADBMobile para Android en su aplicación**: Para obtener más información sobre la documentación del SDK de Adobe Mobile, consulte [SDK de Android 4.x para las soluciones de Experience Cloud.](https://docs.adobe.com/content/help/es-ES/mobile-services/android/overview.html)

* **Proporcione las siguientes capacidades en su reproductor de contenidos**:
   * *Una API para suscribirse a eventos del reproductor*: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.
   * *Una API que proporciona información del reproductor*: Esta información incluye detalles como el nombre del medio y la posición del cabezal de reproducción.

## Implementación del SDK

1. Añada el Media SDK [descargado](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto.

   1. Descomprima el archivo zip de Android (por ejemplo, `MediaSDK-android-v2.*.zip`).
   1. Compruebe si el archivo `MediaSDK.jar` existe en el directorio `libs/`.

   1. Añada la biblioteca al proyecto.

      **IntelliJ IDEA:**

      1. Haga clic con el botón secundario en el proyecto desde el panel **[!UICONTROL Navegación del proyecto]**.
      1. Seleccione **[!UICONTROL Abrir configuración del módulo]**.
      1. En **[!UICONTROL Configuración del proyecto]**, seleccione **[!UICONTROL Bibliotecas]**.

      1. Haga clic en **[!UICONTROL +]** para agregar una biblioteca nueva.
      1. Seleccione **[!UICONTROL Java]** y busque el archivo `MediaSDK.jar`.

      1. Seleccione los módulos en los que va a utilizar la biblioteca móvil.
      1. Haga clic en **[!UICONTROL Aplicar]** y, a continuación, en **[!UICONTROL Aceptar]** para cerrar la ventana Configuración del módulo.
      **Eclipse:**

      1. En Eclipse IDE, haga clic con el botón secundario en el nombre del proyecto.
      1. Haga clic en **[!UICONTROL Ruta de compilación]** > **[!UICONTROL Agregar archivos externos]**.
      1. Seleccione `MediaSDK.jar`.
      1. Haga clic en **[!UICONTROL Abrir]**.
      1. Vuelva a hacer clic con el botón derecho en el proyecto y, a continuación, seleccione **[!UICONTROL Ruta de compilación]** > **[!UICONTROL Configurar ruta de compilación]**.
      1. Haga clic en las pestañas **[!UICONTROL Ordenar]** y **[!UICONTROL Exportar]**.

      1. Asegúrese de que el archivo `MediaSDK.jar` está seleccionado.


1. Importe la biblioteca.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Cree la instancia de `MediaHeartbeatConfig`.

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

1. Implemente la interfaz de `MediaHeartbeatDelegate`.

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

1. Cree la instancia de `MediaHeartbeat`.

   Utilice la instancia de `MediaHeartbeatConfig` y la instancia de `MediaHertbeatDelegate` para crear la instancia de `MediaHeartbeat`.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Asegúrese de que la instancia de `MediaHeartbeat` es accesible y *no se desasigna hasta el final de la sesión*. Esta instancia se utilizará para todos los eventos de seguimiento posteriores.

**Añadir permisos de aplicación**

La aplicación que utiliza Media SDK requiere los siguientes permisos para enviar datos en las llamadas de seguimiento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Para agregar estos permisos, agregue las siguientes líneas al archivo `AndroidManifest.xml` en el directorio del proyecto de la aplicación:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migración de la versión 1.x a 2.x en Android**

En las versiones 2.x, todos los métodos públicos se incluyen en la clase `com.adobe.primetime.va.simple.MediaHeartbeat` para facilitar el trabajo de los desarrolladores. Asimismo, todas las configuraciones están consolidadas en la clase `com.adobe.primetime.va.simple.MediaHeartbeatConfig`.

Para obtener información detallada sobre la migración de 1.x a 2.x, consulte [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
