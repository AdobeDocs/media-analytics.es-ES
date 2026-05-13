---
title: Establecimiento de ID de usuario
description: API para configurar los ID de usuario y qué servidor usar como identificador de cliente único.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: Streaming Media, API
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/AG7KGMEVhpDbGzHKhb94KF8QHzDTw-y1kdkklOdWCFI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 53
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
