---
title: Condiciones de tiempo de espera
description: Obtenga información acerca de las condiciones de tiempo de espera de la API de Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 60%

---

# Condiciones de tiempo de espera{#timeout-conditions}

**Condiciones de tiempo de espera de API de recopilación de contenido**

La API de recopilación de contenido, al no tener estado, no utiliza el mismo mecanismo que Media SDK para emitir un nuevo ID de sesión cuando se pone en espera. Cuando se produce una condición de tiempo de espera, el back end cierra la sesión y se pierden todas las llamadas posteriores realizadas con ese ID de sesión. La lógica que administra un tiempo de espera de sesión debe gestionarse en el cliente. Es decir, el reproductor tendrá que monitorizar las condiciones de tiempo de espera y obtener un nuevo ID de sesión si se agota el tiempo de espera.

* **10 Minutos: Ningún evento de API**

  Si el back end no recibe ningún evento de API, se cerrará la sesión.
* **30 minutos: Sin cambio en el cabezal de lectura**

  Si el cabezal de reproducción no se mueve durante 30 minutos (por ejemplo, el usuario hace clic en Pausa y se marcha), el back end cerrará la sesión.

>[!NOTE]
>
>También puede forzar un final de sesión enviando una solicitud `events` con un tipo de evento `sessionEnd`.
