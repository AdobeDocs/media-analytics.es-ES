---
title: Acerca de la medición del ritmo cardíaco
description: Descubra cómo se utilizan los latidos del corazón para recopilar métricas de vídeo.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 75%

---

# Acerca de la medición del ritmo cardíaco

Adobe Streaming Media Collection utiliza &quot;latidos&quot; para recopilar métricas de vídeo. Durante la reproducción de vídeo, los latidos se envían al servidor de seguimiento de Heartbeat para medir el tiempo de reproducción. Las llamadas de Heartbeat se envían cada diez segundos. Los latidos generan métricas de participación en vídeo granulares e informes de visitas en el orden previsto de vídeo más precisos. Streaming Media mide los latidos mediante Adobe Launch con la extensión Media Analytics, Media SDK y la API de Media Collection. Los componentes `AppMeasurement` y `VisitorID` se utilizan para recibir datos de vídeo.

El uso de latidos en la recopilación de medios de streaming ofrece las siguientes ventajas:

| Función | Descripción |
|---|---|
| Eventos de contenidos | Los eventos detallados y personalizados se envían cada 10 segundos para el contenido principal y cada 1 segundo para los anuncios |
| Métricas y dimensiones | Métricas, dimensiones y puntos de referencia claros y estandarizados para todos los proveedores. Con una solución estandarizada en todas las plataformas, puede utilizar variables coherentes y estandarizadas en todos sus medios y plataformas para permitir una comparación más eficaz entre campañas, dispositivos y proveedores. |
| Integraciones | Experience Cloud ID está vinculado a Adobe Experience Cloud para facilitar el análisis cruzado. Con la integración automática de Adobe Experience Cloud, puedes segmentar tus audiencias de medios, dirigirte a ellas y hacer recomendaciones de medios basadas en las preferencias de los usuarios. |
| Precio | Seguimiento transparente por emisión de contenido (única) |
| Implementación y compatibilidad | Configuración optimizada con actualizaciones y mejoras continuas. Con un proceso de implementación agilizado, puede asignar rápidamente variables a través de la API del reproductor y validar las implementaciones mediante la herramienta de depuración de Adobe para garantizar que todas las variables necesarias se controlan con precisión. |
| Uso compartido de socios | Medios federados y métricas certificadas. Con los datos compartidos a través de Federated Media, puede sacar el máximo partido a las funciones de uso compartido de medios más novedosas y realizar una evaluación integral de los datos en todos sus socios de distribución de medios: operadores, programadores y distribuidores. |
| Seguimiento avanzado | Seguimiento de contenidos descargados, seguimiento de recuperación de errores y espectadores simultáneos. Puede realizar un seguimiento de los contenidos multimedia en streaming que se descargan y reproducen en un dispositivo independientemente de su conectividad. |
