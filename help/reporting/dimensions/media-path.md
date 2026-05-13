---
title: Ruta de medios
description: Registra el ID de contenido como una variable de tráfico para el análisis de rutas.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 4%

---


# Ruta de medios

La dimensión **Ruta de medios** captura el ID de contenido como una variable de tráfico (prop) para que se pueda usar en el análisis de rutas (por ejemplo, los informes de flujo de contenido anterior y siguiente). Es exclusivo de Adobe Analytics: Customer Journey Analytics no almacena variables de tráfico y el control de rutas se realiza directamente en la dimensión Contenido (ID).

## Cómo se rellena esta dimensión

La ruta de medios se deriva automáticamente del ID de contenido establecido al inicio de la sesión. No hay ninguna variable independiente que establecer; la columna de fuente de datos `videopath` se rellena cada vez que se rellena Content (ID).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.name` como una variable de tráfico (prop) cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | N/D — usar [Contenido](content.md) para el análisis de rutas |
| Fuentes de datos | `videopath, post_videopath` |

>[!IMPORTANT]
>
>Los informes de rutas comparan el valor de la propiedad en las visitas individuales dentro de la misma visita. Si el contenido (ID) cambia dentro de una visita (por ejemplo, cuando un visor pasa de un fragmento de contenido a otro), el informe de ruta muestra ese flujo.

## Elementos de dimensión

Cada elemento es un ID de contenido registrado durante una visita. Utilice los informes Flujo de página siguiente y Flujo de página anterior en Contenido > Ruta de medios en Adobe Analytics para ver las rutas de navegación de contenido a contenido.
