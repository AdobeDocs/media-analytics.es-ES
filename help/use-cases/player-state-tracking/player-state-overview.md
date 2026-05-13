---
title: Acerca del seguimiento del estado de reproducción
description: Obtenga información sobre la función de seguimiento del estado de los jugadores, incluidos los requisitos y las directrices para implementar e informar sobre los estados de los jugadores.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/R4ByVgEI65JyN-LFdMX1CCBs4zVyppVgebN9OJxJNMM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 409
ht-degree: 100%

---

# Acerca del seguimiento del estado de reproducción

Para optimizar la experiencia del producto y aumentar el valor para su empresa, es importante comprender el comportamiento del cliente cuando ve los vídeos. Esto incluye el tiempo empleado en diferentes estados del reproductor.  También es importante tener la flexibilidad de crear y medir nuevos estados y eventos del reproductor según sea necesario.

El seguimiento de estado del reproductor ofrece la capacidad de capturar la interacción del visor durante la reproducción mediante un conjunto estándar de variables de solución para pantalla completa, subtítulos, silenciar, imagen en imagen y enfocado.  El seguimiento de estado del reproductor también proporciona la flexibilidad para crear estados de reproductor personalizados. Puede utilizar las variables de seguimiento de estado del reproductor para la creación de informes en Analysis Workspace.

Para capturar los cambios en el estado del reproductor, el seguimiento de estado del reproductor actualiza los metadatos de medición de vídeo. Por ejemplo, para determinar la participación “true” en el vídeo, el seguimiento de estado del reproductor mide el tiempo empleado con el sonido en comparación con las vistas de vídeo pasivas o no comprometidas cuando el sonido está desactivado o el tiempo empleado en el modo Normal frente al modo de Pantalla completa.

El seguimiento del estado del reproductor ofrece las siguientes ventajas:

* Proporciona variables estándar que miden estados comunes como pantalla completa o subtítulos
* Proporciona variables personalizables para medir estados personalizados durante una sesión de reproducción
* Mide el tiempo empleado en un estado de reproductor personalizado
* Mide varios estados que pueden ser simultáneos

![Seguimiento del estado de reproducción](assets/player_state_tracking.png)

## Requisitos

El seguimiento de estado del reproductor requiere una de las siguientes opciones para la recopilación de datos:
* Media JS SDK 3.0+
* SDK de Chromecast 3.0 para las soluciones de Adobe Marketing Cloud
* Extensión de Media Analytics (para uso con los SDK de Adobe Experience Platform (AEP))
   * Web: Adobe Media Analytics (SDK 3.x) para audio y vídeo v1.0 o posterior
   * Móvil: extensión de Adobe Media Analytics para audio y vídeo versión 2.0 o posterior
* API de Media Collection

## Directrices

Antes de implementar el seguimiento de estado del reproductor, considere las siguientes pautas.

* El estado del reproductor se calcula en todos los estados de reproducción (sin división).
* Puede medir varios estados de reproductor al mismo tiempo.
* La cantidad máxima de estados del reproductor que se pueden rastrear durante una reproducción es de 10.
* Las métricas de estado del reproductor se envían a Analytics para sistema de informes solo en la llamada de cierre de medios.
* El conocimiento del estado de la aplicación no se mantiene una vez que se detiene un estado. Una vez finalizado el estado, este debe volver a iniciarse para continuar con el seguimiento. Para cada nuevo estado de reproducción, se debe volver a iniciar el estado del reproductor.
* Los estados del reproductor se capturan para cada sesión de reproducción individual; el estado del reproductor no se calcula entre reproducciones.
