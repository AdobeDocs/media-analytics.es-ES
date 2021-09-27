---
title: Cómo configurar el Media SDK para Roku
description: Siga estos pasos para configurar la aplicación de Media SDK en Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e10f705e135cc6b9c630059596994d12fc787866
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 79%

---

# Configuración de Roku{#set-up-roku}

## Requisitos previos

* **Obtenga parámetros de configuración válidos para Heartbeat**: Estos parámetros se pueden obtener de un representante de Adobe una vez creada la cuenta de Media Analytics.
* **Proporcione las siguientes capacidades en su reproductor de contenidos**:
   * _Una API para suscribirse a eventos del reproductor_: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.
   * _Una API que proporciona información del reproductor_: Esta información incluye detalles como el nombre del medio y la posición del cabezal de reproducción.

Adobe Mobile Services proporciona una nueva interfaz de usuario que aúna las capacidades de marketing móvil para aplicaciones móviles desde Adobe Experience Cloud. Inicialmente, el servicio Mobile ofrece una integración perfecta de las prestaciones de orientación y análisis de aplicaciones de las soluciones Adobe Analytics y Adobe Target.

Para obtener más información, consulte la [documentación de Adobe Mobile Services.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=es)

El SDK 2.x de Roku para las soluciones de Experience Cloud le permite medir aplicaciones Roku escritas en BrightScript, aprovechar y recopilar datos de audiencia mediante la gestión de público y medir la interacción de vídeo a través de latidos de vídeo.

## Implementación del SDK

1. Añada la biblioteca de Roku [descargada](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto.

   1. El archivo de descarga `AdobeMobileLibrary-2.*-Roku.zip` consta de los siguientes componentes de software:

      * `adbmobile.brs`: Este archivo de biblioteca se incluirá en la carpeta de origen de la aplicación Roku.

      * `ADBMobileConfig.json`: Este archivo de configuración del SDK se personaliza en función de la aplicación.
   1. Añada el archivo de biblioteca y el archivo de configuración JSON al origen del proyecto.

      El JSON utilizado para configurar Adobe Mobile tiene una clave exclusiva para los latidos multimedia denominada `mediaHeartbeat`. Es allí donde actúan los parámetros de configuración de los latidos multimedia.

      >[!TIP]
      >
      >Se suministra un archivo JSON `ADBMobileConfig` de muestra con el paquete. Contacte con sus representantes de Adobe para conocer la configuración.

      Por ejemplo:

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
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
         "ssl":true,
         "ovp":"sample-ovp",
         "sdkVersion":"sample-sdk",
         "playerName":"roku"
         }    
      }
      ```

      | Parámetro de configuración | Descripción     |
      | --- | --- |
      | `server` | Cadena que representa la URL del punto final de seguimiento en el servidor. |
      | `publisher` | Cadena que representa el identificador único del editor de contenido. |
      | `channel` | Cadena que representa el nombre del canal de distribución de contenido. |
      | `ssl` | Booleano que representa si SSL debe utilizarse para rastrear llamadas. |
      | `ovp` | Cadena que representa el nombre del proveedor del reproductor de vídeo. |
      | `sdkversion` | Cadena que representa la versión actual de la aplicación/SDK. |
      | `playerName` | Cadena que representa el nombre del reproductor. |

      >[!IMPORTANT]
      >
      >Si `mediaHeartbeat` se configura incorrectamente, el módulo multimedia (VHL) entrará en un estado de error y dejará de enviar llamadas de seguimiento.


1. Configure el ID de visitante de Experience Cloud.

   El servicio de ID de visitante de Experience Cloud ofrece un ID de visitante universal para las soluciones de Experience Cloud. Video Heartbeat y otras integraciones de Experience Cloud requieren el servicio de ID de Visitante.

   Verifique que su configuración de `ADBMobileConfig` contenga su ID de empresa de `marketingCloud`.

   ```
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

   |  Método   | Descripción |
   | --- | --- |
   | `visitorMarketingCloudID` | Recupera el ID del visitante de Experience Cloud del servicio de ID del visitante.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Con el ID de Visitante de Experience Cloud, puede establecer ID de cliente adicionales que se pueden asociar con cada visitante. La API de visitante acepta varios ID de cliente para el mismo visitante y un identificador de tipo de cliente para separar el ámbito de los distintos ID de cliente. Este método corresponde a `setCustomerIDs`. Por ejemplo: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Se utiliza para establecer el ID de Roku para publicidad (RIDA) en el SDK. Por ejemplo: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Obtenga el ID de Roku para publicidad (RIDA) mediante la API de SDK de Roku [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic). |
   | `getAllIdentifiers` | Devuelve una lista de todos los identificadores almacenados por el SDK, incluidos los identificadores de Analytics, Visitante, Audience Manager y personalizado. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   <br/><br/>

   **API públicas adicionales**

   **DebugLogging**
| Método   | Descripción | | — | — | |  `setDebugLogging` | Se utiliza para habilitar o deshabilitar el registro de depuración para el SDK.  <br/><br/>`ADBMobile().setDebugLogging(true)` | |  `getDebugLogging` | Devuelve true si el registro de depuración está habilitado.   <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   <br/><br/>

   **PrivacyStatus**
 | Constante   | Descripción | | — | — | |  `PRIVACY_STATUS_OPT_IN` | Constante que se pasará al llamar a setPrivacyStatus para activar. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN`| |  `PRIVACY_STATUS_OPT_OUT` | Constante que se pasará al llamar a setPrivacyStatus para desactivar.  <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT`|

   <br/>

   |  Método   | Descripción |
   | --- | --- |
   | `setPrivacyStatus` | Establece el estado de privacidad en el SDK. <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Obtiene el estado de privacidad actual establecido en el SDK. <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   <br/><br/>
   >[!IMPORTANT]
   >
   >Asegúrese de llamar a las funciones `processMessages` y `processMediaMessages` en el bucle de evento principal cada 250 ms para asegurarse de que el SDK envía los pings correctamente.

   |  Método   | Descripción |
   | --- | --- |
   | `processMessages` | Responsable de pasar los eventos de Analytics al SDK que se va a gestionar.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Responsable de pasar los eventos de medios al SDK que se va a gestionar. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
