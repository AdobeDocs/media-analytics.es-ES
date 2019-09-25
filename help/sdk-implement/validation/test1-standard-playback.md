---
seo-title: Prueba 1 Reproducción estándar
title: Test 1  Standard playback
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Prueba 1: Reproducción estándar{#test-standard-playback}

Este caso de prueba valida la reproducción general y la secuencia. It is a required element of your certification request.

## Formulario de solicitud de certificación

**Descargue el formulario de solicitud de certificación aquí: ==&gt;Formulario** de solicitud de [certificación.](cert_req_form.docx)

## Descripción general de la prueba de certificación 1

Las implementaciones de Media Analytics incluyen dos tipos de llamadas de seguimiento:
* Llamadas realizadas directamente al servidor de Adobe Analytics (AppMeasurement): estas llamadas se producen en los eventos "Media Start" y "Ad Start".
* Llamadas realizadas al servidor de Media Analytics (latidos), como llamadas dentro y fuera de banda:
   * En banda: el SDK envía llamadas de reproducción temporizadas o "pings" a intervalos de 10 segundos durante la reproducción del contenido y a intervalos de un segundo durante los anuncios.
   * Fuera de banda: estas llamadas pueden ocurrir en cualquier momento e incluyen Pausa, Almacenamiento en búfer, errores, finalización de contenido, finalización de publicidad, etc.

>[!NOTE]
>El seguimiento de medios se comporta igual en todas las plataformas.

## Test procedure

Complete y registre las siguientes acciones (en orden):

1. **Carga de la página o la aplicación**

   **Servidores de seguimiento** (para todos los sitios web y aplicaciones móviles):

   * **Adobe Analytics (AppMeasurement) server - An RDC tracking server or CNAME that resolves to an RDC tracking server is required for the Experience Cloud Visitor ID service.** The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats) server - This server always has the format "", where  specifies your company name.**`[namespace].hb.omtrdc.net``[namespace]` Este nombre lo proporciona Adobe.
   Debe validar ciertas variables clave que son universales en todas las llamadas de seguimiento:

   **`mid`ID de visitante de Adobe (**): La `mid` variable se utiliza para capturar el valor establecido en la cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Se encuentra en llamadas de Adobe Analytics (AppMeasurement) y de Media Analytics (latidos).

   * **Adobe Analytics Start call**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Llamada a la página del sitio web**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Llamada al ciclo vital**

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
      >En las llamadas de inicio de Media Analytics (`s:event:type=start`) es posible que no estén presentes los `mid` valores. Esto es correcto. They may not appear until the Media Analytics Play calls ( ).`s:event:type=play`

   * **Llamada de reproducción de Media Analytics**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Iniciar el reproductor de medios**

   When the media player starts, the Media SDK sends the key calls to the two servers in the following order:

   1. Adobe Analytics server - Start call
   1. Media Analytics server - Start call
   1. Media Analytics server - "Adobe Analytics Start call requested"
   The first two calls above contain additional metadata and variables. For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   The third call above tells the Media Analytics server that the Media SDK requested that the Adobe Analytics Start call () be sent to the Adobe Analytics server.`pev2=ms_s`

1. **Ver el salto de publicidad si está disponible**

   * **Inicio de publicidad**
   Cuando se inicia la publicidad, se envían las siguientes llamadas clave en el siguiente orden:

   1. Servidor de Adobe Analytics: llamada de inicio de anuncio
   1. Servidor de Media Analytics: llamada de inicio de anuncio
   1. Servidor de Media Analytics: "Se solicitó la llamada de inicio de anuncio de Adobe Analytics"
   Las dos primeras llamadas contienen metadatos y variables adicionales. Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   La tercera llamada indica al servidor de Media Analytics que el SDK de medios solicitó que la llamada de inicio de publicidad de Adobe Analytics (`pev2=msa_s`) se enviara al servidor de Adobe Analytics.

   * **Reproducción de publicidad**

      Durante la reproducción del anuncio, el SDK de Media Analytics envía eventos de reproducción de tipo "anuncio" al servidor de Media Analytics cada segundo.

   * **Finalización de publicidad**

      En el punto 100 % de un anuncio, se debe enviar una llamada de finalización de Media Analytics.



1. **Pausar la reproducción de la publicidad durante 30 segundos, si está disponible.**  **Pausa de publicidad**

   Durante la pausa de la publicidad, el SDK envía llamadas de ping o latidos de Media Analytics al servidor de Media Analytics cada segundo.

   >[!NOTE]
   >
   >The playhead value should remain constant during the pause.

   Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Reproducir el contenido principal durante 10 minutos sin interrupciones.**  **Reproducción de contenido**

   Durante la reproducción del contenido principal, el SDK de medios envía latidos (llamadas de reproducción) al servidor de Media Analytics cada 10 segundos.

   Notas:

   * La posición del cursor de reproducción debe aumentar en 10 con cada llamada de reproducción.
   * El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

      Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pausar la reproducción durante 30 segundos como mínimo.** Cuando el reproductor de medios está en pausa, el SDK enviará llamadas de evento de pausa al servidor de Media Analytics cada 10 segundos. Después de la pausa, los eventos de reproducción deben reanudarse.

   Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Buscar/eliminar medios.** Al eliminar el cursor de reproducción de medios, no se envían llamadas de seguimiento especiales; sin embargo, cuando se reanuda la reproducción de medios tras el desplazamiento, el valor del cursor de reproducción debe reflejar la nueva posición dentro del contenido principal.

1. **Reproducir medios (solo VOD).** When media is replayed, a new set of Media Start calls should be sent (as if it were a fresh start).

1. **Ver los siguientes medios en la lista de reproducción.** En el inicio de medios del siguiente medio de una lista de reproducción, se debe enviar un nuevo conjunto de llamadas de inicio de medios.

1. **Cambiar medios o flujo.** When switching live streams, a Media Analytics complete call for the first stream should not be sent. Las llamadas de inicio de medios y las llamadas de reproducción deben comenzar con el nuevo nombre del programa y del flujo, y con los valores de cabeza lectora y duración correctos para el nuevo programa.

