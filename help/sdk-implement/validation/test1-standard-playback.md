---
seo-title: Prueba 1 Reproducción estándar
title: Prueba 1 Reproducción estándar
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Prueba 1: Reproducción estándar{#test-standard-playback}

Este caso de prueba valida la reproducción y secuenciación generales. Es obligatorio como parte del Formulario de solicitud de certificación.

**Descargue aquí el formulario de solicitud de certificación: = = &gt;**  [Formulario de solicitud de certificación.](cert_req_form.docx)

Las implementaciones de medios están compuestas de los siguientes tipos de llamadas de seguimiento:
* Las llamadas de inicio de publicidad y de publicidad se envían directamente al servidor de appmeasurement (Adobe Analytics).
* Las llamadas de Heartbeat de Media Analytics se envían al inicio y cada diez segundos (para el contenido) o un segundo (para las publicidades) al servidor de seguimiento de Media Analytics.

>[!NOTE]
>El seguimiento de medios se comporta de la misma manera en todas las plataformas.

Debe completar y registrar estas acciones en el orden siguiente:

1. **Carga de la página o la aplicación**

   **Servidores de seguimiento** (para todos los sitios web y aplicaciones móviles):

   * **Appmeasurement (Adobe Analytics):** el servicio de ID de visitante de Experience Cloud requiere un servidor de seguimiento RDC o CNAME que responde a un servidor de seguimiento RDC. The Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Latidos):** Este servidor siempre tiene el formato "`[namespace].hb.omtrdc.net`, donde `[namespace]` especifica el nombre de su empresa. Este nombre lo proporciona Adobe.
   Debe validar ciertas variables clave que son universales en todas las llamadas de seguimiento:

   **ID de visitante de Adobe (`mid`):** La `mid` variable se utiliza para capturar el valor establecido en la cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Se encuentra en llamadas de appmeasurement y de Media Analytics.

   * **Llamada de reproducción de Media Analytics**

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
      >On VA Start Calls (`s:event:type=start`) the `mid` values may not be present. Esto es correcto. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `pev2` | ms_s |


1. **Iniciar el reproductor de medios**

   Cuando se inicia el reproductor de medios, las llamadas clave se envían en el orden siguiente:

   1. Inicio de análisis de medios
   1. Inicio de Heartbeat
   1. Inicio del análisis de Heartbeat
   Las dos primeras llamadas de arriba contienen metadatos y variables adicionales. Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md)

1. **Ver el salto de publicidad si está disponible**

   * **Inicio de publicidad**
   Cuando se inicia el anuncio de medios, se envían las siguientes llamadas clave en el orden siguiente:

   1. Inicio de análisis de publicidad de medios
   1. Inicio de publicidad de Heartbeat
   1. Inicio del análisis de publicidad de Heartbeat
   Las dos primeras llamadas contienen metadatos y variables adicionales. Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Reproducción de publicidad**

      Durante la reproducción de publicidad, las llamadas de Heartbeat se envían al servidor Heartbeat cada segundo.

   * **Finalización de publicidad**

      En el punto 100% de una publicidad de medios, se enviará una llamada de finalización de Heartbeat.



1. **Pausar la reproducción de la publicidad durante 30 segundos, si está disponible.**  **Pausa de publicidad**

   Durante la pausa de publicidad, las llamadas de Heartbeat se envían al servidor Heartbeat cada segundo.

   >[!NOTE]
   >
   >El valor del cursor de reproducción debe permanecer constante durante la pausa.

1. **Reproducir contenido principal de contenido durante 10 minutos sin interrupciones.**  **Reproducción de contenido**

   Durante la reproducción del contenido principal, las llamadas de Heartbeat se envían al servidor de Media Analytics cada diez segundos.

   Notas:

   * La posición del cabezal de reproducción debe aumentarse en 10 unidades con cada llamada de reproducción.
   * El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

      Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **Pausar la reproducción durante 30 segundos como mínimo.** Al pausar el reproductor multimedia, las llamadas de pausa del evento se enviarán cada 10 segundos. Después de la pausa, los eventos de reproducción deben reanudarse.

1. **Buscar o anular los medios.** Sin embargo, al anular el cursor de reproducción de medios, no se envían llamadas de seguimiento especiales cuando se reanuda la reproducción de medios tras la anulación del valor del cursor de reproducción debe reflejar la nueva posición dentro del contenido principal.

1. **Reproducir medios (solo VOD).** Cuando se reproduzca el medio, se enviará un nuevo conjunto de llamadas de inicio de medios, como si se tratara de una vista de medios nueva.

1. **Vea los medios siguientes en la lista de reproducción.** Al iniciar medios del siguiente medio en una lista de reproducción, se debe enviar un nuevo conjunto de llamadas de inicio de medios.

1. **Cambiar medios o flujos.** Al cambiar de emisión en directo, no se debe enviar una llamada de finalización de Heartbeat para la primera emisión. Las llamadas de inicio de medios y de reproducción de medios deberían comenzar con la nueva visualización y el nombre de flujo y con los valores de reproducción y cabeza lectora correctos para la nueva visualización.

