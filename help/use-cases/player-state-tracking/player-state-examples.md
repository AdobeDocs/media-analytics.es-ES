---
title: Ejemplos de seguimiento del estado de reproducción
description: Este tema incluye ejemplos de la función de seguimiento de estado del reproductor.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 100%

---

# Ejemplos de seguimiento del estado de reproducción


## Ejemplo de pausa larga

Cuando una sesión de vídeo tiene una duración de pausa superior a 30 minutos, la API requiere una nueva sesión. Cuando esto sucede, el cliente debe generar un nuevo ID de sesión. Para ambas sesiones de vídeo, el cliente debe conservar todos los estados en los que se encuentra un reproductor y enviar toda la información como un `stateStart` evento justo después de la llamada de `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Después de enviar `sessionEnd`, se debe iniciar una nueva sesión de vídeo y los primeros eventos de API serían:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

El ejemplo de pausa larga muestra que el reproductor también almacena sus estados para que se puedan enviar a la nueva sesión de vídeo.
