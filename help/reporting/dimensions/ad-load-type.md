---
title: Cargas publicitarias
description: Informa del tipo de carga de publicidad utilizada para cada sesión de medios de streaming.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# Cargas publicitarias

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Cargas del anuncio**. Consulte [Tipo de carga de anuncio](/help/implementation/variables/standard-metadata/ad-load-type.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Cargas de publicidad** indica el tipo de anuncio cargado al principio de cada sesión de medios de streaming. El valor está definido por el cliente, lo que permite a las organizaciones clasificar las sesiones según su mecanismo de envío de publicidad (por ejemplo, `"linear"`, `"dynamic"` o `"programmatic"`).

## Cómo se rellena esta dimensión

El reproductor establece el tipo de carga de anuncio al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.adLoad` cuando se configura [[!UICONTROL Streaming Media]](/help/reporting/setup/analytics-reporting.md). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## Elementos de dimensión

Cada elemento es el valor literal y la cadena de tipo de carga establecida al inicio de la sesión. Los valores no están restringidos a una enumeración estándar: defina una taxonomía que sea coherente en todas las implementaciones de modo que los valores se acumulen de forma predecible en los informes.
