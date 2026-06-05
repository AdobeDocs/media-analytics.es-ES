---
title: Configuración de informes para implementaciones de Edge
description: Configure Customer Journey Analytics para que informe sobre los datos de medios de streaming recopilados a través de Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 6%

---

# Configuración de informes para implementaciones de Edge

Después de implementar la recopilación de medios de streaming a través de Edge Network, configure Customer Journey Analytics para que informe sobre los datos recopilados.

>[!NOTE]
>
>Esta página cubre la creación de informes en Customer Journey Analytics, el destino recomendado para las implementaciones de Edge. Si la secuencia de datos envía datos de medios de streaming a Adobe Analytics en su lugar, consulte [Configuración de informes para implementaciones solo de Analytics](analytics-reporting.md).

* **Requisitos previos**: complete una implementación de Edge y recopile algunos datos. Consulte la [descripción general de la implementación de Edge](/help/implementation/edge/overview.md) y el método de implementación elegido.

## Crear una conexión en Customer Journey Analytics

1. En Customer Journey Analytics, cree una conexión como se describe en [Crear una conexión](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-connections/create-connection). Al crear la conexión, asegúrese de que la casilla de verificación **[!UICONTROL Importar todos los datos nuevos]** esté habilitada.

## Creación de una vista de datos en Customer Journey Analytics

1. En Customer Journey Analytics, cree una vista de datos como se describe en [Cree o edite una vista de datos](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview).

   1. En el campo **[!UICONTROL Conexión]**, seleccione la conexión que creó anteriormente. Las nuevas conexiones pueden tardar hasta 15 minutos en aparecer.

   1. En la ficha **[!UICONTROL Componentes]**, en la sección **[!UICONTROL Campos de esquema]**, busque cada componente en la tabla siguiente y arrástrelo al panel **[!UICONTROL Dimensiones]** o **[!UICONTROL Métricas]** correspondiente. Si existen varios campos con el mismo nombre, utilice la ruta XDM para confirmar el campo correcto. Aplique la etiqueta de contexto que se muestra en la lista desplegable **[!UICONTROL Etiquetas de contexto]** de la configuración del componente.

      | Componente | Tipo | Ruta de XDM | Etiqueta de contexto |
      |---|---|---|---|
      | [Contenido](/help/reporting/dimensions/content.md) | Dimensión | `mediaReporting.sessionDetails.name` | Medios: ID de contenido |
      | [Nombre del contenido](/help/reporting/dimensions/content-name.md) | Dimensión | `mediaReporting.sessionDetails.friendlyName` | Medios: Nombre del vídeo |
      | [Longitud del contenido](/help/reporting/dimensions/content-length.md) | Dimensión | `mediaReporting.sessionDetails.length` | Medios: duración del vídeo |
      | [Mostrar](/help/reporting/dimensions/show.md) | Dimensión | `mediaReporting.sessionDetails.show` | Medios: mostrar |
      | [Temporada](/help/reporting/dimensions/season.md) | Dimensión | `mediaReporting.sessionDetails.season` | Medios: temporada |
      | [Episodio](/help/reporting/dimensions/episode.md) | Dimensión | `mediaReporting.sessionDetails.episode` | Medios: episodio |
      | Tipo de evento | Dimensión | `eventType` | Medios: Tipo de evento |
      | [Tiempo invertido en contenido](/help/reporting/metrics/content-time-spent.md) | Métrica | `mediaReporting.sessionDetails.timePlayed` | Medios: tiempo invertido en contenido |
      | [Tiempo invertido en contenido](/help/reporting/metrics/media-time-spent.md) | Métrica | `mediaReporting.sessionDetails.totalTimePlayed` | Medios: tiempo invertido en contenido |
      | [Duración total de la pausa](/help/reporting/metrics/total-pause-duration.md) | Métrica | `mediaReporting.sessionDetails.pauseTime` | Medios: Duración total de la pausa |
      | [Tiempo para el inicio](/help/reporting/metrics/time-to-start.md) | Métrica | `mediaReporting.qoeDataDetails.timeToStart` | Medios: tiempo para el inicio |
      | [Duración total del búfer](/help/reporting/metrics/total-buffer-duration.md) | Métrica | `mediaReporting.qoeDataDetails.bufferTime` | Medios: Duración total del búfer |
      | Tiempo de espera del servidor de sesión multimedia | Métrica | `mediaReporting.sessionDetails.secondsSinceLastCall` | Medios: Segundos desde la última llamada |

      >[!IMPORTANT]
      >
      >Las etiquetas de contexto de esta tabla son necesarias para que funcionen los paneles de medios de streaming. Customer Journey Analytics los usa para calcular automáticamente las métricas derivadas de **Espectadores simultáneos** y **Tiempo invertido en la reproducción** (utilizadas por los paneles [Espectadores simultáneos de medios](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) y [Tiempo invertido en la reproducción de medios](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)), y para rellenar las opciones de informes en el panel [Audiencia media por minuto de medios](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel).

      En este momento, puede agregar cualquier otra [dimensión](/help/reporting/dimensions/overview.md) o [métrica](/help/reporting/metrics/overview.md) a la vista de datos. Cada página enumera la ruta XDM para ese componente.

