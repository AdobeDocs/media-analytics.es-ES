---
title: Configuración de informes para implementaciones de Edge
description: Configure Customer Journey Analytics para que informe sobre los datos de medios de streaming recopilados a través de Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 17%

---

# Configuración de informes para implementaciones de Edge

Después de implementar la recopilación de medios de streaming a través de Edge Network, configure Customer Journey Analytics para que informe sobre los datos recopilados. En esta página se describe cómo crear una conexión, una vista de datos y un proyecto para medios de transmisión.

>[!NOTE]
>
>Esta página cubre la creación de informes en Customer Journey Analytics, el destino recomendado para las implementaciones de Edge. Si la secuencia de datos envía datos de medios de streaming a Adobe Analytics en su lugar, consulte [Configuración de informes para implementaciones solo de Analytics](analytics-reporting.md).

* **Requisitos previos**: complete una implementación de Edge y recopile algunos datos. Consulte la [descripción general de la implementación de Edge](/help/implementation/edge/overview.md) y el método de implementación elegido.

## Crear una conexión en Customer Journey Analytics

1. En Customer Journey Analytics, cree una conexión como se describe en [Crear una conexión](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=es).

   Al crear la conexión, se requieren las siguientes selecciones para los medios de transmisión:

   1. Seleccione el conjunto de datos que ha creado durante la implementación.

   1. Asegúrese de que la opción **[!UICONTROL Importar todos los datos nuevos]** esté habilitada.

