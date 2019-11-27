---
title: Información general sobre migración
description: En este tema se ofrece una descripción general de la migración de las versiones 1.x a 2.x de Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Información general sobre migración {#migration-overview}

La migración de VHL 1.x a VHL 2.x resulta sencilla gracias a la nueva versión que incluye API simplificadas para la inicialización, configuración y delegados de reproducción.

Estas son las principales diferencias entre 1.x y 2.x:

* **Plugins, delegados**: ya no es necesario implementar plugins y delegados para Analytics, VideoPlayer y Heartbeat.
* **Configuración**: ya no es necesario crear una instancia de configuración para los plugins 1.x.

## Ventajas de 2.x {#benefits-of-two-x}

* Todos los métodos públicos se consolidan en la clase `MediaHeartbeat` para facilitar la implementación a los desarrolladores.
* Todas las configuraciones están consolidadas en la clase `MediaHeartbeatConfig`.
* Ya no es necesario crear instancias de configuración para los complementos de Analytics, VideoPlayer y Heartbeat. Solo es necesario crear la clase `MediaHeartbeat` con instancias `MediaHeartbeatDelegate` y `MediaHeartbeatConfig`. Esta es la única implementación requerida para iniciar Media Analytics.

   Con la inicialización de `MediaHeartbeat`, puede eliminar con seguridad toda la implementación para el complemento de Analytics, de VideoPlayer y de Heartbeat. Elimine también la implementación existente para la inicialización de que utiliza una matriz de plugins como entrada. Para ver comparaciones de las implementaciones de 1.x y 2.x, haga clic aquí: [Comparación de código: de 1.x a 2.x](./code-comparison-1x-2x.md)..

Las nuevas API en 2.x se describen detalladamente aquí: [Conversión de API 1.x a 2.x.](./1x-2x-api-change.md)
