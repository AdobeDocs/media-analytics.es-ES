---
title: Configuración de un SDK móvil mediante etiquetas para medios de transmisión
description: Aprenda a implementar medios de transmisión de Adobe para aplicaciones móviles.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 31%

---

# Instalación de SDK para móviles {#install-mobile-sdks}

Para implementar medios de transmisión por secuencias para aplicaciones móviles en Android o iOS, instale y configure lo siguiente:

* **SDK móvil de Adobe Experience Platform**

   Para recopilar datos, utilice Etiquetas en Adobe Experience Platform. Las etiquetas en Adobe Experience Platform son una solución de administración de etiquetas que le permite implementar código de Analytics junto con otros requisitos de etiquetado.

* **Media SDK para Android** o **Media SDK para iOS**

* **Extensión de Adobe Media Analytics for Audio and Video**

Para descargar los SDK y para obtener recursos de documentación adicionales, consulte [Obtención de Media SDK, extensiones mediante etiquetas y SDK para OTT](/help/getting-started/download-sdks.md)

* **Obtener parámetros de configuración válidos**

   Estos parámetros se pueden obtener de un representante de Adobes una vez creada la cuenta de Analytics.

* **Incluya las siguientes API en su reproductor de medios**

   * *Una API para suscribirse a eventos del reproductor*: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.

   * *Una API que proporcione información del reproductor* : incluye información sobre la reproducción actual, como el nombre del contenido, la posición del cabezal de reproducción, los anuncios o el capítulo.