1. Continuar con [Crear una vista de datos en Customer Journey Analytics](#create-a-data-view-in-customer-journey-analytics).

## Creación de una vista de datos en Customer Journey Analytics

1. En Customer Journey Analytics, cree una vista de datos como se describe en [Cree o edite una vista de datos](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=es).

   1. En el campo **[!UICONTROL Conexión]**, seleccione la conexión que creó anteriormente.

      La selección de una nueva conexión puede tardar hasta 15 minutos en estar disponible.

   1. En la ficha **[!UICONTROL Componentes]**, en la sección **[!UICONTROL Campos de esquema]**, busque cada componente en las tablas siguientes y arrástrelo al panel **[!UICONTROL Métricas]**. Si existen varios campos con el mismo nombre, utilice la ruta XDM para confirmar el campo correcto.

      **Contenido principal - Métricas de contenido**

      | Nombre del componente | Ruta de XDM |
      |----------|---------|
      | Inicios de contenidos | mediaReporting.sessionDetails.isViewed |
      | Vistas de segmentos de medios | mediaReporting.sessionDetails.hasSegmentView |
      | Inicio de contenido | mediaReporting.sessionDetails.isPlayed |
      | Finalización de contenido | mediaReporting.sessionDetails.isCompleted |
      | Tiempo invertido en contenido | mediaReporting.sessionDetails.timePlayed |
      | Tiempo invertido en contenido | mediaReporting.sessionDetails.totalTimePlayed |
      | Tiempo de reproducción única | mediaReporting.sessionDetails.uniqueTimePlayed |
      | Marcador de progreso del 10% | mediaReporting.sessionDetails.hasProgress10 |
      | Promedio de público por minuto | mediaReporting.sessionDetails.averageMinuteAudience |

      **Capítulo y anuncios - Métricas de capítulo y anuncios**

      | Nombre del componente | Ruta de XDM |
      |----------|---------|
      | Capítulo iniciado | mediaReporting.chapterDetails.isStarted |
      | Capítulo completado | mediaReporting.chapterDetails.isCompleted |
      | Tiempo de reproducción del capítulo | mediaReporting.chapterDetails.timePlayed |
      | Anuncio iniciado | mediaReporting.advertisingDetails.isStarted |
      | Anuncio completado | mediaReporting.advertisingDetails.isCompleted |
      | Tiempo de publicidad reproducida | mediaReporting.advertisingDetails.timePlayed |

      **QoE - métricas de QoE**

      | Nombre del componente | Ruta de XDM |
      |----------|---------|
      | Tiempo para el inicio | mediaReporting.qoeDataDetails.timeToStart |
      | Pérdidas antes del inicio | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | Flujos afectados por el búfer | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | Flujos afectados por el cambio en la velocidad de bits | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | Cambios en la velocidad de bits | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | Velocidad de bits media | mediaReporting.qoeDataDetails.bitrateAverage |
      | Fotogramas perdidos | mediaReporting.qoeDataDetails.droppedFrames |
      | Errores | mediaReporting.qoeDataDetails.errorCount |
      | Flujos afectados por el error | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | Flujos afectados por la pérdida de cuadros | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |

      **Estado del reproductor - Métricas de estado del reproductor**

      | Nombre del componente | Ruta de XDM |
      |----------|---------|
      | Conjunto de estado del reproductor | mediaReporting.states.isSet |
      | Recuento de estados del reproductor | mediaReporting.states.count |
      | Hora de estado del reproductor | mediaReporting.states.time |

   1. Actualice las etiquetas (en el menú desplegable **[!UICONTROL Context labels]**) de los componentes de la siguiente tabla. Busque y arrastre cualquier componente que no esté ya en el panel de métricas al panel.

      | Nombre del componente | Etiqueta de contexto |
      |---------|----------|
      | Tiempo de espera del servidor de sesión multimedia | Medios: Segundos desde la última llamada |
      | Tiempo invertido en contenido | Medios: tiempo invertido en contenido |
      | Duración total del búfer | Medios: Duración total del búfer |
      | Tiempo para el inicio | Medios: tiempo para el inicio |
      | Duración de la pausa | Medios: Duración total de la pausa |

   1. Para agregar desgloses al proyecto, agregue las siguientes dimensiones al panel **[!UICONTROL Dimensiones]**:

      | Ruta de XDM | Nombre del componente |
      |---------|----------|
      | mediaReporting.states.name | Nombre del estado del reproductor |
      | mediaReporting.sessionDetails.ID | ID de sesión de contenidos |

      Además de las dimensiones de esta tabla, puede agregar cualquier otra dimensión por la que desee filtrar datos en sus proyectos.

1. Seleccione **[!UICONTROL Guardar y continuar]** > **[!UICONTROL Guardar y finalizar]** para guardar los cambios.

1. Continúe con [Crear y configurar un proyecto en Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Creación y configuración de un proyecto en Customer Journey Analytics

1. En Customer Journey Analytics, en la ficha **[!UICONTROL Workspace]**, en el área de **[!UICONTROL Proyectos]**, seleccione **[!UICONTROL Crear proyecto]**.

1. Seleccione **[!UICONTROL Proyecto en blanco]** > **[!UICONTROL Crear]**.

1. En el nuevo proyecto, seleccione la vista de datos que creó anteriormente.

   Al crear paneles en el proyecto, puede utilizar cualquier componente que haya agregado a la vista de datos.

1. Seleccione el icono **Paneles** en el carril izquierdo y, a continuación, arrastre el panel **[!UICONTROL Visualizadores simultáneos de medios]** y el panel **[!UICONTROL Tiempo invertido en la reproducción de medios]**.

1. (Condicional) Si agregó metadatos personalizados al esquema, establezca la persistencia de los campos personalizados, tal como se describe en [Configuración del componente de persistencia](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) en la guía de Customer Journey Analytics.

1. Comparta el proyecto como se describe en [Compartir proyectos](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=es).

   >[!NOTE]
   >
   >Si los usuarios con los que desea compartir no están disponibles, asegúrese de que los usuarios tengan acceso de usuario y administrador a Customer Journey Analytics en Adobe Admin Console.

>[!MORELIKETHIS]
>
>* [Paneles de medios en Workspace](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [Resumen de dimensiones](/help/reporting/dimensions/overview.md)
>* [Resumen de métricas](/help/reporting/metrics/overview.md)
