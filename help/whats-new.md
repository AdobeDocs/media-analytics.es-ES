---
title: Novedades de Media Analytics
description: Novedades incluye información sobre nuevas funciones y notificaciones.
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 94%

---


# Novedades de Media Analytics {#whats-new}

![Banner](assets/media_analytics_banner.png)


Esta página describe nuevas funciones, correcciones y avisos importantes de Media Analytics. También se destacan la nueva documentación, los cursos de aprendizaje y los tutoriales de vídeo que le ayudarán a sacar el máximo rendimiento de Media Analytics.


## Notas de la versión

Notas de la versión de Adobe Experience Cloud

Las Notas de la versión de Adobe Experience Cloud describen nuevas funciones, correcciones y avisos importantes de Adobe Experience Cloud. Esto incluye los cambios más recientes de Media Analytics. También se destacan la nueva documentación, los cursos de formación y los tutoriales de vídeo que le ayudarán a sacar el máximo rendimiento de Experience Cloud.

## Nuevas características

| Función | [Disponibilidad general](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) - Fecha de destino | Descripción |
| ----------- | ---------- | ---------- |
| [Panel de visualizadores simultáneos de medios](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 17 de septiembre de 2020 | El panel Visualizadores simultáneos de medios en Workspace le permite comprender dónde se produjo la concurrencia máxima o dónde se produjeron los descensos. Proporciona una valiosa perspectiva de la calidad del contenido y de la participación del visualizador, y ayuda a solucionar problemas o a planificar el volumen o la escala. |
| [Dispositivos y plataformas compatibles](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 18 de junio de 2020 | La [!UICONTROL Extensión Media Launch] con el SDK móvil de AEP ahora es compatible con los siguientes dispositivos OTT:<ul><li>Apple TV (tvOS)</li><li>Fire TV (sistema operativo Fire)</li><li>Android TV</li></ul> |
| [Seguimiento del estado de reproducción](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html) | 29 de mayo de 2020 | Los clientes de [!UICONTROL Media Analytics] pueden capturar la interacción del visor durante la reproducción mediante un conjunto estándar de variables de solución para la pantalla completa, los subtítulos opcionales, el silencio, la imagen en imagen y el enfoque. También tiene la flexibilidad para crear estados de reproductor personalizados. Las variables de [!UICONTROL seguimiento de estado del reproductor] ahora están disponibles para el sistema de informes en [!UICONTROL Analysis Workspace]. Esta función requiere uno de los siguientes elementos: <ul><li>Media [!DNL JavaScript] SDK 3.0 o superior</li><li>Para usar con el SDK [!DNL Adobe Experience Platform] (AEP):</li><li>[!UICONTROL Extensión de Media Analytics] (para la Web): [!UICONTROL Adobe Media Analytics] (SDK 3.x) para audio y vídeo v1.0 o superior</li><li>[!UICONTROL Extensión de Media Analytics] (para móviles): [!UICONTROL Adobe Media Analytics para audio] y vídeo v2.0 o superior</li><li>[!UICONTROL Colección de medios]</li></ul> |


## Notificaciones importantes

| Función | [Disponibilidad general](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) - Fecha de destino | Descripción |
| ----------- | ---------- | ---------- |
| [Dispositivos y plataformas compatibles](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 31 de agosto de 2021 | Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejará de ofrecer compatibilidad con el SDK de Media Analytics para iOS y Android. Para obtener más información, consulte Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics. |
| [Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics](sdk-implement/end-of-support-faqs.md) | Otoño de 2019 | El desarrollo de funciones ha finalizado para los SDK de Media Analytics para iOS y Android.  Las nuevas funciones que se introdujeron a partir del otoño de 2019 se habilitan mediante las extensiones de Media Analytics y la API de Media Collection. |
| [Información general de contenidos](media-overview.md) | 20 de febrero de 2019 | Adobe solo es compatible con TLS 1.1 o posterior. Con este cambio, Adobe ya no recopilará datos de usuarios finales que usan dispositivos o navegadores web más antiguos que implementen TLS 1.0. |
| [Dispositivos y plataformas compatibles](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 19 de febrero de 2019 | A continuación, se enumeran las versiones de plataforma mínimas compatibles con cada SDK. <br>- iOS: iOS 6+ <br>- Android: Android 5.0+ - Lollipop <br>- Chrome: v22+<br>- Mozilla: v27+<br>- Safari: v7+<br>- IE: v1+ |
| [Parámetros de audio y vídeo](metrics-and-metadata/audio-video-parameters.md) | 7 de febrero de 2019 | Adobe Analytics para vídeo y audio lanzó un cambio en el nombre de una métrica. <i>Inicio de contenido</i> pasará a llamarse <i>Comienzo de contenido</i>. El motivo del cambio fue reflejar los estándares del sector en cuanto a métricas e informes, así como facilitar la identificación de la métrica en los informes. |
| [Parámetros de audio y vídeo](metrics-and-metadata/audio-video-parameters.md) | 13 de septiembre de 2018 | Se produjo un cambio en las etiquetas de algunas dimensiones, métricas e informes con el fin de permitir el seguimiento de contenido múltiple de análisis de audio y vídeo. Algunas de las etiquetas que han cambiado son: *inicios de vídeo* a *inicios de contenido*, *duración del vídeo* a *duración del contenido* y *nombre del vídeo* a *nombre del contenido*. Los informes de vídeo de Reports and Analytics se han actualizado para incluir el nombre “contenido” en lugar de “vídeo”. Los cambios de etiqueta no cambiaron la recopilación de datos ni los datos históricos. Tome nota de estos cambios en caso de que las utilice en el Report Builder o en cualquier otro contenido externo de extracción automatizada de datos al que pueda afectar el cambio. |




<!-- | title | date | description | -->
