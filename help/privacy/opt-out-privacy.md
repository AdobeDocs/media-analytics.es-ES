---
title: Explicación de la privacidad y la exclusión
description: Cómo gestionar la inclusión, la exclusión y la privacidad.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 382
ht-degree: 92%

---

# Privacidad y exclusión{#opt-out-and-privacy}

## Inclusión/Exclusión {#opt-out-opt-in}

Puede controlar si se permite el seguimiento de la actividad en un dispositivo determinado:

* **Aplicaciones móviles:** Las extensiones de medios respetan la configuración de privacidad de la recopilación de datos. Para desactivar el seguimiento, debe configurar la privacidad para [Excluido en etiquetas](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property) o [Actualizar el estado de privacidad en el SDK de Mobile](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#getprivacystatus).
* **Aplicaciones JavaScript/de explorador**: la biblioteca de VA respeta la configuración de privacidad y exclusión de `VisitorAPI`. Para desactivar el seguimiento, debe desactivar el servicio API del visitante. Para obtener más información sobre exclusión y privacidad, consulte [Servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es).
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
