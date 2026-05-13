---
title: Ejemplos de seguimiento del estado de reproducción
description: Este tema incluye ejemplos de la función de seguimiento de estado del reproductor.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Ejemplos de seguimiento del estado de reproducción


## Ejemplo de pausa larga

Cuando una sesión de vídeo tiene una duración de pausa superior a 30 minutos, la API requiere una nueva sesión. Cuando esto sucede, el cliente debe generar un nuevo ID de sesión. Para ambas sesiones de vídeo, el cliente debe conservar todos los estados en los que se encuentra un reproductor y enviar toda la información como un `stateStart` evento justo después de la llamada de `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Después de enviar `sessionEnd`, se debe iniciar una nueva sesión de vídeo y los primeros eventos de API serían:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

El ejemplo de pausa larga muestra que el reproductor también almacena sus estados para que se puedan enviar a la nueva sesión de vídeo.
