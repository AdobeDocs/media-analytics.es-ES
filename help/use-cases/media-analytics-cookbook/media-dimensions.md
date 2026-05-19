---
title: ¿Qué es la atribución de flujo de transmisión de medios?
description: Esta función le permite vincular acciones de aplicación a datos de seguimiento de medios sin necesidad de reglas de procesamiento ni variables personalizadas adicionales.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e4f5f438-eabb-4c54-9133-b817e3d125f5
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# Atribución de flujo de transmisión de medios {#media-stream-attribution}

Con Media Stream Attribution, puede vincular las acciones de la aplicación a los datos de seguimiento de medios sin necesidad de reglas de procesamiento adicionales ni variables personalizadas.

## Dimensiones de medios fuera del seguimiento de medios

Puede agregar dimensiones de medios a las llamadas de Analytics, como vistas de página y vínculos personalizados. Durante la implementación, debe agregar los parámetros de datos de contexto de medios a las llamadas de seguimiento de Analytics.

Para habilitar esta función para un informe específico, vuelva a habilitar la configuración de seguimiento de medios desde Admin Console.

>[!NOTE]
>
>Las métricas de medios _no_ están disponibles para su uso fuera del seguimiento de medios porque la mayoría de ellas las calculan los servicios de medios de streaming basados en eventos de latidos. Además, es importante que las métricas de medios no se vean infladas por implementaciones diferentes.

## Atribución de flujo de transmisión de medios

El ejemplo de JavaScript siguiente generará una llamada de seguimiento de vínculos personalizados que tiene el nombre establecido como “Banner principal”.

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
