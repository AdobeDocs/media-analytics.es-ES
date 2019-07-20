---
seo-title: Seguimiento de estados de aplicaciones
title: Seguimiento de estados de aplicaciones
uuid: 2 f 98 fb 43-c 362-4 a 9 b -8732-fa 7 e 963 da 729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# Seguimiento de estados de aplicaciones{#track-app-states}

Los estados son las distintas pantallas o vistas de su aplicación. Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. Los estados suelen verse mediante un informe de ruta, y así se puede ver cuántos usuarios navegan por la aplicación y qué estados se ven más.

## Llamadas trackstate

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. En otras interfaces de Analytics, "Ver estado" se comunica como "Nombre de página"; " Vistas de estado "se comunica como" Vistas de página ".

## Enviar datos de contexto

Además de "Nombre de estado", puede enviar datos de contexto adicionales con cada llamada de estado de seguimiento.

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

