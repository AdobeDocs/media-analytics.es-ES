---
title: Configuración de un SDK móvil mediante etiquetas para medios de transmisión
description: Aprenda a implementar medios de transmisión de Adobe para aplicaciones móviles.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 82%

---

# Instalación de SDK móviles {#install-mobile-sdks}

Para implementar la recopilación de medios de streaming para aplicaciones móviles en Android o iOS, instale y configure lo siguiente:

* **SDK móvil de Adobe Experience Platform**

  Para recopilar datos, utilice cualquiera de las siguientes opciones:
   * Etiquetas en Adobe Experience Platform. Las etiquetas en Adobe Experience Platform son una solución de administración de etiquetas que le permite implementar código de Analytics junto con otros requisitos de etiquetado.
   * Adobe Experience Platform Edge

* **Media SDK para Android** o **Media SDK para iOS**

* **Extensión de Adobe Media Analytics for Audio and Video**

Para descargar los SDK y para obtener recursos de documentación adicionales, consulte [Obtención de Media SDK, extensiones mediante etiquetas y SDK para OTT](/help/getting-started/download-sdks.md)

* **Obtener parámetros de configuración válidos**

  Estos parámetros se los puede proporcionar un representante de Adobe cuando haya configurado la cuenta de Analytics.

* **Incluya las siguientes API en su reproductor multimedia**

   * *Una API para suscribirse a eventos del reproductor*: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.

   * *Una API que proporcione información del reproductor*: incluye información sobre la reproducción actual, como el nombre del contenido, la posición del cabezal de reproducción, los anuncios o el capítulo.
