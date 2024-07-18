---
title: ¿Qué es la atribución de flujo de transmisión de medios?
description: Esta función le permite vincular acciones de aplicación a datos de seguimiento de medios sin necesidad de reglas de procesamiento ni variables personalizadas adicionales.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 87%

---

# Atribución de flujo de transmisión de medios {#media-stream-attribution}

Con Media Stream Attribution, puede vincular las acciones de la aplicación a los datos de seguimiento de medios sin necesidad de reglas de procesamiento adicionales ni variables personalizadas.

## Dimensiones de medios fuera del seguimiento de medios

Puede agregar dimensiones de medios a las llamadas de Analytics, como vistas de página y vínculos personalizados. Durante la implementación, debe agregar los parámetros de datos de contexto de medios a las llamadas de seguimiento de Analytics. Para ver la lista completa de parámetros de datos de contexto disponibles que se utilizan para los contenidos, consulte [Parámetros de audio y vídeo.](/help/implementation/variables/audio-video-parameters.md)

Para habilitar esta función para un informe específico, vuelva a habilitar la configuración de seguimiento de medios desde Admin Console.

>[!NOTE]
>
>Las métricas de medios _no_ están disponibles para su uso fuera del seguimiento de medios porque la mayoría de ellas las calcula el complemento de recopilación de medios de streaming basado en eventos de latidos. Además, es importante que las métricas de medios no se vean infladas por implementaciones diferentes.

## Atribución de flujo de transmisión de medios

El ejemplo de JavaScript siguiente generará una llamada de seguimiento de vínculos personalizados que tiene el nombre establecido como “Hero Banner”.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

En los informes de Analytics, puede utilizar la eVar `Show` para desglosar los datos y contar las instancias de seguimiento de vínculos. El informe sería similar al siguiente:

![](/assets/myShow-rpt-1.png)

## Casos de uso

Los siguientes ejemplos muestran casos de uso para lo siguiente:

* Ubicación de la categoría
* Ubicación de héroes
* Participación
* Suscripciones

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
