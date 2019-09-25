---
seo-title: Seguimiento de estados de aplicaciones
title: Seguimiento de estados de aplicaciones
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# Seguimiento de estados de aplicaciones{#track-app-states}

Los estados son las distintas pantallas o vistas de su aplicación. Each time a new state is displayed in your application, you should send a  call. `trackState` For example, when a user navigates from the home page to the video details screen, send a  call. `trackState` Los estados suelen verse mediante un informe de ruta, y así se puede ver cuántos usuarios navegan por la aplicación y qué estados se ven más.

## Llamadas trackState

You typically call  each time the app loads a new screen.`trackState`

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. In other Analytics interfaces, "View State" is reported as "Page Name"; "State Views" is reported as "Page Views".

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

