---
seo-title: Configuración de Roku
title: Configuración de Roku
uuid: 904dfda0-4782-41da-b4ab-212e81156633
translation-type: tm+mt
source-git-commit: a3a81609046ab5e3c84fe4bf99c92c3dabc58247

---


# Configuración de Roku{#set-up-roku}

## Requisitos previos

* **Obtenga parámetros de configuración válidos para latidos**. Estos parámetros se pueden obtener de un representante de Adobe después de configurar la cuenta de análisis de medios.
* **Proporcione las siguientes capacidades en su reproductor de medios**:
   * _Una API para suscribirse a eventos del reproductor_: el Media SDK requiere que se invoquen varias API sencillas cuando se producen eventos en el reproductor.
   * _Una API que proporcione información del reproductor_: esta información incluye detalles como el nombre del contenido y la posición del cabezal de reproducción.

Adobe Mobile Services proporciona una nueva interfaz de usuario que aúna las capacidades de marketing móvil para aplicaciones móviles desde Adobe Experience Cloud. Inicialmente, el servicio Mobile ofrece una integración perfecta de las prestaciones de orientación y análisis de aplicaciones de las soluciones Adobe Analytics y Adobe Target. 

Para obtener más información, consulte la documentación de [Adobe Mobile Services.](https://marketing.adobe.com/resources/help/en_US/mobile/)

El SDK 2.x de Roku para las soluciones de Experience Cloud le permite medir aplicaciones Roku escritas en BrightScript, aprovechar y recopilar datos de audiencia mediante la gestión de público y medir la interacción de vídeo a través de latidos de vídeo.

## Implementación del SDK

1. Añada la biblioteca de Roku [descargada](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto.

   1. The `AdobeMobileLibrary-2.*-Roku.zip` download file consists of the following software components:

      * `adbmobile.brs`: Este archivo de biblioteca se incluirá en la carpeta de origen de la aplicación Roku.

      * `ADBMobileConfig.json`: Este archivo de configuración del SDK se personaliza en función de la aplicación.
   1. Añada el archivo de biblioteca y el archivo de configuración JSON al origen del proyecto.

      El JSON utilizado para configurar Adobe Mobile tiene una clave exclusiva para los latidos multimedia denominada `mediaHeartbeat`. Es allí donde actúan los parámetros de configuración de los latidos multimedia.

      >[!TIP]
      >
      >A sample `ADBMobileConfig` JSON file is provided with the package. Póngase en contacto con los representantes de Adobe para la configuración.

      Por ejemplo:

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
          "offlineEnabled":false, 
          "lifecycleTimeout":30, 
          "batchLimit":50, 
          "privacyDefault":"optedin", 
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{ 
        "clientCode":"", 
        "timeout":5
      },
      "audienceManager":{ 
        "server":""
      },
      "acquisition":{ 
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{ 
         "server":"example.com", 
         "publisher":"sample-publisher", 
         "channel":"sample-channel", 
         "ssl":false,
         "ovp":"sample-ovp", 
         "sdkVersion":"sample-sdk", 
         "playerName":"roku"
         }    
      }
      ```

      | Parámetro de configuración | Descripción     |
      | --- | --- |
      | `server` | Cadena que representa la URL del punto final de seguimiento en el servidor. |
      | `publisher` | Cadena que representa el identificador exclusivo del editor de contenido. |
      | `channel` | Cadena que representa el nombre del canal de distribución de contenido. |
      | `ssl` | Booleano que representa si SSL debe utilizarse para rastrear llamadas. |
      | `ovp` | Cadena que representa el nombre del proveedor del reproductor de vídeo. |
      | `sdkversion` | Cadena que representa la versión actual de la aplicación/SDK. |
      | `playerName` | Cadena que representa el nombre del reproductor. |

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.


1. Configure el ID de visitante de Experience Cloud.

   El servicio de identificación de visitantes de Experience Cloud proporciona un ID de visitante universal en las soluciones de Experience Cloud. El servicio de medición de vídeos y otras integraciones de Experience Cloud requieren el servicio de ID del visitante.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```
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

   |  Método   | Descripción |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera el ID del visitante de Experience Cloud del servicio de ID del visitante.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Con el ID de visitantes de Experience Cloud puede configurar ID adicionales de clientes que se pueden asociar a cada visitante. La API de visitante acepta múltiples ID de cliente para el mismo visitante y un identificador de tipo de cliente para separar el ámbito de los distintos ID de cliente. Este método corresponde a `setCustomerIDs`. For example: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Se utiliza para establecer el ID de Roku para publicidad (RIDA) en el SDK. Por ejemplo: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` Obtenga <br/><br/><br/>el Roku ID para publicidad (RIDA) mediante la API de Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) . |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->
