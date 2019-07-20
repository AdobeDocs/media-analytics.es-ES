---
seo-title: Condiciones de tiempo de espera
title: Condiciones de tiempo de espera
uuid: 2 a 4 ea 13 e-a 561-4 adf-b 567-f 980301 b 32 c 8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Condiciones de tiempo de espera{#timeout-conditions}

**Condiciones de tiempo de espera de API de recopilación de medios**

La API de recopilación de medios no tiene el mismo mecanismo que el SDK de medios para emitir un nuevo ID de sesión cuando se producen condiciones de tiempo de espera. Cuando se produce una condición de tiempo de espera, el proceso posterior cerrará la sesión y se descartarán todas las llamadas realizadas con ese ID de sesión. El cliente debe controlar la lógica que gestiona el tiempo de espera de la sesión. Es decir, el reproductor deberá controlar el tiempo de espera y obtener un nuevo ID de sesión si se produce una pausa.

* **10 minutos: Ningún evento de API**

   Si el back-end no recibe ningún evento de API, cerrará la sesión.
* **30 minutos: Sin cambio de cabeza lectora**

   Si el cursor de reproducción no se mueve durante 30 minutos (p. ej., el usuario entra en Pausa y sale), el back-end cerrará la sesión.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

