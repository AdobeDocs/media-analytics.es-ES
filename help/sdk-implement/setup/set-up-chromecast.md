---
seo-title: Configuración de Chromecast
title: Configuración de Chromecast
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
translation-type: tm+mt
source-git-commit: a3a81609046ab5e3c84fe4bf99c92c3dabc58247

---


# Configuración de Chromecast{#set-up-chromecast}

## Preguntas más frecuentes

_¿Debería utilizar el SDK de JavaScript de Chromecast o puedo usar el SDK de JavaScript estándar?_

La respuesta correcta es "Chromecast", por los siguientes motivos:
* Las bibliotecas AppMeasurement y VisitorAPI del SDK de JS estándar no están certificadas para funcionar con plataformas OTT. En el SDK de JS de Chromecast, la biblioteca Video Heartbeats Library (VHL), Analytics y VisitorAPI están incorporadas en el único SDK unificado y certificado para Chromecast.
* El SDK de Chromecast es mucho más ligero que el SDK de JS estándar. Esto es esencial para el hardware de nivel inferior utilizado por las plataformas OTT.

## Requisitos previos

* **Obtenga parámetros de configuración válidos para latidos**. Estos parámetros se pueden obtener de un representante de Adobe después de configurar la cuenta de análisis de medios.
* **Proporcione las siguientes capacidades en su reproductor de medios**:
   * *Una API para suscribirse a eventos del reproductor*: el Media SDK requiere que se invoquen varias API sencillas cuando se producen eventos en el reproductor.
   * *Una API que proporcione información del reproductor*: esta información incluye detalles como el nombre del contenido y la posición del cabezal de reproducción.

Adobe Mobile Services proporciona una nueva interfaz de usuario que aúna las capacidades de marketing móvil para aplicaciones móviles desde Adobe Experience Cloud. Inicialmente, el servicio Mobile ofrece una integración perfecta de las prestaciones de orientación y análisis de aplicaciones de las soluciones Adobe Analytics y Adobe Target. Para obtener más información, consulte la documentación de [Adobe Mobile Services.](https://marketing.adobe.com/resources/help/en_US/mobile/)

El SDK 2.x de Chromecast para las soluciones de Experience Cloud le permite medir aplicaciones Chromecast escritas en JavaScript, aprovechar y recopilar datos de audiencia mediante la gestión de público, y medir la intervención de vídeo a través de los latidos de vídeo.

## Implementación del SDK

1. Añada la biblioteca de Chromecast [descargada](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto.

   1. El archivo `AdobeMobileLibrary-Chromecast-[version]` zip consta de los siguientes componentes de software:

      * `adbmobile-chromecast.min.js`:

         Este archivo de biblioteca se incluirá en la carpeta de origen de la aplicación Chromecast.

      * `ADBMobileConfig` config

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
              "ssl": false, 
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
              "ssl": false, 
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
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

      Parámetros de configuración de ADBMobile para la clave de mediaHeartbeat:
   | Parámetro de configuración | Descripción     |
   | --- | --- |
   | `server` | Cadena que representa la URL del punto final de seguimiento en el servidor. |
   | `publisher` | Cadena que representa el identificador exclusivo del editor de contenido. |
   | `channel` | Cadena que representa el nombre del canal de distribución de contenido. |
   | `ssl` | Booleano que representa si SSL debe utilizarse para rastrear llamadas. |
   | `ovp` | Cadena que representa el nombre del proveedor del reproductor de vídeo. |
   | `sdkversion` | Cadena que representa la versión actual de la aplicación/SDK. |
   | `playerName` | Cadena que representa el nombre del reproductor. |


1. Configure el ID de visitante de Experience Cloud.

   El servicio de identificación de visitantes de Experience Cloud proporciona un ID de visitante universal en las soluciones de Experience Cloud. El servicio de medición de vídeos y otras integraciones de Experience Cloud requieren el servicio de ID del visitante.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   Una vez completada la configuración, se genera un ID de visitante de Experience Cloud que se incluye en todas las visitas. Otros ID de visitante, como `custom` y `automatically-generated`, se siguen enviando con cada visita.

   **Métodos de servicio de ID de visitantes de Experience Cloud**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | Método | Descripción |
   | --- | --- |
   | `getMarketingCloudID()` | Recupera el ID del visitante de Experience Cloud del servicio de ID del visitante.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Con el ID de visitantes de Experience Cloud puede configurar ID adicionales de clientes que se pueden asociar a cada visitante. La API de visitante acepta múltiples ID de cliente para el mismo visitante y un identificador de tipo de cliente para separar el ámbito de los distintos ID de cliente. Este método corresponde a `setCustomerIDs()` en la biblioteca de JavaScript.  For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

