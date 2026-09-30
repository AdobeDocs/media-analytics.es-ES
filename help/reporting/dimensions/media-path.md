---
title: Ruta de medios
description: Registra el ID de contenido como una variable de tráfico para el análisis de rutas.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 6%
---

# Ruta de medios

La dimensión **Ruta de medios** captura el ID de contenido como una variable de tráfico (prop) para que se pueda usar en el análisis de rutas (por ejemplo, los informes de flujo de contenido anterior y siguiente). Es exclusivo de Adobe Analytics: Customer Journey Analytics no almacena variables de tráfico y el control de rutas se realiza directamente en la dimensión Contenido (ID).

## Cómo se rellena esta dimensión

La ruta de medios se deriva automáticamente del ID de contenido establecido al inicio de la sesión. No hay ninguna variable independiente que establecer; la columna de fuente de datos `videopath` se rellena cada vez que se rellena Content (ID).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.name` como una variable de tráfico (prop) cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | N/D — usar [Contenido](content.md) para el análisis de rutas. |
| Fuentes de datos | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Las props de Adobe Analytics tienen un límite de 100 bytes. Los valores superiores a 100 bytes se truncan.

>[!IMPORTANT]
>
>Los informes de rutas comparan el valor de la propiedad en las visitas individuales dentro de la misma visita. Si el contenido (ID) cambia dentro de una visita (por ejemplo, cuando un visor pasa de un fragmento de contenido a otro), el informe de ruta muestra ese flujo.

## Elementos de dimensión

Cada elemento es un ID de contenido registrado durante una visita. Puede utilizar los paneles Flujo para ver las rutas de navegación entre el contenido y el contenido.
