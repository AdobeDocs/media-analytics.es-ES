---
title: Seguimiento de anuncios
description: Información general sobre la implementación del seguimiento de anuncios con Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# Seguimiento de anuncios

El seguimiento de reproducción de publicidad cubre las pausas publicitarias y los inicios, finalizaciones y omisiones de publicidad. Utilice la API del reproductor de contenido para identificar eventos clave del reproductor y rellenar las variables de publicidad necesarias.

## Eventos del reproductor

| Evento del reproductor | Acción |
| --- | --- |
| Inicio de pausa publicitaria | Crear objeto de pausa publicitaria; llamar a AdBreakStart |
| Inicio del anuncio | Crear objeto de anuncio; llamar a AdStart |
| Anuncio completado | Llamar a AdComplete |
| Omisión de publicidad | Llamar a AdSkip |
| Pausa publicitaria completa | Llamar a AdBreakComplete |

## Pasos de implementación

1. Identifique cuándo comienza la zona de salto de anuncio, incluido el anuncio previo a la emisión, y cree un objeto de pausa publicitaria. Consulte [Nombre de la pausa publicitaria](/help/implementation/variables/ads/ad-break-name.md) y [Hora de inicio de la pausa publicitaria](/help/implementation/variables/ads/ad-break-start-time.md) para ver las definiciones de los campos.
1. Invoque [Inicio de la pausa publicitaria](/help/implementation/events/ads/ad-break-start.md) para iniciar el seguimiento de esta.
1. Identifique cuándo se inicia el anuncio y cree un objeto de anuncio. Consulte [Nombre del anuncio](/help/implementation/variables/ads/ad-name.md), [ID del anuncio](/help/implementation/variables/ads/ad-id.md), [Duración del anuncio](/help/implementation/variables/ads/ad-length.md), [Posición del anuncio en el pod](/help/implementation/variables/ads/ad-in-pod-position.md) y [Nombre del reproductor del anuncio](/help/implementation/variables/ads/ad-player-name.md) para ver las definiciones de los campos.
1. Opcionalmente, se pueden adjuntar metadatos de publicidad estándar. Consulte [Anunciante](/help/implementation/variables/ads/advertiser.md), [ID de campaña](/help/implementation/variables/ads/campaign-id.md), [ID de Creative](/help/implementation/variables/ads/creative-id.md), [URL de Creative](/help/implementation/variables/ads/creative-url.md), [ID de ubicación](/help/implementation/variables/ads/placement-id.md) e [ID de sitio](/help/implementation/variables/ads/site-id.md) para ver las claves disponibles.
1. Llama a [Inicio del anuncio](/help/implementation/events/ads/ad-start.md) para iniciar el seguimiento del anuncio.
1. Cuando el anuncio se reproduzca hasta su finalización, llame a [Finalización de anuncio](/help/implementation/events/ads/ad-complete.md).
1. Si el visor omitió el anuncio, llama a [Ad skip](/help/implementation/events/ads/ad-skip.md) en lugar de a Ad complete.
1. Para anuncios adicionales en la misma pausa publicitaria, repita los pasos del 3 al 7.
1. Cuando finalice la pausa publicitaria, llama a [Finalización de la pausa publicitaria](/help/implementation/events/ads/ad-break-complete.md).

>[!IMPORTANT]
>
>**Anuncios previos a la emisión: no llame a `trackPlay` antes de `AdBreakStart` y `AdStart`.** El primer ping de `play` en el contenido principal incrementa [El contenido comienza](/help/reporting/metrics/content-starts.md). Si se llama a `trackPlay` antes de que se desencadenen los eventos de anuncio previo a la emisión y el visor se cierra durante la publicidad, el contenido se incrementa aunque nunca se haya reproducido ningún contenido principal. En los casos de anuncio previo a la emisión, se debe retrasar `trackPlay` hasta que se hayan enviado `AdBreakStart` y `AdStart`.

>[!NOTE]
>
>El valor del cabezal de reproducción registrado durante la reproducción del anuncio representa la posición del visor dentro del **contenido principal**, no dentro del anuncio. En el caso de un anuncio previo a la emisión que precede a un vídeo de 10 minutos, el cabezal de reproducción es `0` en todo el anuncio. Para un anuncio mid-roll que comienza en la marca de 5 minutos, el cabezal de reproducción permanece en `300` (segundos) durante la duración del anuncio.

## Problemas comunes

### Llamadas principales :play inesperadas entre anuncios

Si ve llamadas de `main:play` que se producen entre anuncios consecutivos, existe un intervalo de más de 250 milisegundos entre la llamada de AdComplete y la siguiente llamada de AdStart. Cuando se produce este hueco, Media SDK vuelve a enviar pings de contenido principal, lo que puede establecer la métrica Inicio del contenido anticipado para escenarios de anuncio previo a la emisión.

**Causa:** Media SDK no tiene información de publicidad establecida y el reproductor está en estado de reproducción, por lo que acredita la duración del espacio al contenido principal.

**Resolución:** Retrasa la llamada de AdComplete para cada anuncio (excepto el último) en lugar de llamarlo inmediatamente cuando finalice el anuncio. Realice las llamadas por lotes de la siguiente manera:

- En cada **inicio del anuncio**: Si existe un anuncio anterior y aún no se ha marcado como completado, llame a AdComplete *antes* de llamar a AdStart para el anuncio nuevo.
- En cada **fin del recurso publicitario**: no llame a AdComplete inmediatamente, aplace el proceso.
- Al **finalizar la pausa publicitaria**: Invoque AdComplete para el último anuncio (si aún no se ha llamado) y después Invoque AdBreakComplete.

Este patrón garantiza que AdComplete y el siguiente AdStart se activen de forma consecutiva, lo que elimina cualquier brecha.