1. Seleccione **[!UICONTROL Guardar y continuar]** → **[!UICONTROL Guardar y finalizar]** para guardar los cambios.

## Creación y configuración de un proyecto en Customer Journey Analytics

1. En Customer Journey Analytics, en la ficha **[!UICONTROL Workspace]**, en el área de **[!UICONTROL Proyectos]**, seleccione **[!UICONTROL Crear proyecto]**.

1. Seleccione **[!UICONTROL Proyecto en blanco]** → **[!UICONTROL Crear]**.

1. En el nuevo proyecto, seleccione la vista de datos que creó anteriormente.

   Al crear paneles en el proyecto, puede utilizar cualquier componente que haya agregado a la vista de datos.

1. Seleccione el icono **Paneles** en el carril izquierdo y, a continuación, arrastre los paneles **[!UICONTROL Audiencia media por minuto de medios]**, **[!UICONTROL Espectadores simultáneos de medios]** y **[!UICONTROL Tiempo invertido en la reproducción de medios]**.

1. (Condicional) Si agregó metadatos personalizados al esquema, establezca la persistencia de los campos personalizados, tal como se describe en [Configuración del componente de persistencia](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) en la guía de Customer Journey Analytics.

1. Comparta el proyecto como se describe en [Compartir proyectos](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >Si los usuarios con los que desea compartir no están disponibles, asegúrese de que los usuarios tengan acceso de usuario y administrador a Customer Journey Analytics en Adobe Admin Console.

## Paneles de medios disponibles en Customer Journey Analytics

Analysis Workspace en Customer Journey Analytics incluye tres paneles de medios dedicados para clientes con el complemento de recopilación de medios de streaming. Estos paneles proporcionan visualizaciones creadas previamente para las necesidades más comunes de creación de informes de medios de streaming.

* **[Audiencia media por minuto de medios](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**: compara el consumo promedio de contenido entre programas de cualquier género o duración. Admite modos de período de tiempo específicos (basados en la duración) y personalizados, y permite actualizar las clasificaciones de duración después del hecho.
* **[Visores simultáneos de medios](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**: analiza los visores simultáneos a lo largo del tiempo para identificar los puntos de concurrencia máxima y los puntos de entrega. Admite la granularidad configurable y el desglose de series por segmentos, dimensiones o intervalos de fechas.
* **[Tiempo invertido en la reproducción de contenido](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**: analiza la duración de la reproducción a lo largo del tiempo con detalles sobre los períodos pico y valle. Admite granularidad y formato de salida configurables (horas o minutos).

>[!MORELIKETHIS]
>
>* [Resumen de dimensiones](/help/reporting/dimensions/overview.md)
>* [Resumen de métricas](/help/reporting/metrics/overview.md)
