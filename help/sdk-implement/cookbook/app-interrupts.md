---
seo-title: Administración de interrupciones de la aplicación durante la reproducción
title: Administración de interrupciones de la aplicación durante la reproducción
uuid: 1 ccb 4507-bda 6-462 d-bf 67-e 22978 a 4 db 3 d
translation-type: tm+mt
source-git-commit: 8c9592ee7ad97de2cf4aefb226ed1390bc5b53a8

---


# Administración de interrupciones de la aplicación durante la reproducción{#handling-application-interrupts-during-playback}

La reproducción en una aplicación de medios se puede interrumpir de diversas maneras: un usuario pulsa explícitamente la pausa o cuando un usuario coloca la aplicación en segundo plano. Independientemente de qué produzca una interrupción en la reproducción de medios, las instrucciones de seguimiento son las mismas:

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. Si lo hace, la reproducción hasta ese punto no se contabilizará en el tiempo de reproducción total, junto con la pérdida de marcadores de progreso anteriores, segmentos, etc. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## Preguntas frecuentes sobre la administración de interrupciones de aplicaciones: {#section_osf_xqs_h2b}

* _¿Cuánto tiempo debe estar una aplicación en segundo plano para que se cierre la sesión?_

   Si la aplicación permite la reproducción en segundo plano, puede continuar el seguimiento mediante la llamada a nuestras API, y nosotros le enviaremos los pings de seguimiento habituales. No muchas aplicaciones de vídeo permiten la reproducción en segundo plano excepto YouTube rojo, sin embargo, todas las aplicaciones de audio permiten esto. Si la aplicación no permite la reproducción en segundo plano, se recomienda permanecer en Estado Pausa durante un minuto y, a continuación, finalizar la sesión de seguimiento. La aplicación no puede seguir enviando pings de pausa porque en la mayoría de los casos no puede determinar si el usuario regresa para continuar viendo el medio o determinar cuándo se va a matar. Asimismo, no es recomendable seguir enviando pings mientras se ejecuta en segundo plano.

* _¿Cuál es la forma correcta de administrar el seguimiento de reinicio después de que la aplicación haya estado en segundo plano durante un largo periodo de tiempo?_

   La aplicación debería invocar `trackSessionEnd` para finalizar la sesión de seguimiento. A partir de la versión 2.1, el SDK envía un ping de “finalización” para notificar al back-end que la sesión de seguimiento se ha cerrado.

* _¿Cómo funciona el reinicio de la misma sesión?_

   Para obtener instrucciones detalladas sobre el reinicio de una sesión de seguimiento, consulte esta página: [Reanudar sesiones inactivas.](../../sdk-implement/cookbook/resuming-inactive.md) El SDK envía un ping de reanudación para notificar al back-end que el usuario está reanudando la sesión manualmente.

