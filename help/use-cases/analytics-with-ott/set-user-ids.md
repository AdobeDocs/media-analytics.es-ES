---
title: Establecimiento de ID de usuario
description: API para configurar los ID de usuario y qué servidor usar como identificador de cliente único.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Data Engineer
source-git-commit: 70900e305c3ed7a2be4069c6f296d56f1f6e0966
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 100%

---

# Establecimiento de ID de usuario{#set-user-ids}

El ID de usuario es un identificador de visitante personalizado y único que la aplicación define.

Configure y obtenga el ID único de usuario en el SDK de ADBMobile de la siguiente manera:

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
