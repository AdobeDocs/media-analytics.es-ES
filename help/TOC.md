---
product: adobe analytics
audience: end-user
user-guide-title: Complemento de colección de medios de streaming
breadcrumb-title: Guía de colección de medios de streaming
user-guide-description: Implementar medios de streaming. Incluye el SDK de medios y la API de recopilación de medios.
sub-product: media analytics
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 97%

---


# Complemento de colección de medios de streaming {#using}

+ [Guía de colección de medios de streaming](media-overview.md)
+ Notas de la versión {#release-notes}
   + [Notas de la versión de Streaming Media Collection](additional-resources/release-notes.md)
+ Introducción {#getting-started}
   + [Requisitos previos ](getting-started/prereqs.md)
   + [Dispositivos compatibles](getting-started/supported-devices.md)
   + [Documentación de implementación de recopilación de medios de streaming](getting-started/implementation-documentation.md)
   + [SDK, bibliotecas y extensiones](getting-started/download-sdks.md)
   + Fin del soporte técnico {#end-of-support}
      + [Fin de la compatibilidad del SDK móvil de Media Analytics](additional-resources/end-of-support-faqs.md)
      + Heredado: migración de Media SDK independiente a Launch {#sdk-to-launch}
         + [Información general](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android: Media SDK para Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS: Media SDK para Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript: Media SDK para Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Implementación {#implementation}
   + [Información general sobre la implementación](implementation/overview.md)
   + Implementaciones de Edge (recomendado) {#edge-recommended}
      + [Requisitos previos](/help/implementation/edge/prerequisites-edge.md)
      + SDK/extensión de Media Edge {#media-edge-sdk}
         + [Configuración de SDK/extensión de Media Edge](/help/implementation/edge/implementation-edge.md)
         + [SDK web de Media Edge](/help/implementation/edge/edge-web-sdk.md)
         + [SDK de Media Edge Mobile](/help/implementation/edge/edge-mobile-sdk.md)
      + [API de Media Edge](/help/implementation/edge/implementation-edge-api.md)
   + Implementaciones solo de Adobe Analytics {#analytics-only}
      + [Requisitos previos](/help/implementation/media-sdk/setup/prerequisites-analytics.md)
      + Media SDKs/extensión {#media-sdk}
         + [SDK web de JavaScript](implementation/media-sdk/setup/web-implementation.md)
         + [Extensión de Media Analytics](implementation/media-sdk/setup/web-implementation-tags.md)
         + [SDK para móvil](implementation/media-sdk/setup/mobile-implementation.md)
         + SDK para OTT {#ott-setup}
            + [Instalación del SDK de Chromecast](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Instalación del SDK de Roku](implementation/media-sdk/setup/set-up-roku.md)
      + API de recopilación de medios: implementación {#streaming-media-apis}
         + [Colección de medios](implementation/media-collection-api/mc-api-overview.md)
         + [Inicio rápido de API](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [Solicitud de sesiones](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [Solicitud de eventos](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [Parámetros de solicitud](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [Tipos de eventos y descripciones](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + Implementación de la API {#mc-api-impl}
            + [Configuración del tipo de solicitud HTTP en el reproductor](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [Obtención de un ID de sesión](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [Implementación de una solicitud de eventos ](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [Esquemas de validación de JSON](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [Validación de solicitudes de eventos](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [Envío de eventos ping](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [Envío de datos de QoE](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [Compatibilidad con metadatos personalizados](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [Condiciones de tiempo de espera](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [Control del orden de los eventos](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [Poner eventos en cola cuando la respuesta de las sesiones es lenta](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variables {#variables}
      + [Parámetros de Streaming Media](implementation/variables/audio-video-parameters.md)
      + [Parámetros de anuncio](implementation/variables/ad-parameters.md)
      + [Parámetros de capítulo ](implementation/variables/chapter-parameters.md)
      + [Parámetros de estado del reproductor ](implementation/variables/player-state-parameters.md)
      + [Parámetros de calidad ](implementation/variables/quality-parameters.md)
      + [Métricas calculadas ](implementation/variables/calculated-metrics.md)
+ Informes {#media-reports}
   + [Habilitación de informes de medios ](reporting/media-reports-enable.md)
   + Paneles de medios en Workspace {#media-workspace-panels}
      + [Panel de audiencia media por minuto de medios](reporting/workspace/average-minute-audience.md)
      + [Panel Visualizadores simultáneos de medios](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Panel Tiempo invertido en la reproducción de contenido](reporting/workspace/media-playback-time-spent.md)
   + [Informes de medios en Workspace](reporting/workspace/media-workspace-templates.md)
   + [Segmentos de medios](reporting/segments.md)
   + Informes de medios predeterminados {#media-default-reports}
      + [Información general de informes predeterminados](reporting/reports-and-analytics/default-reports-overview.md)
      + [Información general de medios ](reporting/reports-and-analytics/media-reports-overview.md)
      + [Detalles de medios ](reporting/reports-and-analytics/media-reports-detail.md)
      + [Informe de Media Daypart](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Informe de visualizadores simultáneos de medios](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + API de medios {#media-api}
      + [Obtener datos de visualizadores simultáneos](reporting/reports-and-analytics/get-concurrent-json20.md)
      + [Obtener datos del tiempo invertido en la reproducción de medios](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Casos de uso {#media-use-cases}
   + [Casos de uso de Media SDK](use-cases/cookbook/sdk-cookbook-overview.md)
   + Seguimiento del estado de reproducción {#player-state-tracking}
      + [Información general ](use-cases/player-state-tracking/player-state-overview.md)
      + [Estados estándar y personalizados](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Implementación y sistema de informes](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Seguimiento de varios estados de reproductor](use-cases/player-state-tracking/multiple-player-states.md)
      + [Ejemplos de seguimiento del estado de reproducción](use-cases/player-state-tracking/player-state-examples.md)
   + [Seguimiento del contenido descargado ](use-cases/track-downloaded-content.md)
   + [Federated Analytics ](use-cases/federated-analytics.md)
   + [Administración de interrupciones de la aplicación durante la reproducción](use-cases/cookbook/app-interrupts.md)
   + [Atribución de flujo de transmisión de medios](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [Reanudación de sesiones inactivas](use-cases/cookbook/resuming-inactive.md)
   + [Seguimiento de Roku en SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Gestión de espacios entre anuncios](use-cases/cookbook/fix-ad-play-ad.md)
   + Cronologías {#timelines}
      + [Inicio y final del capítulo](use-cases/timelines/chapter-start-end.md)
      + [Ver hasta el final del contenido](use-cases/timelines/view-to-end-of-content.md)
      + [Abandonar sesión](use-cases/timelines/user-abandons-session.md)
   + Uso de Analytics en aplicaciones OTT {#analytics-with-ott}
      + [Seguimiento de estados de aplicaciones](use-cases/analytics-with-ott/track-app-states.md)
      + [Seguimiento de acciones de aplicaciones](use-cases/analytics-with-ott/track-app-actions.md)
      + [Establecimiento de ID de usuario](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT y Audience Manager ](use-cases/analytics-with-ott/ott-am.md)
      + [OTT y Experience Cloud ](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Seguimiento {#tracking}
   + [Información general ](use-cases/track-av-playback/track-core-overview.md)
   + Seguimiento de Core Streaming Media Playback {#track-core}
      + [Seguimiento de reproducción principal en JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Seguimiento de reproducción principal en Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Seguimiento de reproducción principal en Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
   + Seguimiento del almacenamiento en búfer {#track-buffering}
      + [Seguimiento del almacenamiento en búfer en JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [Seguimiento del almacenamiento en búfer en Chromecast](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Seguimiento del almacenamiento en búfer en Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + Seguimiento de llamada a otro punto del contenido {#track-seeking}
      + [Seguimiento de llamada a otro punto del contenido en JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Seguimiento de llamada a otro punto del contenido en Chromecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Seguimiento de llamada a otro punto del contenido en Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + Implementación de metadatos estándar {#impl-std-metadata}
      + [Implementación de metadatos estándar en JavaScript 3.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Implementación de metadatos estándar en Chromecast](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [Parámetros de metadatos estándar: Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Implementación de metadatos estándar en Roku ](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [Parámetros de metadatos estándar: Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Seguimiento de anuncios {#track-ads}
      + [Información general ](use-cases/track-ads/track-ads-overview.md)
      + [Seguimiento de anuncios en JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Seguimiento de anuncios en Chromecast](use-cases/track-ads/track-ads-chromecast.md)
      + [Seguimiento de anuncios en Roku](use-cases/track-ads/track-ads-roku.md)
      + Implementación de los metadatos de anuncios estándar {#impl-std-ad-metadata}
         + [Implementación de metadatos de publicidad estándar en JavaScript 3.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementación de metadatos de publicidad estándar en Roku ](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Seguimiento de capítulos y segmentos {#track-chapters}
      + [Información general ](use-cases/track-chapters/track-chapters-overview.md)
      + [Seguimiento de capítulos y segmentos en JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Seguimiento de capítulos y segmentos en Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Seguimiento de capítulos y segmentos en Roku](use-cases/track-chapters/track-chapters-roku.md)
   + Seguimiento de la calidad de la experiencia {#track-qos}
      + [Información general ](use-cases/track-qos/track-qos-overview.md)
      + [Seguimiento de la calidad de la experiencia en JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Seguimiento de la calidad de la experiencia en Chromecast](use-cases/track-qos/track-qos-chromecast.md)
      + [Seguimiento de la calidad de la experiencia en Roku](use-cases/track-qos/track-qos-roku.md)
   + Seguimiento de errores {#track-errors}
      + [Información general ](use-cases/track-errors/track-errors-overview.md)
      + [Seguimiento de errores en JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Seguimiento de errores en Chromecast](use-cases/track-errors/track-errors-chromecast.md)
      + [Seguimiento de errores en Roku](use-cases/track-errors/track-errors-roku.md)
+ Privacidad y seguridad {#streaming-media-privacy}
   + [Configuración de privacidad y exclusión](privacy/opt-out-privacy.md)
   + [Seguridad](privacy/security.md)
+ Implementaciones heredadas {#legacy-implementations}
   + [Heredado: información general](legacy/setup/legacy-setup-overview.md)
   + [Heredado: descargar SDK](legacy/legacy-download-sdks.md)
   + Heredado: Media SDK {#legacy-media-sdks}
      + [Heredado: información general de Media SDK](legacy/media-sdk/setup/setup-overview.md)
      + [Configuración de Android](legacy/media-sdk/setup/set-up-android.md)
      + [Configuración de iOS](legacy/media-sdk/setup/set-up-ios.md)
      + Configuración de JavaScript {#setup-javascript}
         + [Configuración de JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Acerca de la medición del ritmo cardíaco](legacy/heartbeat-measurement.md)
   + [Adobe Primetime](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Habilitación de Adobe Audience Management](legacy/intro-to-ava/am-enablement.md)
   + [Implementación de Vínculo personalizado](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + Seguimiento de hitos heredado {#legacy-milestone-tracking}
      + [Seguimiento de hitos heredado](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migración de hitos a VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migración de hitos a CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Validación {#validation}
      + [Información general sobre validación](legacy/validation/validation-overview.md)
      + [Prueba 1: Reproducción estándar](legacy/validation/test1-standard-playback.md)
      + [Prueba 2: Interrupción de contenido](legacy/validation/test2-media-interrupt.md)
      + [Detalles de la llamada de prueba](legacy/validation/test-call-details.md)
      + [Descripciones del parámetro de latido](legacy/validation/heartbeat-params.md)
      + Depuración {#debugging}
         + [Depuración de SDK](legacy/validation/debugging/sdk-debugging.md)
   + [Migración heredada: VHL 1.x a VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Comparación del código de la v1.x y la v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [API de seguimiento de 1x a 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Heredado: introducción a AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Ruta del lado del cliente](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + Seguimiento heredado {#track-av-playback}
      + [Seguimiento de reproducción principal en Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Seguimiento de reproducción principal en iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Seguimiento de reproducción principal en JavaScript {#track-core-javascript}
         + [Seguimiento de reproducción principal en JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Seguimiento del almacenamiento en búfer en Android](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [Seguimiento del almacenamiento en búfer en iOS](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + Seguimiento del almacenamiento en búfer en JavaScript {#track-buffering-js}
            + [Seguimiento del almacenamiento en búfer en JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Seguimiento de llamada a otro punto del contenido en Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [Seguimiento de llamada a otro punto del contenido en iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + Seguimiento de llamada a otro punto del contenido en JavaScript {#track-seeking-js}
            + [Seguimiento de llamada a otro punto del contenido en JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Implementación de metadatos estándar en Android](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementación de metadatos estándar en iOS](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Claves de metadatos de iOS](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementación de metadatos estándar en JavaScript {#impl-std-md-js}
            + [Implementación de metadatos estándar en JavaScript 2.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + Seguimiento de anuncios {#track-ads}
         + [Seguimiento de anuncios en Android](use-cases/track-ads/track-ads-android.md)
         + [Seguimiento de anuncios en iOS](use-cases/track-ads/track-ads-ios.md)
         + Seguimiento de anuncios en JavaScript {#track-ads-js}
            + [Seguimiento de anuncios en JavaScript 2.x](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Implementación de metadatos de publicidad estándar en Android ](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Implementación de metadatos de publicidad estándar en iOS ](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Implementación de metadatos de publicidad estándar en JavaScript {#impl-std-ad-md-js}
               + [Implementación de metadatos de publicidad estándar en JavaScript 2.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + Seguimiento de capítulos y segmentos {#track-chapters}
         + [Seguimiento de capítulos y segmentos en Android](use-cases/track-chapters/track-chapters-android.md)
         + [Seguimiento de capítulos y segmentos en iOS](use-cases/track-chapters/track-chapters-ios.md)
         + Seguimiento de capítulos y segmentos en JavaScript {#track-chapters-js}
            + [Seguimiento de capítulos y segmentos en JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Seguimiento de la calidad de la experiencia en Android](use-cases/track-qos/track-qos-android.md)
         + [Seguimiento de la calidad de la experiencia en iOS](use-cases/track-qos/track-qos-ios.md)
         + Seguimiento de la calidad de la experiencia en JavaScript {#track-qos-js}
            + [Seguimiento de la calidad de la experiencia en JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + Seguimiento de errores {#track-errors}
         + [Seguimiento de errores en Android](use-cases/track-errors/track-errors-android.md)
         + [Seguimiento de errores en iOS ](use-cases/track-errors/track-errors-ios.md)
         + Seguimiento de errores en JavaScript {#track-errors-js}
            + [Seguimiento de errores en JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + Situaciones de seguimiento {#tracking-scenarios}
         + [Reproducción de VOD sin anuncios](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [Reproducción de VOD con anuncios previos a la emisión](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [Reproducción de VOD con anuncios omitidos](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [Reproducción de VOD con un capítulo](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [Reproducción de VOD con un capítulo omitido](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [Reproducción de VOD con llamada a otro punto del contenido principal](use-cases/tracking-scenarios/vod-seeking.md)
         + [Reproducción de VOD con almacenamiento en búfer](use-cases/tracking-scenarios/vod-buffering.md)
         + [Varios rastreadores de VOD en paralelo](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [Un rastreador de VOD para varias sesiones](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [Contenido principal en directo](use-cases/tracking-scenarios/live-main-content.md)
         + [Contenido principal activo con seguimiento secuencial](use-cases/tracking-scenarios/live-sequential.md)
