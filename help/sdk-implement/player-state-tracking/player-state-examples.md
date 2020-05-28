---
title: Ejemplos de seguimiento de estado del reproductor
description: Este tema incluye ejemplos de la función de seguimiento de estado del reproductor.
translation-type: tm+mt
source-git-commit: 1c2992d2a5992b07fa24823501d542c1878aa296
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Ejemplos de seguimiento de estado del reproductor


## Ejemplo de pausa larga

Cuando una sesión de vídeo tiene una duración de pausa superior a 30 minutos, la API requiere una nueva sesión. Cuando esto sucede, el cliente debe generar un nuevo ID de sesión. Para ambas sesiones de vídeo, el cliente debe conservar todos los estados en los que se encuentra un reproductor y enviar toda la información como un `stateStart` evento justo después de la `sessionStart` llamada.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

Después de enviar `sessionEnd` , se debe iniciar una nueva sesión de vídeo y los primeros eventos de API serían:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

El ejemplo de pausa larga muestra que el reproductor también almacena sus estados para que se puedan enviar a la nueva sesión de vídeo.
