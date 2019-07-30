---
seo-title: Prueba 1 Reproducción estándar
title: Prueba 1 Reproducción estándar
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Prueba 1: Reproducción estándar{#test-standard-playback}

Este caso de prueba valida la reproducción y secuenciación general, y es obligatoria como parte del formulario de solicitud de certificación. Descargue el formulario de solicitud de certificación aquí:[ formulario de solicitud de certificación.](cert_req_form_nielsen.docx)

Las implementaciones de vídeo constan de los siguientes tipos de llamadas de seguimiento:
* Las llamadas de inicio de contenido y publicidad se envían directamente al servidor de AppMeasurement.
* Las llamadas de Hearttics de Media Analytics (MA) se envían al inicio y cada diez segundos al servidor de seguimiento de Adobe VA.

>[!NOTE]
>El seguimiento de vídeos funciona del mismo modo en todas las plataformas, equipos de escritorio y dispositivos móviles.

Debe completar y registrar las acciones en este orden:

1. **Carga de la página o la aplicación**

   **Servidores de seguimiento** (para todos los sitios web y aplicaciones móviles):

   * **AppMeasurement (Adobe Analytics)**: para el servicio de ID de visitantes de Experience Cloud es necesario un servidor de seguimiento RDC o CNAME que se resuelva en un servidor RDC. The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **Media Analytics (Latidos):** Este servidor siempre tiene el formato `[namespace].hb.omtrdc.net`, en el que `[namespace]` se define su empresa de inicio de sesión y es proporcionado por Adobe.
   Debe validar determinadas variables universales clave en todas las llamadas de seguimiento:

   **ID de visitante de Adobe (`mid`):** La `mid` variable se utiliza para capturar el valor establecido en la cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Se encuentra en llamadas de appmeasurement y Media Analytics (MA).

   * **Llamada de reproducción de Heartbeat**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Llamada de inicio de Media Analytics**

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

   * **Llamada inicial de Heartbeat**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `s:event:type` | start |

   * **Llamada de inicio de VA**

      >[!NOTE]
      >
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. Esto es correcto. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `pev2` | ms_s |


1. **Inicio del reproductor de vídeo**

   Cuando se inicia el reproductor de vídeo, las llamadas clave se envían en el siguiente orden:

   1. Inicio de análisis de vídeo
   1. Inicio de Heartbeat
   1. Inicio del análisis de Heartbeat
   Las dos primeras llamadas de arriba contienen metadatos y variables adicionales. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **Ver el salto de publicidad si está disponible**

   * **Inicio de publicidad**
   Cuando se inicia la publicidad de vídeo, se envían estas llamadas clave en el siguiente orden:

   1. Inicio de análisis de publicidad de vídeo
   1. Inicio de publicidad de Heartbeat
   1. Inicio del análisis de publicidad de Heartbeat
   Las dos primeras llamadas contienen metadatos y variables adicionales. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Reproducción de publicidad**

      Durante la reproducción de publicidad, las llamadas de Heartbeat se envían al servidor Heartbeat cada segundo.

   * **Finalización de publicidad**

      Al 100 % de la publicidad del vídeo, se enviará una llamada de finalización de Heartbeat.



1. **Pausar la reproducción de la publicidad durante 30 segundos, si está disponible.**  **Pausa de publicidad**

   Durante la pausa de publicidad, las llamadas de Heartbeat se envían al servidor Heartbeat cada segundo.

   >[!NOTE]
   >
   >El valor del cursor de reproducción debe permanecer constante durante la pausa.

1. **Reproducir el contenido principal del vídeo durante 10 minutos sin pausarlo.** **Reproducción de contenido **

   Durante la reproducción de contenido principal normal, las llamadas de Heartbeat se envían al servidor cada diez segundos.

   Notas:

   * La posición del cabezal de reproducción debe aumentarse en 10 unidades con cada llamada de reproducción.
   * El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

      For call parameters and metadata, see [Test call details](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **Pausar la reproducción durante 30 segundos como mínimo.** Con el reproductor en pausa, las llamadas de evento de pausa se enviarán cada 10 segundos. Después de la pausa, los eventos de reproducción deben reanudarse.

1. **Arrastrar el cabezal de reproducción/llamar a otro punto de un vídeo.** Al arrastrar el cabezal de reproducción de vídeo, no se envían llamadas de seguimiento especiales, sin embargo, cuando la reproducción de vídeo se reanuda tras el desplazamiento, el valor debe reflejar la nueva posición dentro del contenido principal.

1. **Reproducir el vídeo (solo VOD).** Cuando se reproduce un vídeo, se debe enviar un nuevo conjunto de llamadas al inicio de vídeo, como si se tratara de una nueva visualización.

1. **Ver el vídeo siguiente en la lista de reproducción.** Al inicio del siguiente vídeo de una lista de reproducción, se debe enviar un nuevo conjunto de llamadas de inicio de vídeo.

1. **Cambiar el vídeo o la emisión.** Al cambiar de emisión en directo, no se debe enviar una llamada de finalización de Heartbeat para la primera emisión. Las llamadas de inicio y reproducción de vídeo deben comenzar con el nombre de la nueva emisión y con los valores correctos para el cabezal de reproducción y duración de la emisión.

