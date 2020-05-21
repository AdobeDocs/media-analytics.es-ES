---
title: Acerca del seguimiento del estado del reproductor
description: En este tema se describe la función de seguimiento del estado del reproductor, que incluye requisitos y guías para implementar y estados del reproductor de sistema de informes.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---


# Acerca del seguimiento del estado del reproductor

Para optimizar la experiencia del producto y aumentar el valor para su empresa, es importante comprender el comportamiento del cliente al ver los vídeos. Esto incluye el tiempo empleado en diferentes estados del reproductor.  Y para optimizar su comprensión, necesita la flexibilidad para crear y medir nuevos estados y eventos del reproductor según sea necesario.

El seguimiento de estado del reproductor ofrece la capacidad de capturar la interacción del visor durante la reproducción mediante un conjunto estándar de variables de solución para pantalla completa, subtítulos opcionales, silenciar, imágenes en imagen y enfocadas.  El seguimiento de estado del reproductor también proporciona la flexibilidad para crear estados de reproductor personalizados.  Y las variables de seguimiento de estado del reproductor están disponibles para sistema de informes en Espacio de trabajo de Análisis.

Para capturar los cambios en el estado del reproductor, el seguimiento de estado del reproductor actualiza los metadatos de medición de vídeo. Por ejemplo, para determinar la participación &quot;verdadera&quot; en el vídeo, el seguimiento de estado del reproductor mide el tiempo empleado con el sonido en comparación con las vistas de vídeo pasivas o no comprometidas cuando el sonido está desactivado o el tiempo empleado en el modo Normal frente a Pantalla completa.

El seguimiento del estado del reproductor ofrece las siguientes ventajas:

* Proporciona variables estándar que miden estados comunes como pantalla completa o subtítulos opcionales
* Proporciona variables personalizables para medir estados personalizados durante una sesión de reproducción
* Mide el tiempo empleado en un estado de reproductor personalizado
* Mide varios estados que pueden ser simultáneos

![Seguimiento del estado del reproductor](assets/player_state_tracking.png)

## Requisitos

El seguimiento de estado del reproductor requiere lo siguiente para Media Analytics Extension para su uso con Adobe Experience Platform (AEP SDK):
* Web: Adobe Media Analytics (SDK 3.x) para audio y vídeo v1.0 o posterior
* Móvil: Adobe Media Analytics para audio y vídeo v2.0+

Si decide no utilizar el SDK de AEP, puede utilizar lo siguiente con el seguimiento de estado del reproductor:
* Media JS SDK 3.0+
* ¿Versión de la API de Media Collection?

## Directrices

Antes de implementar el seguimiento de estado del reproductor, considere las siguientes pautas.

* El estado del reproductor se calcula en todos los estados de reproducción (sin división)
* Puede medir varios estados de reproductor al mismo tiempo
* El número máximo de estados del reproductor que se pueden rastrear durante una reproducción es de 10 
* Las métricas de estado del reproductor se envían a Analytics para sistema de informes SOLO en la llamada de cierre de medios
* Los estados del reproductor se capturan para cada sesión de reproducción individual; el estado del reproductor no se calcula entre reproducciones 