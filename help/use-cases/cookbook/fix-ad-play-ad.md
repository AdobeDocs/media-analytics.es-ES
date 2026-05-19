---
title: Resolver la reproducción principal que aparece entre anuncios
description: Aprenda a gestionar llamadas main:play inesperadas entre anuncios.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-Q92qldvgTTgJave-VP6P8IYN1CxbQQzxbtLS3DgYAE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 453
ht-degree: 75%

---

# Gestión de huecos que aparecen entre anuncios{#resolving-main-play-appearing-between-ads}

## PROBLEMA

En algunas situaciones de seguimiento de publicidad, podría encontrar llamadas `main:play` que se producen de forma inesperada entre el final de un anuncio y el comienzo del siguiente. Si el retraso entre la llamada al anuncio completo y la siguiente llamada de inicio de anuncio es mayor que 250 milisegundos, Media SDK volverá a enviar llamadas `main:play`. Si este regreso a `main:play` se produce durante una pausa publicitaria pre-roll, la métrica de inicio del contenido puede configurarse antes.

Media SDK interpreta un espacio entre anuncios como el descrito anteriormente como contenido principal, ya que no se superponen con ningún contenido publicitario. Media SDK no tiene ninguna información de publicidad configurada y el reproductor está en estado de reproducción. Si no hay información de publicidad y se está reproduciendo el estado del reproductor, Media SDK acredita la duración del espacio hacia el contenido principal de forma predeterminada. No puede acreditar la duración de la reproducción de la información de publicidad nula.

## IDENTIFICACIÓN

Al utilizar Adobe Debug o un analizador de paquetes de red como Charles, si ve las siguientes llamadas de Heartbeat en este orden durante una pausa publicitaria de anuncio previo a la emisión:

* Inicio de sesión: `s:event:type=start` &amp; `s:asset:type=main`
* Inicio de publicidad: `s:event:type=start` &amp; `s:asset:type=ad`
* Reproducción de publicidad: `s:event:type=play` &amp; `s:asset:type=ad`
* Finalización de publicidad: `s:event:type=complete` &amp; `s:asset:type=ad`
* Reproducción de contenido principal: `s:event:type=play` y `s:asset:type=main` **(inesperado)**

* Inicio de publicidad: `s:event:type=start` &amp; `s:asset:type=ad`
* Reproducción de publicidad: `s:event:type=play` &amp; `s:asset:type=ad`
* Finalización de publicidad: `s:event:type=complete` &amp; `s:asset:type=ad`
* Reproducción de contenido principal: `s:event:type=play` y `s:asset:type=main` **(inesperado)**

## RESOLUCIÓN

***Retraso al activar la llamada de finalización del anuncio.***

Administre el espacio desde dentro del reproductor invocando `trackEvent:AdComplete` tras el primer anuncio, seguida inmediatamente por `trackEvent:AdStart` para el segundo anuncio. La aplicación debe permanecer desactivada al invocar al evento `AdComplete` tras finalizar el primer anuncio. Asegúrese de invocar a `trackEvent:AdComplete` para el último anuncio de la pausa publicitaria. Si el reproductor puede identificar que el recurso de anuncio actual es el final de la pausa publicitaria, invoque el `trackEvent:AdComplete` inmediatamente. Esta resolución hará que se atribuya menos de 1 segundo del tiempo de publicidad adicional a la unidad de publicidad anterior.

**Al iniciar la pausa publicitaria, incluido el anuncio previo a la emisión:**

* Cree la instancia del objeto `adBreak` para la pausa publicitaria; por ejemplo, `adBreakObject`.

* La llamada `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**En cada inicio de recurso de publicidad:**

* **La llamada`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Invoque esta llamada solo si no se ha completado el anuncio anterior. Utilice un valor booleano para mantener el estado &quot;`isinAd`&quot; para el anuncio anterior.

* Cree la instancia del objeto de anuncio para el recurso de publicidad: por ejemplo, `adObject`.
* Rellenar metadatos de publicidad, `adCustomMetadata`.
* La llamada `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Invoque `trackPlay()` si este es el primer anuncio de una pausa publicitaria del anuncio previo a la emisión.

**En cada recurso de anuncio finalizado:**

* **No realice una llamada**

  >[!NOTE]
  >
  >Si la aplicación sabe que es el último anuncio de la pausa publicitaria, invoque `trackEvent:AdComplete` aquí y omita la configuración de `trackEvent:AdComplete` en `trackEvent:AdBreakComplete`

**Al omitir un anuncio:**

* La llamada `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Al finalizar un anuncio:**

* **La llamada`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Si este paso ya se ha realizado como parte de la última llamada a `trackEvent:AdComplete`, se puede omitir.

* La llamada `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
