---
title: Preguntas más frecuentes sobre el fin de la compatibilidad con el SDK de Media Analytics
description: Este tema incluye preguntas más frecuentes sobre el fin de la compatibilidad con los SDK de Media Analytics.
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---


# Preguntas más frecuentes sobre el fin de la compatibilidad con el SDK de Media Analytics

Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejará de ofrecer compatibilidad con los SDK de Media Analytics para iOS y Android. A partir del 31 de agosto de 2021, Adobe no proporcionará correcciones, actualizaciones relacionadas con el sistema operativo ni compatibilidad con el SDK de Media Analytics.  Durante el proceso de migración a estos nuevos SDK de la plataforma de experiencia, tenga en cuenta que las extensiones [de](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) Media Analytics deben implementarse para habilitar Adobe Analytics para audio y vídeo.

## 5 cosas principales que saber

1. Los SDK de Mobile v4 ya no serán compatibles a partir del 31 de agosto de 2012. Debe migrar a los SDK de Adobe Experience Platform (AEP) para iOS y Android.

1. La implementación de Analytics para audio y vídeo requiere el SDK de AEP y el uso de las extensiones de Analytics y Media Analytics. A partir del 1 de septiembre de 2021, debe utilizar los nuevos SDK y extensiones de AEP.  Las extensiones de Media Analytics se configuran con Adobe Launch.  Para obtener más información, consulte [Migración del SDK de medios independientes a Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. El desarrollo de funciones ha finalizado para los SDK de Media Analytics para iOS y Android.  Las nuevas funciones que se introdujeron a partir del otoño de 2019 se habilitan mediante las extensiones de Media Analytics y la API de Media Collection.

1. Los SDK de Roku y Chromecast siguen estando disponibles para los clientes de Analytics para audio y vídeo. Los SDK de Roku y Chromecast seguirán mejorándose y admitiéndose como SDK independientes.  Si utiliza el SDK de JS para Media Analytics, puede seguir utilizando el SDK independiente o activar la extensión de Media Analytics mediante Adobe Launch.

1. Antes del 1 de septiembre de 2021, Adobe puede, a su propia discreción, desarrollar nuevas correcciones para problemas de alto impacto técnico o exposición empresarial. En función de los datos que proporcione el cliente, Adobe determinará el grado de impacto y exposición y las actividades consiguientes.

Si tiene alguna pregunta, póngase en contacto con el administrador de éxito del cliente de Adobe.

## Preguntas frecuentes

1. **¿Se verá afectada la compatibilidad con los SDK de Roku y Chromecast? &#x200B;**

   No.  Los SDK de Roku y Chromecast seguirán siendo compatibles como SDK independientes por el momento. &#x200B; &#x200B;
1. **¿Se verán afectadas las implementaciones del SDK de JS de Media Analytics por este cambio? &#x200B;**

   No.  Los clientes que utilicen el SDK de JS para Media Analytics pueden seguir utilizando el SDK o habilitarlo mediante Adobe Launch.
&#x200B;
1. **¿Cuál es el nivel de esfuerzo para migrar a las extensiones de Media Analytics? &#x200B;**

   LOE depende de la implementación de cada cliente, por lo que variará.  Después de revisar la documentación de migración que se muestra a continuación, póngase en contacto con el servicio de consultoría o atención al cliente para obtener soporte adicional.

   [Extensiones de Media Analytics: Migración a Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Extensiones de Media Analytics: Migración de iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Extensiones de Media Analytics: nuevas implementaciones](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **¿Necesito tener Launch como sistema de administración de etiquetas? ¿Qué sucede si no deseo usar Launch?**

   Para móviles, Launch es necesario para configurar las extensiones de medios como la interfaz de usuario de Mobile Services. En el caso de uso de la aplicación móvil, no se utiliza como sistema de administración de etiquetas.

1. **¿Afecta este fin de soporte al SDK para tvOS?**

   Sí, para tvOS (versión 10 o posterior) la implementación recomendada es migrar a las extensiones de Media Analytics.  La compatibilidad con AEP SDK y Media Analytics Extension está prevista para junio de 2020.  Para obtener más información, consulte [Migración del SDK de medios independiente a Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **¿Afecta este fin de soporte al SDK para FireTV y AndroidTV? &#x200B;**

   Sí, para FireTV y AndroidTV, la implementación recomendada es migrar a las extensiones de Media Analytics.  La compatibilidad con AEP SDK y Media Analytics Extension está prevista para junio de 2020.  Para obtener más información, consulte [Migración del SDK de medios independiente a Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
