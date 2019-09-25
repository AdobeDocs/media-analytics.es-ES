---
seo-title: Establecimiento de ID de usuario
title: Establecimiento de ID de usuario
uuid: fdd54flash-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Establecimiento de ID de usuario{#set-user-ids}

El ID de usuario es un identificador de visitante personalizado y único que la aplicación define.

Configure y obtenga el ID de usuario único en el SDK de ADBMobile de la siguiente manera:

* **Configure:**

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
