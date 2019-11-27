---
title: Administración de interrupciones de la aplicación durante la reproducción
description: Cómo controlar las interrupciones al seguimiento durante la reproducción del contenido.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Administración de interrupciones de la aplicación durante la reproducción {#handling-application-interrupts-during-playback}

En una aplicación, la reproducción de contenido se puede interrumpir de distintas formas: cuando el usuario pone explícitamente el vídeo en pausa, o cuando este coloca la aplicación en segundo plano. Con independencia de la causa de la interrupción de la reproducción de contenido, las instrucciones de seguimiento son las mismas:

1. Invoque **`trackPause`** cuando la aplicación se interrumpa (se pone en segundo plano, se pausa el contenido, etc.).
1. Invoque **`trackPlay`** cuando la aplicación vuelva a estar en primer plano o cuando la reproducción de contenido se reanude.

>[!NOTE]
>
>El equipo de Media Analytics tiene constancia de casos en los que los clientes invocaron `trackSessionStart` cuando la aplicación volvió al primer plano. Esto hace que el contenido reproducido hasta ese punto no se tenga en cuenta para el tiempo de reproducción total, y ocasiona la pérdida de elementos como marcadores de progreso, segmentos, etc. En su lugar, invoque `trackPlay` cuando la aplicación vuelva o se reanude la reproducción de contenido.

## Preguntas frecuentes sobre la administración de interrupciones de aplicaciones: {#faq-about-handling-application-interrupts}

* _¿Cuánto tiempo debe estar una aplicación en segundo plano para que se cierre la sesión?_

   Si la aplicación permite la reproducción en segundo plano, puede continuar el seguimiento mediante la llamada a nuestras API, y nosotros le enviaremos los pings de seguimiento habituales. No hay muchas aplicaciones de vídeo que permitan la reproducción en segundo plano excepto YouTube Red; sin embargo, todas las aplicaciones de audio lo permiten. Si la aplicación no permite la reproducción en segundo plano, se recomienda poner en pausa la reproducción durante un minuto y, a continuación, finalizar la sesión de seguimiento. La aplicación no puede continuar enviando pings de pausa, ya que, en la mayoría de los casos, no puede determinar si el usuario va a seguir viendo el contenido o cuándo lo va a cerrar. Asimismo, no es recomendable seguir enviando pings mientras se ejecuta en segundo plano.

* _¿Cuál es la forma correcta de administrar el seguimiento de reinicio después de que la aplicación haya estado en segundo plano durante un largo periodo de tiempo?_

   La aplicación debería invocar `trackSessionEnd` para finalizar la sesión de seguimiento. A partir de la versión 2.1, el SDK envía un ping de “finalización” para notificar al back-end que la sesión de seguimiento se ha cerrado.

* _¿Cómo funciona el reinicio de la misma sesión?_

   Para obtener instrucciones detalladas sobre el reinicio de una sesión de seguimiento, consulte esta página: [Reanudar sesiones inactivas.](/help/sdk-implement/cookbook/resuming-inactive.md) El SDK envía un ping de reanudación para notificar al back-end que el usuario está reanudando la sesión manualmente.

