---
title: Acerca de la medición de latidos
description: Descubra cómo se utilizan los latidos para recopilar métricas de vídeo.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 30%

---

# Acerca de la medición de Heartbeat

Adobe Analytics utiliza &quot;latidos&quot; para recopilar métricas de vídeo. Durante la reproducción de vídeo, los latidos se envían al servidor de seguimiento de Heartbeat para medir el tiempo de reproducción. Las llamadas de Heartbeat se envían cada diez segundos. Los latidos generan métricas de participación en vídeo granulares e informes de visitas en el orden previsto de vídeo más precisos. Adobe Analytics para medios de transmisión mide los latidos mediante Adobe Launch con la extensión Media Analytics, Media SDK y la API de Media Collection. Los componentes `AppMeasurement` y `VisitorID` se utilizan para recibir datos de vídeo.

El uso de latidos de Adobe Analytics para Streaming Media ofrece las siguientes ventajas:

| Función | Descripción |
|---|---|
| Eventos de contenidos | Los eventos detallados y personalizados se envían cada 10 segundos para el contenido principal y cada 1 segundo para los anuncios |
| Métricas y dimensiones | Borrar métricas, dimensiones y puntos de referencia estandarizados entre proveedores. Con una solución estandarizada en todas las plataformas, puede utilizar variables coherentes y estandarizadas en todos los medios y plataformas para permitir una comparación más eficiente entre campañas, dispositivos y proveedores. |
| Integraciones | El ID de Experience Cloud está vinculado a Adobe Experience Cloud para facilitar el análisis cruzado. Con la integración automática de Adobe Experience Cloud, puede segmentar las audiencias de los medios, segmentarlas y hacer recomendaciones de medios en función de las preferencias del usuario. |
| Precio | Seguimiento transparente por emisión de contenido (única) |
| Implementación y compatibilidad | Configuración optimizada con actualizaciones y mejoras continuas. Con un proceso de implementación optimizado, puede asignar rápidamente variables a través de la API del reproductor y validar implementaciones mediante la herramienta de depuración de Adobe para garantizar que todas las variables necesarias se rastrean con precisión. |
| Uso compartido de socios | Federated Analytics y métricas certificadas. Con los datos compartidos a través de Federated Analytics, puede sacar provecho de nuestras funciones de uso compartido de medios más novedosas para evaluar los datos de forma integral en todos sus socios de distribución de medios: operadores, programadores y distribuidores. |
| Seguimiento avanzado | Seguimiento de contenido descargado, seguimiento de recuperación de errores y visores simultáneos. Puede rastrear contenido multimedia de flujo continuo descargado y reproducido en un dispositivo, independientemente de su conectividad. |
