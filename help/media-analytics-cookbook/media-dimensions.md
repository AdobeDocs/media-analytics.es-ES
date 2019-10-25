---
title: Dimensiones de medios fuera del seguimiento de medios
seo-title: Dimensiones de medios fuera del seguimiento de medios
translation-type: tm+mt
source-git-commit: 5d20df537cd244a10f6c2e66cea622e98aa17a16

---


# Dimensiones de medios fuera del seguimiento de medios

Esta función le permite vincular acciones de aplicación a datos de seguimiento de medios sin necesidad de reglas de procesamiento y variables personalizadas adicionales.

Ahora los clientes pueden agregar cualquiera de las dimensiones de medios a todas las demás llamadas de análisis, como vistas de página y vínculos personalizados. Durante la implementación, debe agregar los parámetros de datos de contexto de medios a las llamadas de seguimiento de Analytics. La lista completa de parámetros de datos de contexto utilizados para los medios está disponible aquí: Parámetros [de audio y vídeo.](/help/metrics-and-metadata/audio-video-parameters.md)

También deberá volver a habilitar la configuración del seguimiento de medios desde la consola de administración para cada informe para el que desee habilitar esta función.

>[!NOTE]
>Las métricas de medios _no están_ disponibles para su uso fuera del seguimiento de medios, ya que la mayoría de ellas son calculadas por Media Analytics
>en función de los eventos de latidos. Además, es importante que las métricas de medios no se vean infladas por implementaciones diferentes.

## Cómo

El ejemplo de JavaScript siguiente generará una llamada de seguimiento de vínculos personalizados que tiene el nombre establecido en "Hero Banner".

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

En los informes de Analytics, puede utilizar la `Show` eVar para desglosar los datos y podrá contar las instancias de seguimiento de vínculos. El informe sería similar al siguiente:

![](/assets/myShow-rpt-1.png)

## Casos de uso

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
