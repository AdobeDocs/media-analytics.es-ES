---
title: Condiciones de tiempo de espera
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Condiciones de tiempo de espera{#timeout-conditions}

**Condiciones de tiempo de espera de API de recopilación de medios**

La API de Media Collection, sin estado, no tiene el mismo mecanismo que el SDK de medios para emitir un nuevo ID de sesión cuando se dan las condiciones de tiempo de espera. Cuando se produce una condición de tiempo de espera, el proceso posterior cerrará la sesión y se descartarán todas las llamadas realizadas con ese ID de sesión. El cliente debe controlar la lógica que gestiona el tiempo de espera de la sesión. Es decir, el reproductor deberá controlar el tiempo de espera y obtener un nuevo ID de sesión si se produce una pausa.

* **10 Minutos: Ningún evento de API**

   Si el servidor no recibe ningún evento de API, se cerrará la sesión.
* **30 minutos: Sin cambio de cabeza lectora**

   Si el cursor de reproducción no se mueve durante 30 minutos (p. ej., si el usuario hace clic en Pausa y se va), el servidor cerrará la sesión.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

