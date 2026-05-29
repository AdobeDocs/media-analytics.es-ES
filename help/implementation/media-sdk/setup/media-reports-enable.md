---
title: Habilitación de informes de contenidos
description: Obtenga información acerca del grupo de informes multimedia que recopila métricas de medios.  Siga estos pasos para configurar los informes de medios antes de enviar los datos de medios.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 20%

---

# Habilitación de informes de contenidos

Para enviar datos sobre los contenidos, es necesario configurar todos los grupos de informes que recopilan métricas de contenidos.

1. En [Adobe Analytics](https://experience.adobe.com/analytics), vaya a **[!UICONTROL Administrador]** → **[!UICONTROL Grupos de informes]**.
1. Seleccione los grupos de informes que recopilan datos de medios. Seleccione **[!UICONTROL Editar configuración]** → **[!UICONTROL Administración de medios]** → **[!UICONTROL Informes de medios]**.

   ![Captura de pantalla del menú del administrador de grupos de informes](assets/media-reporting.png)

1. En la página **[!UICONTROL Informes de medios]**, habilite los componentes de medios de transmisión deseados (ver a continuación).

1. Seleccionar **[!UICONTROL Guardar].**

   Si este grupo de informes ya está configurado para recopilar datos de contenidos, después de hacer clic en **[!UICONTROL Guardar]**, aparecerá una página de configuración adicional. Si ve la página **[!UICONTROL Medición de Componentes básicos de contenidos]**, continúe con el siguiente paso.

## Módulos de medios de streaming disponibles

La medición de contenidos incluye los siguientes módulos:

* **[!UICONTROL Componentes básicos de medios]**: Necesario para todo el seguimiento de medios de transmisión. Reserva variables de solución para la reproducción de contenido y los datos de sesión.
   * **Dimensiones:**
      * [[!UICONTROL Contenido]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL Canal de contenido]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL Longitud del contenido (variable)]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL Nombre de contenido (variable)]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL Nombre del reproductor de contenido]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL Segmento de contenido]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL Tipo de contenido]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL Ruta de medios]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL ID de sesión de medios]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL Tipo de emisión]](/help/reporting/dimensions/stream-type.md)
   * **Métricas:**
      * [[!UICONTROL Público medio por minuto]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL Contenido finalizado]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL Reanudación del contenido]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL Vistas de segmentos de contenido]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL El contenido comienza]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL Comienzos de medios]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL Pausar eventos]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL Flujos afectados por la pausa]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL Marcadores de progreso]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL Duración total de la pausa]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL Tiempo único reproducido]](/help/reporting/metrics/unique-time-played.md)
* **[!UICONTROL Anuncios multimedia]**: habilita el seguimiento de anuncios dentro del contenido multimedia.
   * **Dimensiones:**
      * [[!UICONTROL Anuncio]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL Posición del anuncio en la secuencia]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL Longitud del anuncio (variable)]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL Nombre del anuncio (variable)]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL Nombre del reproductor del anuncio]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL pod de anuncios]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL Anunciante]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL ID de campaña]](/help/reporting/dimensions/campaign-id.md)
   * **Dimensiones de clasificación:**
      * [[!UICONTROL ID de recurso]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL Clasificación del contenido]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL ID. DE Creative]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL Primera fecha de emisión]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL Primera fecha digital]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL Nombre de la secuencia]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Posición de la secuencia]](/help/reporting/dimensions/pod-position.md)
   * **Métricas:**
      * [[!UICONTROL Finalización del anuncio]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL El anuncio comienza]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL Tiempo invertido en publicidad]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL Tiempo invertido en contenido]](/help/reporting/metrics/media-time-spent.md)
* **[!UICONTROL Capítulos multimedia]**: Habilita el seguimiento de capítulos dentro del contenido multimedia.
   * **Dimension:**
      * [[!UICONTROL Capítulo]](/help/reporting/dimensions/chapter.md)
   * **Dimensiones de clasificación:**
      * [[!UICONTROL Longitud del capítulo]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL Nombre de capítulo]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL Desplazamiento de capítulo]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL Posición del capítulo]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL Creador]](/help/reporting/dimensions/originator.md)
   * **Métricas:**
      * [[!UICONTROL El capítulo finaliza]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL El capítulo comienza]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL Tiempo invertido en el capítulo]](/help/reporting/metrics/chapter-time-spent.md)
* **[!UICONTROL Calidad de los medios]**: Habilita el seguimiento de los datos de calidad de la reproducción, incluidos los eventos de almacenamiento en búfer, velocidad de bits y error.
   * **Dimensiones:**
      * [[!UICONTROL Velocidad de bits media]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL Cambios de velocidad de bits]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL Eventos de búfer]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL Fotogramas perdidos]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL Errores]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL Id. de error externo]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL ID de error del reproductor SDK]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL Tiempo para el inicio]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL Duración total del búfer]](/help/reporting/dimensions/total-buffer-duration.md)
   * **Métricas:**
      * [[!UICONTROL Velocidad de bits media]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL Flujos afectados por cambio de velocidad de bits]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL Cambios de velocidad de bits]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL Eventos de búfer]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL Flujos afectados por búfer]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL Flujos afectados por fotogramas rechazados]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL Fotogramas perdidos]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL Pérdidas antes del inicio]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL Eventos de error]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL Flujos afectados por error]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL Tiempo para el inicio]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL Duración total del búfer]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL Metadatos de vídeo]**: Habilita el seguimiento de atributos de contenido de vídeo estándar, como programa, temporada y género.
   * **Dimensiones:**
      * [!UICONTROL Cargas de publicidad]
      * [[!UICONTROL Parte del día]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL Episodio]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL Género]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL Tipo de fuente de medios]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL Red]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL Temporada]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL Mostrar]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL Mostrar tipo]](/help/reporting/dimensions/show-type.md)
   * **Métrica:**
      * [[!UICONTROL Autorizado]](/help/reporting/metrics/authorized.md)
* **[!UICONTROL Metadatos de audio]**: Habilita el seguimiento de atributos de contenido de audio estándar como artista, álbum y estación.
   * **Dimensiones:**
      * [[!UICONTROL Álbum]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL Artista]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL Autor]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Etiqueta]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL Editor]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL Estación]](/help/reporting/dimensions/station.md)
* **[!UICONTROL Seguimiento de estado del reproductor]**: permite medir estados estándar de la interfaz de usuario del reproductor, como pantalla completa, subtítulos y la imagen en la imagen.
   * **Métricas:**
      * [[!UICONTROL Recuentos de subtítulos]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL Duración total de los subtítulos]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL Recuentos de pantalla completa]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL Duración total de pantalla completa]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL Recuentos de enfoque]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL Duración total del enfoque]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL Recuentos de Silenciar]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL Duración total de Silenciar]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL Recuentos de imagen en imagen]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL Duración total de la imagen en imagen]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL Transmisiones afectadas por los subtítulos]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL Transmisiones afectadas por pantalla completa]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL Transmisiones afectadas por el enfoque]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL Transmisiones afectadas por silenciar]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL Transmisiones afectadas por imagen en imagen]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)
