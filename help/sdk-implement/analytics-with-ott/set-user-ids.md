---
title: Establecimiento de ID de usuario
description: API para configurar los ID de usuario, qué servidor como identificador de cliente único.
uuid: fdd54flash-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Establecimiento de ID de usuario{#set-user-ids}

El ID de usuario es un identificador de visitante personalizado y único que la aplicación define.

Configure y obtenga el ID de usuario único en el SDK de ADBMobile de la siguiente manera:

* **Establezca:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Obtenga:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
