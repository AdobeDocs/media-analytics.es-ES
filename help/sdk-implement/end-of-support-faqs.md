---
title: Descubra las preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics
description: Este tema incluye preguntas frecuentes sobre el fin de la compatibilidad con los SDK de Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 78%

---

# Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics

Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejará de ofrecer compatibilidad con los SDK de Media Analytics para iOS y Android. A partir del 31 de agosto de 2021, Adobe no proporcionará correcciones, actualizaciones relacionadas con el sistema operativo ni compatibilidad con el SDK de Media Analytics.  Durante el proceso de migración a estos nuevos SDK de Experience Platform, tenga en cuenta que las [extensiones de Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) deben implementarse para habilitar Adobe Analytics para medios de transmisión.

## Las cinco cuestiones principales que saber

1. Los SDK de Mobile v4 ya no serán compatibles a partir del 31 de agosto de 2021. Debe migrar a los SDK móviles de Adobe Experience Platform (AEP) para iOS y Android. Para obtener más información, consulte las [preguntas más frecuentes sobre la finalización de la compatibilidad con SDK de Mobile, versión 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. La implementación de Analytics for Streaming Media requiere el SDK de AEP Mobile y el uso de las extensiones de Analytics y Media Analytics. A partir del 1 de septiembre de 2021, deberá utilizar los nuevos SDK y extensiones de AEP Mobile.  Las extensiones de Media Analytics se configuran con Adobe Launch.  Para obtener más información, consulte [Migración de Media SDK independientes a Adobe Launch](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html).

1. El desarrollo de funciones ha finalizado para los SDK de Media Analytics para iOS y Android.  Las nuevas funciones que se introdujeron a partir del otoño de 2019 se habilitan mediante las extensiones de Media Analytics y la API de Media Collection.

1. Los SDK de Roku y Chromecast siguen estando disponibles para los clientes de Analytics para Streaming Media. Los SDK de Roku y Chromecast seguirán mejorándose y admitiéndose como SDK independientes.  Si utiliza el SDK de JS para Media Analytics, puede seguir utilizando el SDK independiente o activar la extensión de Media Analytics mediante Adobe Launch.

1. Antes del 1 de septiembre de 2021, Adobe puede, a su criterio, desarrollar nuevas correcciones para problemas de alto impacto técnico o exposición empresarial. En función de los datos que proporcione el cliente, Adobe determinará el grado de impacto y exposición, y las actividades consiguientes.

Si tiene más preguntas, póngase en contacto con el administrador de satisfacción del cliente de Adobe.

## Preguntas frecuentes

1. **¿Se verá afectada la compatibilidad con los SDK de Roku y Chromecast?**

   No.  Los SDK de Roku y Chromecast seguirán siendo compatibles como SDK independientes por el momento.

1. **¿Se verán afectadas las implementaciones del SDK de JS de Media Analytics por este cambio?&#x200B;**

   No.  Los clientes que utilicen el SDK de JS para Media Analytics pueden seguir utilizando el SDK o habilitarlo mediante Adobe Launch.
&#x200B;
1. **¿Cuál es el nivel de esfuerzo para migrar a las extensiones de Media Analytics?**

   LOE depende de la implementación de cada cliente, por lo que variará.  Después de revisar la documentación de migración que se muestra a continuación, póngase en contacto con el servicio de consultoría o atención al cliente para obtener soporte adicional.

   [Extensiones de Media Analytics: migración a Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Extensiones de Media Analytics: migración a iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Extensiones de Media Analytics: nuevas implementaciones](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **¿Necesito tener Launch como sistema de administración de etiquetas? ¿Qué sucede si no deseo usar Launch?**

   En el caso de uso de la aplicación móvil, Launch no se utiliza como sistema de administración de etiquetas como lo hace para la web.  Se requiere el uso de la interfaz de usuario de Launch para configurar las extensiones de SDK. Esto es similar a cómo se usa la interfaz de usuario de Adobe Mobile Services para configurar la versión 4 del SDK de Mobile. Para la instalación, la ventaja de utilizar Launch es que le proporciona instrucciones de instalación personalizadas en función de la extensión que elija.

1. **¿Afecta este fin de soporte al SDK para tvOS?**

   Sí, para tvOS (versión 10 o posterior) la implementación recomendada es migrar a las extensiones de Media Analytics.  Para obtener más información, consulte [Migración del Media SDK independiente a Adobe Launch: iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **¿Afecta este fin de soporte al SDK para FireTV y AndroidTV?&#x200B;**

   Sí, para FireTV y AndroidTV, la implementación recomendada es migrar a las extensiones de Media Analytics.  Para obtener más información, consulte [Migración del Media SDK independiente a Adobe Launch - Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
