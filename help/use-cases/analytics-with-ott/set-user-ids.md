---
title: Establecimiento de ID de usuario
description: API para configurar los ID de usuario y qué servidor usar como identificador de cliente único.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 45%

---

# Establecimiento de ID de usuario{#set-user-ids}

El ID de usuario es un identificador de visitante personalizado y único definido por la aplicación para un usuario.

Establezca y obtenga el ID único de usuario en el SDK de ADBMobile de la siguiente manera:

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
