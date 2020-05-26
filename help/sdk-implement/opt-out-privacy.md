---
title: Configuración de privacidad y exclusión
description: Cómo gestionar la inclusión, la exclusión y la privacidad.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: ht
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a
workflow-type: ht
source-wordcount: '360'
ht-degree: 100%

---


# Configuración de privacidad y exclusión {#opt-out-and-privacy}

## Inclusión/Exclusión {#opt-out-opt-in}

Puede controlar si se permite el seguimiento de la actividad en un dispositivo determinado:

* **Aplicaciones móviles**: la biblioteca de VA respeta la configuración de privacidad y exclusión de la biblioteca `AdobeMobile`. Para desactivar el seguimiento, debe utilizar la biblioteca `AdobeMobile`. Para obtener más información sobre la configuración de exclusión y privacidad de la biblioteca `AdobeMobile`, consulte [Configuración de privacidad y exclusión](https://docs.adobe.com/content/help/es-ES/mobile-services/android/gdpr-privacy-android/privacy.html).
* **Aplicaciones JavaScript/de explorador**: la biblioteca de VA respeta la configuración de privacidad y exclusión de `VisitorAPI`. Para desactivar el seguimiento, debe desactivar el servicio API del visitante. Para obtener más información sobre la exclusión y privacidad, consulte [Servicio de identidad de Adobe Experience Platform.](https://docs.adobe.com/content/help/es-ES/id-service/using/home.html)
* **Aplicaciones OTT (Chromecast, Roku):** Los SDK de OTT proporcionan API preparadas para el Reglamento general de protección de datos (RGPD) que le permiten establecer indicadores de estado `opt` para la recopilación y la transmisión de datos y sacar identidades almacenadas localmente.

   >[!NOTE]
   >
   >Las llamadas de seguimiento de Heartbeat de contenido también se desactivan si se establece la exclusión como estado de privacidad.

   Puede controlar si los datos de Analytics se envían en un dispositivo específico mediante la configuración siguiente:

   * La configuración `privacyDefault` del archivo de configuración `ADBMobile.json` Este ajuste controla la configuración inicial que persiste hasta que se cambia en el código.

   * El método `ADBMobile().setPrivacyStatus()`.

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
         >Cuando un usuario se excluye del seguimiento, todos los datos e ID del dispositivo persistente se purgarán hasta que el usuario decida volver a entrar.

      * **Volver a activar:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Devuelve la configuración actual:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   Después de cambiar la configuración de privacidad mediante el uso de `setPrivacyStatus`, el cambio es permanente hasta que se vuelva a modificar con este método o bien se desinstale y se vuelva a instalar la aplicación completamente.

## Recuperación de identificadores almacenados (aplicaciones OTT) {#retrieving-stored-identifiers-ott-apps}

Esta información le ayuda a recuperar ID de usuario almacenados localmente desde la aplicación Roku.

>[!IMPORTANT]
>
>Este método de recuperación de todos los ID obtiene todas las identidades de usuarios conocidas y conservadas por el SDK. Debe llamar a este método **antes** de que un usuario se excluya.

Las identidades almacenadas localmente se devuelven en una cadena JSON, que puede contener:

* Contexto de compañía: ID de organización de IMS
* ID de usuario
* Experience Cloud ID (MCID)
* ID de fuentes de datos (DPID, DPUUID)
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

