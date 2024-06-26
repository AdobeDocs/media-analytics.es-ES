---
title: Administración de interrupciones de la aplicación durante la reproducción
description: Aprenda a gestionar las interrupciones del seguimiento durante la reproducción de medios.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 90%

---

# Administración de interrupciones de la aplicación durante la reproducción{#handling-application-interrupts-during-playback}

La reproducción en una aplicación multimedia puede interrumpirse de varias formas. Por ejemplo, un usuario puede pulsar explícitamente la pausa, o puede poner la aplicación en segundo plano. Con independencia de la causa de la interrupción de la reproducción de medios, las instrucciones de seguimiento son las mismas.

1. Invoque **`trackPause`** cuando la aplicación se interrumpa (se pone en segundo plano, se pausa el contenido, etc.).
1. Invoque **`trackPlay`** cuando la aplicación vuelva a estar en primer plano o cuando la reproducción de medios se reanude.

>[!NOTE]
>
>Llamando `trackSessionStart` cuando la aplicación vuelve del fondo, la reproducción hasta ese punto puede no contar para el tiempo total de reproducción, además de perder marcadores de progreso, segmentos, etc. anteriores. En su lugar, invoque `trackPlay` cuando la aplicación vuelva o se reanude la reproducción de contenido.

## Preguntas frecuentes sobre la administración de interrupciones de aplicaciones: {#faq-about-handling-application-interrupts}

* _¿Cuánto tiempo debe estar una aplicación en segundo plano para que se cierre la sesión?_

  Si la aplicación permite la reproducción en segundo plano, puede continuar el seguimiento mediante la llamada a nuestras API, y nosotros le enviaremos los pings de seguimiento habituales. No hay muchas aplicaciones de vídeo que permitan la reproducción en segundo plano excepto YouTube Red; sin embargo, todas las aplicaciones de audio lo permiten. Si la aplicación no permite la reproducción en segundo plano, se recomienda poner en pausa la reproducción durante un minuto y, a continuación, finalizar la sesión de seguimiento. La aplicación no puede continuar enviando pings de pausa, ya que, en la mayoría de los casos, no puede determinar si el usuario va a seguir viendo el contenido o cuándo lo va a cerrar. Asimismo, no es recomendable seguir enviando pings mientras se ejecuta en segundo plano.

* _¿Cuál es la forma correcta de administrar el seguimiento de reinicio después de que la aplicación haya estado en segundo plano durante un largo periodo de tiempo?_

  La aplicación debería invocar `trackSessionEnd` para finalizar la sesión de seguimiento. A partir de la versión 2.1, el SDK envía un ping de “finalización” para notificar al back-end que la sesión de seguimiento se ha cerrado.

* _¿Cómo funciona el reinicio de la misma sesión?_

  Para obtener información sobre cómo reanudar una sesión de seguimiento, consulte [Reanudación de sesiones inactivas](resuming-inactive.md). El SDK envía un ping de reanudación para notificar al back-end que el usuario está reanudando manualmente la sesión.
