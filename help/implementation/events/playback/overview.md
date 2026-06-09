---
title: Seguimiento de reproducción
description: Obtenga información acerca de los eventos de reproducción y cómo implementar el seguimiento de cambios de reproducción, pausa, búfer, ping y velocidad de bits.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 2%

---


# Seguimiento de reproducción

Los eventos de reproducción rastrean las transiciones de estado en el reproductor de contenidos a lo largo de una sesión. Constituyen el núcleo del flujo de eventos y se aplican a cualquier tipo de contenido.

## Eventos del reproductor

| Evento del reproductor | Acción |
| --- | --- |
| Reproducciones o reanudaciones de contenido | Llamar a reproducción |
| Pausas de medios | Inicio de pausa de llamada |
| Comienza el almacenamiento en búfer | Inicio del búfer de llamadas |
| Finaliza el almacenamiento en búfer | Llamar a reproducción |
| Cambios de velocidad de bits | Cambio de velocidad de bits de llamada |
| Activador de temporizador | Llamar a ping |

## Pasos de implementación

1. **Llamar a [Reproducir](play.md)** después del [inicio de la sesión](../session/session-start.md) cuando el primer fotograma de contenido aparece en pantalla. Envíe también Reproducir cuando la reproducción se reanude después de una pausa o detención del búfer. No hay ningún evento de reanudación independiente.
1. **Invocar a [Pausar inicio](pause-start.md)** cuando el usuario pausa la reproducción. Enviar Reproducir cuando se reanude la reproducción.
1. **Invocar a [Inicio del búfer](buffer-start.md)** cuando el reproductor se detenga a la espera de datos. En las API basadas en XDM, el final del búfer se infiere al enviar el siguiente evento de reproducción. En Mobile SDK, llame también a `BufferComplete` explícitamente cuando se resuelva el almacenamiento en búfer.
1. **Llamar a [ping](ping.md)** cada 10 segundos durante la reproducción del contenido principal y cada 1 segundo durante la reproducción del anuncio. Ping mantiene viva la sesión y registra el movimiento del cabezal de reproducción. Los SDK móviles envían pings automáticamente; el resto de plataformas deben enviarlos manualmente.
1. **Invocar a [cambio de velocidad de bits](bitrate-change.md)** cada vez que el reproductor negocie una nueva velocidad de bits. Incluya los datos actuales de QoE (velocidad de bits, fotogramas por segundo, fotogramas perdidos) para que el backend pueda calcular [Velocidad de bits media](/help/reporting/metrics/average-bitrate.md) y las métricas de calidad relacionadas.
