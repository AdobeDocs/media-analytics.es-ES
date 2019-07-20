---
seo-title: Resolución de la reproducción principal entre publicidades
title: Resolución de la reproducción principal entre publicidades
uuid: 228 b 4812-c 23 e -40 c 8-ae 2 b-e 15 ca 69 b 0 bc 2
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Solución cuando aparece main:play entre anuncios{#resolving-main-play-appearing-between-ads}

## PROBLEMA

En algunas situaciones de seguimiento de publicidad, podría encontrar llamadas `main:play` que se producen de forma inesperada entre el final de un anuncio y el comienzo del siguiente. If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. Si este regreso a `main:play` se produce durante una pausa publicitaria pre-roll, la métrica de inicio del contenido puede configurarse antes.

El Media SDK interpreta un espacio entre anuncios como el descrito anteriormente como contenido principal, ya que no existe ninguna superposición con contenido del anuncio. El Media SDK no tiene ningún tipo de información del anuncio, y el reproductor está en estado de reproducción. Si no hay información del anuncio y el reproductor está en estado “reproduciendo”, el Media SDK acreditará la duración del espacio con el contenido principal de forma predeterminada. No puede acreditar la duración de la reproducción de la información de publicidad nula.

## IDENTIFICACIÓN

Mientras utiliza Adobe Debug o un husmeador de paquetes de red como Charles, si ve las siguientes llamadas de Heartbeat en este orden durante una pausa publicitaria previa:

* Inicio de sesión: `s:event:type=start` &amp; `s:asset:type=main`
* Inicio de publicidad: `s:event:type=start` &amp; `s:asset:type=ad`
* Reproducción de publicidad: `s:event:type=play` &amp; `s:asset:type=ad`
* Finalización de publicidad: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(unexpected)**

* Inicio de publicidad: `s:event:type=start` &amp; `s:asset:type=ad`
* Reproducción de publicidad: `s:event:type=play` &amp; `s:asset:type=ad`
* Finalización de publicidad: `s:event:type=complete` &amp; `s:asset:type=ad`
* Main Content Play: `s:event:type=play` &amp; `s:asset:type=main` **(expected)**

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
   >Llame a este solo si no se completó la publicidad anterior. Utilice un valor booleano para mantener el estado "`isinAd`" para el anuncio anterior.

* Cree la instancia del objeto de anuncio para el recurso de publicidad: por ejemplo, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* La llamada `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**En cada recurso de anuncio finalizado:**

* **No realice una llamada**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**Al omitir un anuncio:**

* La llamada `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Al finalizar un anuncio:**

* **Llama a`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* La llamada `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

