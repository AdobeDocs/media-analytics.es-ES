---
title: Prueba 1 Reproducción estándar
description: Obtenga información sobre la prueba de reproducción estándar utilizada en la validación.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 99%

---

# Prueba 1: Reproducción estándar {#test-standard-playback}

Este caso de prueba valida la reproducción y la secuencia general.

Las implementaciones de Media Analytics incluyen dos tipos de llamadas de seguimiento:
* Llamadas realizadas directamente al servidor de Adobe Analytics (AppMeasurement): Estas llamadas se producen en los eventos “Inicio de contenidos” e “Inicio de anuncios”.
* Llamadas realizadas al servidor de Media Analytics (latidos), como llamadas dentro y fuera de banda:
   * En banda: El SDK envía llamadas de reproducción temporizadas o “pings” a intervalos de 10 segundos durante la reproducción del contenido y a intervalos de un segundo durante los anuncios.
   * Fuera de banda: Estas llamadas pueden ocurrir en cualquier momento e incluyen Pausa, Almacenamiento en búfer, errores, finalización de contenido, finalización de publicidad, etc.

>[!NOTE]
>El seguimiento de contenidos funciona igual en todas las plataformas.

## Procedimiento de prueba

Complete y registre las siguientes acciones (en orden):

1. **Carga de la página o la aplicación**

   **Servidores de seguimiento** (para todos los sitios web y aplicaciones móviles):

   * **Servidor de Adobe Analytics (AppMeasurement):** Para el servicio de ID de visitantes de Experience Cloud es necesario un servidor de seguimiento RDC o CNAME que se resuelva en un servidor RDC. El servidor de seguimiento de Adobe Analytics debe finalizar en “`.sc.omtrdc.net`” o ser CNAME.

   * **Servidor de Media Analytics (latidos):** Este servidor siempre tiene el formato “`[namespace].hb.omtrdc.net`”, donde `[namespace]` especifica el nombre de la empresa. Este nombre lo proporciona Adobe.

   Debe validar ciertas variables clave que son universales en todas las llamadas de seguimiento:

   **ID de visitante de Adobe (`mid`):** La variable `mid` se utiliza para capturar el valor establecido en la cookie AMCV. La variable `mid` es el valor de identificación principal para sitios web y aplicaciones móviles, e indica que el servicio de ID de visitantes de Experience Cloud se ha configurado correctamente. Se encuentra en llamadas de Adobe Analytics (AppMeasurement) y de Media Analytics (latidos).

   * **Llamada de inicio de Adobe Analytics**

     | Parámetro | Valor (ejemplo) |
     |---|---|
     | `pev2` | ms_s |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Llamada de página de sitio web**

     | Parámetro | Valor (ejemplo) |
     |---|---|
     | `mid` | 30250035503789876473484580554595324209 |

   * **Llamada de ciclo de vida**

     | Parámetro | Valor (ejemplo) |
     |---|---|
     | `pev2` | ADBINTERNAL:Lifecycle |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Llamada de inicio de Media Analytics**

     | Parámetro | Valor (ejemplo) |
     |---|---|
     | `s:event:type` | start |

     >[!NOTE]
     >
     >En las llamadas de inicio de Media Analytics (`s:event:type=start`) es posible que no estén presentes los valores `mid`. Esto es correcto. Es posible que no aparezcan hasta que se realicen las llamadas de reproducción de Media Analytics (`s:event:type=play`).

   * **Llamada de reproducción de Media Analytics**

     | Parámetro | Valor (ejemplo) |
     |---|---|
     | `s:event:type` | play |
     | `s:user:mid` | 30250035503789876473484580554595324209 |

1. **Iniciar el reproductor de contenidos**

   Cuando se inicia el reproductor de contenido, Media SDK envía las llamadas clave a los dos servidores en el siguiente orden:

   1. Servidor de Adobe Analytics: Llamada de inicio
   1. Servidor de Media Analytics: Llamada de inicio
   1. Servidor de Media Analytics: “Se ha solicitado la llamada de inicio de Adobe Analytics”

   Las dos primeras llamadas descritas contienen metadatos y variables adicionales. Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   La tercera llamada descrita indica al servidor de Media Analytics que Media SDK solicitó que la llamada de inicio (`pev2=ms_s`) de Adobe Analytics se enviara al servidor de Adobe Analytics.

1. **Ver el salto de publicidad si está disponible**

   * **Inicio de publicidad**

   Cuando se inicia el anuncio, se envían estas llamadas clave en el siguiente orden:

   1. Servidor de Adobe Analytics: Llamada de inicio del anuncio
   1. Servidor de Media Analytics: Llamada de inicio del anuncio
   1. Servidor de Media Analytics: “Se ha solicitado la llamada de inicio del anuncio de Adobe Analytics”

   Las dos primeras llamadas contienen metadatos y variables adicionales. Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#view-ad-playback)

   La tercera llamada indica al servidor de Media Analytics que Media SDK solicitó que la llamada de inicio de publicidad de Adobe Analytics (`pev2=msa_s`) se enviara al servidor de Adobe Analytics.

   * **Reproducción de publicidad**

     Durante la reproducción del anuncio, el SDK de Media Analytics envía eventos de reproducción de tipo “anuncio” al servidor de Media Analytics cada segundo.

   * **Finalización de publicidad**

     Al 100 % de la reproducción de la publicidad, se enviará una llamada de finalización de Media Analytics.

1. **Pausar la reproducción de la publicidad durante 30 segundos, si está disponible.** **Pausa de publicidad**

   Durante la pausa de la publicidad, el SDK envía llamadas de “ping” o latidos de Media Analytics al servidor de Media Analytics cada segundo.

   >[!NOTE]
   >
   >El valor del cabezal de reproducción debe permanecer constante durante la pausa.

   Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)

1. **Reproduce el contenido principal durante 10 segundos ininterrumpidos.** **Reproducción de contenido**

   Durante la reproducción del contenido principal, Media SDK envía latidos (llamadas de reproducción) al servidor de Media Analytics cada 10 segundos.

   Notas:

   * La posición del cabezal de reproducción debe aumentarse en 10 unidades con cada llamada de reproducción.
   * El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

     Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Pausar la reproducción durante 30 segundos como mínimo.** Cuando el reproductor de contenidos está en pausa, el SDK enviará llamadas de evento de pausa al servidor de Media Analytics cada 10 segundos. Después de la pausa, los eventos de reproducción deben reanudarse.

   Para ver los parámetros y metadatos de la llamada, consulte [Detalles de la llamada de prueba.](/help/legacy/validation/test-call-details.md#pause-main-content)

1. **Buscar/eliminar contenidos.** Al arrastrar el cabezal de reproducción de contenidos, no se envían llamadas de seguimiento especiales, sin embargo, cuando la reproducción de los contenidos se reanuda tras el desplazamiento, el valor debe reflejar la nueva posición dentro del contenido principal.

1. **Reproducir contenidos (solo VOD).** Cuando se reproduce contenido multimedia, se debe enviar un nuevo conjunto de llamadas de inicio de contenidos (como si fuera un nuevo comienzo).

1. **Ver el contenido siguiente en la lista de reproducción.** Al inicio del siguiente contenido de una lista de reproducción, se debe enviar un nuevo conjunto de llamadas de inicio de contenido.

1. **Cambiar contenido o flujo.** Al cambiar de emisión en directo, no se debe enviar una llamada de finalización de Media Analytics para la primera emisión. Las llamadas de inicio y reproducción de contenidos deben comenzar con el nombre de la nueva emisión y con los valores correctos para el cabezal de reproducción y duración de la emisión.
