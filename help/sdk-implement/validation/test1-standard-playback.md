---
title: Prueba 1 Reproducción estándar
description: En este tema se describe la prueba de reproducción estándar utilizada en la validación.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Prueba 1: Reproducción estándar{#test-standard-playback}

Este caso de prueba valida la reproducción general y la secuencia. Es un elemento requerido de su solicitud de certificación.

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

## Procedimiento de ensayo

Complete y registre las siguientes acciones (en orden):

1. **Carga de la página o la aplicación**

   **Servidores de seguimiento** (para todos los sitios web y aplicaciones móviles):

   * **Servidor de Adobe Analytics (AppMeasurement):** se requiere un servidor de seguimiento RDC o un CNAME que se resuelva en un servidor de seguimiento RDC para el servicio de ID de visitante de Experience Cloud. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Servidor de Media Analytics (latidos) -** Este servidor siempre tiene el formato "`[namespace].hb.omtrdc.net`", donde `[namespace]` especifica el nombre de la empresa. Este nombre lo proporciona Adobe.
   Debe validar ciertas variables clave que son universales en todas las llamadas de seguimiento:

   **`mid`ID de visitante de Adobe (**): La `mid` variable se utiliza para capturar el valor establecido en la cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Se encuentra en llamadas de Adobe Analytics (AppMeasurement) y de Media Analytics (latidos).

   * **Llamada de inicio de Adobe Analytics**

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
      >En las llamadas de inicio de Media Analytics (`s:event:type=start`) es posible que no estén presentes los `mid` valores. Esto es correcto. Es posible que no aparezcan hasta que las llamadas de reproducción de Media Analytics ( `s:event:type=play`).

   * **Llamada de reproducción de Media Analytics**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Iniciar el reproductor de medios**

   Cuando se inicia el reproductor de medios, el SDK de medios envía las llamadas clave a los dos servidores en el siguiente orden:

   1. Servidor de Adobe Analytics: Iniciar llamada
   1. Servidor de Media Analytics: Iniciar llamada
   1. Servidor de Media Analytics: "Se solicitó la llamada de inicio de Adobe Analytics"
   Las dos primeras llamadas anteriores contienen metadatos y variables adicionales. Para ver los parámetros y metadatos de la llamada, consulte Detalles [de la llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La tercera llamada anterior indica al servidor de Media Analytics que el SDK de medios solicitó que la llamada de inicio (`pev2=ms_s`) de Adobe Analytics se enviara al servidor de Adobe Analytics.

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
   >El valor del cursor de reproducción debe permanecer constante durante la pausa.

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

1. **Reproducir medios (solo VOD).** Cuando se reproduce el contenido multimedia, se debe enviar un nuevo conjunto de llamadas de inicio de medios (como si fuera un nuevo comienzo).

1. **Ver los siguientes medios en la lista de reproducción.** En el inicio de medios del siguiente medio de una lista de reproducción, se debe enviar un nuevo conjunto de llamadas de inicio de medios.

1. **Cambiar medios o flujo.** Al cambiar flujos en directo, no se debe enviar una llamada completa de Media Analytics para el primer flujo. Las llamadas de inicio de medios y las llamadas de reproducción deben comenzar con el nuevo nombre del programa y del flujo, y con los valores de cabeza lectora y duración correctos para el nuevo programa.

