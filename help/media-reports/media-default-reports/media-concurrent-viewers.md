---
title: Espectadores simultáneos de medios
description: null
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: ht
source-wordcount: '265'
ht-degree: 100%

---

# Espectadores simultáneos de medios {#media-concurrent-viewers}

El panel Espectadores simultáneos de medios muestra los visualizadores simultáneos durante un día. Dichos datos pueden filtrarse por contenido, tipo de dispositivo o país.

>[!TIP]
>
> Este informe se basa en sesiones de medios activas simultáneas.  Para ver los visualizadores simultáneos por visitante único, con las funcionalidades adicionales para aplicar un segmento, desglosar y comparar, utilice la variable [Panel de visualizadores simultáneos de medios en Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=es).


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
