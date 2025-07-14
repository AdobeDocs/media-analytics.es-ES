---
title: Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics
description: Este tema incluye preguntas frecuentes sobre el fin de la compatibilidad con los SDK de Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 76%

---

# Preguntas frecuentes sobre el fin de la compatibilidad del SDK de Media Analytics

Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejó de ofrecer compatibilidad con los SDK de Media Analytics para iOS y Android. (Esto no incluye Media Analytics SDK para plataformas web (JS) y OTT como Chromecast y Roku, que siguen siendo compatibles).

Esto significa que Adobe ya no proporciona correcciones, actualizaciones relacionadas con el sistema operativo ni compatibilidad con Media Analytics Mobile SDK. Al migrar a los nuevos SDK de Experience Platform, tenga en cuenta que las [extensiones de Media Analytics](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) deben implementarse para habilitar Adobe Streaming Media Collection.


## Las cinco cuestiones principales que saber

1. A partir del 31 de agosto de 2021, los SDK de Mobile v4 ya no serán compatibles. Debe migrar a los SDK de Adobe Experience Platform (AEP) Mobile para iOS y Android.

1. La implementación de Analytics para Streaming Media requiere el SDK Mobile de AEP y el uso de las extensiones de Analytics y Media Analytics. A partir del 1 de septiembre de 2021, debe utilizar los nuevos SDK y las extensiones de AEP Mobile.  Las extensiones de Media Analytics se configuran mediante etiquetas de Adobe (recopilación de datos). Para obtener más información, consulte [Migración de Media SDK independientes a Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. El desarrollo de funciones ha finalizado para los SDK de Media Analytics para iOS y Android. Las nuevas funciones que se introdujeron a partir del otoño de 2019 se habilitan mediante las extensiones de Media Analytics y la API de Media Collection.

1. Los SDK de Roku y Chromecast siguen estando disponibles para los clientes de Analytics para Streaming Media. Los SDK de Roku y Chromecast seguirán mejorándose y admitiéndose como SDK independientes. Si utiliza el SDK de JS para Media Analytics, puede seguir utilizando el SDK independiente o activar la extensión de Media Analytics con la recopilación de datos de Adobe (antes conocida como Adobe Launch).

Si tiene alguna pregunta, póngase en contacto con el equipo de su cuenta de Adobe.

## Preguntas frecuentes

1. **¿Se verá afectada la compatibilidad con los SDK de Roku y Chromecast?**

   No.  Los SDK de Roku y Chromecast seguirán siendo compatibles como SDK independientes por el momento.

1. **¿Se verán afectadas las implementaciones del SDK de JS de Media Analytics por este cambio?&#x200B;**

   No.  Los clientes que utilicen el SDK de JS para Media Analytics pueden seguir utilizando el SDK o habilitarlo mediante Adobe Launch.
&#x200B;
1. **¿Cuál es el nivel de esfuerzo para migrar a las extensiones de Media Analytics?**

   LOE depende de la implementación de cada cliente, por lo que variará.  Después de revisar la documentación de migración que se muestra a continuación, póngase en contacto con el servicio de consultoría o atención al cliente para obtener soporte adicional.

[Extensiones de Media Analytics: migración a Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Extensiones de Media Analytics: migración a iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Extensiones de Media Analytics: nuevas implementaciones](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **¿Necesito tener Launch como sistema de administración de etiquetas? ¿Qué sucede si no deseo usar Launch?**

   En el caso de uso de la aplicación móvil, Launch no se utiliza como sistema de administración de etiquetas como lo hace para la web. Se requiere el uso de la interfaz de usuario de Launch para configurar las extensiones de SDK. Esto es similar a cómo se usa la interfaz de usuario de Adobe Mobile Services para configurar la versión 4 del SDK de Mobile. Para la instalación, la ventaja de utilizar Launch es que le proporciona instrucciones de instalación personalizadas en función de la extensión que elija.

1. **¿Afecta este fin de soporte al SDK para tvOS?**

   Sí, para tvOS (versión 10 o posterior) la implementación recomendada es migrar a las extensiones de Media Analytics. Para obtener más información, consulte [Migración del Media SDK independiente a Adobe Launch: iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **¿Afecta este fin de la compatibilidad al SDK para Fire TV y Android TV?**

   Sí, la implementación recomendada para Fire TV y Android TV es migrar a las extensiones de Media Analytics. Para obtener más información, consulte [Migración del Media SDK independiente a Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
