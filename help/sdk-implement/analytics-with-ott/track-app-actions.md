---
seo-title: Seguimiento de acciones de aplicaciones
title: Seguimiento de acciones de aplicaciones
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Seguimiento de acciones de aplicaciones{#track-app-actions}

Las acciones son los eventos que tienen lugar en su aplicación y que desea medir.

Cada acción tiene una o más métricas correspondientes que se incrementan cada vez que tiene lugar el evento. For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

Las acciones no se rastrean automáticamente, por lo que debe invocar `trackAction` cuando se produce un evento que desee rastrear y asignar la acción a un evento personalizado.

1. When an event that you want to track occurs, call `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. Asigne la acción a un evento personalizado.

   * **Roku:**

      ```js
      dictionary = {} 
      dictionary["myapp.social.SocialSource"] = "Twitter"  
      ADBMobile().trackAction("myapp.SocialShare", dictionary)
      ```

   * **Chromecast:**

      ```js
      var dictionary = {}; 
      dictionary["myapp.social.SocialSource"] = "Twitter"; 
      ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
      ```

También puede enviar datos de contexto adicionales con cada llamada de acción de seguimiento.

