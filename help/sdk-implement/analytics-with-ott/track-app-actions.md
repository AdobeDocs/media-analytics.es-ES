---
title: Seguimiento de acciones de aplicaciones
description: Las acciones de la aplicación son los eventos que tienen lugar en su aplicación y que desea medir.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 100%

---

# Seguimiento de acciones de aplicaciones{#track-app-actions}

Las acciones son los eventos que tienen lugar en su aplicación y que desea medir.

Cada acción tiene una o más métricas correspondientes que se incrementan cada vez que tiene lugar el evento. Por ejemplo, podría enviar una llamada `trackAction` por cada nueva suscripción, cada vez que se clasifique contenido o cada vez que se complete un nivel.

Las acciones no se rastrean automáticamente, por lo que debe invocar `trackAction` cuando se produce un evento que desee rastrear y asignar la acción a un evento personalizado.

1. Cuando se produce un evento para el que desea realizar un seguimiento, invoque a `trackAction`.

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
