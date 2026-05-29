---
title: Resumen de dimensiones de medios de streaming
description: Descubra cómo se rellenan y organizan las dimensiones de medios de streaming en Adobe Analytics y Customer Journey Analytics.
feature: Dimensions
role: User, Admin
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# Resumen de dimensiones de medios de streaming

Las dimensiones en Streaming Media Analytics le permiten cortar y filtrar métricas por nombre de contenido, tipo de flujo, nombre de anuncio y docenas de atributos más. El reproductor establece la mayoría al inicio de la sesión y la lleva al cierre de la sesión.

## Cómo se rellenan las dimensiones

Las dimensiones de medios de streaming siguen tres patrones de población principales:

* **Suministrado por el reproductor de medios**: El origen de la mayoría de las dimensiones. El reproductor envía estos valores en la llamada de [inicio de sesión](/help/implementation/events/session/session-start.md), y el backend de medios los adjunta a cada evento subsiguiente de la sesión. Lo que el reproductor envía al inicio de la sesión es lo que aparece en los informes. Algunos ejemplos son [[!UICONTROL Tipo de emisión]](/help/reporting/dimensions/stream-type.md), [[!UICONTROL Nombre del contenido]](/help/reporting/dimensions/content-name.md) y [[!UICONTROL Longitud del contenido]](/help/reporting/dimensions/content-length.md).

* **Valores derivados**: dimensiones que el servidor multimedia calcula a partir del estado de reproducción acumulado en lugar de leer un valor proporcionado por el reproductor. [[!UICONTROL El segmento de contenido]](/help/reporting/dimensions/content-segment.md) se calcula desde la posición del cabezal de reproducción durante el transcurso de la reproducción. [[!UICONTROL Ruta de medios]](/help/reporting/dimensions/media-path.md) rastrea las transiciones entre el contenido y los estados de anuncios a lo largo de la sesión. El reproductor no puede anular estas dimensiones.

* **Clasificaciones**: Opcional. En lugar de rellenar dimensiones independientes, puede mantener los datos de clasificación con [conjuntos de clasificaciones](https://experienceleague.adobe.com/es/docs/analytics/components/classifications/sets/overview) (Adobe Analytics) o [conjuntos de datos de búsqueda](https://experienceleague.adobe.com/es/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) (Customer Journey Analytics).

## Disponibilidad por sistema de informes

| Sistema de informes | Cómo llegan las dimensiones |
| --- | --- |
| Adobe Analytics | Rellenado con [variables de datos de contexto](https://experienceleague.adobe.com/es/docs/analytics/implementation/vars/page-vars/contextdata). Algunas dimensiones rellenan automáticamente dimensiones usando estas variables de datos de contexto, mientras que otras deben rellenarse usando [Reglas de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). Las dimensiones que rellenan automáticamente los valores deben tener habilitada primero su respectiva configuración del grupo de informes [medios de streaming](../../implementation/media-sdk/setup/media-reports-enable.md). |
| Customer Journey Analytics | Los campos XDM normalmente en `xdm.mediaReporting.sessionDetails`, se originan a partir de cualquier conjunto de datos que incluya datos de medios de streaming. Debe crear cada dimensión con la configuración deseada dentro de [Configuración del componente de vista de datos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Fuentes de datos | Las dimensiones que se rellenan automáticamente tienen sus propios nombres de columnas de fuentes de datos (como `videostreamtype`, `videoname` o `videolength`). Las dimensiones que requieren reglas de procesamiento utilizan `evar` nombres de columna. |
| Audience Manager | Datos de contexto reenviados desde Adobe Analytics. Solo está disponible cuando el reenvío del lado del servidor de Analytics a Audience Manager está configurado. |

>[!MORELIKETHIS]
>
>* [Información general de eventos](/help/implementation/events/overview.md): Los eventos del reproductor que rellenan las dimensiones
>* [Resumen de variables](/help/implementation/variables/overview.md): Los datos que los eventos llevan a Adobe
>* [Resumen de métricas](/help/reporting/metrics/overview.md): Las métricas de informes que rellenan las variables
