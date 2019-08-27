---
seo-title: Prueba 1 Reproducción estándar
title: Prueba 1 Reproducción estándar
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Prueba 1: Reproducción estándar{#test-standard-playback}

Este caso de prueba valida la reproducción y secuenciación generales. Es un elemento requerido de la solicitud de certificación.

## Formulario de solicitud de certificación

**Descargue aquí el formulario de solicitud de certificación: = = &gt;**  [Formulario de solicitud de certificación.](cert_req_form.docx)

## Información general de la prueba de certificación 1

Las implementaciones de Media Analytics incluyen dos tipos de llamadas de seguimiento:
* Llamadas realizadas directamente al servidor de Adobe Analytics (appmeasurement): estas llamadas se producen en los eventos «Inicio de medios» y «Inicio de anuncio».
* Llamadas realizadas al servidor de Media Analytics (latidos): incluyen llamadas en banda y fuera de banda:
   * En banda: El SDK envía llamadas de reproducción temporizadas o «pings» a intervalos de 10 segundos durante la reproducción del contenido y en intervalos de un segundo durante las publicidades.
   * Fuera de banda: Estas llamadas pueden suceder en cualquier momento e incluyen Pausa, Almacenamiento en búfer, errores, finalización de contenido, finalización de publicidad, etc.

>[!NOTE]
>El seguimiento de medios se comporta de la misma manera en todas las plataformas.

## Procedimiento de prueba

Complete y registre las siguientes acciones (en orden):

1. **Carga de la página o la aplicación**

   **Servidores de seguimiento** (para todos los sitios web y aplicaciones móviles):

   * **Servidor de Adobe Analytics (appmeasurement):** el servicio de ID de visitante de Experience Cloud requiere un servidor de seguimiento RDC o CNAME que responde a un servidor de seguimiento RDC. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Servidor de Media Analytics (Latidos):** Este servidor siempre tiene el formato "`[namespace].hb.omtrdc.net`, donde `[namespace]` especifica el nombre de su empresa. Este nombre lo proporciona Adobe.
   Debe validar ciertas variables clave que son universales en todas las llamadas de seguimiento:

   **ID de visitante de Adobe (`mid`):** La `mid` variable se utiliza para capturar el valor establecido en la cookie AMCV. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Se encuentra en llamadas de Adobe Analytics (appmeasurement) y Media Analytics (latidos).

   * **Llamada de inicio de Adobe Analytics**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Llamada a página del sitio Web**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Llamada del ciclo vital**

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
      >En las llamadas de inicio de Media Analytics (`s:event:type=start`), es posible que `mid` los valores no estén presentes. Esto es correcto. Es posible que no aparezcan hasta que Media Analytics Play ( `s:event:type=play`).

   * **Llamada de reproducción de Media Analytics**

      | Parámetro | Valor (ejemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Iniciar el reproductor de medios**

   Cuando se inicia el reproductor de medios, el SDK multimedia envía las llamadas clave a los dos servidores en el orden siguiente:

   1. Servidor de Adobe Analytics: llamada de inicio
   1. Servidor de Media Analytics: llamada de inicio
   1. Servidor de Media Analytics: "Llamada de inicio de Adobe Analytics"
   Las dos primeras llamadas de arriba contienen metadatos y variables adicionales. Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   La tercera llamada anterior indica al servidor de Media Analytics que el SDK de medios ha solicitado que la llamada de inicio de Adobe Analytics (`pev2=ms_s`) se envíe al servidor de Adobe Analytics.

1. **Ver el salto de publicidad si está disponible**

   * **Inicio de publicidad**
   Cuando se inicia la publicidad, se envían las siguientes llamadas clave en el orden siguiente:

   1. Servidor de Adobe Analytics: llamada de inicio de anuncio
   1. Servidor de Media Analytics: llamada de inicio de anuncio
   1. Servidor de Media Analytics: "Llamada de inicio de anuncio de Adobe Analytics"
   Las dos primeras llamadas contienen metadatos y variables adicionales. Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   La tercera llamada indica al servidor de Media Analytics que el SDK de medios solicitó que la llamada de inicio de anuncio de Adobe Analytics (`pev2=msa_s`) se envíe al servidor de Adobe Analytics.

   * **Reproducción de publicidad**

      Durante la reproducción del anuncio, el SDK de Media Analytics envía eventos de reproducción de tipo "ad" al servidor de Media Analytics cada segundo.

   * **Finalización de publicidad**

      En el punto del 100% de una publicidad, se debe enviar una llamada de finalización de Media Analytics.



1. **Pausar la reproducción de la publicidad durante 30 segundos, si está disponible.**  **Pausa de publicidad**

   Durante la pausa publicitaria, el SDK envía las llamadas de Heartbeat o «ping» de Media Analytics al servidor de Media Analytics cada segundo.

   >[!NOTE]
   >
   >El valor del cursor de reproducción debe permanecer constante durante la pausa.

   Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Reproducir contenido principal durante 10 minutos sin interrupciones.**  **Reproducción de contenido**

   Durante la reproducción del contenido principal, el SDK de medios envía latidos (llamadas de reproducción) al servidor de Media Analytics cada 10 segundos.

   Notas:

   * La posición del cursor de reproducción debe incrementarse en 10 con cada llamada de reproducción.
   * El valor `l:event:duration` representa el número de milisegundos desde la última llamada de seguimiento y debe ser aproximadamente el mismo valor en cada llamada de 10 segundos.

      Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pausar la reproducción durante 30 segundos como mínimo.** Al pausar el reproductor multimedia, el SDK enviará las llamadas de evento pause al servidor de Media Analytics cada 10 segundos. Después de la pausa, los eventos de reproducción deben reanudarse.

   Para ver los parámetros de llamada y los metadatos, consulte [Detalles de llamada de prueba.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Buscar o anular los medios.** Sin embargo, al anular el cursor de reproducción de medios, no se envían llamadas de seguimiento especiales. Sin embargo, cuando se reanuda la reproducción de medios después de la anulación, el valor del cursor de reproducción debe reflejar la nueva posición dentro del contenido principal.

1. **Reproducir medios (solo VOD).** Cuando se reproduzca el medio, se enviará un nuevo conjunto de llamadas de inicio de Media (como si se tratara de un inicio nuevo).

1. **Vea los medios siguientes en la lista de reproducción.** En el Inicio de medios del siguiente medio de una lista de reproducción, se debe enviar un nuevo conjunto de llamadas de Inicio de medios.

1. **Cambiar medios o flujos.** Al cambiar los flujos en directo, no se debe enviar una llamada completa de Media Analytics para el primer flujo. Las llamadas de inicio de medios y de reproducción deberían comenzar con la nueva presentación y el nombre de flujo, y con los valores de reproducción y cabeza lectora correctos para la nueva visualización.

