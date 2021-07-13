---
title: Seguimiento de estados de aplicaciones
description: 'Los estados de la aplicación son las diferentes pantallas o vistas de la aplicación. Obtenga información sobre cómo rastrear el estado de la aplicación en la aplicación mediante la llamada trackState . '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 86%

---

# Seguimiento de estados de aplicaciones{#track-app-states}

Los estados son las distintas pantallas o vistas de su aplicación. Cada vez que se muestra un nuevo estado en la aplicación, debe enviar una llamada `trackState`. Por ejemplo, cuando un usuario navega de la página principal a la pantalla de detalles del vídeo, envía una llamada `trackState`. Los estados suelen verse mediante un informe de ruta, y así se puede ver cuántos usuarios navegan por la aplicación y qué estados se ven más.

## llamadas trackState

Normalmente, llama `trackState` cada vez que la aplicación carga una nueva pantalla.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

El nombre del estado se recoge en la variable “Ver estado” de Adobe Mobile Services y se registra una vista para cada llamada `trackState`. En otras interfaces de Analytics, “Ver estado” aparece como “Nombre de página” y “Vistas de estado” aparece como “Vistas de página”.

## Enviar datos de contexto

Además del “Nombre de estado”, puede enviar datos de contexto adicionales con cada llamada de seguimiento de estado.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>El valor de los datos de contexto debe asignarse a variables personalizadas de Adobe Mobile Services.
