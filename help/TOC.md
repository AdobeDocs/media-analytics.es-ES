---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics para medios de transmisión
breadcrumb-title: Guía de Media Analytics
user-guide-description: Implemente Adobe Analytics para medios de transmisión. Incluye el SDK de medios y la API de recopilación de medios.
sub-product: media analytics
source-git-commit: 534f6f77d69a8fe3574c214cd56d2f77758c1643
workflow-type: ht
source-wordcount: '833'
ht-degree: 100%

---


# Adobe Analytics para medios de transmisión {#using}

+ [Medición de Streaming Media en Adobe Analytics](media-overview.md)
+ [Dispositivos y plataformas compatibles](measurement-options/supported-devices.md)
+ Introducción a Streaming Media Analytics {#intro-to-ava}
   + [Requisitos previos](intro-to-ava/prereqs.md)
   + Rutas de implementación {#implementation-paths}
      + [Información general ](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Lado del cliente](intro-to-ava/implementation-paths/client-side-path.md)
      + Otras rutas de implementación {#other-paths}
         + Seguimiento de Milestone en el módulo multimedia {#mm-milestone-tracking}
            + [Información general de Milestone ](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [Migración de Milestone a Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [Migración de Milestone a vínculo personalizado](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Vínculo personalizado en Analytics {#cl-in-aa}
            + [Guía de implementación de Vínculo personalizado](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Habilitación de Audience Manager](intro-to-ava/am-enablement.md)
+ SDK de Media Analytics {#sdk-implement}
   + [Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics](sdk-implement/end-of-support-faqs.md)
   + [Descarga de SDK](sdk-implement/download-sdks.md)
   + Creación y configuración {#setup}
      + [Información general ](sdk-implement/setup/setup-overview.md)
      + [Configuración de Android](sdk-implement/setup/set-up-android.md)
      + [Configuración de iOS](sdk-implement/setup/set-up-ios.md)
      + Configuración de JavaScript {#setup-javascript}
         + [Configuración de JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [Configuración de JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Configuración de Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Configuración de Roku](sdk-implement/setup/set-up-roku.md)
   + Seguimiento de Streaming Media Playback {#track-av-playback}
      + [Información general ](sdk-implement/track-av-playback/track-core-overview.md)
      + Seguimiento de Core Streaming Media Playback {#track-core}
         + [Seguimiento de reproducción principal en Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Seguimiento de reproducción principal en iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + Seguimiento de reproducción principal en JavaScript {#track-core-javascript}
            + [Seguimiento de reproducción principal en JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [Seguimiento de reproducción principal en JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Seguimiento de reproducción principal en Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Seguimiento de reproducción principal en Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Seguimiento del almacenamiento en búfer {#track-buffering}
         + [Seguimiento del almacenamiento en búfer en Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Seguimiento del almacenamiento en búfer en iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + Seguimiento del almacenamiento en búfer en JavaScript {#track-buffering-js}
            + [Seguimiento del almacenamiento en búfer en JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [Seguimiento del almacenamiento en búfer en JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Seguimiento del almacenamiento en búfer en Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Seguimiento del almacenamiento en búfer en Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Seguimiento de llamada a otro punto del contenido {#track-seeking}
         + [Seguimiento de llamada a otro punto del contenido en Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Seguimiento de llamada a otro punto del contenido en iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + Seguimiento de llamada a otro punto del contenido en JavaScript {#track-seeking-js}
            + [Seguimiento de llamada a otro punto del contenido en JavaScript 2.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [Seguimiento de llamada a otro punto del contenido en JavaScript 3.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Seguimiento de llamada a otro punto del contenido en Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Seguimiento de llamada a otro punto del contenido en Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementación de metadatos estándar {#impl-std-metadata}
         + [Implementación de metadatos estándar en Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementación de metadatos estándar en iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Claves de metadatos de iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementación de metadatos estándar en JavaScript {#impl-std-md-js}
            + [Implementación de metadatos estándar en JavaScript 2.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [Implementación de metadatos estándar en JavaScript 3.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Implementación de metadatos estándar en Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Parámetros de metadatos estándar: Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementación de metadatos estándar en Roku ](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Parámetros de metadatos estándar: Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Seguimiento de anuncios {#track-ads}
      + [Información general ](sdk-implement/track-ads/track-ads-overview.md)
      + [Seguimiento de anuncios en Android](sdk-implement/track-ads/track-ads-android.md)
      + [Seguimiento de anuncios en iOS](sdk-implement/track-ads/track-ads-ios.md)
      + Seguimiento de anuncios en JavaScript {#track-ads-js}
         + [Seguimiento de anuncios en JavaScript 2.x](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [Seguimiento de anuncios en JavaScript 3.x](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Seguimiento de anuncios en Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Seguimiento de anuncios en Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementación de los metadatos de anuncios estándar {#impl-std-ad-metadata}
         + [Implementación de metadatos de publicidad estándar en Android ](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementación de metadatos de publicidad estándar en iOS ](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Implementación de metadatos de publicidad estándar en JavaScript {#impl-std-ad-md-js}
            + [Implementación de metadatos de publicidad estándar en JavaScript 2.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Implementación de metadatos de publicidad estándar en JavaScript 3.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementación de metadatos de publicidad estándar en Roku ](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Seguimiento de capítulos y segmentos {#track-chapters}
      + [Información general ](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Seguimiento de capítulos y segmentos en Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Seguimiento de capítulos y segmentos en iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + Seguimiento de capítulos y segmentos en JavaScript {#track-chapters-js}
         + [Seguimiento de capítulos y segmentos en JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Seguimiento de capítulos y segmentos en JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Seguimiento de capítulos y segmentos en Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Seguimiento de capítulos y segmentos en Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Seguimiento de la calidad de la experiencia {#track-qos}
      + [Información general ](sdk-implement/track-qos/track-qos-overview.md)
      + [Seguimiento de la calidad de la experiencia en Android](sdk-implement/track-qos/track-qos-android.md)
      + [Seguimiento de la calidad de la experiencia en iOS](sdk-implement/track-qos/track-qos-ios.md)
      + Seguimiento de la calidad de la experiencia en JavaScript {#track-qos-js}
         + [Seguimiento de la calidad de la experiencia en JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [Seguimiento de la calidad de la experiencia en JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Seguimiento de la calidad de la experiencia en Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Seguimiento de la calidad de la experiencia en Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Seguimiento de errores {#track-errors}
      + [Información general ](sdk-implement/track-errors/track-errors-overview.md)
      + [Seguimiento de errores en Android](sdk-implement/track-errors/track-errors-android.md)
      + [Seguimiento de errores en iOS ](sdk-implement/track-errors/track-errors-ios.md)
      + Seguimiento de errores en JavaScript {#track-errors-js}
         + [Seguimiento de errores en JavaScript 2.x](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [Seguimiento de errores en JavaScript 3.x](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Seguimiento de errores en Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Seguimiento de errores en Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Configuración de privacidad y exclusión](sdk-implement/opt-out-privacy.md)
   + Situaciones de seguimiento {#tracking-scenarios}
      + [Reproducción de VOD sin anuncios](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Reproducción de VOD con anuncios previos a la emisión](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Reproducción de VOD con anuncios omitidos](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [Reproducción de VOD con un capítulo](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [Reproducción de VOD con un capítulo omitido](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [Reproducción de VOD con llamada a otro punto del contenido principal](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [Reproducción de VOD con almacenamiento en búfer](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Varios rastreadores de VOD en paralelo](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [Un rastreador de VOD para varias sesiones](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Contenido principal en directo](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Contenido principal activo con seguimiento secuencial](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validación {#validation}
      + [Información general sobre validación](sdk-implement/validation/validation-overview.md)
      + [Prueba 1: Reproducción estándar](sdk-implement/validation/test1-standard-playback.md)
      + [Prueba 2: Interrupción de contenido](sdk-implement/validation/test2-media-interrupt.md)
      + [Detalles de la llamada de prueba](sdk-implement/validation/test-call-details.md)
      + [Descripciones del parámetro de latido](sdk-implement/validation/heartbeat-params.md)
      + Depuración {#debugging}
         + [Depuración de SDK](sdk-implement/validation/debugging/sdk-debugging.md)
   + Analytics en aplicaciones OTT {#analytics-with-ott}
      + [Seguimiento de estados de aplicaciones](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Seguimiento de acciones de aplicaciones](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Establecimiento de ID de usuario](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT y Audience Manager ](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT y Experience Cloud ](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Guía paso a paso {#cookbook}
      + [Guía de SDK](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Administración de interrupciones de la aplicación durante la reproducción](sdk-implement/cookbook/app-interrupts.md)
      + [Solución cuando aparece main:play entre anuncios](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Reanudar sesiones inactivas](sdk-implement/cookbook/resuming-inactive.md)
      + [Seguimiento en SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migración de Media Analytics 1.x a 2.x {#va-1x-to-2x}
      + [Información general sobre migración](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Comparación de código: 1.x y 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversión de API 1.x a 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + SDK de Media Analytics para la migración a Launch {#sdk-to-launch}
      + [SDK para la migración a Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + SDK para las guías de la plataforma de migración a Launch {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ API de recopilación de contenidos (RESTful) {#media-collection-api}
   + [Información general ](media-collection-api/mc-api-overview.md)
   + Referencia de API {#mc-api-ref}
      + [Solicitud de sesiones](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Solicitud de eventos](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parámetros de solicitud](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Tipos de eventos y descripciones](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [Esquemas de validación de JSON](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementación de la API {#mc-api-impl}
      + [Inicio rápido](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Configuración del tipo de solicitud HTTP en el reproductor](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Obtención de un ID de sesión](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementación de una solicitud de eventos ](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Validación de solicitudes de eventos](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Envío de eventos ping](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Envío de datos de la nube](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Compatibilidad con metadatos personalizados](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Condiciones de tiempo de espera](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Control del orden de los eventos](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Poner eventos en cola cuando la respuesta de las sesiones es lenta](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Cronologías de seguimiento de contenidos {#mc-api-timelines}
      + [Cronología 1: ver hasta el final del contenido](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Línea de tiempo 2: El usuario abandona la sesión](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Línea de tiempo 3: Capítulos](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Guía paso a paso {#media-analytics-cookbook}
   + [Guía paso a paso](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Atribución de flujo de transmisión de contenido](media-analytics-cookbook/media-dimensions.md)
+ Métricas y metadatos {#metrics-and-metadata}
   + [Parámetros de Streaming Media](metrics-and-metadata/audio-video-parameters.md)
   + [Parámetros de anuncio ](metrics-and-metadata/ad-parameters.md)
   + [Parámetros de capítulo ](metrics-and-metadata/chapter-parameters.md)
   + [Parámetros de estado del reproductor ](metrics-and-metadata/player-state-parameters.md)
   + [Parámetros de calidad ](metrics-and-metadata/quality-parameters.md)
   + [Segmentos](metrics-and-metadata/segments.md)
   + [Métricas calculadas](metrics-and-metadata/calculated-metrics.md)
+ Informes y análisis {#media-reports}
   + [Habilitación de informes de contenidos](media-reports/media-reports-enable.md)
   + Informes predeterminados de contenidos {#media-default-reports}
      + [Información general de informes predeterminados](media-reports/media-default-reports/default-reports-overview.md)
      + [Información general de contenidos](media-reports/media-default-reports/media-reports-overview.md)
      + [Detalles de contenidos](media-reports/media-default-reports/media-reports-detail.md)
      + [Informe de Media Daypart](media-reports/media-default-reports/media-reports-daypart.md)
      + [Informe de visualizadores simultáneos de medios](media-reports/media-default-reports/media-concurrent-viewers.md)
   + Paneles de Media Workspace {#media-workspace-panels}
   + [Panel Audiencia media por minuto de medios](media-reports/media-workspace-panels/average-minute-audience.md)
   + [Panel Visualizadores simultáneos de medios](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Panel Tiempo invertido en la reproducción de contenido](media-reports/media-workspace-panels/media-playback-time-spent.md)
   + [Plantillas de Media Workspace](media-reports/media-workspace-templates.md)
   + [Obtener datos de visualizadores simultáneos mediante API](media-reports/media-default-reports/get-concurrent-json20.md)
   + [Obtención de datos del tiempo invertido en la reproducción de medios mediante API](media-reports/media-default-reports/get-mediaplaybacktimespent-json20.md)
+ [Seguimiento del contenido descargado](media-collection-api/track-downloaded-content.md)
+ Seguimiento del estado de reproducción {#player-state-tracking}
   + [Información general ](sdk-implement/player-state-tracking/player-state-overview.md)
   + [Estados estándar y personalizados](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [Implementación y sistema de informes](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [Ejemplos de seguimiento del estado de reproducción](sdk-implement/player-state-tracking/player-state-examples.md)
+ [Federated Analytics](federated-analytics.md)
+ Recursos adicionales {#additional-resources}
   + [Notas de la versión](additional-resources/release-notes.md)
