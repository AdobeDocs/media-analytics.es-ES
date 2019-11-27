---
title: Solución cuando aparece main:play entre anuncios
description: Cómo gestionar llamadas main:play inesperadas entre anuncios.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Solución cuando aparece main:play entre anuncios {#resolving-main-play-appearing-between-ads}

## PROBLEMA

En algunas situaciones de seguimiento de publicidad, podría encontrar llamadas `main:play` que se producen de forma inesperada entre el final de un anuncio y el comienzo del siguiente. Si el retraso entre la llamada al anuncio completo y la siguiente llamada de inicio de anuncio es mayor que 250 milisegundos, Media SDK volverá a enviar llamadas `main:play`. Si este regreso a `main:play` se produce durante una pausa publicitaria pre-roll, la métrica de inicio del contenido puede configurarse antes.

El Media SDK interpreta un espacio entre anuncios como el descrito anteriormente como contenido principal, ya que no existe ninguna superposición con contenido del anuncio. El Media SDK no tiene ningún tipo de información del anuncio, y el reproductor está en estado de reproducción. Si no hay información del anuncio y el reproductor está en estado “reproduciendo”, el Media SDK acreditará la duración del espacio con el contenido principal de forma predeterminada. No puede acreditar la duración de la reproducción de la información de publicidad nula.

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

Administre el espacio desde dentro del reproductor invocando `trackEvent:AdComplete` tras el primer anuncio, seguida inmediatamente por `trackEvent:AdStart` para el segundo anuncio. La aplicación debe permanecer desactivada al invocar al evento `AdComplete` tras finalizar el primer anuncio. Asegúrese de invocar a `trackEvent:AdComplete` para el último anuncio de la pausa publicitaria. Si el reproductor puede identificar que el recurso de anuncio actual es el final de la pausa publicitaria, invoque el `trackEvent:AdComplete` inmediatamente. Esta resolución tendrá como resultado menos de 1 segundo de tiempo adicional de publicidad atribuido a la unidad de publicidad anterior.

**Al comienzo de la pausa publicitaria, incluso pre-roll:**

* Cree la instancia del objeto `adBreak` para la pausa publicitaria; por ejemplo, `adBreakObject`.

* La llamada `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**En cada inicio de recurso de publicidad:**

* **Llama a`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Invoque esta llamada solo si no se ha completado el anuncio anterior. Utilice un valor booleano para mantener el estado "`isinAd`" para el anuncio anterior.

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

* **Llama a`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Si este paso ya se ha realizado como parte de la última llamada a `trackEvent:AdComplete`, se puede omitir.

* La llamada `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

