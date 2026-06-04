---
title: Resumen de métricas de medios de streaming
description: Descubra cómo se calculan y organizan las métricas de medios de streaming en Adobe Analytics y Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---


# Resumen de métricas de medios de streaming

Las métricas de Streaming Media Analytics son recuentos y duraciones impulsados por eventos que calcula el servidor de medios. El reproductor de contenido envía eventos como inicio de sesión, reproducción, ping e inicio de publicidad; el backend de contenido procesa esos eventos y finaliza los valores de las métricas en la llamada de cierre de sesión.

## Cálculo de las métricas

Las métricas de medios de streaming siguen cuatro patrones de cálculo principales:

* **Indicadores activados por eventos**: Configúrelos la primera vez que un evento correspondiente llegue a una sesión. Un evento [`play`](/help/implementation/events/playback/play.md) para el contenido principal establece el indicador [[!UICONTROL El contenido comienza]](content-starts.md); un evento [`adStart`](/help/implementation/events/ads/ad-start.md) establece [[!UICONTROL El anuncio comienza]](ad-starts.md). El indicador se registra una vez por sesión en la llamada de cierre, no por evento.

* **Duraciones acumuladas**: Suma los intervalos entre eventos ping mientras un estado de reproducción en particular está activo. [[!UICONTROL El tiempo invertido en contenido]](content-time-spent.md) se acumula mientras se reproduce el contenido principal; [[!UICONTROL El tiempo invertido en publicidad]](ad-time-spent.md) se acumula mientras se reproduce un anuncio. El intervalo de ping recomendado por Adobe es de 10 segundos para el contenido principal y 1 segundo durante los anuncios, por lo que las métricas de tiempo empleado solo pueden ser tan granulares como el intervalo de ping de la implementación.

* **Recuentos de eventos**: Rastrea el total de ocurrencias dentro de la sesión. Las métricas de calidad como [[!UICONTROL Eventos de búfer]](buffer-events.md), [[!UICONTROL Cambios de velocidad de bits]](bitrate-changes.md), [[!UICONTROL Eventos de error]](error-events.md) y [[!UICONTROL Eventos de pausa]](pause-events.md) cuentan cada ocurrencia, no solo la primera.

* **Flujos afectados**: los indicadores de nivel de sesión se establecen en 1 si el evento correspondiente se produjo en cualquier momento durante la sesión, independientemente de cuántas veces. Utilice estas métricas para medir el alcance, mientras utiliza la métrica de recuento de eventos para medir la gravedad. Por ejemplo, puede usar [[!UICONTROL Flujos afectados por el búfer]](buffer-impacted-streams.md) para determinar la proporción de sesiones que se vieron afectadas por el almacenamiento en búfer en todas las sesiones de reproducción.

## Disponibilidad por sistema de informes

| Sistema de informes | Cómo llegan las métricas |
| --- | --- |
| Adobe Analytics | Rellenado con [variables de datos de contexto](https://experienceleague.adobe.com/es/docs/analytics/implementation/vars/page-vars/contextdata). Algunas métricas rellenan automáticamente eventos de solución usando estas variables de datos de contexto, mientras que otras deben asignarse a un evento personalizado usando [Reglas de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). Las métricas que rellenan automáticamente los valores deben tener habilitada primero su respectiva configuración del grupo de informes [medios de streaming](../setup/analytics-reporting.md). |
| Customer Journey Analytics | Campos XDM en `xdm.mediaReporting.sessionDetails` y nodos relacionados, procedentes de cualquier conjunto de datos que incluya datos de medios de streaming. Debe crear cada métrica con la configuración deseada dentro de [Configuración del componente de vista de datos](https://experienceleague.adobe.com/es/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Fuentes de datos | Las métricas aparecen en las columnas `event_list` y `post_event_list` como ID de evento. Cada archivo de fuente contiene un archivo de `events.csv` que contiene la búsqueda de todas las métricas, incluidas las métricas de medios de transmisión. |

>[!MORELIKETHIS]
>
>* [Información general sobre eventos](/help/implementation/events/overview.md): Los eventos del reproductor que rellenan las métricas
>* [Resumen de variables](/help/implementation/variables/overview.md): Los datos que los eventos llevan a Adobe
>* [Resumen de dimensiones](/help/reporting/dimensions/overview.md): Las dimensiones de informes que rellenan las variables
