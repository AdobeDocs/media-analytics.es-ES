---
title: Administración de interrupciones de la aplicación durante la reproducción
description: Aprenda a gestionar las interrupciones del seguimiento durante la reproducción de medios.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/BlL-c1rf5d3juDKHybex9vrPvQsBIiNXVO2ug9LKl0g
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 358
ht-degree: 55%

---

# Administración de interrupciones de la aplicación durante la reproducción{#handling-application-interrupts-during-playback}

La reproducción en una aplicación multimedia puede interrumpirse de varias formas. Por ejemplo, un usuario puede pulsar explícitamente la pausa, o puede poner la aplicación en segundo plano. Con independencia de la causa de la interrupción de la reproducción de medios, las instrucciones de seguimiento son las mismas.

1. Invoque **`trackPause`** cuando la aplicación se interrumpa (se pone en segundo plano, se pausa el contenido, etc.).
1. Invoque **`trackPlay`** cuando la aplicación vuelva a estar en primer plano o cuando la reproducción de medios se reanude.

>[!NOTE]
>
>Llamar a `trackSessionStart` cuando la aplicación vuelve del segundo plano puede ocasionar que la reproducción hasta ese punto no se tenga en cuenta para el tiempo total de reproducción, además de la pérdida de marcadores de progreso, segmentos, etc. anteriores. En su lugar, invoque `trackPlay` cuando la aplicación vuelva o se reanude la reproducción de contenido.

## Preguntas frecuentes sobre la administración de interrupciones de aplicaciones: {#faq-about-handling-application-interrupts}

* _¿Cuánto tiempo debe estar en segundo plano una aplicación antes de que se cierre la sesión?_

  Si la aplicación permite la reproducción en segundo plano, puede continuar el seguimiento llamando a nuestras API y enviaremos todos nuestros pings de seguimiento regulares. No hay muchas aplicaciones de vídeo que permitan la reproducción en segundo plano excepto YouTube Red; sin embargo, todas las aplicaciones de audio lo permiten. Si la aplicación no permite la reproducción en segundo plano, se recomienda poner en pausa la reproducción durante un minuto y, a continuación, finalizar la sesión de seguimiento. La aplicación no puede continuar enviando pings de pausa, ya que, en la mayoría de los casos, no puede determinar si el usuario va a seguir viendo el contenido o cuándo lo va a cerrar. También es una mala experiencia seguir enviando pings cuando se está en segundo plano.

* _¿Cuál es la manera correcta de controlar el seguimiento de reinicio después de que la aplicación haya estado en segundo plano durante mucho tiempo?_

  La aplicación debería invocar `trackSessionEnd` para finalizar la sesión de seguimiento. En la versión 2.1, SDK envía un ping de &quot;finalización&quot; para notificar al back-end que la sesión de seguimiento está cerrada.

* _¿Qué sucede si se reinicia la misma sesión?_

  Para obtener información acerca de cómo reanudar una sesión de seguimiento, vea [Reanudar sesiones inactivas](resuming-inactive.md).SDK envía un ping de reanudación para notificar al back-end que el usuario está reanudando la sesión manualmente.
