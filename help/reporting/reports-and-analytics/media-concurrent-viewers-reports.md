---
title: Espectadores simultáneos de medios
description: Obtenga información acerca del panel Visualizadores simultáneos de medios que se utiliza para mostrar los visualizadores simultáneos de un día. Los datos pueden filtrarse por contenido, tipo de dispositivo o país.
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Streaming Media, Workspace Basics
role: User, Admin
TQID: https://experienceleague.adobe.com/8pqoGpVCRXvovD-cNPNOvFQFvJco3sWUq3SuXEOVeJI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 299
ht-degree: 91%

---

# Informes de espectadores simultáneos de medios {#media-concurrent-viewers}

El panel de control Espectadores simultáneos de medios muestra los visualizadores simultáneos durante un día. Dichos datos pueden filtrarse por contenido, tipo de dispositivo o país.

>[!TIP]
>
> Este informe se basa en sesiones de medios activas simultáneas.  Para ver los visualizadores simultáneos por visitante único, con las funcionalidades adicionales para aplicar un segmento, desglosar y comparar, utilice la variable [Panel de visualizadores simultáneos de medios en Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=es).
>

![](assets/video-concurrent-viewers.png)

## Características del informe {#report-features}

Estas son algunas de las características de este informe:

* No es en tiempo real. Tiene latencia normal de Adobe Analytics.
* El informe abarca un periodo de 24 horas. El eje x es la hora del día en función del huso horario del grupo de informes.
* Muestra los visores simultáneos en granularidad de minutos.
* Hay un *informe de Espectadores simultáneos de medios* que muestra cuántos visualizadores están viendo o escuchando todo el contenido.
* Hay un informe de Espectadores simultáneos en el informe *Detalles de medios* que muestra cuántos visualizadores están viendo o escuchando un elemento de medios determinado.
* El informe solo funciona durante un día.
* El cliente podrá consultar los informes de espectadores simultáneos históricos (con información de un día).

## Limitaciones {#limitations}

Estas son algunas limitaciones de este informe:

* No se mostrarán datos si el intervalo seleccionado no es un día completo.
* No es posible exportar los datos, como ReportBuilder.
* No se pueden presentar los datos en formato de tabla.
* No puede enviar un informe por correo electrónico.
* Incluso si no rastrea anuncios, debe volver a habilitar el seguimiento de medios y seleccionar el módulo de publicidad de medios.
* Esta funcionalidad proporciona datos precisos cuando se usa una biblioteca de latidos con capacidades de seguimiento de pausa.
