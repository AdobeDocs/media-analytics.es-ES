---
title: Información general sobre migración
description: Obtenga información sobre la migración de las versiones 1.x a 2.x de Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 87%

---

# Información general de la migración heredada de la VHL 1.x a la VHL 2.x {#migration-overview}

La migración de VHL 1.x a VHL 2.x resulta sencilla gracias a la nueva versión que incluye API simplificadas para la inicialización, configuración y delegados de reproducción

Estas son las principales diferencias entre 1.x y 2.x:

* **Complementos, delegados -** Ya no necesita implementar complementos y delegados para Analytics, VideoPlayer y Heartbeat.
* **Configuración -** Ya no necesita crear instancias de configuraciones para los complementos 1.x.

## Ventajas de 2.x {#benefits-of-two-x}

* Todos los métodos públicos se consolidan en la clase `MediaHeartbeat` para facilitar la implementación a los desarrolladores.
* Todas las configuraciones están consolidadas en la clase `MediaHeartbeatConfig`.
* Ya no es necesario crear instancias de configuración para los complementos de Analytics, VideoPlayer y Heartbeat. Solo es necesario crear la clase `MediaHeartbeat` con instancias `MediaHeartbeatDelegate` y `MediaHeartbeatConfig`. Esta es la única implementación requerida para iniciar Media Analytics.

  Con la inicialización de `MediaHeartbeat`, puede eliminar con seguridad toda la implementación para el complemento de Analytics, de VideoPlayer y de Heartbeat. Elimine también la implementación existente para la inicialización de que utiliza una matriz de plugins como entrada. Para ver comparaciones de las implementaciones de 1.x y 2.x, haga clic aquí: [Comparación de código: de 1.x a 2.x](./code-comparison-1x-2x.md)..

Las nuevas API en 2.x se describen detalladamente aquí: [Conversión de API 1.x a 2.x.](./1x-2x-api-change.md)
