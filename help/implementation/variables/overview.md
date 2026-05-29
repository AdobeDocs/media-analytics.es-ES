---
title: Resumen de variables de medios de streaming
description: Descubra cómo se organizan las variables de medios de streaming y cómo se asignan entre Adobe Analytics y Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---


# Resumen de variables de medios de streaming

Las variables son los datos que el reproductor de contenidos proporciona sobre un flujo, como el nombre del contenido, el tipo de flujo, el nombre del anuncio y la calidad de reproducción. La mayoría de las variables se establecen al inicio de la sesión y se transmiten a la sesión cercana mediante el backend de medios, que las utiliza para rellenar las dimensiones y métricas que utiliza en el sistema de informes. Cada página de variable documenta cómo configurar esa variable en cada método de implementación admitido.

## Envío de variables a Adobe

Una sola variable lleva el mismo valor a cada aplicación o servicio de Adobe, pero el formato de ese valor depende de dónde lo envíe. En la tabla siguiente se muestra cada aplicación o servicio y el formato de variable que espera. La tabla de propiedades de cada página de variable muestra el valor exacto que se debe utilizar en cada formato.

| Formato de datos | Descripción |
| --- | --- |
| Variable de datos de contexto | El formato enviado a Adobe Analytics, denominado con un prefijo `a.media` (como `a.media.name`). |
| Campo de colección XDM | El formato enviado a Customer Journey Analytics, expresado como una ruta de campo XDM (como `xdm.mediaCollection.sessionDetails.name`). |
| Característica Audience Manager | El formato reenviado a Audience Manager, con el prefijo `c_contextdata` (como `c_contextdata.a.media.name`). |

>[!MORELIKETHIS]
>
>* [Información general de eventos](/help/implementation/events/overview.md): Los eventos del reproductor que llevan variables
>* [Resumen de dimensiones](/help/reporting/dimensions/overview.md): Las dimensiones de informes que rellenan las variables
>* [Resumen de métricas](/help/reporting/metrics/overview.md): Las métricas de informes que rellenan las variables
