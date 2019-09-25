---
seo-title: Información general sobre migración
title: Información general sobre migración
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Información general sobre migración{#migration-overview}

La migración de VHL 1.x a VHL 2.x resulta sencilla gracias a la nueva versión que incluye API simplificadas para la inicialización, configuración y delegados de reproducción.

Estas son las principales diferencias entre 1.x y 2.x:

* **Plugins, delegados**: ya no es necesario implementar plugins y delegados para Analytics, VideoPlayer y Heartbeat.
* **Configuración**: ya no es necesario crear una instancia de configuración para los plugins 1.x.

## Ventajas de 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Ya no es necesario crear instancias de configuraciones para los complementos de Analytics, VideoPlayer y Heartbeat. Solo es necesario crear instancias de la `MediaHeartbeat` clase con `MediaHeartbeatDelegate` instancias y `MediaHeartbeatConfig` instancias. Esta es la única implementación necesaria para inicializar Media Analytics.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Elimine también la implementación existente para la inicialización de que utiliza una matriz de plugins como entrada. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

Las nuevas API en 2.x se describen detalladamente aquí: [Conversión de API 1.x a 2.x.](./1x-2x-api-change.md)
