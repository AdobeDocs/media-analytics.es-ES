---
title: ¿Qué es la atribución de flujo de recursos multimedia?
description: Obtenga información sobre cómo vincular las acciones de la aplicación a los datos de seguimiento de medios sin necesidad de reglas de procesamiento y variables personalizadas adicionales.
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 89%

---


# Atribución de flujo de transmisión de contenido

Esta función le permite vincular acciones de aplicación a datos de seguimiento de contenido sin necesidad de reglas de procesamiento y variables personalizadas adicionales.

## Dimensiones de contenido fuera del seguimiento de contenido

Con Atribución de flujo de transmisión de contenido, los clientes ahora pueden agregar cualquiera de las dimensiones de contenido a todas las demás llamadas de análisis, como vistas de página y vínculos personalizados. Durante la implementación, debe agregar los parámetros de datos de contexto de contenido a las llamadas de seguimiento de Analytics. La lista completa de parámetros de datos de contexto utilizados para los contenidos está disponible aquí: [Parámetros de audio y vídeo.](/help/metrics-and-metadata/audio-video-parameters.md)

También deberá volver a habilitar la configuración del seguimiento de contenido desde Admin console para cada informe para el que desee habilitar esta función.

>[!NOTE]
>
>Las métricas de contenidos _no_ están disponibles para su uso fuera del seguimiento de contenido, ya que la mayoría de ellas las calcula Media Analytics en función de los eventos de latidos. Además, es importante que las métricas de contenidos no se vean infladas por implementaciones diferentes.

## Cómo

El ejemplo de JavaScript siguiente generará una llamada de seguimiento de vínculos personalizados que tiene el nombre establecido como “Hero Banner”.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

En los informes de Analytics, puede utilizar la eVar `Show` para desglosar los datos y contar las instancias de seguimiento de vínculos. El informe sería similar al siguiente:

![](/assets/myShow-rpt-1.png)

## Casos de uso

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
