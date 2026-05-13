---
title: Acerca de la medición del ritmo cardíaco
description: Descubra cómo se utilizan los latidos del corazón para recopilar métricas de vídeo.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: eb9732ab-8232-4b21-bc4c-89de86dbe4d7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e6c28e30-8689-4bf4-8fa8-561343d308a9id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# Acerca de la medición del ritmo cardíaco

Los servicios de medios de streaming de Adobe utilizan &quot;latidos&quot; para recopilar métricas de vídeo. Durante la reproducción de vídeo, los latidos se envían al servidor de seguimiento de Heartbeat para medir el tiempo de reproducción. Las llamadas de Heartbeat se envían cada diez segundos. Los latidos generan métricas de participación en vídeo granulares e informes de visitas en el orden previsto de vídeo más precisos. Los servicios de medios de streaming miden los latidos mediante Adobe Launch con la extensión Media Analytics, Media SDK y la API de Media Collection. Los componentes `AppMeasurement` y `VisitorID` se utilizan para recibir datos de vídeo.

El uso de latidos en los servicios de medios de streaming ofrece las siguientes ventajas:

| Función | Descripción |
|---|---|
| Eventos de contenidos | Los eventos detallados y personalizados se envían cada 10 segundos para el contenido principal y cada 1 segundo para los anuncios |
| Métricas y dimensiones | Borrar métricas, dimensiones y puntos de referencia estandarizados entre proveedores. Con una solución estandarizada para todas las plataformas, puede utilizar variables coherentes y estandarizadas para todos los medios y plataformas que permitan una comparación más eficaz entre campañas, dispositivos y proveedores. |
| Integraciones | El Experience Cloud ID está vinculado a Adobe Experience Cloud para facilitar el análisis cruzado. Con la integración automática de Adobe Experience Cloud, puede segmentar sus audiencias de medios, dirigirlas y hacer recomendaciones de medios en función de las preferencias del usuario. |
| Precio | Seguimiento transparente por emisión de contenido (única) |
| Implementación y compatibilidad | Configuración optimizada con actualizaciones y mejoras continuas. Con un proceso de implementación optimizado, puede asignar rápidamente variables a través de la API del reproductor y validar implementaciones mediante la herramienta de depuración de Adobe para garantizar que todas las variables necesarias se rastrean con precisión. |
| Uso compartido de socios | Medios federados y métricas certificadas. Con los datos compartidos a través de Federated Media, puede sacar el máximo partido a las funciones de uso compartido de medios más novedosas y realizar una evaluación integral de los datos en todos sus socios de distribución de medios: operadores, programadores y distribuidores. |
| Seguimiento avanzado | Seguimiento de contenido descargado, seguimiento de recuperación de errores y visores simultáneos. Puede hacer un seguimiento del contenido de medios de streaming que se descarga y reproduce en un dispositivo, independientemente de su conectividad. |
