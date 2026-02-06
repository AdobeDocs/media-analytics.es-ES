---
title: Condiciones de tiempo de espera
description: Obtenga información acerca de las condiciones de tiempo de espera de la API de Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '165'
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
