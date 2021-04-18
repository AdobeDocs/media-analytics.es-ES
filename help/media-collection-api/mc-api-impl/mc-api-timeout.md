---
title: Condiciones de tiempo de espera
description: Condiciones de tiempo de espera
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 100%

---

# Condiciones de tiempo de espera {#timeout-conditions}

**Condiciones de tiempo de espera de API de recopilación de contenido**

La API de recopilación de contenido, al no tener estado, no utiliza el mismo mecanismo que Media SDK para emitir un nuevo ID de sesión cuando se pone en espera. Cuando se produce una condición de tiempo de espera, el proceso posterior cerrará la sesión y se descartarán todas las llamadas realizadas con ese ID de sesión. El cliente debe controlar la lógica que gestiona el tiempo de espera de la sesión. Es decir, el reproductor deberá controlar el tiempo de espera y obtener un nuevo ID de sesión si se produce una pausa.

* **10 Minutos: Ningún evento de API**

   Si el back end no recibe ningún evento de API, se cerrará la sesión.
* **30 minutos: Sin cambio en el cabezal de lectura**

   Si el cabezal de reproducción no se mueve durante 30 minutos (por ejemplo, el usuario hace clic en Pausa y se marcha), el back end cerrará la sesión.

>[!NOTE]
>
>También puede forzar un final de sesión enviando una solicitud `events` con un tipo de evento `sessionEnd`.
