---
seo-title: Administración de interrupciones de la aplicación durante la reproducción
title: Administración de interrupciones de la aplicación durante la reproducción
uuid: 1cccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Administración de interrupciones de la aplicación durante la reproducción{#handling-application-interrupts-during-playback}

La reproducción en una aplicación de medios se puede interrumpir de diversas maneras: un usuario presiona explícitamente la pausa o cuando coloca la aplicación en segundo plano. Independientemente de las causas de una interrupción en la reproducción de medios, las instrucciones de seguimiento son las mismas:

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. Si lo hace, la reproducción hasta ese punto no se contabilizará en el tiempo total de reproducción, junto con la pérdida de marcadores de progreso, segmentos, etc. anteriores. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## Preguntas frecuentes sobre la administración de interrupciones de aplicaciones: {#faq-about-handling-application-interrupts}

* _¿Cuánto tiempo debe estar una aplicación en segundo plano para que se cierre la sesión?_

   Si la aplicación permite la reproducción en segundo plano, puede continuar el seguimiento mediante la llamada a nuestras API, y nosotros le enviaremos los pings de seguimiento habituales. No hay muchas aplicaciones de vídeo que permitan la reproducción en segundo plano excepto YouTube Red; sin embargo, todas las aplicaciones de audio lo permiten. Si la aplicación no permite la reproducción en segundo plano, se recomienda permanecer en el estado de pausa durante un minuto y, a continuación, finalizar la sesión de seguimiento. La aplicación no puede continuar enviando pings de pausa porque en la mayoría de los casos no puede determinar si el usuario va a volver para continuar viendo el medio o determinar cuándo va a morir. Asimismo, no es recomendable seguir enviando pings mientras se ejecuta en segundo plano.

* _¿Cuál es la forma correcta de administrar el seguimiento de reinicio después de que la aplicación haya estado en segundo plano durante un largo periodo de tiempo?_

   La aplicación debería invocar `trackSessionEnd` para finalizar la sesión de seguimiento. A partir de la versión 2.1, el SDK envía un ping de “finalización” para notificar al back-end que la sesión de seguimiento se ha cerrado.

* _¿Cómo funciona el reinicio de la misma sesión?_

   Para obtener instrucciones detalladas sobre el reinicio de una sesión de seguimiento, consulte esta página: [Reanudar sesiones inactivas.](/help/sdk-implement/cookbook/resuming-inactive.md) El SDK envía un ping de reanudación para notificar al back-end que el usuario está reanudando la sesión manualmente.

