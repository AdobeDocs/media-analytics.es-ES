---
seo-title: Configuración de privacidad y exclusión
title: Configuración de privacidad y exclusión
uuid: 7 e 60 c 7 bd -8 dba -4 c 7 a -9 c 3 c -0 c 634 b 815397
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# Configuración de privacidad y exclusión{#opt-out-and-privacy}

## Inclusión/Exclusión {#section_zfb_syq_v2b}

Puede controlar si se permite el seguimiento de la actividad en un dispositivo determinado:

* **Aplicaciones móviles**: la biblioteca de VA respeta la configuración de privacidad y exclusión de la biblioteca `AdobeMobile`. Para desactivar el seguimiento, debe utilizar la biblioteca `AdobeMobile`. Para obtener más información sobre la configuración de exclusión y privacidad de la biblioteca `AdobeMobile`, consulte [Configuración de privacidad y exclusión](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html).
* **Aplicaciones JavaScript/de explorador**: la biblioteca de VA respeta la configuración de privacidad y exclusión de `VisitorAPI`. Para desactivar el seguimiento, debe desactivar el servicio API del visitante. For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **Aplicaciones OTT (Chromecast, Roku):** los SDK OTT proporcionan API para el Reglamento General de Protección de Datos (RGPD) que permiten establecer indicadores `opt` de estado para la recopilación y transmisión de datos y para recuperar identidades almacenadas localmente.

   >[!NOTE]
   >
   >Las llamadas de seguimiento de Media Heartbeat también están desactivadas si el estado de privacidad se establece en opt-out.

   Puede controlar si los datos de Analytics se envían en un dispositivo específico mediante la configuración siguiente:

   * `privacyDefault` La configuración del archivo `ADBMobile.json` de configuración. Este ajuste controla la configuración inicial que persiste hasta que se cambia en el código.

   * The `ADBMobile().setPrivacyStatus()` method.

      * **Desactivar:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >Cuando un usuario renuncia al seguimiento, todos los datos del dispositivo persistirán y los ID se purgarán hasta que el usuario vuelva a activarla.

      * **Reactivar:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Volver a la configuración actual:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   Después de cambiar la configuración de privacidad mediante el uso de `setPrivacyStatus`, el cambio es permanente hasta que se vuelva a modificar con este método o bien se desinstale y se vuelva a instalar la aplicación completamente.

## Recuperación de identificadores almacenados (aplicaciones OTT) {#section_mky_2yq_v2b}

Esta información le ayuda a recuperar ID de usuario almacenados localmente desde la aplicación Roku.

>[!IMPORTANT]
>
>El método para recuperar todos los identificadores obtiene todas las identidades de usuario conocidas y persistentes por el SDK. Debe invocar este método **antes** de que el usuario salga.

Los ID almacenados localmente se devuelven en una cadena JSON, que puede contener:

* Contexto sobre la empresa: ID de organización de IMS
* ID de usuarios
* Experience Cloud ID (MCID)
* ID de orígenes de datos (DPID, DPUUID)
* ID de Analytics (AVID, AID, VID y RSID asociados)
* ID de Audience Manager (UUID)

Por ejemplo:

* **Chromecast:**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku:**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

