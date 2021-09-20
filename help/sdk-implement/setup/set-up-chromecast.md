---
title: Configuración del SDK de medios para Chromecast
description: Siga estos pasos para configurar la aplicación de Media SDK en Chromecast.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 270dc48152dd77d7ceff8ce1ea9fbead0d1ce9be
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 95%

---

# Configuración de Chromecast{#set-up-chromecast}

## Preguntas más frecuentes

_¿Debería utilizar el SDK de JavaScript de Chromecast o puedo usar el SDK de JavaScript estándar?_

La respuesta correcta es “Chromecast”, por los siguientes motivos:
* Las bibliotecas de AppMeasurement y VisitorAPI del SDK de JS estándar no están certificadas para funcionar en plataformas OTT. En el SDK de JS de Chromecast, la biblioteca de Video Heartbeats (VHL), Analytics y VisitorAPI están integradas en el SDK único, unificado y certificado para Chromecast.
* El SDK de Chromecast es mucho más ligero que el SDK de JS estándar. Esto es esencial para el hardware de gama baja que utilizan las plataformas OTT.

## Requisitos previos

* **Obtenga parámetros de configuración válidos para Heartbeat**: Estos parámetros se pueden obtener de un representante de Adobe una vez creada la cuenta de Media Analytics.
* **Proporcione las siguientes capacidades en su reproductor de contenidos**:
   * *Una API para suscribirse a eventos del reproductor*: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.
   * *Una API que proporciona información del reproductor*: Esta información incluye detalles como el nombre del medio y la posición del cabezal de reproducción.

Adobe Mobile Services proporciona una nueva interfaz de usuario que aúna las capacidades de marketing móvil para aplicaciones móviles desde Adobe Experience Cloud. Inicialmente, el servicio Mobile ofrece una integración perfecta de las prestaciones de orientación y análisis de aplicaciones de las soluciones Adobe Analytics y Adobe Target. Para obtener más información, consulte la [documentación de Adobe Mobile Services.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=es)

El SDK 2.x de Chromecast para las soluciones de Experience Cloud le permite medir aplicaciones Chromecast escritas en JavaScript, aprovechar y recopilar datos de audiencia mediante la gestión de público, y medir la intervención de vídeo a través de los latidos de vídeo.

## Implementación del SDK

1. Añada la biblioteca de Chromecast [descargada](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto.

   1. El archivo `AdobeMobileLibrary-Chromecast-[version]` zip consta de los siguientes componentes de software:

      * `adbmobile-chromecast.min.js`:

         Este archivo de biblioteca se incluirá en la carpeta de origen de la aplicación Chromecast.

      * Configuración `ADBMobileConfig`

         Este archivo de configuración del SDK se personaliza en función de la aplicación. Con el SDK se proporciona una implementación de muestra de `ADBMobileConfig` (en `samples/`). Consulte con un representante de Adobe la configuración adecuada.
   1. Añada el archivo de biblioteca al archivo `index.html` y cree la variable global `ADBMobileConfig` como se indica a continuación (la variable global utilizada para configurar Adobe Mobile for Heartbeats tiene una clave exclusiva denominada `mediaHeartbeat`):

      ```js
      <script>
          var ADBMobileConfig = {
            "marketingCloud": {
              "org": "972C898555E9F7BC7F000101@AdobeOrg"
            },
            "target": {
              "clientCode": "",
              "timeout": 5
            },
            "audienceManager": {
              "server": "obumobile5.demdex.net"
            },
            "analytics": {
              "rsids": "mobile5vhl.sample.player",
              "server": "obumobile5.sc.omtrdc.net",
              "ssl": true,
              "offlineEnabled": false,
              "charset": "UTF-8",
              "lifecycleTimeout": 300,
              "privacyDefault": "optedin",
              "batchLimit": 0,
              "timezone": "MDT",
              "timezoneOffset": -360,
              "referrerTimeout": 0,
              "poi": []
            },
            "mediaHeartbeat": {
              "server": "obumobile5.hb.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
              "ovp": "chromecast-player",
              "sdkVersion": "chromecast-sdk",
              "playerName": "Chromecast"
            }
          };
        </script>
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >Si `mediaHeartbeat` se configura incorrectamente, el módulo multimedia (VHL) entrará en un estado de error y dejará de enviar llamadas de seguimiento.

      Parámetros de configuración de ADBMobile para la clave de mediaHeartbeat:
   | Parámetro de configuración | Descripción     |
   | --- | --- |
   | `server` | Cadena que representa la URL del punto final de seguimiento en el servidor. |
   | `publisher` | Cadena que representa el identificador único del editor de contenido. |
   | `channel` | Cadena que representa el nombre del canal de distribución de contenido. |
   | `ssl` | Booleano que representa si SSL debe utilizarse para rastrear llamadas. |
   | `ovp` | Cadena que representa el nombre del proveedor del reproductor de vídeo. |
   | `sdkversion` | Cadena que representa la versión actual de la aplicación/SDK. |
   | `playerName` | Cadena que representa el nombre del reproductor. |


1. Configure el ID de visitante de Experience Cloud.

   El servicio de ID de visitante de Experience Cloud ofrece un ID de visitante universal para las soluciones de Experience Cloud. Video Heartbeat y otras integraciones de Experience Cloud requieren el servicio de ID de Visitante.

   Verifique que su configuración de `ADBMobileConfig` contenga su ID de empresa de `marketingCloud`.

   ```js
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Los ID de empresa de Experience Cloud identifican exclusivamente cada empresa de los clientes en Adobe Experience Cloud y aparecen similares al siguiente valor: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Asegúrese de incluir `@AdobeOrg`.

   Una vez completada la configuración, se genera un ID de visitante de Experience Cloud que se incluye en todas las visitas. Otros ID de visitante, como `custom` y `automatically-generated`, se siguen enviando con cada visita.

   **Métodos de servicio de ID de visitantes de Experience Cloud**

   >[!TIP]
   >
   >Los métodos de ID de los visitantes de Experience Cloud cuentan con el prefijo `visitor`.

   | Método | Descripción |
   | --- | --- |
   | `getMarketingCloudID()` | Recupera el ID del visitante de Experience Cloud del servicio de ID del visitante.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Con el ID de Visitante de Experience Cloud, puede establecer ID de cliente adicionales que se pueden asociar con cada visitante. La API de visitante acepta varios ID de cliente para el mismo visitante y un identificador de tipo de cliente para separar el ámbito de los distintos ID de cliente. Este método corresponde a `setCustomerIDs()` en la biblioteca de JavaScript.  Por ejemplo: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. Para realizar el seguimiento de contenidos, implemente el protocolo MediaDelegate

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
